---
title: <shadowCopyVerifyByTimestamp> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- <shadowCopyTimeStampVerification> element
- shadowCopyTimeStampVerification element
ms.assetid: 2f1648e5-997b-435e-a4f9-d236c574c66c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 79d44ff255b1fc12efc6e8488eeab231b9276b90
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252314"
---
# <a name="shadowcopyverifybytimestamp-element"></a>\<shadowCopyVerifyByTimestamp> 요소
섀도 복사가 .NET Framework 4에서 도입 된 기본 시작 동작을 사용 하는지 아니면 이전 버전의 .NET Framework의 시작 동작으로 돌아가는지를 지정 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<p >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<shadowCopyVerifyByTimestamp enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|사용|필수 특성입니다.<br /><br /> 어셈블리를 섀도 복사 하기 전에 어셈블리가 업데이트 되었는지 여부를 확인 하기 위해 섀도 복사를 사용 하는 응용 프로그램 도메인이 시작 시 어셈블리 타임 스탬프를 비교 하는지 여부를 지정 합니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|true|시작 시는 섀도 복사본 디렉터리에 마지막으로 복사 된 이후 업데이트 된 어셈블리만 복사 합니다. .NET Framework 4의 기본값입니다.|  
|false|시작 시 모든 파일을 복사 하는 이전 버전의 .NET Framework의 시작 동작으로 되돌립니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 .NET Framework 4부터 어셈블리는 타임 스탬프가 섀도 복사본 디렉터리에 마지막으로 복사 된 이후에 변경 된 것을 나타내는 경우에만 섀도 복사 됩니다. 이렇게 하면 섀도 복사 [어셈블리](../../../app-domains/shadow-copy-assemblies.md)에 설명 된 대로 섀도 복사를 사용 하는 많은 응용 프로그램의 시작 시간이 향상 됩니다. 어셈블리 업데이트의 높은 비율과 빈도를 갖는 응용 프로그램은 이 동작 변경이 도움이 되지 않을 수 있습니다. 이 경우 이 요소를 사용하여 이전 버전의 .NET Framework의 동작을 복원할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 .NET Framework 4에서 섀도 복사의 기본 시작 동작을 사용 하지 않도록 설정 하 고 이전 버전의 .NET Framework의 시작 동작으로 되돌리는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <runtime>  
      <shadowCopyVerifyByTimestamp enabled="false" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [어셈블리 섀도 복사](../../../app-domains/shadow-copy-assemblies.md)
