---
title: '방법: 무한 개수의 매개 변수 (Visual Basic)를 사용 하는 프로시저 오버 로드'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], parameters
- procedure overloading [Visual Basic], indefinite number of parameters
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- procedure parameters
- procedures [Visual Basic], overloading
- procedures [Visual Basic], multiple versions
ms.assetid: c7042de2-2422-4039-94e8-ac298896af69
ms.openlocfilehash: 3cf75fc6221364704379eb23d308481c34e6c0d6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61955742"
---
# <a name="how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters-visual-basic"></a>방법: 무한 개수의 매개 변수 (Visual Basic)를 사용 하는 프로시저 오버 로드
프로시저에 있는 경우는 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) 매개 변수를 1 차원 배열을 매개 변수 배열에 대 한 오버 로드 된 버전을 정의할 수 없습니다. 자세한 내용은 "암시적 오버 로드는 ParamArray 매개 변수"를 참조 하세요 [프로시저 오버 로드의 고려 사항](./considerations-in-overloading-procedures.md)합니다.  
  
### <a name="to-overload-a-procedure-that-takes-a-variable-number-of-parameters"></a>가변 개수의 매개 변수를 사용 하는 프로시저 오버 로드  
  
1. 절차 및 코드 논리 이점을 호출 버전 두 개를 오버 로드 확인을 `ParamArray` 매개 변수입니다. "오버 로드 및 ParamArrays"를 참조 하세요 [프로시저를 오버 로드할 고려 사항](./considerations-in-overloading-procedures.md)합니다.  
  
2. 제공 된 값의 숫자 프로시저 매개 변수 목록의 변수 부분에 적용 해야 할 결정 합니다. 이 값이 없는 경우 포함 하 고 단일 1 차원 배열의 경우를 포함 될 수 있습니다.  
  
3. 제공 된 값의 각 허용 되는 번호를 작성 한 `Sub` 또는 `Function` 해당 매개 변수 목록을 정의 하는 선언문입니다. 사용 하지 마세요 합니다 `Optional` 또는 `ParamArray` 이 오버 로드 된 버전의 키워드입니다.  
  
4. 각 선언 앞에 `Sub` 또는 `Function` 키워드를 사용 합니다 [오버 로드](../../../../visual-basic/language-reference/modifiers/overloads.md) 키워드입니다.  
  
5. 각 선언 다음 호출 하는 코드는 선언의 매개 변수 목록에 해당 하는 값을 제공 하는 경우 실행 해야 하는 프로시저 코드를 작성 합니다.  
  
6. 각 프로시저를 종료 합니다 `End Sub` 또는 `End Function` 문으로 적절 하 게 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 사용 하 여 정의 된 프로시저를 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) 매개 변수 및 오버 로드 된 프로시저의 해당 집합입니다.  
  
 [!code-vb[VbVbcnProcedures#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#69)]  
  
 [!code-vb[VbVbcnProcedures#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#70)]  
  
 매개 변수 배열은 1 차원 배열의 사용 하는 매개 변수 목록 사용 하 여 이러한 프로시저를 오버 로드할 수 없습니다. 그러나 다른 암시적 오버 로드의 시그니처를 사용할 수 있습니다. 다음 선언은이 보여 줍니다.  
  
 [!code-vb[VbVbcnProcedures#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#71)]  
  
 오버 로드 된 버전의에서 코드 호출 코드에 대 한 하나 이상의 값을 제공 했는지 여부를 테스트 하지 않아도 `ParamArray` 매개 변수를 그렇다면 또는 개수입니다. Visual Basic에서는 호출 인수 목록과 일치 하는 버전 제어를 전달 합니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 때문에 사용 하 여 프로시저를 `ParamArray` 매개 변수는 오버 로드 된 버전의 집합, 이러한 암시적 오버 로드 중 하나에 해당 하는 매개 변수 목록을 사용 하 여 이러한 프로시저를 오버 로드할 수 없습니다. 자세한 내용은 [프로시저 오버 로드의 고려 사항](./considerations-in-overloading-procedures.md)합니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 무한정 커질 수 있는 배열을 사용 하 여 처리할 때마다 응용 프로그램의 일부 내부 용량 오버런이 위험이 있습니다. 매개 변수 배열에 동의 하는 경우 호출 코드에 전달 된 배열의 길이 대 한 테스트 하 고 응용 프로그램에 비해 너무 큰 경우 적절 한 단계를 수행 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [선택적 매개 변수](./optional-parameters.md)
- [매개 변수 배열](./parameter-arrays.md)
- [프로시저 오버로딩](./procedure-overloading.md)
- [프로시저 문제 해결](./troubleshooting-procedures.md)
- [방법: 여러 버전의 프로시저 정의](./how-to-define-multiple-versions-of-a-procedure.md)
- [방법: 오버 로드 된 프로시저 호출](./how-to-call-an-overloaded-procedure.md)
- [방법: 선택적 매개 변수를 사용 하는 프로시저 오버 로드](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [오버로드 확인](./overload-resolution.md)
