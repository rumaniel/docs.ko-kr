---
title: Visual Basic에서 ienumerable 인터페이스를 구현합니다.
ms.date: 07/31/2018
helpviewer_keywords:
- control flow [Visual Basic]
- enumerable interfaces
- loop structures [Visual Basic], optimizing performance
- control flow [Visual Basic]
ms.assetid: c60d7589-51f2-4463-a2d5-22506bbc1554
ms.openlocfilehash: b13fd85ae01fd0b6f3c963d87a372add930be99d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61975301"
---
# <a name="walkthrough-implementing-ienumerableof-t-in-visual-basic"></a>연습: Visual Basic에서 IEnumerable(Of T) 구현
<xref:System.Collections.Generic.IEnumerable%601> 인터페이스는 한 번에 하나의 항목 값의 시퀀스를 반환할 수 있는 클래스에서 구현 됩니다. 한 번에 하나의 항목은 메모리에 로드할 데이터의 전체 집합 작업할 필요가 없습니다 데이터 반환 활용 합니다. 충분 한 메모리를 사용 하 여 데이터의 단일 항목을 로드 해야 합니다. 구현 하는 클래스를 `IEnumerable(T)` 인터페이스를 사용 하 여 사용할 수 `For Each` 루프 또는 LINQ 쿼리 합니다.  
  
 예를 들어 큰 텍스트 파일을 읽고 특정 검색 조건과 일치 하는 파일에서 각 줄을 반환 해야 하는 응용 프로그램을 고려 합니다. 지정된 된 조건과 일치 하는 파일의 줄을 반환 하는 LINQ 쿼리를 사용 하는 응용 프로그램입니다. LINQ 쿼리를 사용 하 여 파일의 콘텐츠를 쿼리하려면 응용 프로그램 배열 또는 컬렉션에 파일의 내용을 로드할 수 있습니다. 그러나 전체 파일을 로드 하는 배열 또는 컬렉션에 필요한 것 보다 훨씬 더 많은 메모리를 사용 합니다. 대신 LINQ 쿼리 검색 조건과 일치 하는 값만 반환 하는 열거 가능한 클래스를 사용 하 여 파일 콘텐츠를 쿼리할 수 있습니다. 일부만 반환 하는 쿼리 훨씬 적은 메모리를 소모는 일치 하는 값입니다.  
  
 구현 하는 클래스를 만들 수는 <xref:System.Collections.Generic.IEnumerable%601> 열거 가능한 데이터와 원본 데이터를 노출 하는 인터페이스입니다. 구현 하는 클래스를 `IEnumerable(T)` 인터페이스를 구현 하는 다른 클래스 해야 합니다.는 <xref:System.Collections.Generic.IEnumerator%601> 원본 데이터를 반복 하는 인터페이스입니다. 이 두 클래스를 사용 하면 데이터 항목을 특정 형식으로 순차적으로 반환할 수 있습니다.  
  
 이 연습에서는 구현 하는 클래스를 만든를 `IEnumerable(Of String)` 인터페이스와 구현 하는 클래스를 `IEnumerator(Of String)` 번에 한 줄씩 텍스트 파일 읽기에 대 한 인터페이스입니다.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="creating-the-enumerable-class"></a>Enumerable 클래스 만들기  
  
**Enumerable 클래스 프로젝트를 만들려면**

1. Visual basic의 경우에 **파일** 메뉴에서 **새로 만들기** 을 클릭 한 다음 **프로젝트**.

1. **새 프로젝트** 대화 상자의 **프로젝트 형식** 창에서 **Windows**가 선택되었는지 확인합니다. **템플릿** 창에서 **클래스 라이브러리**를 선택합니다. **이름** 상자에 `StreamReaderEnumerable`를 입력한 다음 **확인**을 클릭합니다. 새 프로젝트가 표시 됩니다.

1. **솔루션 탐색기**Class1.vb 파일을 마우스 오른쪽 단추로 클릭 하 고 클릭 **이름 바꾸기**합니다. 파일 이름을 `StreamReaderEnumerable.vb`으로 바꾸고 ENTER 키를 누릅니다. 파일 이름을 바꾸면 클래스 이름도 `StreamReaderEnumerable`으로 바뀝니다. 이 클래스는 `IEnumerable(Of String)` 인터페이스를 구현합니다.

1. StreamReaderEnumerable 프로젝트를 마우스 오른쪽 **추가**를 클릭 하 고 **새 항목**합니다. 선택 된 **클래스** 템플릿. 에 **이름을** 상자에 입력 `StreamReaderEnumerator.vb` 클릭 **확인**합니다.

 이 프로젝트의 첫 번째 클래스 enumerable 클래스 이며 구현 된 `IEnumerable(Of String)` 인터페이스입니다. 제네릭 인터페이스를 구현 하는 <xref:System.Collections.IEnumerable> 인터페이스와이 클래스의 소비자로 형식화 된 값에 액세스할 수 있도록 보장 `String`합니다.  
  
**IEnumerable을 구현 하는 코드를 추가 합니다.**

