---

copyright:
  years: 1994, 2017-2019
lastupdated: "2019-03-06"

keywords: Use SSL VPN Navigate, private IP address, private VLAN

subcollection: iaas-vpn

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# SSL VPN 사용
{:#use-ssl-vpn}

1. 탐색 메뉴에서 **지원 > SSL VPN 로그인**을 선택하여 고객 포털의 **SSL VPN 로그인** 링크로 이동한 후 인증 정보를 입력하십시오.
2. 작업 표시줄에서 "A"가 표시되면 SSL VPN 터널이 구축되었습니다.
3. 축하합니다. 이제 사설 VLAN에 있습니다.

## 이제 연결되었습니다. 무엇을 합니까?
{:#now-im-connected-what-do-i-do}

1. SSH 또는 RDC(터미널 서비스)를 사용하여 서버 관리를 위한 사용자 서버의 사설 IP 주소(10.x.x.x)에 연결하십시오.
2. 원격 콘솔 또는 다시 부팅 기능을 이용하려면 SuperMicro 소프트웨어를 통해 IPMI 2.0 카드에 연결하십시오. 다운로드 지시사항에 대해서는 [고객 포털 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/)을 참조하십시오.
3. 드라이브를 서버에 맵핑하거나(Windows) 드라이브를 서버에 마운트(Red Hat)할 수 있습니다.

## 팁과 요령
{:#ssl-vpn-tips-tricks}

1. IPMI IP 및 사설 IP는 한 숫자가 떨어져 있습니다. 혼합하지 마십시오.
2. SSH 또는 RDC를 사용하여 IPMI 카드에 연결할 수 없습니다. 소프트웨어를 사용해야 합니다.
3. IPMI IP 및 사설 IP가 각 **서버** 아래의 하드웨어 섹션에서 발견됩니다.
4. IPMI 카드는 사설 IP 인터페이스에서 "청취"하며 IPMI 트래픽을 IPMI 카드로 경로 재지정합니다.

## 제품별 IPMI 지시사항
{:#product-specific-impi-instructions}

* CIFS 공유에서 IPMI를 사용하는 데 관한 자세한 정보는 [Bare Metal Server에 ISO 마운트](/docs/bare-metal?topic=bare-metal-option-1-preferred-using-ipmi-iso-on-a-cifs-share-#option-1-preferred-using-ipmi-iso-on-a-cifs-share-)를 참조하십시오.
* VMWare와 IPMI를 사용하는 데 관한 자세한 정보는 [원격 콘솔 및 가상 매체를 통해 VMware vSphere ESXi 설치](/docs/infrastructure/vmware?topic=VMware-installing-vsphere-esxi)를 참조하십시오.

* IBM POWER 하드웨어와 IPMI를 사용하는 데 관한 자세한 정보는 [IPMItool 설치](https://www.ibm.com/support/knowledgecenter/TI0003H/p8eih/p8eih_ipmitool.htm)를 참조하십시오.

**경고:**

`eth0`(사설 네트워크 인터페이스)을 사용 안함으로 설정하는 경우 모니터링, 원격 콘솔, 원격 다시 부팅 등을 포함한 모든 IPMI 기능을 잃게 됩니다. 사설 인터페이스에 대한 액세스를 잠그려는 경우, IP 테이블 또는 서버 방화벽에 입력할 수 있는 허용되는 IP 주소의 목록을 참조하십시오.
