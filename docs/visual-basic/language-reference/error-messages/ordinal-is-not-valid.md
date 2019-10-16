---
title: 서수가 잘못되었습니다.
ms.date: 07/20/2015
f1_keywords:
- vbrID452
ms.assetid: 7459562b-cd4f-4590-95e0-6126ae3589a5
ms.openlocfilehash: 740243c744a7ba5391659894812a00d80555fd80
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665661"
---
# <a name="ordinal-is-not-valid"></a>서수가 잘못되었습니다.
프로시저 이름 대신 숫자를 사용 하는 동적 연결 라이브러리 (DLL)를 호출 하 여 표시를 사용 하는 `#num` 구문입니다. 이 오류는 다음과 같은 가능한 원인을:  
  
- 변환 하려는 시도 `#num` 식 실패 하는 서 수입니다.  
  
- `#num` 지정 된 DLL에서 함수를 지정 하지 않습니다.  
  
- 형식 라이브러리에는 잘못 된 서 수의 내부 사용에 잘못 된 선언이 있습니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 식이 올바른 숫자를 나타내는 있는지 확인 하거나 이름으로 프로시저를 호출 합니다.  
  
2. 했는지 `#num` DLL에서 함수를 잘못 식별 합니다.  
  
3. 코드를 주석으로 처리 하 여 문제를 일으키는 프로시저 호출을 격리 합니다. 쓰기를 `Declare` 문을 프로시저를 한 형식 라이브러리 공급 업체에 문제를 보고 합니다.  
  
## <a name="see-also"></a>참고자료

- [Declare 문](../../../visual-basic/language-reference/statements/declare-statement.md)
