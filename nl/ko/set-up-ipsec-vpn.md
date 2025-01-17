---

copyright:
  years: 1994, 2017-2019
lastupdated: "2019-03-06"

keywords: IPSec VPN, IP address, IP traffic

subcollection: iaas-vpn

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# IPSec VPN 설정
{:#setup-ipsec-vpn}

## IPSec VPN의 개념
{:#what-is-ipsec-vpn}

IPSec는 암호화된 사이트간 네트워크를 제공하는 터널 모드를 사용하여 두 위치 사이의 모든 IP 트래픽을 인증 및 암호화하기 위해 디자인된 프로토콜 모음입니다. 보안 데이터가 그렇지 않으면 비보안으로 간주될 네트워크를 통해 이동하도록 허용합니다.   IPSec에 관한 추가 일반 정보에 대해서는 [참조 문서](/docs/infrastructure/iaas-vpn?topic=VPN-external-reference-documentation)를 참조하십시오.


IBM Cloud의 VPN 액세스를 사용하면 사용자가 IBM Cloud의 사설 네트워크를 통해 모든 서버를 원격으로 안전하게 관리할 수 있습니다.  사용자 위치에서 사설 네트워크로의 VPN 연결은 암호화된 VPN 터널을 통한 대역 외 관리 및 서버 복구 기능을 제공합니다.  VPN 액세스를 사용하여 다음을 수행할 수 있습니다.

   * SSL 또는 IPSEC를 통해 사설 네트워크로의 VPN 연결 설정
   * SSH 또는 RDP를 통해 사설 10.x.x.x IP 주소를 통해 서버 액세스
   * 추가 서버 관리 또는 복구 요구를 위해 서버의 IPMI IP 주소에 연결

환경 관리를 위해 고객에게 IPSec 서비스를 제공합니다. 프로덕션 워크로드에는 권장되지 않습니다.


## IPSec 연결 설정
{:#setup-ipsec-connection}

### 협상 매개변수
{:#setup-ipsec-vpn-negotiation-parameters}
![협상 매개변수](images/IPSec_VPN.png)

IPSec VPN의 원격 측에 대한 다음 정보를 알아야 합니다.
- VPN 엔드포인트의 정적 IP 주소
- 사전 공유 키(비밀번호)
- 암호화 알고리즘(DES, 3DES, AES128, AES192, AES256)
- 인증(MD5, SHA1, SHA256, 단계 1&2의 경우)
- Diffie-Hellman 그룹(단계 1&2의 경우)
- PFS(perfect Forward Secrecy) 사용 여부
- 키 수명 시간(단계 1 & 2의 경우) - **참고:** 본 시스템은 이 값을 초 단위로 측정합니다.

이 정보가 사용 가능하면 VPN 연결의 기본 협상 매개변수를 구성할 수 있습니다.

### 보호 네트워크
{:#setup-ipsec-vpn-protected-networks}

VPN 연결 특성에서, 터널에 대한 로컬 네트워크뿐 아니라 터널의 원격 측에 있는 네트워크도 정의해야 합니다. “보호 고객(원격) 서브넷”에서, IPSec 터널의 원격(비IBM) 끝에 대한 사설 IP 주소 공간을 CIDR 표기법으로 입력하십시오.

<span style="text-decoration: underline">예를 들어,</span> 터널의 원격 끝에 있는 네트워크가 넷마스크 255.255.255.0을 갖는 단일 서브넷 10.0.0.0을 사용하는 경우 “보호 고객(원격) 서브넷” 섹션에 대해 IP 주소 10.0.0.0 / CIDR 24를 입력해야 합니다.

### 네트워크 주소 변환(NAT)
{:#setup-ipsec-vpn-nat}

IPSec VPN을 사용하면 트래픽을 VPN 연결의 다른 쪽 끝에 있는 원격 서브넷으로 라우트하는 {{site.data.keyword.BluSoftlayer_notm}} 네트워크에서 사설 IP 주소를 정의할 수도 있습니다.  그러면 원격 위치를 전체 인터넷 액세스에 노출시키지 않고 사설 인터넷 트래픽이 VPN 뒤에 있는 머신의 내부 IP 주소 중 하나로 전달될 수 있습니다.  

### 네트워크 주소 변환/지정된 정적 NAT 서브넷
{:#setup-ipsec-vpn-nat-static-subnets}

정적 NAT 항목을 갖는 원격 VPN IP를 구성하려면 다음을 수행하십시오. 

 * 빨간색 화살표를 선택하여 **지정된 정적 NAT 서브넷** 섹션에 서브넷 목록을 표시하십시오. 서브넷의 각 IP가 표시됩니다.  
 * **고객 IP** 열에 VPN 연결의 원격 끝에 있는 IP를 입력하고 **이름** 열에 맵핑에 대한 이름을 입력하십시오.  
 * **컨텍스트 주소 변환 추가/수정** 및 **구성 적용**을 선택하여 구성을 저장하고 적용하십시오.
 
이 조치는 리턴 트래픽에 대한 정적 일대일 네트워크 변환을 설정하는데, 이것은 IBM Cloud VPN 집선기 뒤에 있는 호스트가 원격 VPN 피어 뒤에 있는 호스트와 통신하는 데 사용됩니다. 예를 들어, IP 10.1.255.92에 대한 모든 트래픽이 변환되어 고객의 IP 192.168.10.15로 전달됩니다. 이 전달은 IBM Cloud 서버에서 추가 라우트 항목이 필요없게 만듭니다.
