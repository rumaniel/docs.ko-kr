---
title: <TimeSpan_LegacyFormatMode> 요소
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- <TimeSpan_LegacyFormatMode> element
- TimeSpan_LegacyFormatMode element
ms.assetid: 865e7207-d050-4442-b574-57ea29d5e2d6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 64bf667c5c9bc20db14f08f18fa6f4f84fa12a24
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252247"
---
# <a name="timespan_legacyformatmode-element"></a>\<TimeSpan_LegacyFormatMode > 요소

런타임에 값을 사용 하 여 <xref:System.TimeSpan?displayProperty=nameWithType> 서식 지정 작업에서 레거시 동작을 유지할지 여부를 결정 합니다.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<TimeSpan_LegacyFormatMode >**  

## <a name="syntax"></a>구문

```xml
<TimeSpan_LegacyFormatMode
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

|특성|설명|
|---------------|-----------------|
|`enabled`|필수 특성입니다.<br /><br /> 런타임에서 값에 레거시 서식 동작을 <xref:System.TimeSpan?displayProperty=nameWithType> 사용할지 여부를 지정 합니다.|

## <a name="enabled-attribute"></a>enabled 특성

|값|설명|
|-----------|-----------------|
|`false`|런타임은 레거시 서식 지정 동작을 복원 하지 않습니다.|
|`true`|런타임이 레거시 서식 지정 동작을 복원 합니다.|

### <a name="child-elements"></a>자식 요소

없음

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|
|`runtime`|런타임 초기화 옵션에 대한 정보를 포함합니다.|

## <a name="remarks"></a>설명

.NET Framework 4부터 구조는 <xref:System.TimeSpan?displayProperty=nameWithType> 인터페이스를 <xref:System.IFormattable> 구현 하 고 표준 및 사용자 지정 서식 문자열을 사용 하 여 서식 지정 작업을 지원 합니다. 구문 분석 메서드에서 지원 되지 않는 서식 지정자 또는 형식 문자열이 발견 되 면이 throw <xref:System.FormatException>됩니다.

이전 버전의 .NET Framework에서 구조는 <xref:System.TimeSpan> 를 구현 <xref:System.IFormattable> 하지 않았으며 형식 문자열을 지원 하지 않았습니다. 그러나 대부분의 개발자는 형식 문자열 <xref:System.TimeSpan> 집합을 지원 하 고와 <xref:System.String.Format%2A?displayProperty=nameWithType>같은 메서드를 사용 하 여 [복합 형식 지정 작업](../../../../standard/base-types/composite-formatting.md) 에 사용 하는 것으로 잘못 된 것으로 가정 합니다. 일반적으로 형식이 형식 문자열을 <xref:System.IFormattable> 구현 하 고 지 원하는 경우 지원 되지 않는 형식 문자열을 사용 하 여 형식 <xref:System.FormatException>지정 메서드를 호출 하면 일반적으로이 throw 됩니다. 그러나가를 <xref:System.TimeSpan> 구현 <xref:System.IFormattable>하지 않았기 때문에 런타임은 형식 문자열을 무시 하 고 대신 메서드 <xref:System.TimeSpan.ToString?displayProperty=nameWithType> 를 호출 했습니다. 즉, 서식 문자열은 서식 지정 작업에 영향을 주지 않지만의 현재 상태는로 설정 되지 않습니다 <xref:System.FormatException>.

레거시 코드가 복합 서식 지정 메서드와 잘못 된 서식 문자열을 전달 하 고 해당 코드를 다시 컴파일할 수 없는 경우에는 `<TimeSpan_LegacyFormatMode>` 요소를 사용 하 여 레거시 <xref:System.TimeSpan> 동작을 복원할 수 있습니다. 이 `enabled` 요소의 특성을로 <xref:System.TimeSpan.ToString?displayProperty=nameWithType> `true`설정 하는 경우 복합 형식 지정 메서드는가 아닌에 대 <xref:System.TimeSpan.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType>한 호출을 발생 하 고 <xref:System.FormatException> 는 throw 되지 않습니다.

## <a name="example"></a>예제

다음 예제에서는 개체를 <xref:System.TimeSpan> 인스턴스화하고 지원 되지 않는 표준 형식 문자열을 <xref:System.String.Format%28System.String%2CSystem.Object%29?displayProperty=nameWithType> 사용 하 여 메서드를 사용 하 여 형식을 지정 하려고 시도 합니다.

[!code-csharp[TimeSpan.BreakingChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/timespan.breakingchanges/cs/legacyformatmode1.cs#1)]
[!code-vb[TimeSpan.BreakingChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/timespan.breakingchanges/vb/legacyformatmode1.vb#1)]

.NET Framework 3.5 또는 이전 버전에서 예제를 실행 하면 다음과 같은 출력이 표시 됩니다.

```
12:30:45
```

.NET Framework 4 이상 버전에서 예제를 실행 하는 경우에는 출력과 현저히 다릅니다.

```
Invalid Format
```

그러나 다음 구성 파일을 예제 디렉터리에 추가한 다음 .NET Framework 4 이상 버전에서 예제를 실행 하는 경우 출력은 3.5 .NET Framework에서 실행 될 때 예제에 의해 생성 된 것과 동일 합니다.

```xml
<?xml version ="1.0"?>
<configuration>
   <runtime>
      <TimeSpan_LegacyFormatMode enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
