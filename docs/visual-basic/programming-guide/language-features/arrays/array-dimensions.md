---
title: Array Dimensions in Visual Basic
ms.date: 07/20/2015
helpviewer_keywords:
- dimensions, arrays
- arrays [Visual Basic], dimensions
- arrays [Visual Basic], rectangular
- arrays [Visual Basic], rank
- rectangular arrays
- ranking, arrays
ms.assetid: 385e911b-18c1-4e98-9924-c6d279101dd9
ms.openlocfilehash: bbc9e523e9b74cf380c65135e7416f1feba01a2e
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512891"
---
# <a name="array-dimensions-in-visual-basic"></a>Array Dimensions in Visual Basic

*차원은* 배열의 요소에 대 한 사양을 변경할 수 있는 방향입니다. 해당 월의 각 날짜에 대 한 판매량 합계를 포함 하는 배열에는 1 차원 (해당 월의 일)이 있습니다. 해당 월의 각 날짜에 대 한 총 판매량을 포함 하는 배열에는 두 개의 차원 (부서 번호와 해당 월의 일)이 있습니다. 배열에 포함 된 차원의 수를 *차수*라고 합니다.

> [!NOTE]
> <xref:System.Array.Rank%2A> 속성을 사용 하 여 배열에 포함 된 차원의 수를 확인할 수 있습니다.

## <a name="working-with-dimensions"></a>차원 작업

배열의 각 차원에 대 한 *인덱스* 또는 *첨자* 를 제공 하 여 배열의 요소를 지정 합니다. 요소는 인덱스 0부터 해당 차원의 가장 높은 인덱스까지 각 차원에 따라 인접 합니다.

다음 그림에서는 차수가 다른 배열의 개념적 구조를 보여 줍니다. 그림의 각 요소는 해당 요소에 액세스 하는 인덱스 값을 보여 줍니다. 예를 들어 인덱스 `(1, 0)`를 지정 하 여 2 차원 배열의 두 번째 행에 있는 첫 번째 요소에 액세스할 수 있습니다.

![1 차원 배열을 표시 하는 다이어그램입니다.](./media/array-dimensions/one-dimensional-array.gif)

![2 차원 배열을 표시 하는 다이어그램입니다.](./media/array-dimensions/two-dimensional-array.gif)

![3 차원 배열을 표시 하는 다이어그램입니다.](./media/array-dimensions/three-dimensional-array.gif)

### <a name="one-dimension"></a>한 차원

많은 배열에는 각 연령의 사용자 수와 같이 하나의 차원만 있습니다. 요소를 지정 하는 유일한 요구 사항은 해당 요소에 개수를 포함 하는 기간입니다. 따라서 이러한 배열은 하나의 인덱스만 사용 합니다. 다음 예에서는 0 ~ 120에 대 한 연령 수의 *1 차원 배열을* 보유 하는 변수를 선언 합니다.

```vb
Dim ageCounts(120) As UInteger
```

### <a name="two-dimensions"></a>두 차원

일부 배열에는 캠퍼스의 각 건물 바닥에 있는 사무실 수와 같이 두 개의 차원이 있습니다. 요소의 사양에는 건물 번호와 층이 모두 필요 하며 각 요소는 빌딩 및 층의 조합 수를 포함 합니다. 따라서 이러한 배열에서는 두 개의 인덱스를 사용 합니다. 다음 예제에서는 0부터 40 까지의 빌딩 및 0에서 5 까지의 *2 차원 배열을* 포함 하는 변수를 선언 합니다.

```vb
Dim officeCounts(40, 5) As Byte
```

2 차원 배열을 *사각형 배열*이 라고도 합니다.

### <a name="three-dimensions"></a>3 차원

일부 배열에 3 차원 공간의 값과 같은 세 개의 차원이 있습니다. 이러한 배열은 세 개의 인덱스를 사용 합니다 .이 경우에는 실제 공간의 x, y 및 z 좌표를 나타냅니다. 다음 예제에서는 3 차원 볼륨의 다양 한 지점에서 *3 차원* 양의 기온 배열을 보유 하는 변수를 선언 합니다.

```vb
Dim airTemperatures(99, 99, 24) As Single
```

### <a name="more-than-three-dimensions"></a>3 개 이상의 차원

배열에는 최대 32 차원이 포함 될 수 있지만,이 경우에는 세 개 이상의 차원이 있을 수 있습니다.

> [!NOTE]
> 배열에 차원을 추가 하면 배열에 필요한 총 저장소가 크게 향상 되므로 다차원 배열을 주의 해 서 사용 합니다.

## <a name="using-different-dimensions"></a>다른 차원 사용

현재 월의 매일 판매 금액을 추적 하려는 경우를 가정해 보겠습니다. 다음 예제와 같이 월의 각 날짜에 하나씩 31 개의 요소가 포함 된 1 차원 배열을 선언할 수 있습니다.

```vb
Dim salesAmounts(30) As Double
```

이제 월의 모든 날 뿐만 아니라 월 마다 동일한 정보를 추적 하려고 한다고 가정 합니다. 다음 예제와 같이 12 개 행 (월)과 31 개 열 (일)을 사용 하 여 2 차원 배열을 선언할 수 있습니다.

```vb
Dim salesAmounts(11, 30) As Double
```

이제 배열에 1 년 이상 정보를 저장 하도록 결정 한다고 가정 합니다. 5 년 동안의 판매량을 추적 하려는 경우 다음 예제와 같이 5 개 계층, 12 개 행 및 31 열이 포함 된 3 차원 배열을 선언할 수 있습니다.

```vb
Dim salesAmounts(4, 11, 30) As Double
```

각 인덱스는 0부터 최대값까지 다르므로의 `salesAmounts` 각 차원은 해당 차원의 필수 길이 보다 하나로 선언 됩니다. 또한 배열의 크기가 새 차원 마다 늘어납니다. 위의 예제에서 세 가지 크기는 각각 31, 372 및 1860 요소입니다.

> [!NOTE]
> `Dim` 문`New` 또는 절을 사용 하지 않고 배열을 만들 수 있습니다. 예를 들어 <xref:System.Array.CreateInstance%2A> 메서드를 호출 하거나 다른 구성 요소에서 이러한 방식으로 만든 배열에 코드를 전달할 수 있습니다. 이러한 배열의 하한값은 0이 될 수 없습니다. 항상 메서드나 <xref:System.Array.GetLowerBound%2A> `LBound` 함수를 사용 하 여 차원의 하 한을 테스트할 수 있습니다.

## <a name="see-also"></a>참고자료

- [배열](../../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [배열 문제 해결](../../../../visual-basic/programming-guide/language-features/arrays/troubleshooting-arrays.md)
