---
title: LINQ를 지원하는 Visual Basic 기능
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic, LINQ features
- LINQ [Visual Basic], features supporting LINQ
ms.assetid: c821bb50-b6f6-4cf9-8aba-2717e465bd3a
ms.openlocfilehash: 155d5c36483accc12d066a5530fea20a563e1498
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61977563"
---
# <a name="visual-basic-features-that-support-linq"></a>LINQ를 지원하는 Visual Basic 기능
이름을 [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)] 쿼리 구문을 지원 하 고 다른 언어 구문이 도입 되면서 언어로 직접 Visual Basic의 기술을 나타냅니다. 사용 하 여 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)], 외부 데이터 원본에 대 한 쿼리는 새 언어를 배울 필요가 없습니다. Visual Basic을 사용 하 여 데이터 관계형 데이터베이스, XML 저장소 또는 개체에 대해 쿼리할 수 있습니다. 언어에 대 한 쿼리 기능이 통합이 컴파일 타임 구문 오류 및 형식 안전성 확인 수 있습니다. 이 통합은 또한 Visual Basic의 다양 한 기능의 다양 한 쿼리를 작성할 수 있는 새로운 대부분이 이미 알고 있다고 보장 합니다.  
  
 다음 섹션에서는 LINQ 소개 문서, 코드 예제 및 예제 응용 프로그램을 읽기 시작할 수 있도록 충분 한 세부 정보에서 지 원하는 언어 구문을 설명 합니다. 언어 기능 함께 일 하 언어 통합 쿼리를 사용 하도록 설정 하는 방법의 더 자세한 설명을 보려면 링크를 클릭할 수도 있습니다. 시작 하는 것이 좋습니다 [연습: Visual Basic에서 쿼리 작성](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md)합니다.  
  
