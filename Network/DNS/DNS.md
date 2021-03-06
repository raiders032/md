## IP 주소

* 컴퓨터 네트워크에서 장치들이 서로를 인식하고 통신을 하기 위해서 사용하는 특수한 번호이다.
* 네트워크에 연결된 장치가 라우터이든 일반 서버이든, 모든 기계는 이 특수한 번호를 가지고 있어야 한다.



___



## domain

> ip는 사람이 이해하고 기억하기 어렵기 때문에 이를 위해서 각 ip에 이름을 부여할 수 있게 했는데, 이것을 도메인이라고 합니다.
>
> 넓은 의미로는 네트워크상에서 컴퓨터를 식별하는 호스트명을 가리키며, 좁은 의미에서는 도메인 레지스트리에게서 등록된 이름을 의미합니다.

**도메인 이름의 구조**

![image-20210419230348508](/Users/YT/GoogleDrive/dev/TIL/Network/DNS/images/image-20210419230348508.png)

* root domain : .

* Top-level domain: .com

* Second-level domain: example

* Sub domain: blog

  

___



## Host

> 네트워크에 연결된 장치(컴퓨터, 서버 등)들에게 부여되는 고유한 이름이다. 도메인과 유사하지만 더 넓은 의미를 가지고 있다. 
>
> 인터넷에서 호스트 이름은 인터넷에 연결된 호스트(컴퓨터)의 이름으로, 보통 호스트의 지역 이름에 도메인 이름을 붙인 것이다.
>
> 예를 들면, www.naver.com (웹 서버), mail.naver.com (메일 서버) 와 같이 네이버에서 사용되는 모든 호스트 이름에 naver.com이란 도메인 이름이 붙는다.



### 호스트 설정

> domain과 IP를 연결하는 행위



### 포워딩 설정

> domain을 다른 domain이나 다른 IP로 보내는 과정



### 네임서버

> domain에 대응되는 IP를 알려주는 서비스.



___

## hosts 파일

> hosts 파일은 운영 체제가 호스트 이름을 IP 주소에 매핑할 때 사용하는 컴퓨터 파일이다.

**위치**

