---
title: IsFalse 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.isfalse
helpviewer_keywords:
- AndAlso operator [Visual Basic]
- IsFalse operator [Visual Basic]
ms.assetid: 37fc9dbf-e5cc-4570-b93f-7213447974df
ms.openlocfilehash: 49b8493575685a220808df1522ce16835b3ce0ed
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917152"
---
# <a name="isfalse-operator-visual-basic"></a>IsFalse 연산자(Visual Basic)
식이 인지 여부를 확인 `False`합니다.  
  
 코드에서 명시적 `IsFalse` 으로 호출할 수는 없지만 Visual Basic 컴파일러는이를 사용 하 여 절에서 `AndAlso` 코드를 생성할 수 있습니다. 클래스 또는 구조체를 정의한 다음 해당 형식의 변수를 `AndAlso` 절에서 사용 하는 경우 해당 클래스 또는 구조체에 대해를 정의 `IsFalse` 해야 합니다.  
  
 컴파일러는 및 `IsTrue` 연산자 `IsFalse` 를 일치 하는 *쌍*으로 간주 합니다. 즉, 이러한 항목 중 하나를 정의 하는 경우 다른 항목을 정의 해야 합니다.  
  
> [!NOTE]
> 연산자를 오버 로드할 수 있습니다. 즉, 해당 피연산자의 형식이 해당 클래스 또는 구조체의 형식인 경우 클래스 또는 구조체에서 해당 동작을 다시 정의할 수 있습니다. `IsFalse` 코드가 이러한 클래스 또는 구조체에서이 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 `IsFalse` 및 `IsTrue` 연산자에 대 한 정의를 포함 하는 구조체의 개요를 정의 합니다.  
  
 [!code-vb[VbVbalrOperators#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#28)]  
  
## <a name="see-also"></a>참고자료

- [IsTrue 연산자](../../../visual-basic/language-reference/operators/istrue-operator.md)
- [방법: 연산자 정의](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [AndAlso 연산자](../../../visual-basic/language-reference/operators/andalso-operator.md)
