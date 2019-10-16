---
title: IsNot 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.isnot
helpviewer_keywords:
- IsNot operator [Visual Basic]
ms.assetid: 8dd2bcdb-0166-48a2-9094-60dfb448f36c
ms.openlocfilehash: 32e8f9532244679d2994b0e3d98279d75f7e77b4
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701046"
---
# <a name="isnot-operator-visual-basic"></a>IsNot 연산자(Visual Basic)

두 개체 참조 변수를 비교 합니다.

## <a name="syntax"></a>구문

```vb
result = object1 IsNot object2
```

## <a name="parts"></a>요소
 `result` 필수입니다. `Boolean` 값입니다.

 `object1` 필수입니다. 모든 @no__t 0 변수 또는 식입니다.

 `object2` 필수입니다. 모든 @no__t 0 변수 또는 식입니다.

## <a name="remarks"></a>설명
 @No__t-0 연산자는 두 개체 참조가 서로 다른 개체를 참조 하는지 여부를 결정 합니다. 그러나 값 비교를 수행 하지는 않습니다. @No__t-0 및 `object2`이 모두 정확히 동일한 개체 인스턴스를 참조 하는 경우에는 `result`가 `False`입니다. 그렇지 않은 경우-4는-5 @no__t @no__t.

 `IsNot`은 `Is` 연산자와 반대입니다. @No__t-0의 장점은 읽기가 어려울 수 있는 `Not` 및 `Is`로 인 한 구문을 방지할 수 있다는 것입니다.

 @No__t-0 및 `IsNot` 연산자를 사용 하 여 초기 바인딩과 런타임에 바인딩된 개체를 모두 테스트할 수 있습니다.

## <a name="example"></a>예제
 다음 코드 예제에서는 `Is` 연산자와 `IsNot` 연산자를 모두 사용 하 여 동일한 비교를 수행 합니다.

 [!code-vb[VbVbalrOperators#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#29)]

## <a name="see-also"></a>참조

- [Is 연산자](is-operator.md)
- [TypeOf 연산자](typeof-operator.md)
- [Visual Basic에서의 연산자 우선 순위](operator-precedence.md)
- [방법: 두 개체가 동일한 @ no__t 인지 여부를 테스트 합니다.
