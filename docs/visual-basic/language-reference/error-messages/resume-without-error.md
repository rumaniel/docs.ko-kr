---
title: 오류 없이 계속됩니다.
ms.date: 07/20/2015
f1_keywords:
- vbrID20
ms.assetid: f9631804-fd36-4443-b36c-30db827e6176
ms.openlocfilehash: 61332486b20af66af24eac06b222a38353578c16
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62055162"
---
# <a name="resume-without-error"></a>오류 없이 계속됩니다.
`Resume` 문을 오류 처리 코드 외부에 있거나 오류가 없는 경우에 코드 오류 처리기로 점프 합니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 이동 된 `Resume` 오류 처리기로 문 또는 삭제 합니다.  
  
2. 오류 처리기를 식별 하는 레이블에 대 한 프로시저를 검색 프로시저에서 레이블로 점프 발생할 수 없습니다. 대상으로 지정 하는 레이블과 중복 하는 경우는 `GoTo` 문이 아닌는 `On Error GoTo` 문에서 원하는 대상와 일치 하도록 줄 레이블을 변경 합니다.  
  
## <a name="see-also"></a>참고자료

- [Resume 문](../../../visual-basic/language-reference/statements/resume-statement.md)
- [On Error 문](../../../visual-basic/language-reference/statements/on-error-statement.md)
