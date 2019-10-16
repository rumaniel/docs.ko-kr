---
title: Visual Basic의 수명
ms.date: 07/20/2015
helpviewer_keywords:
- static variables [Visual Basic], lifetime
- static variables [Visual Basic], Visual Basic
- declared elements [Visual Basic], lifetime
- Shared variable lifetime [Visual Basic]
- lifetime [Visual Basic], declared elements
- lifetime [Visual Basic], Visual Basic
- lifetime [Visual Basic]
ms.assetid: bd91e390-690a-469a-9946-8dca70bc14e7
ms.openlocfilehash: 7a8730834c5241ddb1271d689cdda8942741f15f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61917932"
---
# <a name="lifetime-in-visual-basic"></a>Visual Basic의 수명
합니다 *수명* 선언 된 요소의 기간 자신이 하는 동안 사용할 수 있습니다. 변수는 수명이 하는 유일한 요소입니다. 이 목적을 위해 컴파일러가 처리 프로시저 매개 변수 및 변수의 특별 한 경우로 반환 합니다. 변수의 수명 값을 보관할 수 있는 기간을 나타냅니다. 해당 값은 해당 수명 동안 변경할 수 있지만 항상 어떤 값을 가집니다.  
  
## <a name="different-lifetimes"></a>다른 수명  
 A *멤버 변수* (다른 프로시저 외부 모듈 수준에서 선언 됨) 일반적으로 수명이 같은 선언 되는 요소입니다. 클래스 또는 구조체에서 선언 하는 비공유 변수 또는 선언 된 구조체는 클래스의 각 인스턴스에 대해 별도 복사본으로 존재 합니다. 각 변수는 해당 인스턴스로 수명이 동일 합니다. 그러나는 `Shared` 변수는 응용 프로그램이 실행 되는 전체 기간 동안 지속 되는 단일 수명만 가집니다.  
  
 A *지역 변수* (프로시저 내에서 선언 됨) 이전에 선언 된 프로시저를 실행 하는 동안에 존재 합니다. 또한 모든 함수를 반환 하는 프로시저의 매개 변수에 적용 됩니다이. 그러나 해당 프로시저가 다른 프로시저를 호출 하는 경우 지역 변수 값을 유지 호출된 된 프로시저가 실행 되는 동안.  
  
## <a name="beginning-of-lifetime"></a>수명의 시작  
 로컬 변수의 수명 제어가 이전에 선언 된 프로시저를 입력할 때 시작 합니다. 모든 로컬 변수 절차를 시작 하는 즉시 해당 데이터 형식에 대 한 기본 값으로 초기화 됩니다 실행 합니다. 프로시저를 발견할 경우는 `Dim` 를 초기 값을 지정 하는 문에서 해당 변수를 설정 하려면 이러한 값을 코드에 다른 값 할당 이미 있는 경우에 합니다.  
  
 구조체 변수의 각 멤버는 별도 변수 처럼 초기화 됩니다. 마찬가지로, 각 요소의 배열 변수를 개별적으로 초기화 됩니다.  
  
 프로시저 내에서 블록 내에서 선언 된 변수 (예를 `For` 루프) 절차 항목에 초기화 됩니다. 이러한 초기화 코드 블록 실행 여부 적용 합니다.  
  
## <a name="end-of-lifetime"></a>수명 끝  
 프로시저 종료 되 면 해당 로컬 변수 값이 유지 되지 않습니다 하 고 Visual Basic의 메모리를 회수 합니다. 프로시저를 호출 하면 다음에 모든 로컬 변수 생성 새로 되어 다시 초기화 합니다.  
  
 클래스 또는 구조체의 인스턴스 종료 되 면 해당 메모리 및 해당 값 비공유 변수의 손실 됩니다. 클래스 또는 구조체의 새 인스턴스 각각 만들고 해당 공유 되지 않는 변수를 다시 초기화 합니다. 그러나 `Shared` 변수는 응용 프로그램 실행이 중지 될 때까지 유지 됩니다.  
  
## <a name="extension-of-lifetime"></a>수명의 확장  
 지역 변수를 선언 하는 경우는 `Static` 키워드, 수명이 해당 프로시저의 실행 시간 보다 오래입니다. 다음 표에서 프로시저 선언 기간 결정 하는 방법을 보여 줍니다는 `Static` 변수가 있습니다.  
  
