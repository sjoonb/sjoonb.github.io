---
layout: post
title:  "differences between Proxy vs VPN"
categories: curiosity network
date:  2022-12-02 19:04:34 +0900
---

<br/>
[프락시]({% post_url 2022-12-01-http-architecture %}#프락시)의 역할 중 `익명화 프락시는` HTTP 메시지에서 신원을 식별할 수 있는 특성들(IP, From, Referer, Cookie, URI Session ID 등)을 제거해 주는 기능을 한다.

해당 기능이 VPN의 역할과 비슷하단 생각이 들어, VPN이 혹시 프락시 서버일까 궁금했다. 결론은 아니다고, 그렇다면 VPN은 무엇이고 어떻게 다른 것인지 알아보고자 한다. 

<br/>

- [VPN 이란?](#vpn-이란)
- [VPN과 프락시의 공통점](#vpn과-프락시의-공통점)
- [VPN과 프락시의 차이점](#vpn과-프락시의-차이점)
- [VPN 의 동작과정](#vpn-의-동작과정)
- [결론](#결론)

<br/>
# VPN 이란?

> A VPN, which stands for virtual private network, is a service that establishes a secure and private connection to the internet.

VPN은 개인 정보를 보호하는 서비스인 가상 사설망 서비스이며, 이는 퍼블릭 네트워크를 통해 데이터를 안전하게 익명으로 전송하는 데 사용되어 진다. 뿐만아니라, VPN은 사용자 IP 주소를 마스킹하고, 데이터를 암호화하여 수신 권한이 없는 사람이 읽을 수 없도록 하는 기능도 제공해 준다.

<br/>
# VPN과 프락시의 공통점

> Both VPNs and proxy servers are tools you can use to help keep your activity private when browsing the internet, sending emails, reading online message boards, streaming video, and downloading files. 

VPN과 프락시 서버 모두 사용자의 개인 정보를 지키는 역할을 위한 도구로 사용될 수 있다. 

<br/>
# VPN과 프락시의 차이점

 > While a proxy works with a single app or site, a VPN secures your network traffic. <br/><br/>
 Like a proxy, a VPN will hide your IP address when you first visit a website after logging in and replace it with the VPN provider’s IP address. However, only a VPN will redirect your internet data through an encrypted tunnel, keeping your online activity private.

 VPN과 프락시 서버 모두 IP를 가리는 기능이 존재하지만, 프락시 서버는 각각의 앱이나 웹에 대응하며 그 기능을 수행하는 반면, VPN은 한 디바이스의 모든 네트워크 트래픽에 해당 기능을 제공해 준다.

더 나아가 VPN은 프락시와 달리 `encryption` 기능을 구현하여, 네트워크를 통해 주고 받는 모든 종류의 데이터를 보호할 수 있다. 이를 통해, 사용자는 정부의 감시, 해커의 공격, ISP tracking 등을 방지할 수 있다.

다만, VPN은 더 다양한 기능을 제공하기 때문에 프락시에 비해선 느린편이며, 주로 비용을 지불해야 사용할 수 있는 경우가 대부분이다.


<br/>
# VPN 의 동작과정
VPN이 어떻게 동작하는지 살펴보자 <br/>

![how-vpn-works](/asset/images/how-vpn-works.png){:class="img-responsive"}

> When connected to the internet without a virtual private network, your internet service provider (ISP) is the main intermediary between your device and the internet. Your ISP assigns your device a unique IP address and tracks all the websites you visit. <br/><br/>
On the other hand, when a VPN connection is activated on a device, all web requests travel through an encrypted tunnel and are routed through a VPN server before reaching the target server.<br/><br/>
After a request is processed, the data sent back to the device goes through the same encrypted VPN connection and routing process. <br/><br/>
When using a VPN, your device’s internet connection still passes through your internet service provider. However, since it’s encrypted and routed via a VPN server, your ISP won’t see the websites you visit anymore. It just knows that you are connected to a VPN and that encrypted traffic travels from your device to a server.

VPN 서비스는 클라이언트와 서버를 모두 활용한다. VPN connection 이 device 에서 활성화 되면, 모든 웹 요청은 encrypted tunnel 을 통해 전송되며, ISP를 거쳐 VPN 서버에 도달하고, 마찬가지로 respone 는 같는 encrypted connection 을 통해 device 에게 돌아온다.

데이터가 ISP를 통해 전송되는건 마찬가지 이지만, VPN의 encryption 덕에 ISP 에서는 암호화된 데이터를 이해하지 못하게 되는 것이다.


<br/>
# 결론

VPN과 프락시 모두 유저의 정보를 보호하는데 활용되지만, VPN은 프락시보다 발전된 형태로 다양한 기능을 제공한다. 프락시는 하나의 서버라고 볼 수 있지만, VPN 은 서버와 클라이언트를 모두 활용하는 네트워크의 한 형태라고 볼 수 있을 것 같다.


<br/>
<br/>
참고

- [Proxy vs. VPN: 4 differences you should know](https://us.norton.com/blog/privacy/proxy-vs-vpn)
- [NordVPN](https://nordvpn.com/blog/vpn-vs-proxy/)
- [what is vpn](https://www.hostinger.com/tutorials/what-is-vpn)