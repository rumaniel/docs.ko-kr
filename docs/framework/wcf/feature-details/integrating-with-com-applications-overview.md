---
title: COM 애플리케이션과 통합 개요
ms.date: 03/30/2017
helpviewer_keywords:
- COM [WCF], integration overview
ms.assetid: 02c5697f-6e2e-47d6-b715-f3a28aebfbd5
ms.openlocfilehash: 99e3c2f4445673f3b74048a2b466203af7bc2795
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045888"
---
# <a name="integrating-with-com-applications-overview"></a>COM 애플리케이션과 통합 개요

WCF (Windows Communication Foundation)는 관리 코드 개발자에 게 연결 된 응용 프로그램을 만들기 위한 풍부한 환경을 제공 합니다. 그러나 관리 되지 않는 COM 기반 코드에 상당한 투자가 필요 하지만 마이그레이션하지 않으려는 경우 WCF 서비스 모니커를 사용 하 여 WCF 웹 서비스를 기존 코드에 직접 통합할 수 있습니다. 서비스 모니커는 Office VBA, Visual Basic 6.0 또는 Visual C++ 6.0과 같은 다양한 범위의 COM 기반 개발 환경에서 사용할 수 있습니다.

> [!NOTE]
> 서비스 모니커는 모든 통신에 대해 WCF 통신 채널을 사용 합니다. 이 채널의 보안 및 ID 메커니즘은 표준 COM 및 DCOM 프록시에 사용되는 메커니즘과 다릅니다. 또한 서비스 모니커가 WCF 통신 채널을 사용 하기 때문에 모든 호출에 대해 기본 제한 시간은 1 분입니다.

서비스 모니커는 `GetObject` 함수와 함께 사용 되어 관리 되지 않는 개발자에 게 WCF 웹 서비스를 호출 하기 위한 강력한 형식의 COM 관련 접근 방법을 제공 합니다. 이렇게 하려면 WCF 웹 서비스 계약의 로컬 및 COM에 표시 되는 정의와 사용할 바인딩을 사용 해야 합니다. 다른 WCF 클라이언트와 마찬가지로,이 채널 생성은 첫 번째 메서드 호출에서 COM 프로그래머에 게 투명 하 게 발생 하지만 서비스 모니커는 서비스에 형식화 된 채널을 생성 해야 합니다.

다른 WCF 클라이언트와 일반적으로 모니커를 사용 하는 경우 응용 프로그램은 서비스와 통신 하는 주소, 바인딩 및 계약을 지정 합니다. 계약은 다음 방법 중 하나로 지정할 수 있습니다.

- 형식화된 계약 – 계약이 클라이언트 컴퓨터에 COM 노출 형식으로 등록됩니다.

- WSDL 계약 – 계약이 WSDL 문서 형식으로 제공됩니다.

- MEX 계약 – 계약이 MEX(메타데이터 교환) 엔드포인트에서 런타임에 검색됩니다.

## <a name="parameters-supported-by-the-service-moniker"></a>서비스 모니커에서 지원하는 매개 변수

다음 표에서는 서비스 모니커에서 지원하는 매개 변수를 보여 줍니다.

|매개 변수|설명|
|---------------|-----------------|
|`address`|서비스의 URL 위치입니다.|
|`binding`|애플리케이션 구성의 바인딩 섹션 이름입니다.|
|`bindingConfiguration`|명명된 바인딩 섹션 내의 명명된 바인딩 인스턴스입니다.|
|`contract`|MEX에서 서비스 계약이나 계약 이름을 나타내는 IID(인터페이스 식별자)입니다.|
|`wsdl`|계약 정의에 대한 대체 형식을 제공하는 WSDL 문서입니다.|
|`spnIdentity`|서비스와의 통신에 사용되는 SPN(서비스 사용자 이름) ID입니다.|
|`upnIdentity`|서비스와의 통신에 사용되는 UPN(User Principal Name) ID입니다.|
|`dnsIdentity`|서비스와의 통신에 사용되는 DNS ID입니다.|
|`mexAddress`|서비스의 MEX(메타데이터 교환) 엔드포인트에 대한 URL 위치입니다.|
|`mexBinding`|MEX 엔드포인트와 연결하기 위한 애플리케이션 구성의 바인딩 섹션 이름입니다.|
|`mexBindingConfiguration`|MEX 엔드포인트와 연결하기 위한 명명된 바인딩 섹션 내의 명명된 바인딩 인스턴스입니다.|
|`bindingNamespace`|검색된 MEX의 바인딩 섹션 이름에 대한 네임스페이스입니다.|
|`contractNamespace`|검색된 MEX의 계약에 대한 네임스페이스입니다.|
|`mexSpnIdentity`|MEX 엔드포인트와의 통신에 사용되는 SPN(서버 사용자 이름) ID입니다.|
|`mexUpnIdentity`|MEX 엔드포인트와의 통신에 사용되는 UPN(User Principal Name) ID입니다.|
|`mexDnsIdentity`|MEX 엔드포인트와의 통신에 사용되는 DNS ID입니다.|
|`serializer`|"xml" 또는 "datacontract" serializer 사용을 지정합니다.|

> [!NOTE]
> 전체 COM 기반 클라이언트와 함께 사용 하는 경우에도 서비스 모니커는 WCF와 지원 .NET Framework 2.0를 클라이언트 컴퓨터에 설치 해야 합니다. 또한 서비스 모니커를 사용하는 클라이언트 애플리케이션에서 올바른 버전의 .NET Framework 런타임을 로드해야 하는 점도 중요합니다. Office 애플리케이션에서 모니커를 사용할 때 올바른 프레임워크 버전이 로드되도록 하기 위해 구성 파일이 필요할 수 있습니다. 예를 들어 Excel을 사용하는 경우, 다음 텍스트가 Excel.exe 파일과 동일한 디렉터리의 Excel.exe.config라는 파일에 있어야 합니다.
>
> `<?xml version="1.0" encoding="utf-8"?>`
>
> `<configuration xmlns=` `http://schemas.microsoft.com/.NetConfiguration/v2.0` `>`
>
> `<startup>`
>
> `<requiredRuntime version="v2.0.50727" />`
>
> `</startup>`
>
> `</configuration>`

## <a name="see-also"></a>참고자료

- [방법: 서비스 모니커 등록 및 구성](../../../../docs/framework/wcf/feature-details/how-to-register-and-configure-a-service-moniker.md)
