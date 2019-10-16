---
title: 인터넷 프로토콜 버전 6
ms.date: 03/30/2017
helpviewer_keywords:
- IPv6, improvements
- IPv4
- IPv6
- Internet Protocol version 6, improvements
- Internet Protocol version 6
ms.assetid: e6fa8ebd-010a-4c48-a5ec-a5102c53c06f
ms.openlocfilehash: 367db4fa4e585d6066009dbd1afacb154829319a
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71047873"
---
# <a name="internet-protocol-version-6"></a>인터넷 프로토콜 버전 6
IPv6(인터넷 프로토콜 버전 6)은 인터넷 네트워크 계층에 대한 새로운 표준 프로토콜 도구 모음입니다. IPv6은 주소 고갈, 보안, 자동 구성, 확장성 등에 관련된 현재 버전 인터넷 프로토콜 도구 모음(IPv4라고 함)의 많은 문제를 해결하도록 설계되었습니다. IPv6은 피어 투 피어 및 모바일 애플리케이션을 포함한 새로운 종류의 애플리케이션을 구현하기 위해 인터넷 기능을 확장합니다. 현재 IPv4 프로토콜의 주요 문제는 다음과 같습니다.  
  
- 주소 공간의 빠른 고갈.  
  
     이 문제로 인해 여러 개인 주소를 단일 공용 IP 주소에 매핑하는 NAT(Network Address Translator)를 사용하게 됩니다. 이 메커니즘에서 발생하는 주요 문제는 처리 오버헤드 및 엔드투엔드 연결 부족입니다.  
  
- 계층 구조 지원 없음.  
  
     고유의 미리 정의된 클래스 조직으로 인해 IPv4에는 실제 계층 구조 지원이 없습니다. 실제로 네트워크 토폴로지를 매핑하는 방식으로 IP 주소를 구조화할 수는 없습니다. 이 중대한 설계 결함으로 인해 IPv4 패킷을 인터넷의 임의 위치에 전달하기 위해 큰 라우팅 테이블이 필요하게 되었습니다.  
  
- 복잡한 네트워크 구성.  
  
     IPv4를 사용할 경우 주소를 정적으로 할당하거나 주소에 DHCP 등의 구성 프로토콜을 사용 중이어야 합니다. 이상적인 상황에서는 호스트가 DHCP 인프라의 관리에 의존할 필요가 없습니다. 대신에 호스트는 배치되어 있는 네트워크 세그먼트를 기반으로 구성될 수 있습니다.  
  
- 기본 제공 인증 및 기밀성 없음.  
  
     IPv4의 경우 교환된 데이터에 대한 인증이나 암호화를 제공하는 메커니즘을 지원할 필요가 없습니다. 이 내용은 IPv6에서 변경됩니다. IPSec(인터넷 프로토콜 보안)는 IPv6 지원 요구 사항입니다.  
  
 새로운 프로토콜 도구 모음은 다음 기본 요구 사항을 충족해야 합니다.  
  
- 낮은 오버헤드가 발생하는 대규모 라우팅 및 주소 지정.  
  
- 다양한 연결 상황에 대한 자동 구성.  
  
- 기본 제공 인증 및 기밀성.  
  
 자세한 내용은 [IPv6 주소 지정](ipv6-addressing.md), [IPv6 라우팅](ipv6-routing.md), [IPv6 자동 구성](ipv6-auto-configuration.md), [IPv6 사용 및 사용 안 함](enabling-and-disabling-ipv6.md) 및 [방법: IPv6 지원을 사용하도록 컴퓨터 구성 파일 수정](how-to-modify-the-computer-configuration-file-to-enable-ipv6-support.md)을 참조하세요.  
  
## <a name="references"></a>참조  
 [IETF(Internet Engineering Task Force)](https://www.ietf.org/) 웹 사이트에서 찾을 수 있는 선택된 RFC 문서는 다음과 같습니다.  
  
- RFC 1287, Towards the Future Internet Architecture.  
  
- RFC 1454, Comparison of Proposals for Next Version of IP.  
  
- RFC 2373, IP Version 6 Addressing Architecture.  
  
- RFC 2374, An IPv6 Aggregatable Global Unicast Address Format.  
  
 또한 [IPv6(IP 버전 6)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379498%28v=ws.10%29)에서 IPv6 관련 정보를 찾을 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [IPv6 소켓 샘플](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.0/ms180981%28v=vs.85%29)
- [네트워크 프로그래밍 샘플](network-programming-samples.md)
- [소켓](sockets.md)
