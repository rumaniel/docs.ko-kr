---
title: <legacyCorruptedStateExceptionsPolicy> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- <legacyCorruptedStateExceptionsPolicy> element
- legacyCorruptedStateExceptionsPolicy element
ms.assetid: e0a55ddc-bfa8-4f3e-ac14-d1fc3330e4bb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6566437d899b768cda1bab74bb1310deb7aa74db
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252511"
---
# <a name="legacycorruptedstateexceptionspolicy-element"></a>\<legacyCorruptedStateExceptionsPolicy > 요소
공용 언어 런타임에서 관리 코드에서 액세스 위반 및 기타 손상 된 상태 예외를 catch 할 수 있는지 여부를 지정 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<legacyCorruptedStateExceptionsPolicy>**  
  
## <a name="syntax"></a>구문  
  
```xml  
<legacyCorruptedStateExceptionsPolicy enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`enabled`|필수 특성입니다.<br /><br /> 응용 프로그램에서 액세스 위반과 같은 손상 된 상태 예외 오류를 catch 하도록 지정 합니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|`false`|응용 프로그램은 액세스 위반과 같은 손상 된 상태 예외 오류를 catch 하지 않습니다. 이 값이 기본값입니다.|  
|`true`|응용 프로그램은 액세스 위반과 같은 손상 된 상태 예외 오류를 catch 합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 .NET Framework 버전 3.5 및 이전 버전에서 공용 언어 런타임에서는 관리 코드를 허용 하 여 손상 된 프로세스 상태에 의해 발생 한 예외를 catch 했습니다. 액세스 위반은 이러한 형식의 예외에 대 한 예입니다.  
  
 .NET Framework 4부터 관리 코드는 더 이상 블록에서 `catch` 이러한 형식의 예외를 catch 하지 않습니다. 그러나 다음과 같은 두 가지 방법으로이 변경을 재정의 하 고 손상 된 상태 예외 처리를 유지할 수 있습니다.  
  
- 요소의 특성을 로`true`설정 합니다. `enabled` `<legacyCorruptedStateExceptionsPolicy>` 이 구성 설정은 processwide로 적용 되 고 모든 메서드에 영향을 줍니다.  
  
 또는  
  
- <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute?displayProperty=nameWithType> 예외`catch` 블록이 포함 된 메서드에 특성을 적용 합니다.  
  
 이 구성 요소는 .NET Framework 4 이상 에서만 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 응용 프로그램이 .NET Framework 4 이전의 동작으로 되돌아가고 모든 손상 상태 예외 오류를 catch 하도록 지정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <runtime>  
      <legacyCorruptedStateExceptionsPolicy enabled="true" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>
- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
