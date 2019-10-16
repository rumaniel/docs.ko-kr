---
title: '연습: 데이터 조작(Visual Basic)'
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: 1f6a54f6-ec33-452a-a37d-48122207bf14
ms.openlocfilehash: 7acce3f8483fab3c2978de7cbd1b9d875900f1d3
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72003390"
---
# <a name="walkthrough-manipulating-data-visual-basic"></a>연습: 데이터 조작(Visual Basic)
이 연습에서는 데이터베이스의 데이터를 추가, 수정 및 삭제하기 위한 기본 엔드투엔드 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 시나리오를 제공합니다. Northwind 샘플 데이터베이스의 복사본을 사용하여 고객을 추가하고, 고객의 이름을 변경하고, 주문을 삭제합니다.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 이 연습은 Visual Basic 개발 설정을 사용하여 작성했습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 연습에서는 다음 사항이 필요합니다.  
  
- 이 연습에서는 전용 폴더("c:\linqtest2")를 사용하여 파일을 저장합니다. 연습을 시작하기 전에 먼저 이 폴더를 만듭니다.  
  
- Northwind 샘플 데이터베이스  
  
     이 데이터베이스가 개발 컴퓨터에 없는 경우 Microsoft 다운로드 사이트에서 다운로드할 수 있습니다. 지침은 [샘플 데이터베이스 다운로드](downloading-sample-databases.md)를 참조 하세요. 이 데이터베이스를 다운로드한 후 northwnd.mdf 파일을 c:\linqtest2 폴더에 복사합니다.  
  
- Northwind 데이터베이스에서 생성된 Visual Basic 코드 파일  
  
     개체 관계형 디자이너 또는 SQLMetal 도구를 사용 하 여이 파일을 생성할 수 있습니다. 이 연습은 다음 명령줄을 사용하여 SQLMetal 도구를 통해 작성했습니다.  
  
     **sqlmetal /code:"c:\linqtest2\northwind.vb" /language:vb "C:\linqtest2\northwnd.mdf" /pluralize**  
  
     자세한 내용은 [SqlMetal.exe(코드 생성 도구)](../../../../tools/sqlmetal-exe-code-generation-tool.md)를 참조하세요.  
  
## <a name="overview"></a>개요  
 이 연습은 다음과 같은 여섯 가지 주요 작업으로 구성됩니다.  
  
- Visual Studio에서 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 솔루션을 만듭니다.  
  
- 데이터베이스 코드 파일을 프로젝트에 추가  
  
- 새 Customer 개체 만들기  
  
- 고객의 연락처 이름 수정  
  
- 주문 삭제  
  
- 이러한 변경 내용을 Northwind 데이터베이스로 전송  
  
## <a name="creating-a-linq-to-sql-solution"></a>LINQ to SQL 솔루션 만들기  
 이 첫 번째 작업에서는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 프로젝트를 빌드하고 실행 하는 데 필요한 참조를 포함 하는 Visual Studio 솔루션을 만듭니다.  
  
#### <a name="to-create-a-linq-to-sql-solution"></a>LINQ to SQL 솔루션을 만들려면  
  
1. Visual Studio의 **파일** 메뉴에서 **새 프로젝트**를 클릭합니다.  
  
2. **새 프로젝트** 대화 상자의 **프로젝트 형식** 창에서 **Visual Basic**을 클릭 합니다.  
  
3. **템플릿** 창에서 **콘솔 애플리케이션**을 클릭합니다.  
  
4. **이름** 상자에 **linqdatamanipulationapp 입력**을 입력 합니다.  
  
5. **확인**을 클릭합니다.  
  
## <a name="adding-linq-references-and-directives"></a>LINQ 참조 및 지시문 추가  
 이 연습에서는 프로젝트에 기본적으로 설치되어 있지 않을 수 있는 어셈블리를 사용합니다. @No__t-0이 프로젝트에 참조로 나열 되어 있지 않으면 ( **솔루션 탐색기** 의 **모든 파일 표시** 를 클릭 하 고 **참조** 노드를 확장) 다음 단계에 설명 된 대로 추가 합니다.  
  
#### <a name="to-add-systemdatalinq"></a>System.Data.Linq를 추가하려면  
  
1. **솔루션 탐색기**에서 **참조**를 마우스 오른쪽 단추로 클릭 한 다음 **참조 추가**를 클릭 합니다.  
  
2. **참조 추가** 대화 상자에서 **.net**을 클릭 하 고 system.xml 어셈블리를 클릭 한 다음 **확인**을 클릭 합니다.  
  
     어셈블리가 프로젝트에 추가됩니다.  
  
