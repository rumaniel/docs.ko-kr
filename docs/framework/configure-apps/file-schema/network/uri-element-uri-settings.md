---
title: <uri> 요소(URI 설정)
ms.date: 03/30/2017
ms.assetid: c22bab8b-477c-4ae4-8498-65ad409e0847
ms.openlocfilehash: a492baf9951466383ca0277a2927b8554e5bb332
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697433"
---
# <a name="uri-element-uri-settings"></a>\<uri > 요소 (Uri 설정)
.NET Framework Uri (uniform resource identifier)를 사용 하 여 표현 된 웹 주소를 처리 하는 방법을 지정 하는 설정을 포함 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t **\<uri >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<uri>  
</uri>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|**요소**|**설명**|  
|-----------------|---------------------|  
|[idn](idn-element-uri-settings.md)|IDN(Internationalized Domain Name) 구문 분석이 도메인 이름에 적용되는지 지정합니다.|  
|[iriParsing](iriparsing-element-uri-settings.md)|IRI (국가별 리소스 식별자) 구문 분석이 <xref:System.Uri>에 적용 되는지 여부와 IRI 구문 분석 규칙을 적용할지 여부를 지정 합니다.|  
|[schemeSettings](schemesettings-element-uri-settings.md)|특정 체계에 대해 <xref:System.Uri>가 구문 분석되는 방법을 지정합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|**요소**|**설명**|  
|-----------------|---------------------|  
|[configuration](../configuration-element.md)|모든 네임 스페이스에 대 한 설정을 포함 합니다.|  
  
## <a name="remarks"></a>설명  
 @No__t-0 요소는 <xref:System.Net> 네임 스페이스의 클래스에서 사용 하는 @no__t 1 클래스의 멤버에 대 한 설정을 포함 합니다. 설정은 IRI 및 IDN에 대 한 지원을 구성 합니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 다음 예제에서는 <xref:System.Uri> 클래스에서 IRI 구문 분석 및 IDN 이름을 지원 하기 위해 사용 하는 구성을 보여 줍니다. 또한이 예제에서는 모든 구성표 설정을 지운 다음 http 체계의 백분율 인코딩된 경로 구분 기호를 이스케이프 하지 않는 지원을 추가 합니다.  
  
### <a name="code"></a>코드  
  
```xml  
<configuration>  
  <uri>  
    <idn enabled="All" />  
    <iriParsing enabled="true" />  
    <schemeSettings>  
      <clear/>  
      <add name="http" genericUriParserOptions="DontUnescapePathDotsAndSlashes"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- [네트워크 설정 스키마](index.md)
