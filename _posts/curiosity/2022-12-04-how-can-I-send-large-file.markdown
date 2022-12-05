---
layout: post
title:  "How does HTTP deliver a large file"
categories: curiosity network
date:  2022-12-04 14:10:30 +0900
comments_id: 1
---



[HTTP]({% post_url 2022-11-29-http %})와 [TCP/IP]({% post_url 2022-11-29-tcp-ip %})를 공부하면서, 커넥션이 어떻게 이루어지고, 트랜잭션이 어떻게 이루어지는지 공부하였다.


하지만, 큰 용량의 콘텐츠(이미지, 영상 등)를 HTTP로 어떻게    전송할 수 있는지, 어떤식으로 커넥션 및 트랜잭션이 처리되는건지 감이 잘 오지 않아, 이에 대하여 알아보려고 한다.

<br/>

- [HTTP body 의 크기 제한](#http-body-의-크기-제한)
- [크기 제한을 넘어가는 콘텐츠를 전송하는 방법](#크기-제한을-넘어가는-콘텐츠를-전송하는-방법)
  - [Compress Data](#compress-data)
  - [Transfer chunked data](#transfer-chunked-data)
  - [Request data in a selected range](#request-data-in-a-selected-range)
- [결론](#결론)



<br/>
## HTTP body 의 크기 제한

> - The HTTP protocol does not specify a limit.<br/>
- The POST method allows sending far more data than the GET method, which is limited by the URL length - about 2KB.<br/>
- The maximum POST request body size is configured on the HTTP server and typically ranges from
1MB to 2GB<br/>
- The HTTP client (browser or other user agent) can have its own limitations. Therefore, the maximum POST body request size is min(serverMaximumSize, clientMaximumSize).<br/>


**서버**

> - Nginx (largest web server market share as of April 2019) - default 1MB, no practical maximum (2**63) <br/>
- Apache - maximum 2GB, no default documented <br/>

**클라이언트**

> - IE: 2GB <br/>
- Firefox: 2GB <br/>
- Chrome: 4 GB <br/>
- Opera: 4 GB <br/>

HTTP body에는 크기 제한이 없어, POST 메시지와 같은 경우 큰 데이터를 보낼 때에도 사용이 가능하다. 하지만, 이는 사실상  클라이언트나 서버에 의하여 제한되며, 주로 1MB ~ 2GB 정도의 크기로 결정된다.

사이즈를 왜 제한하는 걸까?

> POST allows for an arbitrary length of data to be sent to a server, but there are limitations based on timeouts/bandwidth etc.

timouts과, bandwidth 등을 고려한 제한이라고 하는데, 명쾌하게 이해가 되진 않았다. 응답이 돌아오는데 너무 오래걸릴 경우 이를 timeout 처리하는 경우가 있다. 용량이 크다면, 에러가 일찍이 발생했음에도 이를 기다리는 자원 낭비가 발생할 것이고, 그러한 비효율이 사이즈를 제한하는 이유가 되지 않을까 싶다.


결론은, 클라이언트와 서버에 의하여 제한된 크기 내의 콘텐츠는 커넥션이 맺어진 뒤 한번의 요청과 응답과정에 의하여 처리할 수 있는 것이다. 

그렇다면, 그 제한을 넘어가는 콘텐츠는 어떻게 처리할 수 있을까?


<br/>
## 크기 제한을 넘어가는 콘텐츠를 전송하는 방법


<br/>
### Compress Data

용량이 큰 파일을 압축시켜 보내는 방법이 존재한다. 클라이언트는 `Accept-Encoding` 헤더를, 서버는`Content-Encoding` 헤더를 활용하여 압축 시킨 데이터를 주고 받을 수 있다.

하지만, 압축 방식은 Text 형식의 데이터에는 충분하겠지만, 비디오와 같이 용량이 큰 데이터를 압축하는데에는 충분하지 않다. 

<br/>
### Transfer chunked data

<br/>
![chunked-encoding-response-stream](/asset/images/chunked-encoding-response-stream.gif){:class="img-responsive"}

<br/>


**HTTP/1.1**에서는, `Transfer-Encoding:chunked` 라는 헤더와 함께 데이터를 쪼개서 보낼 수 있는 기능을 제공한다. 청크 인코딩의 규칙에 따라, 송신측은 데이터를 쪼개어 이를 데이터 스트림의 형태로 한 커넥션에서 연속적으로 데이터를 보내고, 수신측에선 이를 끝까지 받은 뒤 조합하여 사용한다. 

청크 인코딩을 사용할 때는 Content-Length 헤더 없이 지속 커넥션을 사용할 수 있으며, 따라서 위 이미지는 지속 커넥션을 통해서 일어나는 과정이라고 볼 수 있다. 

> Chunking is nice but it is only meant for when you (the one sending the large response) don't know the actual total size of your response until you have streamed it. If you know the size beforehand, use the content-length header.

청크 인코딩은 큰 데이터를 여러개의 메시지로 나누어 보내기 때문에, 기존 body 크기의 제한을 넘는 사이즈를 나누어 보내는 것으로는 합리적인 것처럼 보여진다. 

 다만, 청크 인코딩은 body가 동적으로 생성될 때에 유용한 방법인데, 현재 가정한 상황과는 결이 달라 보인다. 큰 용량에 데이터가 정적으로 보관되어 있는 상황에서, 이를 보낼 때 사이즈 제한을 피하기 위해 사용할 방법이 필요한 것이기 때문에, 이게 적절한 예시일지에 대하여 의구심이 든다.


<br/>
### Request data in a selected range

유튜브에서 영상 전송을 위하여 활용하는 방식으로, 서버가 `Accept-Ranges: bytes` 라는 헤더와 함께 요청받은 ranges에 해당하는 만큼의 본문 데이터를 보내는 방식이다. 이 방법을 통하여 클라이언트는 큰 사이즈의 연속적인 콘텐츠를 지속적으로 적절한 ranges 로 나누어 받을 수 있을 것이다.

지속 커넥션 적용 여부에 따라 다르겠지만, 일반적으로는 한 커넥션에서 지정된 범위만큼에 데이터를 받를 뒤, 해당 커넥션은 끝난다고 볼 수 있을 것 같다.

<br/>
## 결론

HTTP에서는 body size 에 제한을 두지 않는다. 하지만, 이는 실질적으로 클라이언트나 서버에 의하여 제한된다. 제한을 초과하는 콘텐츠를 주고 받기 위해선 콘텐츠를 압축하거나, 청크 인코딩이나 ranges 헤더를 통해 나누어 보내는 방법 등을 활용해야 할 것이다.

<br/>
<br/>
참고

- [How does HTTP Deliver a Large File?](https://cabulous.medium.com/how-http-delivers-a-large-file-78af8840aad5)
- [Is there a limit of the size of response I can read over HTTP](https://stackoverflow.com/questions/27309773/is-there-a-limit-of-the-size-of-response-i-can-read-over-http)
- [Is there a maximum size for content of an HTTP POST?](https://serverfault.com/questions/151090/is-there-a-maximum-size-for-content-of-an-http-post)
- [Can HTTP POST be limitless?](https://stackoverflow.com/questions/2880722/can-http-post-be-limitless)