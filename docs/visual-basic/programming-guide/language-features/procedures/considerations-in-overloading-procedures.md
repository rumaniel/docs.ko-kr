---
title: 프로시저를 오버로드할 때 고려해야 할 사항(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- signatures [Visual Basic], ParamArray arguments
- ParamArray keyword [Visual Basic], parameter arrays
- ParamArray keyword [Visual Basic], arguments and signatures
- function overloading [Visual Basic], implicit overloads for ParamArray
- ParamArray keyword [Visual Basic], signatures
- Visual Basic code, procedures
- arguments [Visual Basic], parameter arrays
- procedures [Visual Basic], overloading
- parameters [Visual Basic], lists
- function overloading [Visual Basic], typeless programming
- typeless programming
- function overloading [Visual Basic], restrictions
- arguments [Visual Basic], optional
- optional arguments [Visual Basic], overloading
- signatures [Visual Basic], procedure
- parameter lists [Visual Basic]
- parameter arrays [Visual Basic], overloading arguments
- Visual Basic code, parameter lists
- procedure overloading [Visual Basic], considerations
- Option Explicit statement [Visual Basic]
- restrictions [Visual Basic], overloading procedures
- procedures [Visual Basic], parameter lists
ms.assetid: a2001248-10d0-42c5-b0ce-eeedc987319f
ms.openlocfilehash: b5a26a8b68a2f786213aa49f30247d692b3de2f7
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64649654"
---
# <a name="considerations-in-overloading-procedures-visual-basic"></a>프로시저를 오버로드할 때 고려해야 할 사항(Visual Basic)
프로시저를 오버 로드할 때는 다른 사용 해야 합니다 *서명을* 각 오버 로드 된 버전에 대 한 합니다. 일반적으로 즉, 각 버전에는 다른 매개 변수 목록을 지정 해야 합니다. 자세한 내용은 "다른 시그니처"를 참조 하세요 [프로시저 오버 로딩](./procedure-overloading.md)합니다.  
  
 오버 로드할 수 있습니다는 `Function` 사용 하 여 프로시저를 `Sub` 프로시저 반대로 시그니처가 다르면를 제공 합니다. 두 개의 오버 로드가 없습니다는 다를 하나에 반환 값 및 다른 그렇지 않습니다.  
  
 마찬가지로 프로시저를 오버 로드를 속성에 오버 로드와 동일한 제한이 적용 됩니다. 프로시저를 오버 로드할 수 없습니다. 단, 속성 또는 그 반대의 경우도 마찬가지입니다.  
  
## <a name="alternatives-to-overloaded-versions"></a>오버 로드 된 버전에 대 한 대안  
 경우에 따라 해당 번호는 변수 또는 인수를 생략할 경우에 특히 오버 로드 된 버전에 대 한 대안 있는 합니다.  
  
 선택적 인수 모든 언어에서 지원 되는 것은 아니며을 매개 변수 배열은 Visual basic 제한 염두에 둡니다. 여러 다른 언어로 작성 된 코드에서 호출할 가능성이 있는 프로시저를 작성 하는 경우 버전 제품 융통성 오버 로드 됩니다.  
  
### <a name="overloads-and-optional-arguments"></a>오버 로드 및 선택적 인수  
 호출 코드 필요에 따라 제공 하거나 하나 이상의 인수를 생략할 수, 하는 경우에 여러 오버 로드 된 버전을 정의 수도 있고 선택적 매개 변수를 사용할 수 있습니다.  
  
#### <a name="when-to-use-overloaded-versions"></a>오버 로드 된 버전을 사용 하는 경우  
 다음 경우에는 일련의 오버 로드 된 버전을 정의 고려할 수 있습니다.  
  
- 프로시저 코드의 논리 여부 호출 코드에서 선택적 인수를 제공 하는 여부에 따라 크게 다릅니다.  
  
- 프로시저 코드를 호출 하는 코드는 선택적 인수를 제공 하는지 여부를 안정적으로 테스트할 수 없습니다. 이 경우, 예를 들어, 기본 값에 대 한 가능한 후보가 없는 경우 호출 코드 되지 않을 제공 합니다.  
  
#### <a name="when-to-use-optional-parameters"></a>선택적 매개 변수를 사용 하는 경우  
 다음 경우에 하나 이상의 선택적 매개 변수를 선호할 수 있습니다.  
  
- 필요한 작업만 호출 코드는 선택적 인수를 제공 하지 않습니다 하는 경우 기본 값으로 매개 변수를 설정 하는 것입니다. 이러한 경우 프로시저 코드 수 덜 복잡 하 게 하나를 사용 하 여 단일 버전을 정의 하는 경우 `Optional` 매개 변수입니다.  
  
 자세한 내용은 [선택적 매개 변수](./optional-parameters.md)합니다.  
  
### <a name="overloads-and-paramarrays"></a>오버 로드와 ParamArrays  
 호출 코드에서 가변 개수의 인수를 전달할 수 여러 오버 로드 된 버전을 정의할 수도 있고 매개 변수 배열을 사용할 수 있습니다.  
  
#### <a name="when-to-use-overloaded-versions"></a>오버 로드 된 버전을 사용 하는 경우  
 다음 경우에는 일련의 오버 로드 된 버전을 정의 고려할 수 있습니다.  
  
- 호출 되지를 전달 합니다 적은 수의 값 보다 더 많은 매개 변수 배열에 알 수 있습니다.  
  
- 프로시저 코드에서 논리 호출 코드에서 전달 횟수 값에 따라 크게 다릅니다.  
  
- 호출 코드에서 서로 다른 데이터 형식의 값을 전달할 수 있습니다.  
  
#### <a name="when-to-use-a-parameter-array"></a>매개 변수 배열을 사용 하는 경우  
 여는 것이 좋습니다는 `ParamArray` 다음과 같은 경우 매개 변수:  
  
- 호출 코드에서 매개 변수 배열에 전달할 수는 얼마나 많은 값을 예측할 수 없는 및 많은 수 있습니다.  
  
- 프로시저 논리가 기본적으로 모든 값에 동일한 작업을 수행 하는 호출 코드가 전달 되는 모든 값을 반복에 적합 합니다.  
  
 자세한 내용은 [매개 변수 배열](./parameter-arrays.md)합니다.  
  
## <a name="implicit-overloads-for-optional-parameters"></a>선택적 매개 변수에 대 한 암시적 오버 로드  
 사용 하 여 프로시저를 [선택 사항](../../../../visual-basic/language-reference/modifiers/optional.md) 매개 변수는 선택적 매개 변수를 사용 하 여 하나 및 하지 않는 두 개의 오버 로드 된 프로시저입니다. 이 중 하나에 해당 하는 매개 변수 목록을 사용 하 여 이러한 프로시저를 오버 로드할 수 없습니다. 있습니다. 다음 선언은이 보여 줍니다.  
  
 [!code-vb[VbVbcnProcedures#58](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#58)]  
  
 [!code-vb[VbVbcnProcedures#60](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#60)]  
  
 [!code-vb[VbVbcnProcedures#61](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#61)]  
  
 둘 이상의 선택적 매개 변수를 사용 하 여 프로시저를 앞의 예제와 비슷한 논리에서 도착 하는 암시적 오버 로드의 집합이 있습니다.  
  
## <a name="implicit-overloads-for-a-paramarray-parameter"></a>ParamArray 매개 변수에 대해 암시적 오버 로드  
 컴파일러에서 사용 하 여 프로시저를 고려 하는 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) 무한 수의 오버 로드가 어떤 호출 코드에서 전달 된 매개 변수 배열에 다음과 같이 서로 다른 매개 변수:  
  
- 호출 코드에 인수를 제공 하지 않는 한 오버 로드는 `ParamArray`  
  
- 호출 코드는 1 차원 배열의 제공 하는 경우 하나의 오버 로드는 `ParamArray` 요소 형식  
  
- 양의 정수에 대해 하나의 오버 로드에 대 한 호출 코드의 각 인수를 해당 수를 제공 하는 경우는 `ParamArray` 요소 형식  
  
 다음 선언에서는 이러한 암시적 오버 로드를 보여 줍니다.  
  
 [!code-vb[VbVbcnProcedures#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#68)]  
  
 [!code-vb[VbVbcnProcedures#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#70)]  
  
 매개 변수 배열은 1 차원 배열의 사용 하는 매개 변수 목록 사용 하 여 이러한 프로시저를 오버 로드할 수 없습니다. 그러나 다른 암시적 오버 로드의 시그니처를 사용할 수 있습니다. 다음 선언은이 보여 줍니다.  
  
 [!code-vb[VbVbcnProcedures#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#71)]  
  
## <a name="typeless-programming-as-an-alternative-to-overloading"></a>오버 로드 하는 대신 관대 한 형식의 프로그래밍  
 호출 코드가 데이터 형식이 서로 다른 매개 변수를 전달할 수 있도록 하려는 경우 또 다른 방법은 관대 한 형식의 프로그래밍입니다. 형식 검사 스위치를 설정할 수 있습니다 `Off` 중 하나를 사용 하 여 합니다 [Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 또는 [/optionstrict](../../../../visual-basic/reference/command-line-compiler/optionstrict.md) 컴파일러 옵션입니다. 다음 매개 변수의 데이터 형식을 선언할 필요가 없습니다. 그러나이 접근 방식에는 오버 로드에 비해 다음과 같은 단점이 있습니다.  
  
- 관대 한 형식의 프로그래밍 비효율적인 실행 코드를 생성합니다.  
  
- 프로시저는 전달 될 수 있는 모든 데이터 형식에 대해 테스트 해야 합니다.  
  
- 호출 코드에서 프로시저를 지원 하지 않는 데이터 형식을 전달 하는 경우 오류가 컴파일러에 알립니다 수 없습니다.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [프로시저 문제 해결](./troubleshooting-procedures.md)
- [방법: 여러 버전의 프로시저 정의](./how-to-define-multiple-versions-of-a-procedure.md)
- [방법: 오버 로드 된 프로시저 호출](./how-to-call-an-overloaded-procedure.md)
- [방법: 선택적 매개 변수를 사용 하는 프로시저 오버 로드](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [방법: 무한 개수의 매개 변수를 사용 하는 프로시저 오버 로드](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [오버로드 확인](./overload-resolution.md)
- [오버로드](../../../../visual-basic/language-reference/modifiers/overloads.md)
