---
title: '&lt;httpWebRequest&gt; 요소 (네트워크 설정)'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/httpWebRequest
- http://schemas.microsoft.com/.NetConfiguration/v2.0#httpWebRequest
helpviewer_keywords:
- <httpWebRequest> element
- httpWebRequest element
ms.assetid: 52acd9d2-5bdc-4dc4-9c2a-f0a476ccbb31
ms.openlocfilehash: 0d3feb168acbd623270a2038bf06a3c97126bd05
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50205154"
---
# <a name="lthttpwebrequestgt-element-network-settings"></a>&lt;httpWebRequest&gt; 요소 (네트워크 설정)
웹 요청 매개 변수를 지정합니다.  
  
 \<configuration>  
\<system.net>  
\<settings>  
\<httpWebRequest >  
  
## <a name="syntax"></a>구문  
  
```xml  
<httpWebRequest  
  maximumResponseHeadersLength="size"  
  maximumErrorResponseLength="size"  
  maximumUnauthorizedUploadLength="size"  
  useUnsafeHeaderParsing="true|false"  
/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|**특성**|**설명**|  
|-------------------|---------------------|  
|`maximumResponseHeadersLength`|(킬로바이트), 응답 헤더의 최대 길이 지정 합니다. 기본값은 64입니다. 값이-1 크기 제한이 응답 헤더에 적용 됩니다 나타냅니다.|  
|`maximumErrorResponseLength`|(킬로바이트)는 오류 응답의 최대 길이 지정 합니다. 기본값은 64입니다. 값이-1은 오류 응답에 크기 제한이 적용을 나타냅니다.|  
|`maximumUnauthorizedUploadLength`|권한이 없는 오류 코드, 바이트에서에 대 한 응답에서 업로드할 경우의 최대 길이 지정합니다. 기본값은 -1입니다. 값이-1은 업로드할 때 크기 제한이 적용을 나타냅니다.|  
|`useUnsafeHeaderParsing`|안전 하지 않은 헤더를 구문 분석 사용 되는지 여부를 지정 합니다. 기본값은 `false`입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|**요소**|**설명**|  
|-----------------|---------------------|  
|[settings](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|<xref:System.Net> 네임스페이스에 대한 기본 네트워크 옵션을 구성합니다.|  
  
## <a name="remarks"></a>설명  
 기본적으로.NET Framework URI 구문 분석에 대 한 RFC 2616 엄격 하 게 적용합니다. 일부 서버 응답 하면는 허용 되지 않는 필드에 제어 문자를 포함할 수 있습니다 합니다 <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType> throw 하는 메서드를 <xref:System.Net.WebException>입니다. 하는 경우 **useUnsafeHeaderParsing** 로 설정 된 **true**, <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType> 있지만 경우에 throw 하지 것입니다, 응용 프로그램은 여러 형태의 URI 구문 분석 공격에 취약 하 게 됩니다. 가장 적합 한 솔루션 응답 제어 문자가 포함 되지 않습니다 있도록 서버를 변경 하는 것입니다.  
  
## <a name="configuration-files"></a>구성 파일  
 이 요소는 응용 프로그램 구성 파일 또는 컴퓨터 구성 파일(Machine.config)에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 큰 값을 지정 하는 방법 보다 일반적인 최대 헤더 길이입니다.  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <httpWebRequest  
        maximumResponseHeadersLength="128"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목  
- <xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A>  
- [네트워크 설정 스키마](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