* mac : /etc/hosts
* Window : [%SystemRoot%](https://ko.wikipedia.org/wiki/환경_변수)\System32\drivers\etc\hosts 

**예시**

```txt
127.0.0.1  localhost loopback
::1        localhost
```



___



## Domain Name System

> DNS(Domain Name System)는 인터넷 전화번호부입니다. 사람은 nytimes.com 또는 espn.com과 같은 도메인 이름을 통해 온라인으로 정보에 액세스합니다. 웹 브라우저는 인터넷 프로토콜(IP) 주소를 통해 상호작용합니다. DNS는 브라우저가 인터넷 자원을 로드할 수 있도록 도메인 이름을 IP 주소로 변환합니다.
>
> DNS 확인 프로세스에는 호스트 이름(예: www.example.com)을 컴퓨터 친화적인 IP 주소(예: 192.168.1.1)로 변환하는 과정이 포함됩니다. IP 주소는 인터넷의 각 기기에 제공되며, 거리 주소가 특정한 집을 찾는 데 사용되는 것처럼, 적절한 인터넷 기기를 찾기 위해서는 IP 주소가 필요합니다. 사용자가 어떤 웹페이지를 로드하려고 할 때에는, 사용자가 웹브라우저에 입력한 내용(예: example.com)을 example.com 웹페이지를 찾는 데 필요한 컴퓨터 친화적 주소로 변환해야 합니다.



## 웹 페이지 로딩에는 4개의 DNS 서버가 관련됩니다.

**DNS 리커서**(DNS Server/ Local DNS)

>   리커서는 도서관의 어딘가에서 특정한 책을 찾아달라고 요청받는 사서로 생각할 수 있습니다. DNS 리커서는 웹 브라우저 등의 애플리케이션을 통해 클라이언트 컴퓨터로부터 쿼리를 받도록 고안된 서버입니다. 
>
>  재귀 확인자(DNS 리커서라고도 함)는 DNS 쿼리의 첫 단계입니다. 재귀 확인자는 클라이언트와 DNS 네임서버 사이의 중개자 역할을 합니다. 재귀 확인자는 웹 클라이언트로부터 DNS 쿼리를 받은 후 캐시된 데이터로 응답하거나 요청을 루트 네임서버로 보내고 또 다른 요청을 TLD 네임서버로 보낸 후 마지막 요청을 권한 있는 네임서버로 보냅니다. 재귀 확인자는 요청된 IP 주소가 있는 권한 있는 네임서버로부터 응답을 받은 후 응답을 클라이언트에 보냅니다.
>
>  대부분의 인터넷 사용자는 ISP에서 제공하는 DNS server를 사용하지만 아래와 같은 퍼블릭 DNS server를 이용하도록 설정할 수 있습니다.
>
>  <img src="./images/image-20210419225940424.png" alt="image-20210419225940424" style="zoom:50%;" />
>
>  - [Cisco OpenDNS](https://www.opendns.com/setupguide/): 208.67.222.222 and 208.67.220.220;
>  - [Cloudflare 1.1.1.1](http://1.1.1.1/): 1.1.1.1 and 1.0.0.1;
>  - [Google Public DNS](https://dns.google.com/): 8.8.8.8 and 8.8.4.4; and
>  - [Quad9](https://www.quad9.net/): 9.9.9.9 and 149.112.112.112.

**루트 네임 서버**

> 3개의 DNS 루트 네임서버가 모든 재귀 확인자에 알려져 있으며 이들은 재귀 확인자가 DNS 레코드를 요청하는 과정의 첫 단계입니다. 루트 서버는 도메인 이름을 포함한 재귀 확인자의 쿼리를 수용하며 루트 네임서버는 해당 도메인의 확장자(.com,. net, .org, etc.)에 따라 재귀 확인자를 TLD 네임서버에 보내 응답합니다. 
>
> * 루트 네임서버는 비영리 단체인 ICANN(Internet Corporation for Assigned Names and Numbers)이 관리합니다

**TLD 네임 서버**(Top-level Domain)

> TLD 네임서버는 .com, .net 또는 URL의 마지막 점 뒤에 오는 것 같은 일반적인 도메인 확장자를 공유하는 모든 도메인 이름의 정보를 유지합니다. 예를 들어 TLD 네임서버는 ‘.com’으로 끝나는 모든 웹사이트의 정보를 갖고 있습니다. 사용자가 google.com을 검색하는 경우 재귀 확인자는 루트 네임서버로부터 응답을 받은 후 쿼리를 .com TLD 네임서버에 보내고, 해당 네임서버는 해당 도메인의 권한 있는 네임서버를 가리켜 응답합니다.
>
> - 일반 최상위 도메인: 국가별로 고유하지 않은 도메인으로, 가장 잘 알려진 일반적인 TLD에는 .com, .org, .net, .edu 및 .gov가 있습니다.
> - 국가 코드 최상위 도메인: 여기에는 국가 또는 주와 관련된 모든 도메인이 포함됩니다. 예로는 .uk, .us, .ru 및 .jp가 포함됩니다.
> - TLD 네임 서버는 Registry(등록소)가 관리합니다.
>   - 예) .com, .net TLD 네임 서버는 VeriSign Global Registry Services 라는 기업이 관리한다.

**authoritative 네임 서버**(권한 있는 네임 서버)

>  재귀 확인자가 TLD 네임서버로부터 응답을 받으면, 확인자는 해당 응답을 권한 있는 네임서버로 보냅니다. 일반적으로 권한 있는 네임서버는 IP 주소를 확인하는 확인자의 마지막 단계입니다. 권한 있는 네임서버는 도메인 이름에 고유한 정보(예: google.com)를 포함하며 DNS A 레코드에서 찾은 도메인의 IP 주소를 재귀 확인자에 제공하거나, 도메인에 CNAME 레코드(별칭)가 있는 경우 재귀 확인자에 별칭 도메인을 제공하며, 이 때 재귀 확인자는 권한 있는 네임서버에서 레코드(종종 IP 주소를 포함하는 A 레코드)를 얻기 위해 완전히 새로운 DNS 조회를 수행해야 합니다
>
>  * 보통 권한 있는 네임 서버를 직접 구축하지않고 Registrar(등록대행자)가 제공하는 권한 있는 네임 서버를 사용한다.
>  * Registrar(등록대행자)
>    * 예) 가비아



## 브라우저가 도메인에 해당하는 IP를 찾는 순서

![how-route-53-routes-traffic](./images/123.png)

1. 사용자가 웹 브라우저를 열어 주소 표시줄에 www.example.com을 입력하고 Enter 키를 누릅니다.
2. www.example.com에 대한 요청은 일반적으로 케이블 인터넷 공급업체, DSL 광대역 공급업체 또는 기업 네트워크 같은 인터넷 서비스 제공업체(ISP)가 관리하는 DNS 해석기로 라우팅됩니다.
3. ISP의 DNS 해석기는 www.example.com에 대한 요청을 DNS 루트 이름 서버에 전달합니다.
4. ISP의 DNS 해석기는 www.example.com에 대한 요청을 이번에는 .com 도메인의 TLD 이름 서버 중 하나에 다시 전달합니다. .com 도메인의 이름 서버는 example.com 도메인과 연관된 4개의 Amazon Route 53 이름 서버의 이름을 사용하여 요청에 응답합니다.
5. ISP의 DNS 해석기는 Amazon Route 53 이름 서버 하나를 선택해 www.example.com에 대한 요청을 해당 이름 서버에 전달합니다.
6. Amazon Route 53 이름 서버는 example.com 호스팅 영역에서 www.example.com 레코드를 찾아 웹 서버의 IP 주소 192.0.2.44 등 연관된 값을 받고 이 IP 주소를 DNS 해석기로 반환합니다.
7. ISP의 DNS 해석기가 마침내 사용자에게 필요한 IP 주소를 확보하게 됩니다. 해석기는 이 값을 웹 브라우저로 반환합니다. 또한, DNS 해석기는 다음에 누군가가 example.com을 탐색할 때 좀 더 빠르게 응답할 수 있도록 사용자가 지정하는 일정 기간 동안 example.com의 IP 주소를 캐싱(저장)합니다. 자세한 내용은 TTL(Time to Live)을 참조하십시오.
8. 웹 브라우저는 DNS 해석기로부터 얻은 IP 주소로 www.example.com에 대한 요청을 전송합니다. 여기가 콘텐츠가 있는 곳으로, 예를 들어 웹 사이트 엔드포인트로 구성된 Amazon S3 버킷 또는 Amazon EC2 인스턴스에서 실행되는 웹 서버입니다.
9. 192.0.2.44에 있는 웹 서버 또는 그 밖의 리소스는 www.example.com의 웹 페이지를 웹 브라우저로 반환하고, 웹 브라우저는 이 페이지를 표시합니다.



참조

* [생활코딩](https://www.youtube.com/watch?v=zrqivQVj3JM&list=PLuHgQVnccGMCI75J-rC8yZSVGZq3gYsFp&index=1)
* https://aws.amazon.com/ko/route53/what-is-dns/
* https://www.cloudflare.com/ko-kr/learning/dns/dns-server-types/#authoritative-nameserver