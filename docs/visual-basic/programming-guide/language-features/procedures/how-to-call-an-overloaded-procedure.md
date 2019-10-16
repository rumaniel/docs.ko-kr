---
title: '방법: 오버 로드 된 프로시저 호출 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- procedures [Visual Basic], overloading
- procedures [Visual Basic], calling
- procedures [Visual Basic], multiple versions
- procedure calls [Visual Basic], overloaded
ms.assetid: 3bb331fb-f6bc-406f-9ca0-9609b497014c
ms.openlocfilehash: d325c09516b4ce03facedce86f17ea49480b997a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61666016"
---
# <a name="how-to-call-an-overloaded-procedure-visual-basic"></a>방법: 오버 로드 된 프로시저 호출 (Visual Basic)
프로시저 오버 로드의 장점은 호출의 유연한입니다. 호출 코드를 프로시저에 전달 하 고 단일 프로시저 이름을 전달 하는 어떤 인수 없이 호출 하는 데 필요한 정보를 가져올 수 있습니다.  
  
### <a name="to-call-a-procedure-that-has-more-than-one-version-defined"></a>정의 된 버전이 둘 이상 있는 프로시저를 호출 하려면  
  
1. 호출 코드에서 프로시저에 전달할 데이터를 결정 합니다.  
  
2. 프로시저 호출 인수 목록의 데이터를 표시 합니다. 일반적인 방법으로 작성 합니다. 인수는 프로시저에 정의 된 버전 중 하나에 매개 변수 목록과 일치 해야 합니다.  
  
3. 호출 프로시저의 버전을 확인할 필요가 없습니다. Visual Basic에서 인수 목록과 일치 하는 버전 제어를 전달 합니다.  
  
     다음 예제에서는 합니다 `post` 프로시저에서 선언 [방법: 여러 버전의 프로시저 정의](./how-to-define-multiple-versions-of-a-procedure.md)합니다. 고객 id를 받아 인지 여부를 확인을 `String` 또는 `Integer`, 한 다음 두 경우 모두 같은 프로시저를 호출 합니다.  
  
     [!code-vb[VbVbcnProcedures#56](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#56)]  
  
     [!code-vb[VbVbcnProcedures#57](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#57)]  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [프로시저 오버로딩](./procedure-overloading.md)
- [프로시저 문제 해결](./troubleshooting-procedures.md)
- [방법: 여러 버전의 프로시저 정의](./how-to-define-multiple-versions-of-a-procedure.md)
- [방법: 선택적 매개 변수를 사용 하는 프로시저 오버 로드](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [방법: 무한 개수의 매개 변수를 사용 하는 프로시저 오버 로드](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [프로시저를 오버로드할 때 고려해야 할 사항](./considerations-in-overloading-procedures.md)
- [오버로드 확인](./overload-resolution.md)
- [오버로드](../../../../visual-basic/language-reference/modifiers/overloads.md)
