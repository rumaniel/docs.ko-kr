---
title: '연습: DataGrid 컨트롤에서 SQL Server 데이터베이스의 데이터 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGrid [WPF], displaying data from SQL Server
- controls [WPF], DataGrid
ms.assetid: 6810b048-0a23-4f86-bfa5-97f92b3cfab4
ms.openlocfilehash: 30f3123a70e414e80842f726584623534994ab95
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645651"
---
# <a name="walkthrough-display-data-from-a-sql-server-database-in-a-datagrid-control"></a>연습: DataGrid 컨트롤에는 SQL Server 데이터베이스에서 데이터를 표시 합니다.

이 연습에서는 SQL Server 데이터베이스에서 데이터를 검색 하 고이 해당 데이터를 표시 한 <xref:System.Windows.Controls.DataGrid> 제어 합니다. ADO.NET Entity Framework를 사용 하 여 데이터를 나타내고, LINQ를 사용 하 여 엔터티 클래스에서 지정된 된 데이터를 검색 하는 쿼리를 작성 하는 엔터티 클래스를 만듭니다.

## <a name="prerequisites"></a>전제 조건

이 연습을 완료하려면 다음 구성 요소가 필요합니다.

- Visual Studio.

- SQL Server 또는 연결 된 AdventureWorks 샘플 데이터베이스가 있는 SQL Server Express의 실행 중인 인스턴스에 액세스 합니다. AdventureWorks 데이터베이스를 다운로드할 수 있습니다 합니다 [GitHub](https://github.com/Microsoft/sql-server-samples/releases)합니다.

## <a name="create-entity-classes"></a>엔터티 클래스 만들기

1. Visual Basic 또는 C#에서 새 WPF 응용 프로그램 프로젝트를 만들고 이름을 `DataGridSQLExample`입니다.

2. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 **추가**를 선택한 후 **새 항목**합니다.

     새 항목 추가 대화 상자가 나타납니다.

3. 설치 된 템플릿 창에서 선택 **데이터** 템플릿의 목록에서 선택 하 고 **ADO.NET Entity Data Model**합니다.

     ![ADO.NET 엔터티 데이터 모델 항목 템플릿](../../wcf/feature-details/./media/ado-net-entity-data-model-item-template.png)

4. 파일 이름을 `AdventureWorksModel.edmx` 을 클릭 한 다음 **추가**합니다.

     엔터티 데이터 모델 마법사가 나타납니다.

5. Model 콘텐츠 선택 화면에서 선택 **데이터베이스의 EF 디자이너** 을 클릭 한 다음 **다음**합니다.

6. 데이터 연결 선택 화면에서 AdventureWorksLT2008 데이터베이스에 대 한 연결을 제공 합니다. 자세한 내용은 [데이터 연결 선택 대화 상자](https://go.microsoft.com/fwlink/?LinkId=160190)합니다.

    이름 인지 확인 `AdventureWorksLT2008Entities` 하 고는 **으로 App.Config의 entity 연결 설정 저장** 확인란을 선택한 다음 클릭 **다음**합니다.

7. 데이터베이스 개체 선택 화면에서 테이블 노드를 확장 하 고 선택 합니다 **제품** 하 고 **ProductCategory** 테이블입니다.

     모든 테이블;에 대 한 엔터티 클래스를 생성할 수 있습니다. 그러나이 예제의에서 데이터를 검색할 테이블입니다.

     ![Product 및 ProductCategory 테이블에서 선택](./media/datagrid-sql-ef-step4.png "DataGrid_SQL_EF_Step4")

8. **마침**을 클릭합니다.

     Product 및 ProductCategory 엔터티는 Entity Designer에 표시 됩니다.

     ![Product 및 ProductCategory 엔터티 모델](./media/datagrid-sql-ef-step5.png "DataGrid_SQL_EF_Step5")

## <a name="retrieve-and-present-the-data"></a>검색 및 데이터를 표시 합니다.

1. MainWindow.xaml 파일을 엽니다.

2. 설정 합니다 <xref:System.Windows.FrameworkElement.Width%2A> 속성에는 <xref:System.Windows.Window> 450으로 합니다.

3. XAML 편집기에서 다음을 추가 <xref:System.Windows.Controls.DataGrid> 간의 태그를 `<Grid>` 및 `</Grid>` 추가할 태그를 <xref:System.Windows.Controls.DataGrid> 라는 `dataGrid1`.

     [!code-xaml[DataGrid_SQL_EF_Walkthrough#3](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_SQL_EF_Walkthrough/CS/MainWindow.xaml#3)]

     ![DataGrid가 있는 창](./media/datagrid-sql-ef-step6.png "DataGrid_SQL_EF_Step6")

4. <xref:System.Windows.Window>를 선택합니다.

5. 에 대 한 이벤트 처리기를 만들고 속성 창 또는 XAML 편집기를 사용 하는 <xref:System.Windows.Window> 라는 `Window_Loaded` 에 대 한는 <xref:System.Windows.FrameworkElement.Loaded> 이벤트입니다. 자세한 내용은 [방법: 단순 이벤트 처리기를 만들고](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb675300(v=vs.100))합니다.

     다음은 XAML MainWindow.xaml에 대 한 표시 합니다.

    > [!NOTE]
    > Visual Basic의 경우 MainWindow.xaml의 첫 번째 줄을 사용 하는 경우 대체 `x:Class="DataGridSQLExample.MainWindow"` 사용 하 여 `x:Class="MainWindow"`입니다.

     [!code-xaml[DataGrid_SQL_EF_Walkthrough#1](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_SQL_EF_Walkthrough/CS/MainWindow.xaml#1)]

6. (MainWindow.xaml.vb 또는 MainWindow.xaml.cs)의 코드 숨김 파일을 엽니다는 <xref:System.Windows.Window>합니다.

7. 조인된 된 테이블의 특정 값만 검색 하 고 설정에 다음 코드를 추가 합니다 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 의 속성을 <xref:System.Windows.Controls.DataGrid> 쿼리의 결과에.

     [!code-csharp[DataGrid_SQL_EF_Walkthrough#2](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_SQL_EF_Walkthrough/CS/MainWindow.xaml.cs#2)]
     [!code-vb[DataGrid_SQL_EF_Walkthrough#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_SQL_EF_Walkthrough/VB/MainWindow.xaml.vb#2)]

8. 예제를 실행합니다.

     표시 된 <xref:System.Windows.Controls.DataGrid> 데이터를 표시 하는 합니다.

     ![SQL database에서 데이터를 사용 하 여 DataGrid](./media/datagrid-sql-ef-step7.png "DataGrid_SQL_EF_Step7")

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.DataGrid>
- [어떻게 할까요 WPF 응용 프로그램에서 Entity Framework를 사용 하 여 시작 합니다.](https://go.microsoft.com/fwlink/?LinkId=159868)
