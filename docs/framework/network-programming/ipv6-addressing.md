---
title: IPv6 주소 지정
ms.date: 03/30/2017
helpviewer_keywords:
- Internet Protocol version 6, addresses in
- Neighbor Discovery
- IPv6, enabling
- IPv6, mobility and
- Internet Protocol version 6, anycast addresses
- IPv6, Neighbor Discovery
- Internet Protocol version 6, auto-configuring
- Internet Protocol version 6, enabling
- IPv6, unicast addresses
- IPv6, auto-configuring
- Internet Protocol version 6, routing
- IPv6, RFC documents
- IPv6, routing
- Internet Protocol version 6, disabling
- Internet Protocol version 6, unicast addresses
- IPv6, multicast addresses
- Internet Protocol version 6, mobility and
- Internet Protocol version 6, RFC documents
- Internet Protocol version 6, Neighbor Discovery
- IPv6, anycast addresses
- Internet Protocol version 6, multicast addresses
- IPv6, addresses in
- IPv6, disabling
ms.assetid: 20a104ae-1649-4649-a005-531a5cf74c93
ms.openlocfilehash: ac8b8bae69ba20f34bb74fbff533ba53f915a150
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50183414"
---
# <a name="ipv6-addressing"></a>IPv6 주소 지정
IPv6(인터넷 프로토콜 버전 6)에서 주소의 길이는 128비트입니다. 주소 공간이 이렇게 큰 하나의 이유는 사용 가능한 주소를 인터넷 토폴로지를 반영하는 라우팅 도메인 계층 구조로 세분화하기 위한 것입니다. 또 다른 이유는 장치를 네트워크에 연결하는 네트워크 어댑터(또는 인터페이스)의 주소를 매핑하기 위한 것입니다. IPv6은 최하위 수준인 네트워크 인터페이스 수준에서 주소를 확인하는 고유한 기능과 자동 구성 기능을 제공합니다.  
  
## <a name="text-representation"></a>텍스트 표현  
 IPv6 주소를 텍스트 문자열로 표현하는 데 사용되는 세 가지 기존 형식은 다음과 같습니다.  
  
-   **콜론-16진수 형식**. 권장되는 형식인 n:n:n:n:n:n:n:n입니다. 각 n은 주소를 구성하는 8개의 16비트 요소 중 하나에 대한 16진수 값을 나타냅니다. 예: `3FFE:FFFF:7654:FEDA:1245:BA98:3210:4562`  
  
-   **압축된 형식**. 주소 길이 때문에 일반적으로 0으로 구성된 긴 문자열이 있는 주소를 포함합니다. 이러한 주소 작성을 간소화하려면 0 블록의 단일 연속 시퀀스를 이중 콜론 기호(::)로 표현하는 압축된 형식을 사용합니다. 이 기호는 주소에서 한 번만 표시될 수 있습니다. 예를 들어 압축된 형식의 멀티캐스트 주소 `FFED:0:0:0:0:BA98:3210:4562`는 `FFED::BA98:3210:4562`입니다. 압축된 형식의 유니캐스트 주소 `3FFE:FFFF:0:0:8:800:20C4:0`은 `3FFE:FFFF::8:800:20C4:0`입니다. 압축된 형식의 루프백 주소 `0:0:0:0:0:0:0:1`은 `::`1입니다. 압축된 형식의 지정되지 않은 주소 `0:0:0:0:0:0:0:0`은 `::`입니다.  
  
-   **혼합된 형식**. 이 형식은 IPv4 주소와 IPv6 주소를 결합합니다. 이 경우 주소 형식은 n:n:n:n:n:n:d.d.d.d입니다. 여기서 각 n은 6개의 IPv6 높은 순서 16비트 주소 요소의 16진수 값을 나타내고 각 d는 IPv4 주소의 10진수 값을 나타냅니다.  
  
