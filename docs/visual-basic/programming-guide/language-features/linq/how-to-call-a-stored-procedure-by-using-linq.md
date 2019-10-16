---
title: '방법: LINQ (Visual Basic)를 사용 하 여 저장된 프로시저를 호출 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- queries [LINQ in Visual Basic], stored procedure calls
- stored procedures sample [Visual Basic]
- stored procedures [LINQ to SQL]
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: 6436d384-d1e0-40aa-8afd-451007477260
ms.openlocfilehash: af25ebe10681ebb1c346f90afc0291e53224833a
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59319575"
---
# <a name="how-to-call-a-stored-procedure-by-using-linq-visual-basic"></a>방법: LINQ (Visual Basic)를 사용 하 여 저장된 프로시저를 호출 합니다.
언어 통합 쿼리 (LINQ) 쉽게 데이터베이스 개체와 같은 저장 프로시저를 포함 하 여 데이터베이스 정보에 액세스할 수 있습니다.  
  
 다음 예제에는 SQL Server 데이터베이스에서 저장된 프로시저를 호출 하는 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플은 데이터베이스에 두 개의 다른 저장된 프로시저를 호출 하는 방법을 보여 줍니다. 각 프로시저의 쿼리 결과 반환합니다. 하나의 프로시저는 입력된 매개 변수를 사용 하 고 다른 프로시저 매개 변수를 사용 하지 않습니다.  
  
 이 항목의 예제는 Northwind 샘플 데이터베이스를 사용합니다. 개발 컴퓨터에이 데이터베이스가 없는 경우에 Microsoft 다운로드 센터에서 다운로드할 수 있습니다. 자세한 내용은 [샘플 데이터베이스 다운로드](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md)합니다.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-connection-to-a-database"></a>데이터베이스에 대 한 연결을 만들려면  
  
1. Visual Studio에서 엽니다 **서버 탐색기**/**데이터베이스 탐색기** 를 클릭 하 여 **서버 탐색기**/**데이터베이스 탐색기** 에 **보기** 메뉴.  
  
2. 마우스 오른쪽 단추로 클릭 **데이터 연결** 에 **서버 탐색기**/**데이터베이스 탐색기** 을 클릭 한 다음 **연결 추가**합니다.  
  
3. Northwind 샘플 데이터베이스에 올바른 연결을 지정 합니다.  
  
### <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>LINQ to SQL 파일을 포함 하는 프로젝트를 추가 하려면  
  
1. Visual Studio의 **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다. Visual basic **Windows Forms 응용 프로그램** 프로젝트 유형으로 합니다.  
  
2. **프로젝트** 메뉴에서 **새 항목 추가**를 클릭합니다. 선택 된 **LINQ to SQL 클래스** 항목 템플릿.  
  
3. 파일 이름을 `northwind.dbml`로 지정합니다. **추가**를 클릭합니다. 개체 관계형 디자이너 (O/R 디자이너) northwind.dbml 파일이 열립니다.  
  
### <a name="to-add-stored-procedures-to-the-or-designer"></a>저장된 프로시저를 O/R 디자이너에 추가 하려면  
  
1. **서버 탐색기**/**데이터베이스 탐색기**, Northwind 데이터베이스에 연결을 확장 합니다. 확장 된 **Stored Procedures** 폴더입니다.  
  
     O/R 디자이너를 닫은 경우 이전에 추가한 northwind.dbml 파일을 두 번 클릭 하 여 다시 열 수 있습니다.  
  
2. 클릭 합니다 **연도별 판매량** 저장 프로시저를 디자이너의 오른쪽 창으로 끌어 놓습니다. 클릭 합니다 **Ten Most Expensive Products** 저장된 프로시저 디자이너의 오른쪽 창으로 끕니다.  
  
3. 변경 내용을 저장 하 고 디자이너를 닫습니다.  
  
4. 프로젝트를 저장합니다.  
  
### <a name="to-add-code-to-display-the-results-of-the-stored-procedures"></a>저장된 프로시저의 결과 표시 하는 코드를 추가 하려면  
  
1. **도구 상자**를 끌어를 <xref:System.Windows.Forms.DataGridView> Form1 프로젝트에 대 한 기본 Windows Form 컨트롤입니다.  
  
2. 코드를 추가 하는 Form1을 두 번 클릭 해당 `Load` 이벤트입니다.  
  
3. 디자이너의 추가 저장된 프로시저를 O/R 디자이너에 추가 하는 경우는 <xref:System.Data.Linq.DataContext> 프로젝트에 대 한 개체입니다. 이 개체는 해당 프로시저에 액세스 해야 하는 코드를 포함 합니다. <xref:System.Data.Linq.DataContext> .dbml 파일의 이름에 따라 프로젝트에 대해 개체입니다. 이 프로젝트에는 <xref:System.Data.Linq.DataContext> 개체의 이름은 `northwindDataContext`합니다.  
  
     인스턴스를 만들 수는 <xref:System.Data.Linq.DataContext> O/R 디자이너에서 지정 된 저장된 프로시저 메서드 코드에서 호출 합니다. 바인딩할 합니다 <xref:System.Windows.Forms.DataGridView> 개체를 호출 하 여 즉시 실행 하도록 쿼리를 강제 적용 해야 할 수 있습니다는 <xref:System.Linq.Enumerable.ToList%2A> 메서드 저장된 프로시저의 결과를 합니다.  
  
     다음 코드를 추가 합니다 `Load` 이벤트에서 데이터에 대해 메서드로 노출할 프로시저 중 하나를 호출 합니다.  
  
     [!code-vb[VbLINQtoSQLHowTos#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form3.vb#1)]  
    [!code-vb[VbLINQtoSQLHowTos#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form3.vb#2)]  
  
4. F5 키를 눌러 프로젝트를 실행 하 고 결과 확인 합니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
- [쿼리](../../../../visual-basic/language-reference/queries/index.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [DataContext 메서드(O/R 디자이너)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
- [방법: 저장 프로시저를 할당하여 업데이트, 삽입 및 삭제 수행(O/R 디자이너)](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)
