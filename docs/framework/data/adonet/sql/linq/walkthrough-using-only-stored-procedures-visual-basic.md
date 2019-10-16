---
title: '연습: 저장 프로시저만 사용(Visual Basic)'
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: 5a736a30-ba66-4adb-b87c-57d19476e862
ms.openlocfilehash: a1994d100c4d18d5fa3642e27d0dcb8823800549
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780963"
---
# <a name="walkthrough-using-only-stored-procedures-visual-basic"></a>연습: 저장 프로시저만 사용(Visual Basic)
이 연습에서는 저장 프로시저만 사용하여 데이터에 액세스하기 위한 기본 종단 간 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 시나리오를 제공합니다. 일반적으로 데이터베이스 관리자는 데이터 저장소에 액세스하는 방법을 제한하기 위해 이 방법을 사용합니다.  
  
> [!NOTE]
> 또한 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 응용 프로그램에서 저장 프로시저를 사용하여 특히 `Create`, `Update` 및 `Delete` 프로세스의 경우에 기본 동작을 재정의할 수 있습니다. 자세한 내용은 [삽입, 업데이트 및 삭제 작업 사용자 지정](customizing-insert-update-and-delete-operations.md)을 참조 하세요.  
  
 이 연습에서는 Northwind 샘플 데이터베이스의 저장 프로시저에 매핑되는 두 개의 메서드를 사용 합니다. CustOrdersDetail 및 CustOrderHist. 이 매핑은 SqlMetal 명령줄 도구를 실행 하 여 Visual Basic 파일을 생성할 때 발생 합니다. 자세한 내용은 이 연습 뒷부분의 사전 요구 사항 단원을 참조하세요.  
  
 이 연습에서는 개체 관계형 디자이너을 사용 하지 않습니다. Visual Studio를 사용 하는 개발자는 O/R 디자이너를 사용 하 여 저장 프로시저 기능을 구현할 수도 있습니다. [Visual Studio의 LINQ to SQL 도구를](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)참조 하세요.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 이 연습은 Visual Basic 개발 설정을 사용하여 작성했습니다.  
  
## <a name="prerequisites"></a>전제 조건  
 이 연습에서는 다음 사항이 필요합니다.  
  
- 이 연습에서는 파일을 보유하기 위해 전용 폴더("c:\linqtest3")가 사용됩니다. 연습을 시작하기 전에 먼저 이 폴더를 만듭니다.  
  
- Northwind 샘플 데이터베이스  
  
     이 데이터베이스가 개발 컴퓨터에 없는 경우 Microsoft 다운로드 사이트에서 다운로드할 수 있습니다. 지침은 [샘플 데이터베이스 다운로드](downloading-sample-databases.md)를 참조 하세요. 이 데이터베이스를 다운로드한 후 northwnd.mdf 파일을 c:\linqtest3 폴더에 복사합니다.  
  
- Northwind 데이터베이스에서 생성된 Visual Basic 코드 파일  
  
     이 연습은 다음 명령줄을 사용하여 SqlMetal 도구를 통해 작성했습니다.  
  
     **sqlmetal /code:"c:\linqtest3\northwind.vb" /language:vb "c:\linqtest3\northwnd.mdf" /sprocs /functions /pluralize**  
  
     자세한 내용은 [SqlMetal.exe(코드 생성 도구)](../../../../tools/sqlmetal-exe-code-generation-tool.md)를 참조하세요.  
  
## <a name="overview"></a>개요  
 이 연습은 다음과 같은 여섯 가지 주요 작업으로 구성됩니다.  
  
- Visual Studio에서 솔루션 설정 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]  
  
- System.Data.Linq 어셈블리를 프로젝트에 추가  
  
- 데이터베이스 코드 파일을 프로젝트에 추가  
  
- 데이터베이스 연결 만들기  
  
- 사용자 인터페이스 설정  
  
- 응용 프로그램 실행 및 테스트  
  
## <a name="creating-a-linq-to-sql-solution"></a>LINQ to SQL 솔루션 만들기  
 이 첫 번째 작업에서는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 프로젝트를 빌드하고 실행 하는 데 필요한 참조를 포함 하는 Visual Studio 솔루션을 만듭니다.  
  
