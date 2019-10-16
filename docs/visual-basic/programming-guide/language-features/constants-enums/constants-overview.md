---
title: 상수 개요(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- constants [Visual Basic]
ms.assetid: 29016fe8-78b3-4dc8-90b8-1cfec2fa8ac9
ms.openlocfilehash: 0c866f3d03d26bd882d5a6596d40d1dc639da011
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69934779"
---
# <a name="constants-overview-visual-basic"></a>상수 개요(Visual Basic)
상수는 변경 되지 않는 숫자 또는 문자열을 대신 사용 하는 의미 있는 이름입니다. 상수는 이름이 암시 하는 것 처럼 응용 프로그램 실행 전체에서 동일 하 게 유지 되는 값을 저장 합니다. 코드의 가독성을 크게 향상 시키고 상수를 사용 하 여 더 쉽게 유지 관리할 수 있습니다. 이러한 값을 포함 하는 코드에서 사용 하거나, 기억할 수 없는 특정 숫자에 따라 달라 지는 코드 또는 분명 한 의미가 없는 코드에서 사용 합니다.  
  
## <a name="how-to-create-and-use-constants"></a>상수를 만들고 사용 하는 방법  
 Visual Basic에는 인쇄 및 표시를 위해 주로 사용 되는 미리 정의 된 여러 상수가 포함 되어 있습니다. 변수 이름을 만드는 것과 동일한 지침을 사용 `Const` 하 여 문을 사용 하 여 사용자 고유의 상수를 만들 수도 있습니다. `Option Strict` 가`On`이면 상수 형식을 명시적으로 선언 해야 합니다.  
  
 이름을 한정 하지 않고이를 참조할 수 있는 모든 코드 집합인 상수 범위는 동일한 위치에 선언 된 변수의 변수와 동일 합니다. 특정 프로시저의 범위 내에 있는 상수를 만들려면 해당 프로시저 내에서 선언 합니다. 응용 프로그램 전체에서 사용할 수 있는 상수를 만들려면 클래스의 선언 섹션에서 `Public` 키워드를 사용 하 여 선언 합니다.  
  
> [!NOTE]
> 상수는 변수와 유사 하지만 변수를 수정할 수 있는 값으로 변경 하거나 새 값을 할당할 수 없습니다.  
  
 사용자가 작업 하는 컨트롤 또는 구성 요소에 대 한 개체 모델을 사용 하 여 코드에서 사용 하는 상수를 정의 하거나 사용자가 직접 만든 상수를 사용자가 정의할 수 있습니다.  
  
## <a name="compile-time-and-run-time-constants"></a>컴파일 시간 및 런타임 상수  
 컴파일 타임 상수는 코드를 컴파일할 때 계산 되지만 런타임 상수는 응용 프로그램이 실행 되는 동안에만 계산할 수 있습니다. 컴파일 타임 상수는 응용 프로그램이 실행 될 때마다 동일한 값을 갖게 되지만 런타임 상수는 매번 변경 될 수 있습니다. 배열 범위, case 식 또는 열거자 이니셜라이저와 같은 경우에는 컴파일 시간 상수가 필요 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|정의|용어|  
|---|---|  
|[방법: 상수 선언](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)|`Const` 문을 사용 하 여 상수를 선언 하 고 값을 설정 하는 방법을 설명 합니다. 상수를 선언 하 여 값에 의미 있는 이름을 할당 합니다.|  
|[사용자 정의 상수](../../../../visual-basic/programming-guide/language-features/constants-enums/user-defined-constants.md)|범위 지정 및 순환 참조를 방지 하는 방법에 대 한 정보를 포함 하 여 고유한 상수를 만드는 방법을 설명 합니다.|  
|[상수 및 리터럴 데이터 형식](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)|가 해제 될 때 `Option Explicit` Visual Basic 컴파일러가 상수를 초기화 하는 방법에 대 한 정보를 제공 합니다.|  
|[방법: 관련 상수 값 그룹화](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-group-related-constant-values-together.md)|관련 된 상수 값을 그룹화 하는 방법을 보여 줍니다.|  
  
## <a name="reference"></a>참조  
  
|정의|용어|  
|---|---|  
|[상수 및 열거형](../../../../visual-basic/language-reference/constants-and-enumerations.md)|Visual Basic에서 미리 정의 된 상수를 나열 합니다.|  
|[Const 문](../../../../visual-basic/language-reference/statements/const-statement.md)|`Const` 문과 사용에 대해 설명 합니다.|  
|[Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md)|`Option Strict` 문과 사용에 대해 설명 합니다.|  
  
## <a name="see-also"></a>참고자료

- [열거형 개요](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)
- [방법: Visual Basic에서 배열 변수를 초기화 합니다.](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)
