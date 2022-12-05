---
layout: post
title:  "chunked transfer encoding"
categories: network
date: 2022-11-30 15:01:04 +0900
---



<br/>
![chunked-encoding-response-stream](/asset/images/chunked-encoding-response-stream.gif){:class="img-responsive"}

<br/>


**HTTP/1.1**에서는, `Transfer-Encoding:chunked` 라는 헤더와 함께 데이터를 쪼개서 보낼 수 있는 기능을 제공한다. 청크 인코딩의 규칙에 따라, 송신측은 데이터를 쪼개어 이를 데이터 스트림의 형태로 한 커넥션에서 연속적으로 데이터를 보내고, 수신측에선 이를 끝까지 받은 뒤 조합하여 사용한다. 

청크 인코딩을 사용할 때는 Content-Length 헤더 없이 지속 커넥션을 사용할 수 있으며, 따라서 위 이미지는 지속 커넥션을 통해서 일어나는 과정이라고 볼 수 있다. 

<br/>
<br/>
<br/>
엔터티와 인코딩을 공부하며 더 정리할 예정이다.