### <a name="to-create-a-linq-to-sql-solution"></a>LINQ to SQL 솔루션을 만들려면  
  
1. Visual Studio의 **파일** 메뉴에서 **새 프로젝트**를 클릭합니다.  
  
2. **새 프로젝트** 대화 상자의 **프로젝트 형식** 창에서 **Visual Basic**을 확장하고 **Windows**를 클릭합니다.  
  
3. **템플릿** 창에서 **Windows Forms 응용 프로그램**을 클릭합니다.  
  
4. **이름** 상자에 **Sproconlyapp**을 입력 합니다.  
  
5. **확인**을 클릭합니다.  
  
     Windows Forms 디자이너가 열립니다.  
  
## <a name="adding-the-linq-to-sql-assembly-reference"></a>LINQ to SQL 어셈블리 참조 추가  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 어셈블리는 표준 Windows Forms 응용 프로그램 템플릿에 포함되어 있지 않습니다. 다음 단계에 설명된 대로 이 어셈블리를 직접 추가해야 합니다.  
  
### <a name="to-add-systemdatalinqdll"></a>System.Data.Linq.dll을 추가하려면  
  
1. **솔루션 탐색기**에서 **모든 파일 표시**를 클릭 합니다.  
  
2. **솔루션 탐색기**에서 **참조**를 마우스 오른쪽 단추로 클릭 한 다음 **참조 추가**를 클릭 합니다.  
  
3. **참조 추가** 대화 상자에서 **.net**을 클릭 하 고 system.xml 어셈블리를 클릭 한 다음 **확인**을 클릭 합니다.  
  
     어셈블리가 프로젝트에 추가됩니다.  
  
## <a name="adding-the-northwind-code-file-to-the-project"></a>Northwind 코드 파일을 프로젝트에 추가  
 이 단계에서는 SqlMetal 도구를 사용하여 Northwind 샘플 데이터베이스에서 코드 파일을 생성했다고 가정합니다. 자세한 내용은 이 연습 앞부분의 사전 요구 사항 단원을 참조하세요.  
  
### <a name="to-add-the-northwind-code-file-to-the-project"></a>northwind 코드 파일을 프로젝트에 추가하려면  
  
1. **프로젝트** 메뉴에서 **기존 항목 추가**를 클릭합니다.  
  
2. **기존 항목 추가** 대화 상자에서 c:\linqtest3\northwind.vb으로 이동한 다음 **추가**를 클릭 합니다.  
  
     northwind.vb 파일이 프로젝트에 추가됩니다.  
  
## <a name="creating-a-database-connection"></a>데이터베이스 연결 만들기  
 이 단계에서는 Northwind 샘플 데이터베이스에 대한 연결을 정의합니다. "c:\linqtest3\northwnd.mdf"가 이 연습에서 경로로 사용됩니다.  
  
### <a name="to-create-the-database-connection"></a>데이터베이스 연결을 만들려면  
  
1. **솔루션 탐색기**에서 **Form1**을 마우스 오른쪽 단추로 클릭 한 다음 **코드 보기**를 클릭 합니다.  
  
     `Class Form1`이 코드 편집기에 나타납니다.  
  