1. StreamReaderEnumerable.vb 파일을 엽니다.

2. 다음 줄에 `Public Class StreamReaderEnumerable`를 입력 한 다음 ENTER 키를 누릅니다.

     [!code-vb[VbVbalrIteratorWalkthrough#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#1)]

   Visual Basic에 필요한 멤버를 사용 하 여 클래스를 자동으로 채우려고 합니다 `IEnumerable(Of String)` 인터페이스입니다.
  
3. 이 enumerable 클래스는 한 번에는 한 줄씩 텍스트 파일에서에서 줄을 읽습니다. 파일 경로 입력된 매개 변수로 받아들이는 public 생성자를 노출 하려면 클래스에 다음 코드를 추가 합니다.

     [!code-vb[VbVbalrIteratorWalkthrough#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#2)]

4. 구현의 합니다 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 메서드를 `IEnumerable(Of String)` 인터페이스의 새 인스턴스를 반환 합니다는 `StreamReaderEnumerator` 클래스. 구현의 `GetEnumerator` 메서드를 `IEnumerable` 인터페이스를 만들 수 있습니다 `Private`의 구성원만 노출 해야 하므로는 `IEnumerable(Of String)` 인터페이스. Visual Basic에 대해 생성 된 코드는 `GetEnumerator` 메서드를 다음 코드로 합니다.

     [!code-vb[VbVbalrIteratorWalkthrough#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#3)]  
  
**IEnumerator를 구현 하는 코드를 추가 합니다.**

1. StreamReaderEnumerator.vb 파일을 엽니다.

2. 다음 줄에 `Public Class StreamReaderEnumerator`를 입력 한 다음 ENTER 키를 누릅니다.

     [!code-vb[VbVbalrIteratorWalkthrough#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#4)]

   Visual Basic에 필요한 멤버를 사용 하 여 클래스를 자동으로 채우려고 합니다 `IEnumerator(Of String)` 인터페이스입니다.

3. 열거자 클래스 텍스트 파일이 열리고 파일 I/O 파일에서 줄 읽기를 수행 합니다. 읽기에 대 한 텍스트 파일을 열고 파일 경로 입력된 매개 변수로 받아들이는 public 생성자를 노출 하려면 클래스에 다음 코드를 추가 합니다.

     [!code-vb[VbVbalrIteratorWalkthrough#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#5)]

4. `Current` 둘 다에 대 한 속성을 `IEnumerator(Of String)` 및 `IEnumerator` 으로 텍스트 파일에서 현재 항목을 반환 하는 인터페이스를 `String`입니다. 구현의 `Current` 의 속성을 `IEnumerator` 인터페이스를 만들 수 있습니다 `Private`의 멤버를 노출 해야 하므로는 `IEnumerator(Of String)` 인터페이스. Visual Basic에 대해 생성 된 코드는 `Current` 다음 코드를 사용 하 여 속성입니다.

     [!code-vb[VbVbalrIteratorWalkthrough#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#6)]

5. `MoveNext` 메서드를 `IEnumerator` 인터페이스 텍스트 파일에서 다음 항목으로 이동 하 고 반환 되는 값을 업데이트 하는 `Current` 속성입니다. 내용은 더 이상 항목이 없으면 합니다 `MoveNext` 메서드가 반환 되는 `False`이 고 그렇지 않으면 합니다 `MoveNext` 메서드가 반환 되는 `True`합니다. `MoveNext` 메서드에 다음 코드를 추가합니다.

     [!code-vb[VbVbalrIteratorWalkthrough#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#7)]

6. 합니다 `Reset` 메서드는 `IEnumerator` 인터페이스는 반복기를 텍스트 파일의 시작 부분을 가리키도록 지시 하 고 현재 항목 값을 지웁니다. `Reset` 메서드에 다음 코드를 추가합니다.

     [!code-vb[VbVbalrIteratorWalkthrough#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#8)]

7. 합니다 `Dispose` 메서드는 `IEnumerator` 인터페이스 보장 하는 반복기를 제거 하기 전에 관리 되지 않는 모든 리소스가 해제 합니다. 사용 되는 파일 핸들을 `StreamReader` 개체는 관리 되지 않는 리소스를 반복기 인스턴스를 제거 하기 전에 닫아야 합니다. Visual Basic에 대해 생성 된 코드는 `Dispose` 메서드를 다음 코드로 합니다.

     [!code-vb[VbVbalrIteratorWalkthrough#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#9)] 
  
## <a name="using-the-sample-iterator"></a>샘플 반복기 사용

 Enumerable 클래스를 구현 하는 개체를 필요로 하는 제어 구조와 함께 코드에서 사용할 수 있습니다 `IEnumerable`와 같은 `For Next` 루프 또는 LINQ 쿼리입니다. 다음 예제는 `StreamReaderEnumerable` LINQ 쿼리에서 합니다.  
  
 [!code-vb[VbVbalrIteratorWalkthrough#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/Module1.vb#10)]  
  
## <a name="see-also"></a>참고자료

- [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [제어 흐름](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)
- [루프 구조](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)
- [For Each...Next 문](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)
