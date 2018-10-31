---
title: '&lt;추가&gt; schemeSettings (Uri 설정)에 대 한'
ms.date: 03/30/2017
ms.assetid: 594a7b3b-af23-4cfa-b616-0b2dddb1a705
ms.openlocfilehash: 07bcaf470c68a4d400057b0fe19e96524b2859cb
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50205180"
---
# <a name="ltaddgt-element-for-schemesettings-uri-settings"></a>&lt;추가&gt; schemeSettings (Uri 설정)에 대 한
스키마 이름에 대 한 스키마 설정을 추가합니다.  
  
 \<configuration>  
\<uri >  
\<schemeSettings >  
\<add>  
  
## <a name="syntax"></a>구문  
  
```xml  
<add
  name="http|https"
  genericUriParserOptions="DontUnescapePathDotsAndSlashes"
/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|name|이 설정은 적용 되는 체계 이름입니다. 이름과 "http"만 지원 되는 값 이름 = = "https"입니다.|  
  
## <a name="attribute-name-attribute"></a>{0} 특성 이름} 특성  
  
|값|설명|  
|-----------|-----------------|  
|genericUriParserOptions|이 스키마에 대 한 파서 옵션을 지정 합니다. 지원 되는 값은 genericUriParserOptions만 = "DontUnescapePathDotsAndSlashes"입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<schemeSettings> 요소 (URI 설정)](../../../../../docs/framework/configure-apps/file-schema/network/schemesettings-element-uri-settings.md)|특정 체계에 대해 <xref:System.Uri>가 구문 분석되는 방법을 지정합니다.|  
  
## <a name="remarks"></a>설명  
 기본적으로 <xref:System.Uri?displayProperty=nameWithType> 클래스 이스케이프 해제 백분율로 인코딩된 경로 압축을 실행 하기 전에 경로 구분 기호입니다. 다음과 같은 공격에 대 한 보안 메커니즘으로 구현 되었습니다.  
  
 `http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 이 URI에 전달 하는 경우 모듈까지 %를 처리 하지 못할 경우 인코딩된 문자를 올바르게, 서버에서 실행 되 고 다음 명령에서 발생할 수 있습니다.  
  
 `c:\Windows\System32\cmd.exe /c dir c:\`  
  
 이러한 이유로 <xref:System.Uri?displayProperty=nameWithType> 클래스가 먼저 이스케이프 해제 경로 구분 기호 및 경로 압축을 적용 합니다. 위의 악성 URL을 전달 하는 결과 <xref:System.Uri?displayProperty=nameWithType> 클래스 생성자에 다음 URI:  
  
 `http://www.microsoft.com/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 SchemeSettings 구성 옵션을 사용 하 여 특정 스키마에 대 한 이스케이프 해제 백분율로 인코딩된 경로 구분 되지에이 기본 동작을 수정할 수 있습니다.  
  
## <a name="configuration-files"></a>구성 파일  
 이 요소는 응용 프로그램 구성 파일 또는 컴퓨터 구성 파일(Machine.config)에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서 사용 하는 구성을 보여 줍니다는 <xref:System.Uri> http 체계에 대 한 백분율로 인코딩된 경로 구분 기호를 이스케이프 하지 않아도 되도록 지원 하기 위해 클래스입니다.  
  
```xml  
<configuration>  
  <uri>  
    <schemeSettings>  
      <add name="http" genericUriParserOptions="DontUnescapePathDotsAndSlashes"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목  
- <xref:System.Configuration.SchemeSettingElement?displayProperty=nameWithType>  
- <xref:System.Configuration.SchemeSettingElementCollection?displayProperty=nameWithType>  
- <xref:System.Configuration.UriSection?displayProperty=nameWithType>  
- <xref:System.Configuration.UriSection.SchemeSettings%2A?displayProperty=nameWithType>  
- <xref:System.GenericUriParserOptions?displayProperty=nameWithType>  
- <xref:System.Uri?displayProperty=nameWithType>  
- [네트워크 설정 스키마](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