2. 다음 코드를 `Form1` 코드 블록에 입력합니다.  
  
     [!code-vb[DLinqWalk4VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#1)]  
  
## <a name="setting-up-the-user-interface"></a>사용자 인터페이스 설정  
 이 작업에서는 사용자가 저장 프로시저를 실행하여 데이터베이스의 데이터에 액세스할 수 있도록 인터페이스를 만듭니다. 이 연습을 사용하여 개발하는 응용 프로그램에서 사용자는 응용 프로그램에 포함된 저장 프로시저를 통해서만 데이터베이스의 데이터에 액세스할 수 있습니다.  
  
### <a name="to-set-up-the-user-interface"></a>사용자 인터페이스를 설정하려면  
  
1. Windows Forms 디자이너 (form1.vb **[Design]** )로 돌아갑니다.  
  
2. **보기** 메뉴에서 **도구 상자**를 클릭합니다.  
  
     도구 상자가 열립니다.  
  
    > [!NOTE]
    > 자동 **숨기기** 압정 아이콘을 클릭 하 여이 섹션의 나머지 단계를 수행 하는 동안 도구 상자를 열어 둡니다.  
  
3. 두 개의 단추, 두 개의 텍스트 상자 및 두 개의 레이블을 도구 상자에서 **Form1**로 끌어 옵니다.  
  
     함께 나와 있는 그림과 같이 컨트롤을 정렬합니다. 컨트롤이 쉽게 들어가도록 **Form1** 을 확장 합니다.  
  
4. **Label1**을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.  
  
5. **텍스트** 속성을 **Label1** 에서 **Enter OrderID:** 로 변경 합니다.  
  
6. **Label2**와 동일한 방식으로 **텍스트** 속성을 **Label2** 에서 **Enter CustomerID:** 로 변경 합니다.  
  
7. 이와 같은 방법으로 **Button1** 의 **텍스트** 속성을 **Order Details**로 변경 합니다.  
  
8. **Button2** 의 **Text** 속성을 **Order History**로 변경 합니다.  
  
     모든 텍스트를 볼 수 있도록 단추 컨트롤을 넓힙니다.  
  
### <a name="to-handle-button-clicks"></a>단추 클릭을 처리하려면  
  
1. **Form1** 에서 `Button1` **Order Details** 를 두 번 클릭 하 여 이벤트 처리기를 만들고 코드 편집기를 엽니다.  
  
2. 다음 코드를 `Button1` 처리기에 입력합니다.  
  
     [!code-vb[DLinqWalk4VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#2)]  
  
3. 이제 Form1에서 **Button2** 를 두 번 클릭 하 여 `Button2` 이벤트 처리기를 만들고 코드 편집기를 엽니다.  
  
4. 다음 코드를 `Button2` 처리기에 입력합니다.  
  
     [!code-vb[DLinqWalk4VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#3)]  
  
## <a name="testing-the-application"></a>애플리케이션 테스트  
 이제 응용 프로그램을 테스트할 차례입니다. 데이터 저장소와의 연결은 두 개의 저장 프로시저가 수행할 수 있는 작업으로 제한됩니다. 이러한 작업은 입력한 orderID에 대한 포함된 제품을 반환하거나 입력한 CustomerID에 대한 주문된 제품의 기록을 반환하는 것입니다.  
  
### <a name="to-test-the-application"></a>애플리케이션을 테스트하려면  
  
1. F5 키를 눌러 디버깅을 시작합니다.  
  
     Form1이 나타납니다.  
  
2. **Enter OrderID** 상자에 **10249** 를 입력 한 다음 **Order Details**를 클릭 합니다.  
  
     메시지 상자에는 주문 10249에 포함된 제품이 나열됩니다.  
  
     **확인** 을 클릭 하 여 메시지 상자를 닫습니다.  
  
3. **CustomerID 입력** 상자에를 입력 `ALFKI`한 다음 **Order History**를 클릭 합니다.  
  
     메시지 상자에는 고객 ALFKI에 대한 주문 기록이 나열됩니다.  
  
     **확인** 을 클릭 하 여 메시지 상자를 닫습니다.  
  
4. **Enter OrderID** 상자에를 입력 `123`하 고 **Order Details**를 클릭 합니다.  
  
     메시지 상자에는 "No results"가 표시됩니다.  
  
     **확인** 을 클릭 하 여 메시지 상자를 닫습니다.  
  
5. **디버그** 메뉴에서 **디버깅 중지**를 클릭 합니다.  
  
     디버그 세션이 닫힙니다.  
  
6. 실험을 완료 한 경우 **파일** 메뉴에서 **프로젝트 닫기** 를 클릭 하 고 메시지가 표시 되 면 프로젝트를 저장할 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계  
 약간의 변경을 통해 이 프로젝트를 향상시킬 수 있습니다. 예를 들어 목록 상자에 사용 가능한 저장 프로시저를 나열하고 사용자가 실행할 프로시저를 선택하도록 만들 수 있습니다. 또한 보고서의 출력을 텍스트 파일에 스트리밍할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [연습으로 학습](learning-by-walkthroughs.md)
- [저장 프로시저](stored-procedures.md)
