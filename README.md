# 42Seoul-Netwhat

## 소개
* 네트워크를 이해하고 내부 동작에 대해 알아보자.
* 이를 통해 일상 생활에서 이미 어떻게 사용되고 동작하는지 이해할 수 있다. 

## 목차
* IP주소란?
* Netmask란?
* Netmask가 있는 IP주소의 subnet은 무엇인가?
* subnet의 broadcast주소는 무엇인가?
* Public IP와 Private IP의 차이점
* IP주소 class란 무엇인가?
* TCP란?
* UDP란?
* 네트워크계층이란 무엇인가?
* OSI모델이란 무엇인가?
* DHCP서버 및 DHCP프로토콜이란 무엇인가?
* DNS서버 및 DNS프로토콜이란 무엇인가?
* 2개의 장치가 IP주소를 사용하여 통신하도록 하는 규칙은 무엇인가?
* 라우팅과 IP는 어떻게 동작하는가?
* 라우팅을 위한 기본 게이트웨이는 무엇인가?
* IP관점의 포트는 무엇이고 다른장치에 연결할 때 사용되는 포트는 무엇인가?

## 1. IP주소란? (Internet Protocal Version 4/6)
* IP주소란 집주소와 같이 특정한 컴퓨터의 위치를 특정하는 '일종의 주소'와 같은 것이다.
* 네트워킹이 가능한 장비를 식별하는 주소를 우리는 IP주소라고 말한다.
* 네트워크상에서 통신을 하기 위해서는 몇가지 통신규약(Protocol)을 따라야 하는데, 그러한 규약들 중에는 네트워킹을 하는 장비들에게 숫자 12개의 고유한 주소를 주어서 그 주소로 통신을 할 상대를 구분하는데 그 숫자 12개가 IP주소이다.
* 네트워크 주소 + 호스트로 구성이 되어있다.
* xxx.xxx.xxx.xxx.으로 표현이 되어있다.
  * xxx의 범위는 0 ~ 255 (총 256 = 2^8 = 8bit)
* 기존 IPv4의 주소는 32자리 2진수이므로 약 40억개에 달하는 ip주소가 있지만 요즘 개인 한 사람이 네트워킹이 가능한 장비를 2~3개 이상을 가지게 되자 ip주소의 개수가 부족하게 되어 나온것이 IPv6이다.
  * IPv4의 총 사이즈는 32bit
  * IPv6의 총 사이즈는 128bit
* localhost의 IP주소는 127.0.0.1이다.

## 2. Netmask란?
* 네트워크 주소 부분의 비트를 1로 치환한것.
* IP주소와 넷마스크를 AND연산하면 네트워크 주소를 얻을수가 있다.
* Netmask란 하나의 네트워크를 몇 개의 네트워크로 나누어 사용할 때에 나눠진 각각의 네트워크를 구분하기 위해 사용하는 특수한 bit를 의미한다. 정환한 표현은 'Subnet Mask'이다.
* 하나의 네트워크를 여러개의 네트워크로 분리하는 이유는 트래픽부하는 줄이기 위함이며, 나눠진 각각 네트워크는 독립된 네트워크 구성이 가능하다. 결국 Netmask는 하나의 네트워크를 2개 이상의 네트워크로 나눠 사용할 때 각각의 네트워크를 구분할 수 있도록 해주는것이다.

## 3. Netmask가 있는 IP주소의 subnet은 무엇인가?
* 기본 서브넷 마스크(Default Subnet Mask)
  * A클래스 : 255.0.0.0
    * 표기법 예시 : 10.1.2.30/8 "/8"부분
  * B클래스 : 255.255.0.0
    * 표기법 예시: 128.1.2.30/16 "/16"부분
  * C클래스 : 255.255.255.0
    * 표기법 예시 : 192.168.0.2/24 "/24"부분

## CIDR (Classless Inter-Domain Routing, 사이더)
* 클래스없는 도메인 간 라우팅 기법(기존의 IP클래스로 네트워크 구분을 하지 않음)
* 부족해지는 IPv4주소를 효율적으로 사용하기 위해 고안된 방법
* 사이더 표기법 / 넷마스크도 다음과 같이 표기한다.
  * 사이더와 서브넷 마스크의 차이 : 사이더는 가변길이 서브넷 마스크를 사용한다. 기존의 클래스 구분으로 서브넷 마스크를 나눈 것이 아님.
  * 표기법 예시 : 192.168.10.2/24 "/24"부분
  * 비트를 의미하며 0 ~ 32 까지 표현이 가능하다.
  * 해당 비트부분이 네트워크 영역이라는 의미다. 전체 비트의 24bit가 네트워크 영역이므로 실제 사용가능한 호스트 영역은 8bit인데 총 2^8 = 256개에서 - 2(예약된 주소)개를 뺀 254개가 사용 가능하다.

