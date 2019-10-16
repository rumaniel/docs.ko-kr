---
title: 제네릭 인터페이스
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- generic interfaces [.NET Framework]
- equality comparisons [.NET Framework]
- generics [.NET Framework], interfaces
- ordering comparisons [.NET Framework]
ms.assetid: 88bf5b04-d371-4edb-ba38-01ec7cabaacf
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 09e9a51fe9c1fd25a6791cf924180329718138c8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69915888"
---
# <a name="generic-interfaces"></a>제네릭 인터페이스
이 항목에서는 여러 제네릭 형식 패밀리에 대해 공통 기능을 제공하는 제네릭 인터페이스에 대해 간략하게 설명합니다.  
  
## <a name="generic-interfaces"></a>제네릭 인터페이스  
 제네릭 인터페이스는 순서 및 같음 비교와 제네릭 컬렉션 형식에서 공유되는 기능을 위해 제네릭이 아닌 인터페이스에 형식이 안전한 대응 항목을 제공합니다.  
  
> [!NOTE]
> .NET Framework 4부터 여러 제네릭 인터페이스의 형식 매개 변수는 공 분산 또는 반공 분산으로 표시되어 이러한 인터페이스를 구현하는 형식을 유연하게 할당 및 사용할 수 있게 해줍니다. [공변성(Covariance) 및 반공변성(Contravariance)](../../../docs/standard/generics/covariance-and-contravariance.md)을 참조하세요.  
  
### <a name="equality-and-ordering-comparisons"></a>같음 및 순서 비교  
 <xref:System> 네임스페이스에서 <xref:System.IComparable%601?displayProperty=nameWithType> 및 <xref:System.IEquatable%601?displayProperty=nameWithType> 제네릭 인터페이스는 제네릭이 아닌 대응 항목과 마찬가지로 각각 순서 비교와 같음 비교를 위한 메서드를 정의합니다. 형식은 이러한 인터페이스를 구현하여 비교 수행 능력을 제공합니다.  
  
 <xref:System.Collections.Generic> 네임스페이스에서 <xref:System.Collections.Generic.IComparer%601> 및 <xref:System.Collections.Generic.IEqualityComparer%601> 제네릭 인터페이스는 <xref:System.IComparable%601?displayProperty=nameWithType> 또는 <xref:System.IEquatable%601?displayProperty=nameWithType> 제네릭 인터페이스를 구현하지 않는 형식에 대해 순서 또는 같음 비교를 정의하는 방법을 제공하며 수행하는 형식에 대해 이러한 관계를 다시 정의하는 방법도 제공합니다. 이러한 인터페이스는 여러 제네릭 컬렉션 클래스의 메서드 및 생성자에서 사용됩니다. 예를 들어 제네릭 <xref:System.Collections.Generic.IComparer%601> 개체를 <xref:System.Collections.Generic.SortedDictionary%602> 클래스의 생성자에 전달하여 제네릭 <xref:System.IComparable%601?displayProperty=nameWithType>을 구현하지 않는 형식에 대한 정렬 순서를 지정할 수 있습니다. 제네릭 <xref:System.Collections.Generic.IComparer%601> 구현을 사용하여 배열 및 목록을 정렬하기 위한 <xref:System.Array.Sort%2A?displayProperty=nameWithType> 제네릭 정적 메서드 및 <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=nameWithType> 인스턴스 메서드의 오버로드가 있습니다.  
  
 <xref:System.Collections.Generic.Comparer%601> 및 <xref:System.Collections.Generic.EqualityComparer%601> 제네릭 클래스는 <xref:System.Collections.Generic.IComparer%601> 및 <xref:System.Collections.Generic.IEqualityComparer%601> 제네릭 인터페이스의 구현을 위한 기본 클래스를 제공하며 해당 <xref:System.Collections.Generic.Comparer%601.Default%2A?displayProperty=nameWithType> 및 <xref:System.Collections.Generic.EqualityComparer%601.Default%2A?displayProperty=nameWithType> 속성을 통해 기본 순서 및 같음 비교도 제공합니다.  
  
### <a name="collection-functionality"></a>컬렉션 기능  
 <xref:System.Collections.Generic.ICollection%601> 제네릭 인터페이스는 제네릭 컬렉션 형식에 대한 기본 인터페이스입니다. 요소를 추가, 제거, 복사 및 열거하기 위한 기본 기능을 제공합니다. <xref:System.Collections.Generic.ICollection%601>은 제네릭 <xref:System.Collections.Generic.IEnumerable%601> 및 제네릭이 아닌 <xref:System.Collections.IEnumerable> 둘 다에서 상속합니다.  
  
 <xref:System.Collections.Generic.IList%601> 제네릭 인터페이스는 인덱싱된 검색을 위한 메서드를 사용하여 <xref:System.Collections.Generic.ICollection%601> 제네릭 인터페이스를 확장합니다.  
  
 <xref:System.Collections.Generic.IDictionary%602> 제네릭 인터페이스는 키 검색을 위한 메서드를 사용하여 <xref:System.Collections.Generic.ICollection%601> 제네릭 인터페이스를 확장합니다. .NET Framework 기본 클래스 라이브러리의 제네릭 사전 형식은 제네릭이 아닌 <xref:System.Collections.IDictionary> 인터페이스도 구현합니다.  
  
 <xref:System.Collections.Generic.IEnumerable%601> 제네릭 인터페이스는 제네릭 열거자 구조를 제공합니다. 제네릭 열거자에 의해 구현된 <xref:System.Collections.Generic.IEnumerator%601> 제네릭 인터페이스는 제네릭이 아닌 <xref:System.Collections.IEnumerator> 인터페이스를 상속합니다. 형식 매개 변수 `T`에 종속되지 않는 <xref:System.Collections.IEnumerator.MoveNext%2A> 및 <xref:System.Collections.IEnumerator.Reset%2A> 멤버는 제네릭이 아닌 인터페이스에만 나타납니다. 즉, 제네릭이 아닌 인터페이스의 소비자는 제네릭 인터페이스도 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Collections.Generic?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel?displayProperty=nameWithType>
- [제네릭](../../../docs/standard/generics/index.md)
- [.NET Framework의 제네릭 컬렉션](../../../docs/standard/generics/collections.md)
- [배열과 목록을 조작하기 위한 제네릭 대리자](../../../docs/standard/generics/delegates-for-manipulating-arrays-and-lists.md)
- [공 분산 및 반공 분산](../../../docs/standard/generics/covariance-and-contravariance.md)
