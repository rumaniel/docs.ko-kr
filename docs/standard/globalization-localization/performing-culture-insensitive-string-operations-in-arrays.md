---
title: 배열에서 문화권을 구분하지 않는 문자열 작업 수행
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- culture-insensitive string operations, in arrays
- arrays [.NET Framework], culture-insensitive string operations
- comparer parameter
ms.assetid: f12922e1-6234-4165-8896-63f0653ab478
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b52ff8d72132c1076dfdece5e1ce47bbece37b81
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70856000"
---
# <a name="performing-culture-insensitive-string-operations-in-arrays"></a>배열에서 문화권을 구분하지 않는 문자열 작업 수행

<xref:System.Array.Sort%2A?displayProperty=nameWithType> 및 <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType> 메서드의 오버로드는 기본적으로 <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> 속성을 사용하여 문화권 구분 정렬을 수행합니다. 이러한 메서드에서 반환한 문화권 구분 결과는 정렬 순서의 차이로 인해 문화권에 따라 다를 수 있습니다. 문화권 구분 동작을 제거하려면 `comparer` 매개 변수를 수락하는 이 메서드의 오버로드 중 하나를 사용합니다. `comparer` 매개 변수는 배열의 요소를 비교할 때 사용할 <xref:System.Collections.IComparer> 구현을 지정합니다. 매개 변수의 경우 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>를 사용하는 사용자 지정 고정 비교자 클래스를 지정합니다. 사용자 지정 고정 비교자 클래스의 예제는 [컬렉션에서 문화권을 구분하지 않는 문자열 작업 수행](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-collections.md) 항목의 “SortedList 클래스 사용” 하위 항목에서 제공합니다.

> [!NOTE]
> 비교 메서드에 **CultureInfo.InvariantCulture**를 전달하면 문화권을 구분하지 않는 비교가 수행됩니다. 그러나 파일 경로, 레지스트리 키 및 환경 변수 등과 같은 비언어적 비교는 수행되지 않습니다. 비교 결과에 따라 보안 결정을 지원하지도 않습니다. 비언어적 비교 또는 결과 기반 보안 의사 결정에 대한 지원의 경우는 애플리케이션이 <xref:System.StringComparison> 값을 수락하는 비교 메서드를 사용해야 합니다. 그런 다음, 애플리케이션이 <xref:System.StringComparison.Ordinal>을 전달해야 합니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Array.Sort%2A?displayProperty=nameWithType>
- <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType>
- <xref:System.Collections.IComparer>
- [Culture의 영향을 받지 않는 문자열 작업 수행](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)
