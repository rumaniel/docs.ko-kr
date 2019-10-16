---
title: <httpListener> 요소(네트워크 설정)
ms.date: 03/30/2017
ms.assetid: 62f121fd-3f2e-4033-bb39-48ae996bfbd9
ms.openlocfilehash: 3f75096681ab07dd6d4788fbded5ca5c4a024aef
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698188"
---
# <a name="httplistener-element-network-settings"></a>\<httpListener > 요소 (네트워크 설정)
@No__t-0 클래스에서 사용 하는 매개 변수를 사용자 지정 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t -4c.net >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t[ **\<settings >** ](settings-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 **\<httpListener >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<httpListener  
  unescapeRequestUrl="true|false"  
/>  
```  
  
## <a name="type"></a>type  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|unescapeRequestUrl|@No__t-0 인스턴스가 변환 된 URI 대신 이스케이프 되지 않은 원시 URI를 사용 하는지 여부를 나타내는 부울 값입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|**요소**|**설명**|  
|-----------------|---------------------|  
|[settings](settings-element-network-settings.md)|<xref:System.Net> 네임스페이스에 대한 기본 네트워크 옵션을 구성합니다.|  
  
## <a name="remarks"></a>설명  
 **UnescapeRequestUrl** 특성은% 인코딩된 값이 변환 되 고 다른 정규화 단계가 수행 되는 경우-1 @no__t 변환 된 uri 대신 이스케이프 되지 않은 원시 uri를 사용 하는지 여부를 나타냅니다.  
  
 경우는 <xref:System.Net.HttpListener> 인스턴스를 통해 요청을 수신 합니다 `http.sys` 제공한 URI 문자열의 인스턴스를 만들고 서비스를 `http.sys`,으로 노출를 <xref:System.Net.HttpListenerRequest.Url%2A?displayProperty=nameWithType> 속성.  
  
 `http.sys` 서비스는 두 요청 URI 문자열을 노출 합니다.  
  
- 원시 URI  
  
- 변환 된 URI  
  
 원시 URI가는 <xref:System.Uri?displayProperty=nameWithType> HTTP 요청의 요청 줄에 제공 합니다.  
  
 `GET /path/`  
  
 `Host: www.contoso.com`  
  
 제공 된 URI의 원시 `http.sys` 위에서 언급 한 요청에 "경로 /"입니다. 이 네트워크를 통해 전송 된 HTTP 동사를 다음 문자열을 나타냅니다.  
  
 `http.sys` 서비스는 HTTP 요청에서에서 제공 하는 URI를 사용 하 여 요청에 제공 된 정보에서 변환된 된 URI를 만듭니다 및 원본 서버에서 요청을 확인 하도록 호스트 헤더를 전달 해야 합니다. 이 등록 된 URI 접두사를 사용 하 여 요청에서 정보를 비교 하 여 이루어집니다. HTTP 서버 SDK 설명서는 변환 된이 URI를 HTTP_COOKED_URL 구조체로 참조 합니다.  
  
 등록 된 URI 접두사를 사용 하 여 요청을 비교할 수 있도록 요청에 일부 정규화를 수행 해야 합니다. 변환 된 URI 위의 샘플은 다음과 같을 수 됩니다.  
  
 `http://www.contoso.com/path/`  
  
 합니다 `http.sys` 결합 서비스는 <xref:System.Uri.Host%2A?displayProperty=nameWithType> 속성 값과 문자열을 변환된 된 URI를 만드는 요청 줄에 있습니다. 또한 `http.sys` 및 <xref:System.Uri?displayProperty=nameWithType> 클래스는 다음을 수행 합니다.  
  
- 이스케이프 해제 인코딩된 모든 백분율 값입니다.  
  
- Utf-16 문자 표현으로 변환 백분율로 인코딩된 비 ASCII 문자입니다. 유니코드 문자 (유니코드 %uXXXX 형식을 사용 하 여 인코딩) 및 u t F-8과 ANSI/DBCS 문자는 사용할 수는 note 합니다.  
  
- 경로 압축 등의 다른 정규화 단계를 실행합니다.  
  
 백분율로 인코딩된 값에 사용 되는 인코딩에 대 한 정보가 요청 없으므로 백분율로 인코딩된 값을 구문 분석 하 여 올바른 인코딩을 결정 못할 수 있습니다.  
  
 따라서 `http.sys` 프로세스를 수정 하는 것에 대 한 두 개의 레지스트리 키를 제공 합니다.  
  
|레지스트리 키|기본값|설명|  
|------------------|-------------------|-----------------|  
|EnableNonUTF8|1|0 이면 `http.sys` u t F-8로 인코딩된 Url만 허용 합니다.<br /><br /> 0이 아닌 경우 `http.sys` 도 요청에서 ANSI로 인코딩된 또는 DBCS 인코딩된 Url을 허용 합니다.|  
|FavorUTF8|1|0이 아닌 경우 `http.sys` 디코딩할 URL u t F-8로 먼저 해당 변환에 실패 이며 EnableNonUTF8 0이 아닌 경우 항상 시도 차례로 Http.sys을 ANSI 또는 DBCS 디코딩해야 하는 작업을 하려고 합니다.<br /><br /> 0 (그리고 EnableNonUTF8 0이 아닌 경우) `http.sys` 있는지을 ANSI 또는 DBCS; 디코딩 하려고 성공 하면를 u t F-8로 변환 하려고 합니다.|  
  
 때 <xref:System.Net.HttpListener> 요청이 수신에서 변환 된 URI를 사용 하 여 `http.sys` 대 한 입력으로 <xref:System.Net.HttpListenerRequest.Url%2A> 속성입니다.  
  
 Uri에서 문자 및 숫자 이외의 문자를 지원할 필요가 있습니다. 예로 고객에 대 한 고객 정보를 검색 하는 데 사용 되는 다음 URI를 "1/3812" 번호:  
  
 `http://www.contoso.com/Customer('1%2F3812')/`  
  
 Uri (%2F)의 백분율로 인코딩된 슬래시를 note 합니다. 이것이 필요 하므로 경우 슬래시 문자 데이터 및 경로 구분 기호가 아니라입니다.  
  
 Uri 생성자에 문자열을 전달에 다음 URI를 일으킵니다.  
  
 `http://www.contoso.com/Customer('1/3812')/`  
  
 경로를 세그먼트로 분한 다음 요소에 만들어집니다.  
  
 `Customer('1`  
  
 `3812')`  
  
 요청을 보낸 사람의 의도 아닙니다.  
  
 **UnescapeRequestUrl** 특성이 **false**로 설정 된 경우 <xref:System.Net.HttpListener>가 요청을 받으면 <xref:System.Net.HttpListenerRequest.Url%2A> 속성에 대 한 입력으로 `http.sys`의 변환 된 uri 대신 원시 uri를 사용 합니다.  
  
 **UnescapeRequestUrl** 특성의 기본값은 **true**입니다.  
  
 @No__t-0 속성은 적용 가능한 구성 파일에서 **unescapeRequestUrl** 특성의 현재 값을 가져오는 데 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Net.HttpListenerRequest.Url%2A> 속성에 대 한 입력으로 `http.sys`의 변환 된 URI 대신 원시 URI를 사용 하는 요청을 받을 때 <xref:System.Net.HttpListener> 클래스를 구성 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <httpListener  
        unescapeRequestUrl="false"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="element-information"></a>요소 정보  
  
|||
|-|-|  
|네임스페이스|System.Net|  
|스키마 이름||  
|유효성 검사 파일||  
|비워 둘 수 있음||  
  
## <a name="see-also"></a>참조

- <xref:System.Net.Configuration.HttpListenerElement>
- <xref:System.Net.HttpListener>
- <xref:System.Net.HttpListenerRequest.Url%2A>
- [네트워크 설정 스키마](index.md)
