# NAT

* Network Address Translation

> NAT(네트워크 주소 변환)은 IP 패킷의 TCP/UDP **포트 숫자와 소스 및 목적지의 IP 주소 등을 재기록**하면서 라우터를 통해 네트워크 트래픽을 주고 받는 기술이다. 패킷에 변화가 생기기 때문에 IP나 TCP/UDP의 체크섬(checksum)도 다시 계산되어 재기록해야 한다. 그렇기 때문에 네트워크의 성능에 영향을 줄 수 밖에 없다.
>
> NAT를 쓰는 이유는 여러 대의 호스트가 하나의 공인 IP 주소를 사용하여 인터넷에 접속하기 위한 경우가 대부분이다. 예를 들어 인터넷 회선을 하나 개통하고 인터넷 공유기를 달아서 여러 PC 를 연결하여 사용 하는데, 이 것이 가능한 이유가 인터넷 공유기에 NAT 기능이 탑재되어 있기 때문이다.
>
> 중요한 자료가 들어있는 서버를 외부에 공개하지 않게 하기 위해서 중간에 방화벽을 두어서 보호한다. 하지만, 방화벽 내부의 컴퓨터는 인터넷에 접속할 수 있도록 해줘야 하기에 방화벽에 NAT를 탑재하여, 외부로 통신 가능하도록 열어 준다.
>



## 포트포워딩

* 특정 포트로 들어온 요청을 다른 특정 IP의 특정 포트로 전달한다.
* 포트 포워딩은 원격 컴퓨터가 근거리 통신망(LAN) 내에 위치한 특정 컴퓨터나 서비스에 연결할 수 있게 한다.

> 포트 포워딩(port forwarding) 또는 포트 매핑(port mapping)은 컴퓨터 네트워크에서 패킷이 라우터나 방화벽과 같은 네트워크 게이트웨이를 가로지르는 동안 하나의 IP 주소와 포트 번호 결합의 통신 요청을 다른 곳으로 넘겨주는 네트워크 주소 변환(NAT)의 응용이다. 이 기법은 게이트웨이(외부망)의 반대쪽에 위치한 보호/내부망에 상주하는 호스트에 대한 서비스를 생성하기 위해 흔히 사용되며, 통신하는 목적지 IP 주소와 포트 번호를 내부 호스트에 다시 매핑함으로써 이루어진다.