3. 코드 편집기에서 **Module1**위에 다음 지시문을 추가 합니다.  
  
     [!code-vb[DLinqWalk3VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#1)]  
  
## <a name="adding-the-northwind-code-file-to-the-project"></a>Northwind 코드 파일을 프로젝트에 추가  
 이 단계에서는 SQLMetal 도구를 사용하여 Northwind 샘플 데이터베이스에서 코드 파일을 생성했다고 가정합니다. 자세한 내용은 이 연습 앞부분의 사전 요구 사항 단원을 참조하세요.  
  
#### <a name="to-add-the-northwind-code-file-to-the-project"></a>northwind 코드 파일을 프로젝트에 추가하려면  
  
1. **프로젝트** 메뉴에서 **기존 항목 추가**를 클릭합니다.  
  
2. **기존 항목 추가** 대화 상자에서 c:\linqtest2\northwind.vb으로 이동한 다음 **추가**를 클릭 합니다.  
  
     northwind.vb 파일이 프로젝트에 추가됩니다.  
  
## <a name="setting-up-the-database-connection"></a>데이터베이스 연결 설정  
 먼저 데이터베이스에 대한 연결을 테스트합니다. 특히 데이터베이스 이름 Northwnd에 i 문자가 없는 것을 확인합니다. 다음 단계에서 오류를 생성하는 경우 northwind.vb 파일을 검토하여 Northwind partial 클래스의 맞춤법을 확인합니다.  
  
#### <a name="to-set-up-and-test-the-database-connection"></a>데이터베이스 연결을 설정하고 테스트하려면  
  
1. `Sub Main`에 다음 코드를 입력하거나 붙여넣습니다.  
  
     [!code-vb[DLinqWalk3VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#2)]  
  
2. 이때 F5 키를 눌러 애플리케이션을 테스트합니다.  
  
     **콘솔** 창이 열립니다.  
  
     **콘솔** 창에서 enter 키를 누르거나 Visual Studio **디버그** 메뉴에서 **디버깅 중지** 를 클릭 하 여 응용 프로그램을 닫습니다.  
  
## <a name="creating-a-new-entity"></a>새 엔터티 만들기  
 새 엔터티를 만드는 과정은 단순합니다. `Customer` 키워드를 사용하여 개체(예: `New`)를 만들 수 있습니다.  
  
 이 단원과 다음 단원에서는 로컬 캐시만 변경합니다. 이 연습의 끝에서 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>를 호출할 때까지 변경 내용이 데이터베이스로 전송되지 않습니다.  
  
#### <a name="to-add-a-new-customer-entity-object"></a>새 Customer 엔터티 개체를 추가하려면  
  
1. `Customer`의 `Console.ReadLine` 앞에 다음 코드를 추가하여 새 `Sub Main`를 만듭니다.  
  
     [!code-vb[DLinqWalk3VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#3)]  
  
2. F5 키를 눌러 솔루션을 디버깅합니다.  
  
     콘솔 창에 표시되는 결과는 다음과 같습니다.  
  
     `Customers matching CA before insert:`  
  
     `Customer ID: CACTU`  
  
     `Customer ID: RICAR`  
  
     새 행이 결과에 나타나지 않습니다. 새 데이터가 아직 데이터베이스로 전송되지 않았습니다.  
  
3. **콘솔** 창에서 enter 키를 눌러 디버깅을 중지 합니다.  
  
## <a name="updating-an-entity"></a>엔터티 업데이트  
 다음 단계에서는 `Customer` 개체를 검색하고 해당 속성 중 하나를 수정합니다.  
  
#### <a name="to-change-the-name-of-a-customer"></a>Customer 이름을 변경하려면  
  
- `Console.ReadLine()` 위에 다음 코드를 추가합니다.  
  
     [!code-vb[DLinqWalk3VB#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#4)]  
  
## <a name="deleting-an-entity"></a>엔터티 삭제  
 동일한 Customer 개체를 사용하여 첫 번째 주문을 삭제할 수 있습니다.  
  
 다음 코드에서는 행 간의 관계를 끊는 방법과 데이터베이스에서 행을 삭제하는 방법을 보여 줍니다.  
  
#### <a name="to-delete-a-row"></a>행을 삭제하려면  
  
- `Console.ReadLine()` 바로 위에 다음 코드를 추가합니다.  
  
     [!code-vb[DLinqWalk3VB#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#5)]  
  
## <a name="submitting-changes-to-the-database"></a>변경 내용을 데이터베이스로 전송  
 개체를 만들고 업데이트 및 삭제하는 데 필요한 첫 번째 단계는 실제로 변경 내용을 데이터베이스로 전송하는 것입니다. 이 단계를 수행하지 않으면 변경 내용은 로컬에만 적용되고 쿼리 결과에 나타나지 않습니다.  
  
#### <a name="to-submit-changes-to-the-database"></a>변경 내용을 데이터베이스로 전송하려면  
  
1. `Console.ReadLine` 바로 위에 다음 코드를 삽입합니다.  
  
     [!code-vb[DLinqWalk3VB#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#6)]  
  
2. `SubmitChanges` 뒤에 다음 코드를 삽입하여 변경 내용 전송 전후의 결과를 보여 줍니다.  
  
     [!code-vb[DLinqWalk3VB#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#7)]  
  
3. F5 키를 눌러 솔루션을 디버깅합니다.  
  
     콘솔 창이 다음과 같이 나타납니다.  
  
    ```console
    Customers matching CA before update:  
    Customer ID: CACTU  
    Customer ID: RICAR  
  
    The Order Detail to be deleted is: OrderID = 10643  
  
    Customers matching CA after update:  
    Customer ID: A3VCA  
    Customer ID: CACTU  
    Customer ID: RICAR  
    ```  
  
4. **콘솔** 창에서 enter 키를 눌러 디버깅을 중지 합니다.  
  
> [!NOTE]
> 변경 내용을 전송하여 새 고객을 추가한 후에는 동일한 고객을 있는 그대로 다시 추가할 수 없으므로 이 솔루션을 있는 그대로 다시 실행할 수 없습니다. 솔루션을 다시 실행하려면 추가할 고객 ID의 값을 변경합니다.  
  
## <a name="see-also"></a>참조

- [연습으로 학습](learning-by-walkthroughs.md)
