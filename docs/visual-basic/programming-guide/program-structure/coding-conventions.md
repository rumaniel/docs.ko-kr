---
title: Visual Basic 코딩 규칙
ms.date: 07/20/2015
helpviewer_keywords:
- coding conventions [Visual Basic], Visual Basic
- examples [Visual Basic], coding conventions
- Visual Basic code, conventions
ms.assetid: c1df130b-fec6-49a5-becf-0a7e494a1d0f
ms.openlocfilehash: 18c309e22cccfa5d835394996fc6974d95825b65
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72003113"
---
# <a name="visual-basic-coding-conventions"></a>Visual Basic 코딩 규칙
Microsoft는 이 항목의 지침에 따라 예제와 설명서를 개발합니다. 사용자가 동일한 코딩 규칙을 따른다면, 다음과 같은 이점을 얻을 수 있습니다.  
  
- 코드는 판독기 레이아웃이 아닌 내용에 집중할 수 있도록 일관된 모양을 갖습니다.  
  
- 읽는 사람이 이전 경험을 기반으로 예상할 수 있으므로 코드를 더 신속하게 이해합니다.  
  
- 코드를 더 쉽게 복사, 변경 및  유지 관리할 수 있습니다.  
  
- 코드가 Visual basic을 위한 "모범 사례"가 될 것입니다.  
  
## <a name="naming-conventions"></a>명명 규칙  
  
- 명명 지침에 대한 정보를 더 보려면, [명명 지침](../../../standard/design-guidelines/naming-guidelines.md) 항목을 참조하십시오.  
  
- 변수 이름의 일부로 "My" 또는 "my"를 사용하지 마십시오. 이것은 `My`개체와 혼동을 일으킵니다.  
  
- 지침에 맞게 자동으로 생성된 코드에서 개체의 이름을 변경할 필요가 없습니다.  
  
## <a name="layout-conventions"></a>레이아웃 규칙  
  
- 공백으로 탭을 삽입하고, 4칸 들여쓰기하는 스마트 들여쓰기를 사용하십시오.  
  
- 코드 편집기에서 코드의 서식을 재조정하기 위해서는 **Pretty listing(reformatting)of code** 옵션을 이용하십시오. 자세한 내용은 [옵션, 텍스트 편집기, 기본(Visual Basic)](/visualstudio/ide/reference/options-text-editor-basic-visual-basic)을 참조하십시오.  
  
- 한 줄에 하나의 문을 사용하십시오. Visual Basic의 줄 구분 기호 문자(:)를 사용하지 마십시오.  
  
- 언어에서 허용하더라도, 암시적 줄 연속 문자를 위해 명시적 줄 연속 문자 "_"를 사용하지 마십시오.  
  
- 한 줄에 하나의 선언만 사용하십시오.  
  
- 만약 **Pretty listing(reformatting)of code**가 연속 줄 형식을 자동으로 지정하지 않는다면, 수동으로 연속된 줄을 들여쓰기하십시오. 그러나 목록의 항목을 항상 왼쪽 맞춤으로 하십시오.  
  
    ```vb  
    a As Integer,  
    b As Integer  
    ```  
  
- 메서드와 속성의 정의 사이에는 하나 이상의 빈 줄을 추가하십시오.  
  
## <a name="commenting-conventions"></a>주석 규칙  
  
- 코드 줄의 끝이 아닌, 별도 줄에 주석을 작성하십시오.  
  
- 주석은 대문자로 시작하고, 주석의 끝에 마침표를 찍으십시오.  
  