## <a name="address-types"></a>주소 형식  
 주소의 선행 비트는 특정 IPv6 주소 형식을 정의합니다. 이러한 선행 비트가 포함된 가변 길이 필드를 FP(Format Prefix)라고 합니다.  
  
 IPv6 유니캐스트 주소는 두 부분으로 구분됩니다. 첫 번째 부분에는 주소 접두사가 포함되고 두 번째 부분에는 인터페이스 식별자가 포함됩니다. IPv6 주소/접두사 조합을 표시하는 간결한 방법은 다음과 같습니다. ipv6-address/prefix-length.  
  
 64비트 접두사가 포함된 주소의 예는 다음과 같습니다.  
  
 `3FFE:FFFF:0:CD30:0:0:0:0/64`.  
  
 이 예의 접두사는 `3FFE:FFFF:0:CD30`입니다. 주소는 압축된 형식으로 기록될 수도 있습니다(예: `3FFE:FFFF:0:CD30::/64`).  
  
 IPv6은 다음 주소 형식을 정의합니다.  
  
-   **유니캐스트 주소**. 단일 인터페이스의 식별자입니다. 이 주소에 전송된 패킷은 식별된 인터페이스에 전달됩니다. 유니캐스트 주소는 높은 순서 8진수 값으로 멀티캐스트 주소와 구별됩니다. 멀티캐스트 주소의 높은 순서 8진수에는 16진수 값 FF가 포함됩니다. 이 8진수 식별자의 다른 값은 유니캐스트 주소를 식별합니다. 다양한 형식의 유니캐스트 주소는 다음과 같습니다.  
  
    -   **링크-로컬 주소**. 이러한 주소는 단일 링크에서 사용되고 FE80::*InterfaceID* 형식을 사용합니다. 링크-로컬 주소는 자동 주소 구성, 네트워크 환경 검색을 위해 또는 라우터가 없는 경우 링크에서 노드 간에 사용됩니다. 링크-로컬 주소는 주로 시작 시 사용되고 시스템이 더 큰 범위의 주소를 아직 획득하지 못한 경우 사용됩니다.  
  
    -   **사이트-로컬 주소**. 이러한 주소는 단일 사이트에서 사용되고 FEC0::*SubnetID*:*InterfaceID* 형식을 사용합니다. 사이트-로컬 주소는 전역 접두사를 사용할 필요 없이 사이트 내에서 주소 지정에 사용됩니다.  
  
    -   **전역 IPv6 유니캐스트 주소**. 이러한 주소는 인터넷에서 사용될 수 있고 010(FP, 3비트) TLA ID(13 bits) Reserved(8비트) NLA ID(24비트) SLA ID(16비트) *InterfaceID*(64비트) 형식을 사용합니다.  
  
-   **멀티캐스트 주소**. 인터페이스 집합의 식별자입니다(일반적으로 서로 다른 노드에 속함). 이 주소에 전송된 패킷은 주소로 식별되는 모든 인터페이스에 전달됩니다. 멀티캐스트 주소 형식이 IPv4 브로드캐스트 주소보다 우선합니다.  
  
-   **애니캐스트 주소**. 인터페이스 집합의 식별자입니다(일반적으로 서로 다른 노드에 속함). 이 주소에 전송된 패킷은 주소로 식별되는 하나의 인터페이스에만 전달됩니다. 이 주소는 라우팅 메트릭으로 식별되는 가장 가까운 인터페이스입니다. 애니캐스트 주소는 유니캐스트 주소 공간에서 가져오고 구문상 구별할 수 없습니다. 주소 지정된 인터페이스는 유니캐스트 주소와 애니캐스트 주소를 구성 함수로 구별합니다.  
  
 일반적으로 노드에는 항상 링크-로컬 주소가 포함됩니다. 사이트-로컬 주소 및 하나 이상의 전역 주소가 포함될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터넷 프로토콜 버전 6](../../../docs/framework/network-programming/internet-protocol-version-6.md)  
 [소켓](../../../docs/framework/network-programming/sockets.md)
