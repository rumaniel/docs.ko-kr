---
title: Visual Basic에서 속성과 변수의 차이점
ms.date: 07/20/2015
helpviewer_keywords:
- property values [Visual Basic]
- variables [Visual Basic]
- Visual Basic code, procedures
- values [Visual Basic], properties
- variables [Visual Basic], definition
- Visual Basic code, variables
- Visual Basic code, properties
- properties [Visual Basic], values
- properties [Visual Basic], defined
- variables [Visual Basic], and properties
- properties [Visual Basic], and variables
ms.assetid: 7a03a8be-5381-431f-bd7c-16e887e4e07b
ms.openlocfilehash: de4800e23519c2cc1c8b2b219287b9fa018b9bbf
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61864576"
---
# <a name="differences-between-properties-and-variables-in-visual-basic"></a>Visual Basic에서 속성과 변수의 차이점
변수 및 속성에 모두 액세스할 수 있는 값을 나타냅니다. 그러나 저장소 구현에는 차이점이 있습니다.  
  
## <a name="variables"></a>변수  
 A *변수* 메모리 위치에 직접 해당 합니다. 단일 선언 문 사용 하 여 변수를 정의할 수 있습니다. 변수를 사용할 수는 *지역 변수*, 정의 된 프로시저 안에 있는 및 해당 프로시저 내 에서만 사용할 수 있습니다 또는 수를 *멤버 변수*, 모듈, 클래스 또는 구조체의 내부가 아닌 모든 정의 프로시저입니다. 멤버 변수 라고 한 *필드*합니다.  
  
## <a name="properties"></a>속성  
 A *속성* 모듈, 클래스 또는 구조에 정의 된 데이터 요소입니다. 사이의 코드 블록을 사용 하 여 속성을 정의 합니다 `Property` 및 `End Property` 문입니다. 코드 블록에는 `Get` 프로시저는 `Set` 프로시저 중 하나 또는 둘 다. 이러한 프로시저는 호출 *속성 프로시저* 하거나 *속성 접근자*합니다. 검색 또는 속성의 값을 저장 하는 것 외에도 액세스 카운터를 업데이트 하는 등의 사용자 지정 작업을 수행할 수도 있습니다.  
  
## <a name="differences"></a>차이점  
 다음 표에서 변수 및 속성 간의 몇 가지 중요 한 차이점을 보여 줍니다.  
  
|차이점|변수|속성|  
|-------------------------|--------------|--------------|  
|선언|단일 선언문|일련의 문 코드 블록에|  
|구현|단일 저장소 위치|실행 코드 (property 프로시저)|  
|스토리지|변수의 값을 사용 하 여 직접 연결|일반적으로는 내부 저장소 속성의 포함 된 클래스나 모듈 외부에 사용할 수 없음<br /><br /> 속성의 값은 저장 된 요소로 존재 하지 않을 수도 <sup>1</sup>|  
|실행 코드|없음|프로시저를 적어도 하나 있어야 합니다.|  
|읽기 및 쓰기 액세스|읽기/쓰기 또는 읽기 전용|읽기/쓰기, 읽기 전용 또는 쓰기 전용|  
|사용자 지정 작업 (또는 외에도 수락 값 반환)|불가능|속성 값을 검색 또는 설정의 일부로 수행할 수 있습니다.|  
  
 <sup>1</sup> 변수와 달리 속성의 값은 저장소의 단일 항목에 직접 맞지 않을 수 있습니다. 저장소 편의 또는 보안에 대 한 부분으로 분할할 수 있습니다 또는 암호화 된 형식으로 값을 저장할 수 있습니다. 이러한 경우는 `Get` 프로시저는 구성 요소 조립 또는 저장 된 값을 해독 및 `Set` 프로시저는 새 값을 암호화 또는 구성 저장소로 분할 합니다. 속성 값이 경우, 하루 중 시간과 같은 사용 후 삭제 될 수 있습니다는 `Get` 프로시저 계산 하 고 즉석에서 속성에 액세스할 때마다 합니다.  
  
## <a name="see-also"></a>참고자료

- [속성 프로시저](./property-procedures.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [Property 문](../../../../visual-basic/language-reference/statements/property-statement.md)
- [Dim 문](../../../../visual-basic/language-reference/statements/dim-statement.md)
- [방법: 속성 만들기](./how-to-create-a-property.md)
- [방법: 액세스 수준이 혼합된 된 속성 선언](./how-to-declare-a-property-with-mixed-access-levels.md)
- [방법: 속성 프로시저 호출](./how-to-call-a-property-procedure.md)
- [방법: 선언 및 Visual Basic의 기본 속성을 호출](./how-to-declare-and-call-a-default-property.md)
- [방법: 속성 값 입력](./how-to-put-a-value-in-a-property.md)
- [방법: 속성에서 값 가져오기](./how-to-get-a-value-from-a-property.md)
