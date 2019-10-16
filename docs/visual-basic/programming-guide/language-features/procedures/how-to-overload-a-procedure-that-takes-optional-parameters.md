---
title: '방법: 선택적 매개 변수 (Visual Basic)를 사용 하는 프로시저 오버 로드'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], parameters
- procedure overloading [Visual Basic], optional parameters
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- procedure parameters
- procedures [Visual Basic], overloading
- procedures [Visual Basic], multiple versions
ms.assetid: 825f9d56-4cde-43fd-993a-b9171717e2eb
ms.openlocfilehash: 4374a229392d51b67c99210da91ae05dd3342e96
ms.sourcegitcommit: 10986410e59ff29f2ec55c6759bde3eb4d1a00cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66424061"
---
# <a name="how-to-overload-a-procedure-that-takes-optional-parameters-visual-basic"></a>방법: 선택적 매개 변수 (Visual Basic)를 사용 하는 프로시저 오버 로드
프로시저에 있는 경우 하나 이상의 [선택 사항](../../../../visual-basic/language-reference/modifiers/optional.md) 매개 변수를 암시적 오버 로드 중 하 나와 일치 하는 오버 로드 된 버전을 정의할 수 없습니다. 자세한 내용은 "암시적 오버 로드에 대 한 선택적 매개 변수"를 참조 하세요 [프로시저 오버 로드의 고려 사항](./considerations-in-overloading-procedures.md)합니다.  
  
## <a name="one-optional-parameter"></a>하나의 선택적 매개 변수  
  
#### <a name="to-overload-a-procedure-that-takes-one-optional-parameter"></a>하나의 선택적 매개 변수를 사용 하는 프로시저 오버 로드  
  
1. 작성 한 `Sub` 또는 `Function` 매개 변수 목록의 선택적 매개 변수를 포함 하는 선언문입니다. 사용 하지 마십시오는 `Optional` 이 오버 로드 된 버전의 키워드입니다.  
  
2. 앞에 야 합니다 `Sub` 또는 `Function` 키워드를 사용 합니다 [오버 로드](../../../../visual-basic/language-reference/modifiers/overloads.md) 키워드입니다.  
  
3. 호출 코드는 선택적 인수를 제공 하는 경우 실행 해야 하는 프로시저 코드를 작성 합니다.  
  
4. 사용 하 여 프로시저를 종료 합니다 `End Sub` 또는 `End Function` 문으로 적절 하 게 합니다.  
  
5. 첫 번째 선언에 동일한 점을 제외 하 고 선택적 매개 변수는 매개 변수 목록에 포함 되지 않습니다 하는 두 번째 선언문을 작성 합니다.  
  
6. 호출 코드 선택적 인수를 제공 하지 않는 경우 실행 해야 하는 프로시저 코드를 작성 합니다. 사용 하 여 프로시저를 종료 합니다 `End Sub` 또는 `End Function` 문으로 적절 하 게 합니다.  
  
     다음 예제에서는 두 오버 로드 된 프로시저 및 마지막으로 잘못 된 및 유효한 오버 로드 된 버전의 예제 집합을 해당 하는 선택적 매개 변수를 사용 하 여 정의 된 프로시저를 보여 줍니다.  
  
     [!code-vb[VbVbcnProcedures#59](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#59)]  
  
     [!code-vb[VbVbcnProcedures#60](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#60)]  
  
     [!code-vb[VbVbcnProcedures#61](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#61)]  
  
## <a name="multiple-optional-parameters"></a>여러 선택적 매개 변수  
 일반적으로 둘 이상의 선택적 매개 변수를 사용 하 여 프로시저를 두 개 이상의 오버 로드 된 버전이 필요합니다. 예를 들어, 두 가지 선택적 매개 변수를 호출 하는 코드 수 제공 또는 서로 독립적으로 각각을 생략 하는 경우 제공 된 인수의 가능한 각 조합에 대해 하나씩 네 개의 오버 로드 된 버전이 필요 합니다.  
  
 선택적 매개 변수 수가 늘어나면 오버 로드의 복잡성이 증가 합니다. 이 아닌 경우 제공 된 인수의 일부 조합은 허용 되지 않는 선택적 매개 변수 N 필요 2 ^ N 오버 로드 된 버전입니다. 프로시저의 특성에 따라는 논리의 명확성 들여야 모든 오버 로드 된 버전을 정의 하는 것을 확인할 수 있습니다.  
  
#### <a name="to-overload-a-procedure-that-takes-more-than-one-optional-parameter"></a>둘 이상의 선택적 매개 변수를 사용 하는 프로시저 오버 로드  
  
1. 프로시저의 논리를 제공 된 선택적 인수의 조합을 결정 합니다. 허용 된 조합이 하나의 선택적 매개 변수는 다른 종속 된 경우에 발생할 수 있습니다. 예를 들어, 1 개의 매개 변수가 사람 이름이 허용 하 고 다른 사람의 나이 수락, 보존 기간을 제공 하지만 이름을 생략 인수의 조합을 허용 되지 않습니다.  
  
2. 선택적 인수를 제공 된 각 허용 가능한 조합에 대해 작성 된 `Sub` 또는 `Function` 해당 매개 변수 목록을 정의 하는 선언문입니다. 사용 하지 마십시오는 `Optional` 키워드입니다.  
  
3. 각 선언 앞에 `Sub` 또는 `Function` 키워드를 사용 합니다 [오버 로드](../../../../visual-basic/language-reference/modifiers/overloads.md) 키워드입니다.  
  
4. 각 선언 다음 호출 코드를 해당 선언 매개 변수 목록에 해당 하는 인수 목록을 제공 하는 경우 실행 해야 하는 프로시저 코드를 작성 합니다.  
  
5. 각 프로시저를 종료 합니다 `End Sub` 또는 `End Function` 문으로 적절 하 게 합니다.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [선택적 매개 변수](./optional-parameters.md)
- [매개 변수 배열](./parameter-arrays.md)
- [프로시저 오버로딩](./procedure-overloading.md)
- [프로시저 문제 해결](./troubleshooting-procedures.md)
- [방법: 여러 버전의 프로시저 정의](./how-to-define-multiple-versions-of-a-procedure.md)
- [방법: 오버 로드 된 프로시저 호출](./how-to-call-an-overloaded-procedure.md)
- [방법: 무한 개수의 매개 변수를 사용 하는 프로시저 오버 로드](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [오버로드 확인](./overload-resolution.md)
