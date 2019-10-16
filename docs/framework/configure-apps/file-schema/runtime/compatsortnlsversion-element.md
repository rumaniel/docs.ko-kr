---
title: <CompatSortNLSVersion> 요소
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- <CompatSortNLSVersion> element
- CompatSortNLSVersion element
ms.assetid: 782cc82e-83f7-404a-80b7-6d3061a8b6e3
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 575d44ad9ecf445ba5d4b7fbe47032127ccb33ae
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252728"
---
# <a name="compatsortnlsversion-element"></a>\<CompatSortNLSVersion > 요소
문자열 비교를 수행할 때 런타임에서 레거시 정렬 순서를 사용하도록 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<CompatSortNLSVersion>**  
  
## <a name="syntax"></a>구문  
  
```xml  
<CompatSortNLSVersion    
   enabled="4096"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`enabled`|필수 특성입니다.<br /><br /> 정렬 순서를 사용할 로캘 ID를 지정합니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|4096|대체 정렬 순서를 나타내는 로캘 ID입니다. 이 경우 4096는 .NET Framework 3.5 이전 버전의 정렬 순서를 나타냅니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|런타임 초기화 옵션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 .NET Framework 4의 <xref:System.Globalization.CompareInfo?displayProperty=nameWithType> 클래스에서 수행 하는 문자열 비교, 정렬 및 대/소문자 구분 연산은 유니코드 5.1 표준을 따르기 때문에 <xref:System.String.Compare%28System.String%2CSystem.String%29?displayProperty=nameWithType> 및와 같은 문자열 비교 메서드의 결과는와 <xref:System.String.LastIndexOf%28System.String%29?displayProperty=nameWithType> 다를 수 있습니다. 이전 버전의 .NET Framework입니다. 응용 프로그램이 레거시 동작에 의존 하는 경우 응용 프로그램의 구성 파일에 요소를 `<CompatSortNLSVersion>` 포함 하 여 .NET Framework 3.5 이전 버전에서 사용 되는 문자열 비교 및 정렬 규칙을 복원할 수 있습니다.  
  
> [!IMPORTANT]
> 레거시 문자열 비교 복원 및 정렬 규칙을 실행하려면 로컬 시스템에서 sort00001000.dll 동적 링크 라이브러리를 사용할 수 있어야 합니다.  
  
 응용 프로그램 도메인을 만들 때 "NetFx40_Legacy20SortingBehavior" 문자열을 <xref:System.AppDomainSetup.SetCompatibilitySwitches%2A> 메서드로 전달하여 특정 응용 프로그램 도메인에 레거시 문자열 정렬과 비교 규칙을 사용할 수도 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 현재 문화권의 규약을 사용하여 두 가지 <xref:System.String> 개체를 인스턴스화하고 <xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 메서드를 호출하여 두 개체를 비교합니다.  
  
 [!code-csharp[String.BreakingChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/string.breakingchanges/cs/example1.cs#1)]
 [!code-vb[String.BreakingChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/string.breakingchanges/vb/example1.vb#1)]  
  
 .NET Framework 4에서 예제를 실행 하면 다음과 같은 출력이 표시 됩니다.  
  
```  
sta follows a in the sort order.  
```  
  
 이는 .NET Framework 3.5에서 예제를 실행할 때 표시 되는 출력과 완전히 다릅니다.  
  
```  
sta equals a in the sort order.  
```  
  
 그러나 다음 구성 파일을 예제 디렉터리에 추가한 다음 .NET Framework 4에서 예제를 실행 하는 경우 출력은 3.5 .NET Framework에서 실행 될 때 예제에 의해 생성 된 것과 동일 합니다.  
  
```xml  
<?xml version ="1.0"?>  
<configuration>  
   <runtime>  
      <CompatSortNLSVersion enabled="4096"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
