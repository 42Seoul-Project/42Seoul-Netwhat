# 42Seoul-Netwhat

## 소개
* 네트워크를 이해하고 내부 동작에 대해 알아보자.
* 이를 통해 일상 생활에서 이미 어떻게 사용되고 동작하는지 이해할 수 있다. 

## 목차
* [1. IP주소란?](#-1-ip주소란)
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

## 1. IP주소란?
* IP주소란 집주소와 같이 특정한 컴퓨터의 위치를 특정하는 '일종의 주소'와 같은 것이다.
* 네트워킹이 가능한 장비를 식별하는 주소를 우리는 IP주소라고 말한다.
* 네트워크상에서 통신을 하기 위해서는 몇가지 통신규약(Protocol)을 따라야 하는데, 그러한 규약들 중에는 네트워킹을 하는 장비들에게 숫자 12개의 고유한 주소를 주어서 그 주소로 통신을 할 상대를 구분하는데 그 숫자 12개가 IP주소이다.
* 네트워크 주소 + 호스트로 구성이 되어있다.
* xxx.xxx.xxx.xxx.으로 표현이 되어있다.
* 기존 IPv4의 주소는 32자리 2진수이므로 약 40억개에 달하는 ip주소가 있지만 요즘 개인 한 사람이 네트워킹이 가능한 장비를 2~3개 이상을 가지게 되자 ip주소의 개수가 부족하게 되어 나온것이 IPv6이다.

## 2. Netmask란?
* Netmask란 하나의 네트워크를 몇 개의 네트워크로 나누어 사용할 때에 나눠진 각각의 네트워크를 구분하기 위해 사용하는 특수한 bit를 의미한다. 정환한 표현은 'Subnet Mask'이다.
* 하나의 네트워크를 여러개의 네트워크로 분리하는 이유는 트래픽부하는 줄이기 위함이며, 나눠진 각각 네트워크는 독립된 네트워크 구성이 가능하다. 결국 Netmask는 하나의 네트워크를 2개 이상의 네트워크로 나눠 사용할 때 각각의 네트워크를 구분할 수 있도록 해주는것이다.

## 2. Netmask가 있는 IP주소의 subnet은 무엇인가?
* Subnet이 사전적의미는 특정 지역에서 관리되는 IP영역을 몇 개의 영역으로 나누어서 관리하는것을 말한다.
* 한 클래스에서 한 호스트가 지나치게 많은 트개픽을 차지해서 다른 영역의 호스트까지 영향을 끼치게 될 때, 관리하는것이 상당히 힘들다. 이럴 경우 같은 클래스에 있는 호스트들이라 할지라도 관리상의 목적으로 서로 나누어서 관리하게 되면 훨씬 관리하기가 편해진다. 결국 커다란 하나의 호스트영역을 관리하는것이 아닌 목적에 따라서 여러개로 나누어서 관리하자는 의미다.
* Netmask는 인터넷상에서 서브넷이 필요하지 않는 경우 사용되는 마스크로 어떤 비트들이 net영역이며, 어떤부분이 host영역인지를 계산하기 위해 사용이 된다. 
* subnet의 구성은 mask의 비트를 어떻게 조작하냐에 따라 결정이 되며 만약 255.255.255.128로 subnet mask의 bit를 확장시켰다면 2^1(2)개의 서브넷 네트워크를 구성할 수 있다.
* 예시로 C클리스 영역을 가지며 네트워크 주소가 203.211.5.0 일 때, 서브넷마스크를 255.255.255.128로 하였다면 각각 사용가능한 호스트주소의 범위가 203.211.5.1 ~ 203.211.5.128, 203.211.5.129 ~ 203.211.5.254인 2개의 서브네트워크를 구성할 수 있다.
* 만약 4개의 서브네트워크로 구성한다면 서브넷마스크를 11111111.11111111.11111111.11000000과 같이 설정햐주면 된다.

## 3. subnet의 broadcast주소는 무엇인가?
