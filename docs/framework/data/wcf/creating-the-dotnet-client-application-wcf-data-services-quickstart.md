---
title: .NET Framework 클라이언트 응용 프로그램 만들기(WCF Data Services 빠른 시작)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 41ade767-eeab-437d-9121-9797e8fb8045
ms.openlocfilehash: 9995a509bf997298d991a1f66cfdf3cae6cd0395
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790960"
---
# <a name="creating-the-net-framework-client-application-wcf-data-services-quickstart"></a>.NET Framework 클라이언트 응용 프로그램 만들기(WCF Data Services 빠른 시작)

WCF Data Services 빠른 시작의 최종 작업입니다. 이 작업에서는 솔루션에 콘솔 응용 프로그램을 추가 하 고,이 새 클라이언트 응용 프로그램에 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 피드에 대 한 참조를 추가 하 고, 생성 된 클라이언트 데이터 서비스 클래스 및 클라이언트 라이브러리를 사용 하 여 클라이언트 응용 프로그램에서 OData 피드에 액세스 합니다. .

> [!NOTE]
> 데이터 피드에 액세스하기 위해 .NET Framework 기반 클라이언트 응용 프로그램이 필요하지는 않습니다. 데이터 서비스는 OData 피드를 사용 하는 모든 응용 프로그램 구성 요소에서 액세스할 수 있습니다. 자세한 내용은 [클라이언트 응용 프로그램에서 데이터 서비스 사용](using-a-data-service-in-a-client-application-wcf-data-services.md)을 참조 하세요.

## <a name="to-create-the-client-application-by-using-visual-studio"></a>Visual Studio를 사용하여 클라이언트 응용 프로그램을 만들려면

1. **솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 프로젝트**를 클릭 합니다.

2. 왼쪽 창에서 **설치 됨** > [**Visual C#**  or **Visual Basic**] > **Windows 바탕 화면**을 선택 하 고 **WPF 앱** 템플릿을 선택 합니다.

3. 프로젝트 `NorthwindClient` 이름으로를 입력 한 다음 **확인**을 클릭 합니다.

4. MainWindow.xaml 파일을 열고 XAML 코드를 다음 코드로 바꿉니다.

     [!code-xaml[Astoria Quickstart Client#Window1Xaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_client/vb/window1.xaml#window1xaml)]

## <a name="to-add-a-data-service-reference-to-the-project"></a>프로젝트에 데이터 서비스 참조를 추가하려면

1. **솔루션 탐색기**에서 NorthwindClient 프로젝트를 마우스 오른쪽 단추로 클릭 하 고**서비스 참조** **추가** > 를 클릭 한 다음 **검색**을 클릭 합니다.

     첫 번째 작업에서 만든 Northwind 데이터 서비스가 표시됩니다.

2. **네임 스페이스** 텍스트 상자에을 입력 `Northwind`한 다음 **확인**을 클릭 합니다.

     데이터 서비스 리소스에 개체로 액세스하고 상호 작용하는 데 사용되는 데이터 클래스가 포함된 새 코드 파일이 프로젝트에 추가됩니다. 데이터 클래스는 `NorthwindClient.Northwind` 네임스페이스에 만들어집니다.

## <a name="to-access-data-service-data-in-the-wpf-application"></a>WPF 응용 프로그램에서 데이터 서비스 데이터에 액세스하려면

1. **NorthwindClient**아래의 **솔루션 탐색기** 에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **참조 추가**를 클릭 합니다.

2. **참조 추가** 대화 상자에서 **.net** 탭을 클릭 하 고, system.web. .dll 어셈블리를 선택한 후 **확인**을 클릭 합니다.

3. **NorthwindClient**아래의 `using` **솔루션 탐색기** 에서 mainwindow.xaml 파일에 대 한 코드 페이지를 열고 Visual Basic`Imports` 에 다음 문을 추가 합니다.

    [!code-csharp[Astoria Quickstart Client#Using](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_client/cs/window1.xaml.cs#using)]
    [!code-vb[Astoria Quickstart Client#Using](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_client/vb/window1.xaml.vb#using)]

4. 해당 데이터 서비스를 쿼리하고 결과를 <xref:System.Data.Services.Client.DataServiceCollection%601>에 바인딩하는 다음 코드를 `MainWindow` 클래스에 삽입합니다.

    > [!NOTE]
    > Northwind 데이터 서비스 인스턴스를 호스트하는 서버 및 포트로 호스트 이름 `localhost:12345`를 바꾸어야 합니다.

     [!code-csharp[Astoria Quickstart Client#QueryCode](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_client/cs/window1.xaml.cs#querycode)]
     [!code-vb[Astoria Quickstart Client#QueryCode](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_client/vb/window1.xaml.vb#querycode)]

5. 변경 내용을 저장하는 다음 코드를 `MainWindow` 클래스에 삽입합니다.

     [!code-csharp[Astoria Quickstart Client#SaveChanges](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_client/cs/window1.xaml.cs#savechanges)]
     [!code-vb[Astoria Quickstart Client#SaveChanges](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_client/vb/window1.xaml.vb#savechanges)]

## <a name="to-build-and-run-the-northwindclient-application"></a>NorthwindClient 응용 프로그램을 빌드 및 실행하려면

1. **솔루션 탐색기**에서 NorthwindClient 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트로 설정**을 선택 합니다.

2. **F5** 키를 눌러 응용 프로그램을 시작 합니다.

     솔루션이 빌드되고 클라이언트 응용 프로그램이 시작됩니다. 서비스에서 데이터가 요청되고 콘솔에 표시됩니다.

3. 데이터 표의 **수량** 열에서 값을 편집 하 고 **저장**을 클릭 합니다.

     변경 내용이 데이터 서비스에 저장됩니다.

    > [!NOTE]
    > 이 버전의 NorthwindClient 응용 프로그램은 엔터티의 추가와 삭제를 지원하지 않습니다.

## <a name="next-steps"></a>다음 단계

Sample Northwind OData 피드에 액세스 하는 클라이언트 응용 프로그램을 성공적으로 만들었습니다. WCF Data Services 퀵 스타트도 완료 했습니다.

.NET Framework 응용 프로그램에서 OData 피드에 액세스 하는 방법에 대 한 자세한 내용은 [WCF Data Services 클라이언트 라이브러리](wcf-data-services-client-library.md)를 참조 하세요.

## <a name="see-also"></a>참고자료

- [시작](getting-started-with-wcf-data-services.md)
- [리소스](wcf-data-services-resources.md)