- 주석 구분 기호(')와 주석 내용 사이에 빈 칸을 하나 삽입하십시오.  
  
     [!code-vb[VbVbalrGuidelines#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#2)]  
  
- 서식이 지정된 별표 블록으로 주석을 둘러싸지 마십시오.  
  
## <a name="program-structure"></a>프로그램 구조  
  
- @No__t-0 메서드를 사용 하는 경우 새 콘솔 응용 프로그램에 대 한 기본 구문을 사용 하 고 명령줄 인수에 대해 `My`을 사용 합니다.  
  
     [!code-vb[VbVbalrGuidelines#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#3)]  
  
## <a name="language-guidelines"></a>언어 지침  
  
### <a name="string-data-type"></a>문자열 데이터 형식  
  
- 다음 코드에 나와 있는 것처럼 [문자열 보간](https://docs.microsoft.com/dotnet/visual-basic/programming-guide/language-features/strings/interpolated-strings)을 사용하여 짧은 문자열을 연결합니다.
  
     ```vb
     MsgBox($"hello{vbCrLf}goodbye")
     ```
  
- 루프에서 문자열을 추가 하려면 <xref:System.Text.StringBuilder> 개체를 사용 합니다.  
  
     [!code-vb[VbVbalrGuidelines#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#5)]  
  
### <a name="relaxed-delegates-in-event-handlers"></a>완화된 대리자 이벤트 처리기  
 인수 (개체 및 EventArgs)를 이벤트 처리기로 명시적으로 한정 하지 마십시오. 이벤트에 전달 되는 이벤트 인수를 사용 하지 않는 경우 (예: sender as Object, e를 EventArgs로), 완화 된 대리자를 사용 하 고 이벤트 인수를 코드에 남겨 둡니다.  
  
 [!code-vb[VbVbalrGuidelines#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#7)]  
  
### <a name="unsigned-data-type"></a>부호 없는 데이터 형식  
  
- 필요한 경우를 제외 하 고는 부호 없는 형식 대신 `Integer`을 사용 합니다.  
  
### <a name="arrays"></a>배열  
  
- 선언 줄에서 배열을 초기화할 때는 간단한 구문을 사용 합니다. 예를 들어 다음 구문을 사용 합니다.  
  
     [!code-vb[VbVbalrGuidelines#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#8)]  
  
     다음 구문을 사용 하지 마십시오.  
  
     [!code-vb[VbVbalrGuidelines#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#9)]  
  
- 변수가 아니라 형식에 배열 지정자를 추가 합니다. 예를 들어 다음 구문을 사용 합니다.  
  
     [!code-vb[VbVbalrGuidelines#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#11)]  
  
     다음 구문을 사용 하지 마십시오.  
  
     [!code-vb[VbVbalrGuidelines#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#10)]  
  
- 기본 데이터 형식의 배열을 선언 하 고 초기화할 때 {} 구문을 사용 합니다. 예를 들어 다음 구문을 사용 합니다.  
  
     [!code-vb[VbVbalrGuidelines#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#12)]  
  
     다음 구문을 사용 하지 마십시오.  
  
     [!code-vb[VbVbalrGuidelines#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#13)]  
  
### <a name="use-the-with-keyword"></a>With 키워드 사용  
 하나의 개체에 대 한 일련의 호출을 수행 하는 경우 `With` 키워드를 사용 하는 것이 좋습니다.  
  
 [!code-vb[VbVbalrGuidelines#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#15)]  
  
### <a name="use-the-trycatch-and-using-statements-when-you-use-exception-handling"></a>Try ...를 사용 합니다. 예외 처리를 사용 하는 경우 문 Catch 및 사용  
 `On Error Goto`를 사용하지 마세요.  
  
### <a name="use-the-isnot-keyword"></a>IsNot 키워드 사용  
 -1 @no__t 대신 `IsNot` 키워드를 사용 합니다.  
  
### <a name="new-keyword"></a>New 키워드  
  
- 약식 인스턴스화를 사용 합니다. 예를 들어 다음 구문을 사용 합니다.  
  
     [!code-vb[VbVbalrGuidelines#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#21)]  
  
     위의 줄은 다음과 같습니다.  
  
     [!code-vb[VbVbalrGuidelines#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#22)]  
  
- 매개 변수가 없는 생성자 대신 새 개체에 대 한 개체 이니셜라이저를 사용 합니다.  
  
     [!code-vb[VbVbalrGuidelines#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#23)]  
  
### <a name="event-handling"></a>이벤트 처리  
  
- @No__t-1이 아닌 `Handles`을 사용 합니다.  
  
     [!code-vb[VbVbalrGuidelines#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#24)]  
  
- @No__t-0을 사용 하 고 대리자를 명시적으로 인스턴스화하지 않습니다.  
  
     [!code-vb[VbVbalrGuidelines#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#25)]  
  
- 이벤트를 정의할 때는 간단한 구문을 사용 하 고 컴파일러가 대리자를 정의 하도록 합니다.  
  
     [!code-vb[VbVbalrGuidelines#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#26)]  
  
- @No__t-1 메서드를 호출 하기 전에 이벤트가 @no__t 있는지 여부를 확인 하지 않습니다 (null). `RaiseEvent`은 이벤트를 발생 시키기 전에 `Nothing` 인지 확인 합니다.  
  
### <a name="using-shared-members"></a>공유 멤버 사용  
 인스턴스 변수가 아닌 클래스 이름을 사용 하 여 `Shared` 멤버를 호출 합니다.  
  
### <a name="use-xml-literals"></a>XML 리터럴 사용  
 XML 리터럴은 XML로 작업할 때 가장 자주 발생 하는 작업 (예: 로드, 쿼리 및 변환)을 단순화 합니다. XML을 사용 하 여 개발 하는 경우 다음 지침을 따르세요.  
  
- Xml Api를 직접 호출 하는 대신 xml 리터럴을 사용 하 여 XML 문서 및 조각을 만듭니다.  
  
- XML 리터럴에 대 한 성능 최적화를 활용 하려면 파일 또는 프로젝트 수준에서 XML 네임 스페이스를 가져옵니다.  
  
- Xml 축 속성을 사용 하 여 XML 문서의 요소 및 특성에 액세스 합니다.  
  
- @No__t-0 메서드와 같은 API 호출을 사용 하는 대신 포함 식을 사용 하 여 값을 포함 하 고 기존 값에서 XML을 만듭니다.  
  
     [!code-vb[VbVbalrGuidelines#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#27)]  
  
### <a name="linq-queries"></a>LINQ 쿼리  
  
- 쿼리 변수에 의미 있는 이름을 사용 합니다.  
  
     [!code-vb[VbVbalrGuidelines#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#28)]  
  
- 쿼리의 요소 이름을 지정 하 여 익명 형식의 속성 이름이 파스칼식 대/소문자를 사용 하 여 올바르게 대문자로 되어 있는지 확인 합니다.  
  
     [!code-vb[VbVbalrGuidelines#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#29)]  
  
- 결과의 속성 이름이 모호하면 속성 이름을 바꿉니다. 예를 들어 쿼리에서 고객 이름과 주문 ID를 반환 하는 경우 결과에서-0 @no__t으로 유지 하 고-1을 @no__t 하지 않고 이름을 바꿉니다.  
  
     [!code-vb[VbVbalrGuidelines#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#30)]  
  
- 쿼리 변수 및 범위 변수의 선언에서 형식 유추를 사용 합니다.  
  
     [!code-vb[VbVbalrGuidelines#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#31)]  
  
- @No__t-0 문 아래의 쿼리 절을 정렬 합니다.  
  
     [!code-vb[VbVbalrGuidelines#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#32)]  
  
- 이후 쿼리 절이 필터링 된 데이터 집합에 대해 작동 하도록 다른 쿼리 절 앞에 `Where` 절을 사용 합니다.  
  
     [!code-vb[VbVbalrGuidelines#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#33)]  
  
- @No__t-1 절을 사용 하 여 조인 작업을 암시적으로 정의 하는 대신 `Join` 절을 사용 하 여 조인 작업을 명시적으로 정의 합니다.  
  
     [!code-vb[VbVbalrGuidelines#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#34)]  
  
## <a name="see-also"></a>참조

- [보안 코딩 지침](../../../standard/security/secure-coding-guidelines.md)