## 4. subnet의 broadcast주소는 무엇인가?
* 특정 네트워크에 속하는 모든 호스트들이 갖게되는 주소.
* 네트워크에 있는 모든 클라이언트들에게 데이터를 보내기 위함.
* 해당 서브넷의 마지막주소이다.
* 네트워크 영역을 제외한 호스트 영역에서 모든 비트가 1인 주소

## 5. Public IP와 Private IP의 차이점
* 공인 IP주소는 인터넷과 같은 공인 환경에 직접 연결이 가능한 주소를 말한다. 즉 인터넷을 하기 위해서는 공인 IP주소가 필요하며 이 주소는 ISP업체로부터 임대를 받아서 사용해야한다.
  * 우리나라는 인터넷진흥원(KISA)에서 우리나라 내 사용 주소를 관리하고 있다.
* 사설 IP주소는 공인환경이 아닌 기업 내부 사설 환경에서 사용을 권장하는 주소이다. 이 주소는 인터넷과 연결되지 않기 때문에 WAN 구간을 연결하는 Router는 사설 IP주소를 외부로 전송할 수 없다.
  * 가정이나, 소규모 사무공간에서 공유기/라우터 등의 장비가 하나의 공인 IP를 할당 받고 NAT방식으로 여러 컴퓨터에게 나누어 줄 때의 주소이다.
* 사설 IP주소 특징
  * A클래스 : 10.xxx.xxx.xxx
  * B클래스 : 172.16.xxx.xxx로 보통 되어 있으며 범위는 다음과 같다. 172.16.0.0 ~ 172.31.255.255까지
  * C클래스 : 192.168.xxx.xxx

## 6. IP주소 class란 무엇인가?
* class : 네트워크 영역과 호스트 영역을 나누는 방법
  * 하나의 네트워크 안에서 IP주소의 네트워크 영역은 같고 호스트 영역이 달라야 통신이 가능하다.
* 각 클래스별 네트워크 영역, 호스트
  * A클래스 : 0 ~ 127 | 0.0.0 ~ 255.255.255 | 2진수 시작 범위 : 0SSS SSSS.hhhh hhhh.hhhh hhhh.hhhh hhhh | 네트워크 수 : 2^7 - 1 | 호스트 범위 : 2^24 - 2
  * B클래스 : 128.0 ~ 191.255 | 0.0 ~ 255.255 | 2진수 시작 범위 : 10SS SSSS.SSSS SSSS.hhhh hhhh.hhhh hhhh | 네트워크 수 : 2^14 | 호스트 범위 : 2^16 - 2
  * C클래스 : 224.0.0 ~ 223.255.255 | 0 ~ 255 | 2진수 시작 범위 : 110S SSSS.SSSS SSSS.SSSS SSSS.hhhh hhhh | 네트워크 수 : 2^22 | 호스트 범위 : 2^8 - 2
* 총 5개의 클래스로 정의되지만 위의 3개 A, B, C를 제외한 D, E는 일반 사용자가 대개 사용하지 않는다.
* 위와 같이 클래스로 정의됨으로써 IP주소 낭비방지와 효율적인 서브넷 관리가 가능하다.
* 각 주소 클래스는 서로 다른 기본 서브넷 마스크를 가지고 있다.
* 첫 번째 옥텟을 보면 IP주소의 클래스를 식별할 수 있다.

## 7. TCP란? 
* Transmission Control Protocol, 전송 제어 프로토콜
* 세그먼트가 TCP 프로토콜 데이터 유닛을 의미하는 정확한 표현이다.
* 연결 지향적이다.
  * 데이터를 주고 받을 양단 간에 먼저 연결을 설정하고 양방향으로 데이터를 전송한다.
* 안정적이다.
* 순서대로 전송된다.
* 에러없이 교환한다.
  * 흐름제어, 오류제어, 혼잡제어를 지원한다.
* 패킷 전달 여부를 보증해준다.
  * 확인응답을 수신하기 전까지 버퍼에 계속 보관한다.
  * 일대다 통신을 못한다. 일대다 통신은 IP에서 UDP(브로드캐스팅, 멀티캐스팅, 유니캐스팅도 가능)만 가능
  * 유니캐스팅(일대일 통신)가능
* 사용처
  * 웹 브라우저들이 월드 와이드 웹에서 서버에 연결할 때 사용
  * 이메일 전송 및 파일 전송 등
  