## <a name="query-expressions"></a>쿼리 식  
 쿼리 식 Visual Basic에는 SQL 이나 XQuery와 유사한 선언적 구문으로 표현할 수 있습니다. 컴파일 타임에 쿼리 구문은 표준 쿼리 연산자 확장 메서드는 LINQ 공급자 구현에 대 한 메서드 호출으로 변환 됩니다. 표준 쿼리 연산자 범위에서 사용 하 여 해당 네임 스페이스를 지정 하 여 응용 프로그램 제어는 `Imports` 문입니다. Visual Basic 쿼리 식 구문은 다음과 같습니다.  
  
 [!code-vb[VbLINQVbFeatures#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#1)]  
  
 자세한 내용은 [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)합니다.  
  
## <a name="implicitly-typed-variables"></a>암시적으로 형식화 된 변수  
 대신 명시적으로 유형을 지정 하는 선언 하 고 변수를 초기화할 때 컴파일러 유추 하 고 할당 형식에 사용할 수 있습니다. 이 이라고 *지역 형식 유추*합니다.  
  
 변수 형식이 유추 되는 강력한 형식, 변수 형식을 명시적으로 지정 하 마찬가지로 합니다. 지역 형식 유추 메서드 본문 내의 지역 변수를 정의 하는 경우에 작동 합니다. 자세한 내용은 [Option Infer 문](../../../../visual-basic/language-reference/statements/option-infer-statement.md) 하 고 [로컬 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)합니다.  
  
 다음 예제에서는 로컬 형식 유추를 보여 줍니다. 이 예제를 사용 하려면 설정 해야 `Option Infer` 에 `On`입니다.  
  
 [!code-vb[VbLINQVbFeatures#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#2)]  
  
 지역 형식 유추를 통해 LINQ 쿼리에 필요한 및이 섹션의 뒷부분에서 설명 되는 무명 형식을 만들 수 있습니다.  
  
 다음 LINQ 예의 경우 형식 유추가 발생 `Option Infer` 중 하나는 `On` 또는 `Off`합니다. 컴파일 타임 오류가 발생 하는 경우 `Option Infer` 됩니다 `Off` 하 고 `Option Strict` 는 `On`합니다.  
  
 [!code-vb[VbLINQVbFeatures#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#3)]  
  
## <a name="object-initializers"></a>개체 이니셜라이저  
 개체 이니셜라이저는 쿼리 결과를 저장할 무명 형식을 만드는 경우 쿼리 식에 사용 됩니다. 또한 용도 쿼리 외부에서 명명 된 형식의 개체를 초기화 합니다. 개체 이니셜라이저를 사용 하 여 명시적으로 생성자를 호출 하지 않고 한 줄에 개체를 초기화할 수 있습니다. 라는 클래스가 있다고 가정 `Customer` 있는 공용 `Name` 고 `Phone` 속성을 다른 속성과 함께 개체 이니셜라이저를 사용할 수 이러한 방식으로:  
  
 [!code-vb[VbLINQVbFeatures#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#4)]  
  
 자세한 내용은 참조 하세요. [개체 이니셜라이저: 명명 된 형식과 익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)합니다.  
  
## <a name="anonymous-types"></a>익명 형식  
 익명 형식은 일시적으로 쿼리 결과에 포함 하려는 요소로 속성 집합을 그룹화 하는 편리한 방법을 제공 합니다. 이 요소에 대 한 명명 된 데이터 형식을 정의 하지 않고 순서에 관계 없이 쿼리에서 사용할 수 있는 필드의 조합을 선택할 수 있습니다.  
  
 *무명 형식* 컴파일러에 의해 동적으로 생성 됩니다. 컴파일러에 의해 할당 된 형식의 이름 및 각 새 컴파일으로 변경 될 수 있습니다. 따라서 이름은 직접 사용할 수 없습니다. 익명 형식은 다음과 같은 방법으로 초기화 됩니다.  
  
 [!code-vb[VbLINQVbFeatures#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#5)]  
  
 자세한 내용은 [무명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)을 참조하세요.  
  
## <a name="extension-methods"></a>확장명 메서드  
 확장 메서드를 사용 하면 메서드는 데이터 형식 또는 정의 외부에서 인터페이스를 추가할 수 있습니다. 이 기능을 사용 하면 실제로 형식이 실제로 수정 하지 않고도 기존 형식에 새 메서드를 추가할 수 있습니다. 표준 쿼리 연산자는 제공 하는 확장 메서드 집합을 자체 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리 기능을 구현 하는 모든 형식에 대 한 <xref:System.Collections.Generic.IEnumerable%601>합니다. 다른 확장을 <xref:System.Collections.Generic.IEnumerable%601> 포함 <xref:System.Linq.Enumerable.Count%2A>하십시오 <xref:System.Linq.Enumerable.Union%2A>, 및 <xref:System.Linq.Enumerable.Intersect%2A>합니다.  
  
 다음 확장 메서드를 추가 하는 인쇄 메서드를 <xref:System.String> 클래스입니다.  
  
 [!code-vb[VbLINQVbFeatures#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#6)]  
  
 일반적인 인스턴스 메서드와 같은 메서드는 <xref:System.String>:  
  
 [!code-vb[VbLINQVbFeatures#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#7)]  
  
 자세한 내용은 [확장 메서드](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)를 참조하세요.  
  
## <a name="lambda-expressions"></a>람다 식  
 람다 식은 계산 하 고 단일 값을 반환 하는 이름이 없는 함수입니다. 명명 된 함수와 달리 람다 식은 정의 하 고 동시에 실행 합니다. 다음 예에서는 4를 표시합니다.  
  
 [!code-vb[VbLINQVbFeatures#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#8)]  
  
 변수 이름에 람다 식 정의 할당 하 고 이름을 사용 하 여 함수를 호출할 수 있습니다. 다음 예제에는 4 표시 됩니다.  
  
 [!code-vb[VbLINQVbFeatures#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#12)]  
  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)], 람다 식의 기반이 되 다양 한 표준 쿼리 연산자입니다. 컴파일러는 람다 식과 같은 기본 쿼리 메서드에 정의 된 계산을 캡처하려면를 만듭니다 `Where`, `Select`, `Order By`, `Take While`, 등.  
  
 예를 들어, 다음 코드는 모든 학생 들이 선임에서 학생의 목록을 반환 하는 쿼리를 정의 합니다.  
  
 [!code-vb[VbLINQVbFeatures#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#9)]  
  
 쿼리 정의 대 한 인수를 지정 하려면 두 람다 식을 사용 하는 다음 예제와 유사한 코드로 컴파일될 `Where` 고 `Select`입니다.  
  
 [!code-vb[VbLINQVbFeatures#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#10)]  
  
 두 버전 중 하나를 사용 하 여 실행할 수 있습니다는 `For Each` 루프:  
  
 [!code-vb[VbLINQVbFeatures#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#11)]  
  
 자세한 내용은 [람다 식](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [LINQ(Language-Integrated Query)(Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/index.md)
- [Visual Basic에서 LINQ 시작](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)
- [LINQ 및 문자열 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)
- [Option Infer 문](../../../../visual-basic/language-reference/statements/option-infer-statement.md)
- [Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
