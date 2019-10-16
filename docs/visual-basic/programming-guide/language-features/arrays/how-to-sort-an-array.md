---
title: '방법: Visual Basic 배열 정렬'
ms.date: 07/20/2015
f1_keywords:
- Array.Sort
helpviewer_keywords:
- arrays [Visual Basic], sorting
- examples [Visual Basic], arrays
ms.assetid: 9289aeaa-9626-4698-94a7-1d1fd3702b87
ms.openlocfilehash: 467d1bcce6bda2feb5a8e59c152cb292d753e79b
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700971"
---
# <a name="how-to-sort-an-array-in-visual-basic"></a>방법: Visual Basic 배열 정렬

이 문서에서는 Visual Basic에서 문자열 배열을 정렬 하는 방법의 예를 보여 줍니다.

## <a name="example"></a>예제

이 예제에서는 `zooAnimals` 이라는 `String` 개체의 배열을 선언 하 여 채운 다음 사전순으로 정렬 합니다.
  
```vb
Private Sub SortAnimals()
    Dim zooAnimals(2) As String
    zooAnimals(0) = "lion"
    zooAnimals(1) = "turtle"
    zooAnimals(2) = "ostrich"
    Array.Sort(zooAnimals)
End Sub
```

## <a name="robust-programming"></a>강력한 프로그래밍

다음 조건에서 예외가 발생합니다.

- 배열이 비어 있습니다 (<xref:System.ArgumentNullException> 클래스).
- 배열이 다차원 (<xref:System.RankException> 클래스) 인 경우
- 배열의 하나 이상의 요소가 <xref:System.IComparable> 인터페이스 (<xref:System.InvalidOperationException> 클래스)를 구현 하지 않습니다.

## <a name="see-also"></a>참조

- <xref:System.Array.Sort%2A?displayProperty=nameWithType>
- [배열](index.md)
- [배열 문제 해결](troubleshooting-arrays.md)
- [컬렉션](../../concepts/collections.md)
- [For Each...Next 문](../../../language-reference/statements/for-each-next-statement.md)