|프로시저 위치 및 공유|정적 변수 수명을 시작합니다|정적 변수 수명 종료|  
|------------------------------------|-------------------------------------|-----------------------------------|  
|(기본적으로 공유 됨) 모듈의|프로시저가 호출 된 첫 번째 시간|응용 프로그램 실행을 중지 하는 경우|  
|클래스에서 `Shared` (절차는 인스턴스 멤버를이 아님)|처음으로 프로시저를 호출할 특정 인스턴스 또는 자체 클래스 또는 구조체 이름|응용 프로그램 실행을 중지 하는 경우|  
|클래스의 인스턴스에 없습니다 `Shared` (프로시저란 인스턴스 멤버)|특정 인스턴스에서 프로시저가 호출 된 첫 번째 시간|GC (가비지 수집)에 대 한 인스턴스가 해제 되는 경우|  
  
## <a name="static-variables-of-the-same-name"></a>이름이 같은 정적 변수  
 둘 이상의 프로시저에서 동일한 이름 가진 정적 변수를 선언할 수 있습니다. 이 작업을 수행 하는 경우 Visual Basic 컴파일러는 각 변수는 별도 요소를 고려 합니다. 이러한 변수 중 하나를 초기화는 다른 값을 적용 되지 않습니다. 오버 로드 집합을 사용 하 여 프로시저를 정의 하 고 각 오버 로드에 동일한 이름 가진 정적 변수를 선언 하는 경우에 마찬가지입니다.  
  
## <a name="containing-elements-for-static-variables"></a>정적 변수에 대 한 요소가 포함 된  
 해당 클래스의 프로시저 내부 즉, 클래스 내의 정적 지역 변수를 선언할 수 있습니다. 그러나 구조체 멤버 또는 해당 구조 내에서 프로시저의 지역 변수로 구조체에 정적 지역 변수를 선언할 수 없습니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 다음 예제에서는 사용 하 여 변수를 선언 합니다 [정적](../../../../visual-basic/language-reference/modifiers/static.md) 키워드입니다. (참고 필요 하지 않은 `Dim` 키워드 때를 [Dim 문](../../../../visual-basic/language-reference/statements/dim-statement.md) 와 같은 한정자를 사용 하 여 `Static`.)  
  
### <a name="code"></a>코드  
 [!code-vb[VbVbalrKeywords#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/class7.vb#13)]  
  
### <a name="comments"></a>설명  
 변수, 이전 예제의 `applesSold` 계속 절차 다음에 나오는 존재 `runningTotal` 호출 코드로 반환 합니다. 다음 번 `runningTotal` 가 호출 `applesSold` 는 이전에 계산 된 값을 유지 합니다.  
  
 하는 경우 `applesSold` 를 사용 하지 않고 선언 된 것 `Static`에 대 한 호출에서 누적 된 이전 값을 유지 되는 `runningTotal`합니다. 다음에 `runningTotal` 가 호출 되 면 `applesSold` 다시 되었으며 0으로 초기화 됩니다 및 `runningTotal` 는 호출 된 동일한 값을 반환 하기만 하면 됩니다.  
  
### <a name="compiling-the-code"></a>코드 컴파일  
 정적 지역 변수 선언의 일부로 값을 초기화할 수 있습니다. 배열을 선언 하는 경우 `Static`, 차수 (차원 수), 각 차원의 길이 및 개별 요소의 값을 초기화할 수 있습니다.  
  
### <a name="security"></a>보안  
 앞의 예제에서 선언 하 여 동일한 수명 주기를 생성할 수 있습니다 `applesSold` 모듈 수준입니다. 그러나 변수의 범위를이 이렇게 변경 하면 프로시저 단독으로 액세스할 수를 더 이상 됩니다. 다른 프로시저에 액세스할 수 있으므로 `applesSold` 및 해당 값을 변경, 누계를 신뢰할 수 없고 및 코드 관리가 더욱 어려워질 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [공유](../../../../visual-basic/language-reference/modifiers/shared.md)
- [Nothing](../../../../visual-basic/language-reference/nothing.md)
- [선언 요소 이름](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [선언된 요소 참조](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [Visual Basic의 범위](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)
- [Visual Basic의 액세스 수준](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [변수](../../../../visual-basic/programming-guide/language-features/variables/index.md)
- [변수 선언](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
- [데이터 형식 문제 해결](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [정적](../../../../visual-basic/language-reference/modifiers/static.md)
