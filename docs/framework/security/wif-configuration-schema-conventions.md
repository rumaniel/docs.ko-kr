---
title: WIF 구성 스키마 규칙
ms.date: 03/30/2017
ms.assetid: f7864356-f72f-4cae-995c-18e0431f8a58
author: BrucePerlerMS
ms.openlocfilehash: c02d467260a5197cdd01a3819f8a323655a8a08f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045093"
---
# <a name="wif-configuration-schema-conventions"></a>WIF 구성 스키마 규칙
이 항목에서는 WIF(Windows Identity Foundation) 구성 항목 전체에서 사용되는 규칙을 설명하고 [\<system.identityModel>](../configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md) 및 [\<system.identityModel.services>](../configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md) 섹션에서 사용되는 몇 가지 일반적인 기능과 특성을 설명합니다.  
  
<a name="BKMK_Modes"></a>   
## <a name="modes"></a>모드  
 WIF 구성 요소에는 대부분 `mode` 특성이 있습니다. 이 특성은 일반적으로 처리의 특정 부분을 수행하는 데 사용되는 클래스 및 현재 요소의 자식 요소로 허용되는 구성 요소를 제어합니다. 구성 파일에 포함된 요소가 모드 설정 때문에 무시되는 경우 구성 오류가 발생합니다.  
  
<a name="BKMK_TimespanValues"></a>   
## <a name="timespan-values"></a>Timespan 값  
 여기서 <xref:System.TimeSpan>은 특성의 형식으로 사용됩니다. 허용되는 형식을 확인하려면 <xref:System.TimeSpan.Parse%28System.String%29> 메서드를 참조하세요. 이 형식은 다음 사양을 따릅니다.  
  
`[ws][-]{ d | [d.]hh:mm[:ss[.ff]] }[ws]`  
  
 예를 들어 “30”, “30.00:00”, “30.00:00:00”은 모두 30일을 의미하고 “00:05”, “00:05:00”, “0.00:05:00.00”은 모두 5분을 의미합니다.  
  
<a name="BKMK_CertificateReferences"></a>   
## <a name="certificate-references"></a>인증서 참조  
 몇 가지 요소는 `<certificateReference>` 요소를 사용하여 인증서를 참조합니다. 인증서를 참조하는 경우 다음 특성을 사용할 수 있습니다.  
  
|||  
|-|-|  
|`storeLocation`|<xref:System.Security.Cryptography.X509Certificates.StoreLocation> 열거형 값 `CurrentUser` 또는 `CurrentMachine`입니다.|  
|`storeName`|<xref:System.Security.Cryptography.X509Certificates.StoreName> 열거형의 값. 이 컨텍스트에서 가장 유용한 값은 `My` 및 `TrustedPeople`입니다.|  
|`x509FindType`|<xref:System.Security.Cryptography.X509Certificates.X509FindType> 열거형의 값. 이 컨텍스트에서 가장 유용한 값은 `FindBySubjectName` 및 `FindByThumbprint`입니다. 오류 발생 가능성을 제거하려면 `FindByThumbprint` 형식을 프로덕션 환경에서 사용하는 것이 좋습니다.|  
|`findValue`|`x509FindType` 특성에 따라 인증서를 찾는 데 사용되는 값. 오류 발생 가능성을 제거하려면 `FindByThumbprint` 형식을 프로덕션 환경에서 사용하는 것이 좋습니다. `FindByThumbPrint`가 지정된 경우 이 특성은 16진수 문자열 형식의 인증서 지문인 값을 사용합니다(예: “97249e1a5fa6bee5e515b82111ef524a4c91583f”).|  
  
<a name="BKMK_CustomTypeReferences"></a>   
## <a name="custom-type-references"></a>사용자 지정 형식 참조  
 여러 요소는 `type` 특성을 사용하여 사용자 지정 형식을 참조합니다. 이 특성은 사용자 지정 형식의 이름을 지정해야 합니다. GAC(전역 어셈블리 캐시)의 형식을 참조하려면 강력한 이름을 사용해야 합니다. Bin/ 디렉터리에 있는 어셈블리의 형식을 참조하려면 간단한 어셈블리 정규화된 참조를 사용할 수 있습니다. App_Code/ 디렉터리에 정의된 형식은 한정하는 어셈블리 없이 형식 이름만 지정하여 참조할 수도 있습니다.  
  
 사용자 지정 형식은 지정된 형식에서 파생되어야 하며 `public` 기본(0 인수) 생성자를 제공해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [\<system.identityModel>](../configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md)
- [\<system.identityModel.services>](../configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md)
