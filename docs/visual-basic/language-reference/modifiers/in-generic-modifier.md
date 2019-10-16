---
title: In (제네릭 한정자)-Visual Basic
ms.date: 07/20/2015
f1_keywords:
- vb.VarianceIn
helpviewer_keywords:
- contravariance, In keyword [Visual Basic]
- In keyword [Visual Basic]
ms.assetid: 59bb13c5-fe96-42b8-8286-86293d1661c5
ms.openlocfilehash: 9c0f7d454767112e1e309af81407b5fdef22eee9
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004875"
---
# <a name="in-generic-modifier-visual-basic"></a>In(제네릭 한정자)(Visual Basic)

제네릭 형식 매개 변수에서 `In` 키워드는 형식 매개 변수를 반공변(contravariant)으로 지정합니다.

## <a name="remarks"></a>설명

반공변성(Contravariance)을 통해 제네릭 매개 변수에 지정된 것보다 적은 파생 형식을 사용할 수 있습니다. 따라서 variant 인터페이스를 구현하는 클래스의 암시적 변환과 대리자 형식의 암시적 변환이 허용됩니다.

자세한 내용은 [공변성(Covariance) 및 반공변성(Contravariance)](../../programming-guide/concepts/covariance-contravariance/index.md)을 참조하세요.

## <a name="rules"></a>규칙

제네릭 인터페이스 및 대리자에서 `In` 키워드를 사용할 수 있습니다.
  
메서드 인수의 형식 으로만 사용 되 고 메서드 반환 형식으로 사용 되지 않는 경우 제네릭 인터페이스 또는 대리자에서 형식 매개 변수를 반공 변 (contravariant)으로 선언할 수 있습니다. 0 @no__t 매개 변수는 공변 (covariant) 또는 반공 변 (contravariant) 일 수 없습니다.

공분산 및 반공 분산은 참조 형식에 대해 지원 되 고 값 형식에 대해서는 지원 되지 않습니다.

Visual Basic에서는 대리자 형식을 지정 하지 않고 반공 변 (contravariant) 인터페이스에서 이벤트를 선언할 수 없습니다. 또한 반공 변 (contravariant) 인터페이스에는 중첩 된 클래스, 열거형 또는 구조체를 사용할 수 없지만 중첩 된 인터페이스가 있을 수 있습니다.

## <a name="behavior"></a>동작

반공변(contravariant) 형식 매개 변수가 있는 인터페이스는 해당 메서드가 인터페이스 형식 매개 변수에 지정된 형식보다 덜 파생된 형식의 인수를 사용할 수 있도록 합니다. 예를 들어 .NET Framework 4에서 <xref:System.Collections.Generic.IComparer%601> 인터페이스에서 T 형식은 반공 변입니다. `Employee`이 `Person`에서 상속 되는 경우 특수 변환 메서드를 사용 하지 않고 `IComparer(Of Person)` 형식의 개체를 `IComparer(Of Employee)` 형식의 개체에 할당할 수 있습니다.

반공변(contravariant) 대리자에 동일한 형식의 다른 대리자를 할당할 수 있지만 덜 파생된 제네릭 형식 매개 변수가 필요합니다.

## <a name="example---contravariant-generic-interface"></a>예제-반공 변 (contravariant) 제네릭 인터페이스

다음 예제에서는 반공변(contravariant) 제네릭 인터페이스를 선언, 확장 및 구현하는 방법을 보여 줍니다. 또한 이 인터페이스를 구현하는 클래스에 대해 암시적 변환을 사용하는 방법을 보여 줍니다.

[!code-vb[vbVarianceKeywords#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvariancekeywords/vb/module1.vb#1)]

## <a name="example---contravariant-generic-delegate"></a>예제-반공 변 (contravariant) 제네릭 대리자

다음 예제에서는 반공변(contravariant) 제네릭 대리자를 선언, 인스턴스화 및 호출하는 방법을 보여 줍니다. 또한 대리자 형식을 암시적으로 변환하는 방법을 보여 줍니다.

[!code-vb[vbVarianceKeywords#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvariancekeywords/vb/module1.vb#2)]

## <a name="see-also"></a>참조

- [제네릭 인터페이스의 가변성](../../programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)
- [Out](out-generic-modifier.md)
