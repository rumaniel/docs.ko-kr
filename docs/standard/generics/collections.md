---
title: .NET의 제네릭 컬렉션
ms.date: 02/15/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- generics [.NET], collections
- generic collections [.NET]
- generic types [.NET]
ms.assetid: 5b646751-6ab7-465c-916c-b1a76aefa9f5
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 51938dade8ebd1b84010533e04b26cf989ed5f24
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353949"
---
# <a name="generic-collections-in-net"></a>.NET의 제네릭 컬렉션

 .NET 클래스 라이브러리는 <xref:System.Collections.Generic> 및 <xref:System.Collections.ObjectModel> 네임스페이스에서 다양한 제네릭 컬렉션 클래스를 제공합니다. 이러한 클래스에 대한 자세한 내용은 [일반적으로 사용되는 컬렉션 형식](../../../docs/standard/collections/commonly-used-collection-types.md)을 참조하세요.  
  
### <a name="systemcollectionsgeneric"></a>System.Collections.Generic  
 대부분의 제네릭 컬렉션 형식은 제네릭이 아닌 형식과 직접적인 연관이 있습니다. <xref:System.Collections.Generic.Dictionary%602>는 <xref:System.Collections.Hashtable>의 제네릭 버전으로, <xref:System.Collections.DictionaryEntry> 대신 제네릭 구조체인 <xref:System.Collections.Generic.KeyValuePair%602>를 열거형에 사용합니다.  
  
 <xref:System.Collections.Generic.List%601>은 <xref:System.Collections.ArrayList>의 제네릭 버전입니다. 제네릭이 아닌 버전에 해당하는 제네릭 <xref:System.Collections.Generic.Queue%601> 및 <xref:System.Collections.Generic.Stack%601> 클래스가 있습니다.  
  
 <xref:System.Collections.Generic.SortedList%602>의 제네릭 버전과 제네릭이 아닌 버전이 있습니다. 두 버전은 모두 사전과 목록의 하이브리드입니다. <xref:System.Collections.Generic.SortedDictionary%602> 제네릭 클래스는 순수 사전이며 제네릭이 아닌 대응 항목이 없습니다.  
  
 <xref:System.Collections.Generic.LinkedList%601> 제네릭 클래스는 연결된 목록입니다. 제네릭이 아닌 대응 항목이 없습니다.  
  
### <a name="systemcollectionsobjectmodel"></a>System.Collections.ObjectModel  
 <xref:System.Collections.ObjectModel.Collection%601> 제네릭 클래스는 고유한 제네릭 컬렉션 형식을 파생시키기 위한 기본 클래스를 제공합니다. <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 클래스는 <xref:System.Collections.Generic.IList%601> 제네릭 인터페이스를 구현하는 형식에서 읽기 전용 컬렉션을 생성하는 편리한 방법을 제공합니다. <xref:System.Collections.ObjectModel.KeyedCollection%602> 제네릭 클래스는 고유한 키를 포함하는 개체를 저장하는 방법을 제공합니다.  
  
## <a name="other-generic-types"></a>기타 제네릭 형식  
 <xref:System.Nullable%601> 제네릭 구조체를 통해 `null`이 할당될 수 있는 것처럼 값 형식을 사용할 수 있습니다. 이 기능은 값 형식을 포함하는 필드가 누락될 수 있는 데이터베이스 쿼리를 사용할 때 유용할 수 있습니다. 제네릭 형식 매개 변수는 임의의 값 형식일 수 있습니다.  
  
> [!NOTE]
> C# 및 Visual Basic에서는 언어에 nullable 형식에 대한 구문이 있기 때문에 명시적으로 <xref:System.Nullable%601>을 사용할 필요가 없습니다. [Nullable 값 형식(C# 프로그래밍 가이드)](../../csharp/programming-guide/nullable-types/index.md) 및 [Nullable 값 형식(Visual Basic)](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)을 참조하세요.
  
 <xref:System.ArraySegment%601> 제네릭 구조체는 0부터 시작하는 임의 형식의 1차원 배열 내에서 요소 범위를 구분하는 방법을 제공합니다. 제네릭 형식 매개 변수는 배열 요소의 형식입니다.  
  
 이벤트가 .NET Framework에서 사용되는 이벤트 처리 패턴을 따르는 경우 <xref:System.EventHandler%601> 제네릭 대리자를 사용하면 이벤트를 처리할 대리자 형식을 선언할 필요가 없습니다. 예를 들어 이벤트 데이터를 저장할 <xref:System.EventArgs>에서 파생된 `MyEventArgs` 클래스를 만들었다고 가정합니다. 그런 다음 이벤트를 다음과 같이 선언할 수 있습니다.  
  
 [!code-cpp[Conceptual.Generics.Overview#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Generics.Overview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source2.cs#7)]
 [!code-vb[Conceptual.Generics.Overview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source2.vb#7)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Collections.Generic?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel?displayProperty=nameWithType>
- [제네릭](../../../docs/standard/generics/index.md)
- [배열과 목록을 조작하기 위한 제네릭 대리자](../../../docs/standard/generics/delegates-for-manipulating-arrays-and-lists.md)
- [제네릭 인터페이스](../../../docs/standard/generics/interfaces.md)