## 8. UDP란?
* User Datagram Protocol, 사용자 데이터그램 
* 연결을 설정하지 않고 단방향으로 정보를 전송한다.
* 데이터그램으로 알려진 단문 메시지를 교환하기 위해서 사용된다.
* 서비스의 신뢰성아 낮다.
  * 수신자가 수신했는지 확인할 수 없기 때문에
* 도착 순서가 바귀거나, 중복되거나, 누락되기도 한다.
  * 메시지 도착 순서를 예측할 수가 없다.
* 속도가 일반적으로 빠르고 오버헤드가 적다.
  * TCP는 신뢰성과 순서 정렬을 위한 기능이 들어가기 때문에 상대적으로 느릴 수 밖에 없다.
* 적인 오류 제어 기능은 제공한다.
* 사용처
  * 단일 요청으로만 구성되어 있는 DNS 
  * SNMP
  * DHCP (동적 호스트 구성 프로토콜)
  * RIP (라우팅 정보 프로토콜)

## 9.네트워크 계층이란 무엇인가?

## 10. OSI모델이란 무엇인가?
* OSI 7계층은 네트워크에서 통신이 일어나는 과정을 7단계로 나눈것을 말한다.
* 7계층으로 나누었을 때 흐름을 한눈에 알아보기가 쉬우며, 사람들이 이해하기 쉽고, 7단계 중 특정한 곳에 이상이 생기면 다른 단계의 장비 및 소프트웨어를 건들이지 않고도 이상이 생긴 단계만 고칠 수 있기 때문이다.
* OSI 7계층
  * 1계층 : 물리계층(Physical Layer)
  * 2계층 : 데이터 링크 계층(DataLink Layer)
  * 3계층 : 네트워크 계층 (Network Layer)
  * 4계층 : 전송 계층 (Transport Layer)
  * 5계층 : 세션 계층 (Session Layer)
  * 6계층 : 표현 계층 (Presentation Layer)
  * 7계층 : 응용 계층 (Application Layer)
* 보통 통신이 일어날 때 높은 계층 -> 낮은 계층(디캡슐화) -> 낮은 계층 -> 높은 계층(인캡술화) 순서로 간다.
  * 여기서 캡슐화는 높이 올라갈수록 마트료시카처럼 겹겹이 붙고 아래로 내려갈수록 붙은걸 다시 떼어주는걸 말한다.
  
## 11. DHCP서버 및 DHCP프로토콜이란 무엇인가?
* DHCP(Dynamic Host Configuration Protocol) 동적 호스트 구성 프로토콜
  * IP구성을 자동화하는 매커니즘을 구현할 때 사용하는 프로토콜
* DHCP를 사용하지 않게 된다면?
  * 각 컴퓨터마다 IP주소가 수작업으로 입력되어야 한다.
  * 네트워크가 변동이 생기면 IP주소를 새로이 입력해야 핝다.
* 전송계층에서 UDP프로토콜을 사용한다.
  * DHCP의 동작원리를 보면 왜 사용하는지 알 수 있다.
* DHCP동작원리 
  * DHCP Discover -> DHCP Offer -> DHCP Request -> DHCP Ack
  * UDP를 기반으로 하는 일대다 통신으로 브로드캐스팅을 사용한다.

## 12. DNS서버 및 DNS프로토콜이란 무엇인가?
* DNS(Domain Name System)
  * 사람이 읽을 수 있는 도메인 이름을 컴퓨터가 읽는 IP주소로 변환해주는 시스템이다. 혹은 그 반대도 가능하다.
* DNS 서버
  * 도메인 이름과 해당 도메인의 IP주소를 DNS레코드라고 하는데 이를 저장하고 있는 서버이다.
  * 우리가 인터넷에 도메인 이름(www.naver.com)을 친다면 웹 브라우저는 DNS서버에 해당 도메인의 IP주소를 요청하게 된다. 그럼 서버는 요청에 맞는 응답을 보내고 그렇게 최종적으로 네이버가 보여지게 되는 것이다.

## 13. 2개의 장치가 IP주소를 사용하여 통신하도록 하는 규칙은 무엇인가?
* 프로토콜 IP(Internet Protocol)

## 14. 라우팅과 IP는 어떻게 동작하는가?

## 15. 라우팅을 위한 기본 게이트웨이는 무엇인가?

## 16. IP관점의 포트는 무엇이고 다른장치에 연결할 때 사용되는 포트는 무엇인가?

## 17. 추가 자료
* [정리 잘된 곳1](https://www.notion.so/netwhat-f16994257d49440eacc07f8ecf7bb3ce)
