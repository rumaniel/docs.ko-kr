---
title: '방법: 클라이언트 응용 프로그램 서비스 구성'
ms.date: 03/30/2017
helpviewer_keywords:
- client application services, configuring
ms.assetid: 34a8688a-a32c-40d3-94be-c8e610c6a4e8
ms.openlocfilehash: 6f754a2a66187ac94d31d0d5a3a665c969652d26
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2018
ms.locfileid: "48846515"
---
# <a name="how-to-configure-client-application-services"></a>방법: 클라이언트 응용 프로그램 서비스 구성
이 항목에서는 Visual Studio **프로젝트 디자이너**를 사용하여 클라이언트 응용 프로그램 서비스를 사용하도록 설정하고 구성하는 방법을 설명합니다. 클라이언트 응용 프로그램 서비스를 사용하면 기존 [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 응용 프로그램 서비스에서 사용자의 유효성을 검사하고 사용자 역할과 설정을 검색할 수 있습니다. 구성 후에는 [클라이언트 응용 프로그램 서비스 개요](../../../docs/framework/common-client-technologies/client-application-services-overview.md)의 설명에 따라 응용 프로그램 코드에서 사용하도록 설정된 서비스에 액세스할 수 있습니다. [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] 응용 프로그램 서비스에 대한 자세한 내용은 [ASP.NET 응용 프로그램 서비스 개요](https://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013)를 참조하세요.  
  
 **프로젝트 디자이너**의 **서비스** 페이지에서 클라이언트 응용 프로그램 서비스를 사용하도록 설정하고 구성할 수 있습니다. **서비스** 페이지에서 프로젝트 App.config 파일의 값을 업데이트합니다. **프로젝트 디자이너**에 액세스하려면 **프로젝트** 메뉴의 **속성** 명령을 사용합니다. **서비스** 페이지에 대한 자세한 내용은 [프로젝트 디자이너, 서비스 페이지](/visualstudio/ide/reference/services-page-project-designer)를 참조하세요.  
  
 다음 절차에서는 클라이언트 응용 프로그램 서비스에 대한 기본 구성을 수행하는 방법을 설명합니다. 고급 구성 옵션에 대해서는 이후 섹션에서 설명합니다.  
  
### <a name="to-configure-client-application-services"></a>클라이언트 응용 프로그램 서비스를 구성하려면  
  
1.  **솔루션 탐색기**에서 프로젝트 노드를 선택하고, **프로젝트** 메뉴에서 **속성**을 클릭합니다.  
  
     **프로젝트 디자이너**가 표시됩니다.  
  
2.  **서비스** 탭을 클릭합니다. 다음 그림과 같이 **서비스** 페이지가 표시됩니다.  
  
     ![프로젝트 디자이너의 서비스 탭](../../../docs/framework/common-client-technologies/media/casdesigner.png "casdesigner")  
  
3.  **서비스** 페이지에서 **클라이언트 응용 프로그램 서비스 사용**을 선택합니다.  
  
    > [!NOTE]
    >  클라이언트 응용 프로그램 서비스를 사용하려면 .NET Framework 정식 버전이 필요합니다. .NET Framework Client Profile에서는 클라이언트 응용 프로그램 서비스가 지원되지 않습니다. **클라이언트 응용 프로그램 서비스 사용** 확인란이 사용하지 않도록 설정되어 있으면 **대상 프레임워크**가 .NET Framework 3.5 이상으로 설정되어 있는지 확인합니다. C#에서 **대상 프레임워크** 설정을 확인하려면 프로젝트 디자이너를 열고 **응용 프로그램** 페이지를 클릭합니다. Visual Basic에서 **대상 프레임워크** 설정을 확인하려면 프로젝트 디자이너를 열고 **컴파일** 페이지를 클릭한 다음 **고급 컴파일 옵션**을 클릭합니다.  
  
4.  고유한 로그인 컨트롤 또는 대화 상자를 제공하려면 **양식 인증 사용**을 선택하고, 운영 체제에서 제공하는 ID를 사용하려면 **Windows 인증 사용**을 선택합니다. 자세한 내용은 [클라이언트 응용 프로그램 서비스 개요](../../../docs/framework/common-client-technologies/client-application-services-overview.md)를 참조하세요.  
  
    > [!NOTE]
    >  **Windows 인증 사용**을 선택하는 경우 클라이언트 응용 프로그램 서비스는 SQL Server Compact 데이터베이스를 사용하도록 자동으로 구성됩니다. 이 설정은 다음 섹션에서 설명하는 것처럼 **서비스의 고급 설정** 대화 상자에 표시됩니다. **양식 인증 사용**을 선택하는 경우에는 **사용자 지정 연결 문자열 사용** 설정의 선택이 자동으로 취소되지 않습니다. Windows 인증에 사용할 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 데이터베이스가 이미 생성된 경우에는 이로 인해 오류가 발생할 수 있습니다. 이러한 오류를 해결하려면 **서비스의 고급 설정** 대화 상자에서 **사용자 지정 연결 문자열 사용** 설정의 선택을 취소합니다.  
  
5.  **양식 인증 사용**을 선택한 경우 **인증 서비스 위치** 상자에서 파일 이름을 제외한 서비스 호스트의 URL을 지정합니다. 디자이너는 값을 구성 파일에 쓸 때 표준 파일 이름(Authentication_JSON_AppService.axd)을 자동으로 추가합니다.  
  
6.  **양식 인증 사용**을 선택한 경우 필요에 따라 **자격 증명 공급자** 상자에 값을 지정할 수 있습니다. 자격 증명 공급자는 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider> 인터페이스를 구현해야 합니다. 자격 증명 공급자를 사용하면 로그인 사용자 인터페이스를 다른 응용 프로그램 코드와 분리할 수 있습니다. 이렇게 하면 여러 응용 프로그램에 사용할 단일 로그인 대화 상자를 만들 수 있습니다. 자세한 내용은 [방법: 클라이언트 응용 프로그램 서비스에서 사용자 로그인 구현](../../../docs/framework/common-client-technologies/how-to-implement-user-login-with-client-application-services.md)을 참조하세요.  
  
     자격 증명 공급자를 지정하는 경우에는 해당 공급자를 정규화된 어셈블리 형식 이름으로 지정해야 합니다. 자세한 내용은 <xref:System.Type.AssemblyQualifiedName%2A?displayProperty=nameWithType> 및 [어셈블리 이름](../../../docs/framework/app-domains/assembly-names.md)을 참조하세요. 가장 단순한 형식의 정규화된 어셈블리 형식 이름은 다음 예제와 같습니다.  
  
    ```  
    MyNamespace.MyLoginClass, MyAssembly  
    ```  
  
7.  **역할 서비스 위치** 및 **웹 설정 서비스 위치** 텍스트 상자에서 파일 이름을 제외한 각 서비스의 서비스 위치를 지정합니다. 디자이너는 값을 구성 파일에 쓸 때 표준 파일 이름(Role_JSON_AppService.axd 및 Profile_JSON_AppService.axd)을 자동으로 추가합니다.  
  
8.  필요한 경우 **고급**을 클릭하여 로컬 캐싱 동작과 같은 고급 설정을 수정합니다. 자세한 내용은 다음 절차를 참조하세요.  
  
## <a name="advanced-configuration"></a>고급 구성  
 다음 절차에서는 흔하지 않은 시나리오용으로 클라이언트 응용 프로그램 서비스를 구성하는 방법을 설명합니다. 예를 들어 이러한 구성 옵션은 공공 장소에 배포된 응용 프로그램에 사용할 수도 있고 암호화된 SQL Server Compact 데이터베이스를 로컬 데이터 캐시로 사용하기 위해 사용할 수도 있습니다.  
  
#### <a name="to-configure-advanced-settings-for-client-application-services"></a>클라이언트 응용 프로그램 서비스에 대한 고급 설정을 구성하려면  
  
1.  **프로젝트 디자이너**의 **서비스** 페이지에서 **고급**을 클릭합니다.  
  
     다음 그림에 나와 있는 것처럼 **서비스의 고급 설정** 대화 상자가 표시됩니다. 이 대화 상자에 대한 자세한 내용은 [서비스의 고급 설정 대화 상자](/visualstudio/ide/reference/advanced-settings-for-services-dialog-box)를 참조하세요.  
  
     ![서비스의 고급 설정 대화 상자](../../../docs/framework/common-client-technologies/media/casdialog.png "casdialog")  
  
2.  **오프라인으로 로그인할 수 있도록 로컬에 암호 해시 저장**을 선택하거나 선택을 취소합니다. 이 옵션을 선택하면 암호화된 형식의 사용자 암호가 로컬로 캐시됩니다. 이 옵션은 응용 프로그램에 대해 오프라인 모드를 구현하는 경우 적합합니다. 이 옵션을 선택하면 <xref:System.Web.ClientServices.ConnectivityStatus.IsOffline%2A> 속성을 `true`로 설정했더라도 사용자의 유효성을 검사할 수 있습니다.  
  
3.  **서버 쿠키가 만료될 때마다 다시 사용자 로그온**을 선택하거나 선택을 취소합니다. 인증 쿠키는 원격 서비스에서 구성되며 사용자 로그인이 활성 상태로 유지되는 시간을 나타냅니다. 쿠키를 구성하는 방법에 대한 자세한 내용은 [authentication 요소에 대한 forms 요소(ASP.NET 설정 스키마)](https://msdn.microsoft.com/library/8163b8b5-ea6c-46c8-b5a9-c4c3de31c0b3)의 `timeout` 특성을 참조하세요.  
  
     이 옵션을 선택하는 경우 인증 쿠키가 만료된 후 원격 역할 또는 웹 설정 서비스에 액세스하려고 하면 <xref:System.Net.WebException>이 throw됩니다. 이 예외를 처리하고 로그인 대화 상자를 표시하여 사용자의 유효성을 다시 검사할 수 있습니다. 이 동작의 예는 [연습: 클라이언트 응용 프로그램 서비스 사용](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md)을 참조하세요. 이 옵션은 공공 장소에 배포된 응용 프로그램에서 응용 프로그램을 사용한 후 실행 중인 상태로 유지하는 사용자가 계속 인증된 상태로 유지되지 않도록 하는 데 유용합니다.  
  
     이 옵션의 선택을 취소하는 경우 인증 쿠키가 만료된 후 원격 서비스에 액세스하려고 하면 사용자의 유효성을 자동으로 다시 검사합니다.  
  
4.  **역할 서비스 캐시 제한 시간**의 값을 지정합니다. 이 시간 간격은 역할 업데이트 빈도가 높으면 작은 값으로 설정하고 빈도가 낮으면 큰 값으로 설정합니다. 오프라인 모드를 구현하는 경우 응용 프로그램이 오프라인 상태인 동안 역할 정보가 만료되지 않도록 시간 간격을 큰 값으로 설정합니다.  
  
     <xref:System.Web.Security.RolePrincipal.IsInRole%2A> 메서드를 호출하면 역할 공급자가 캐시된 역할 값 또는 역할 서비스에 액세스합니다. 프로그래밍 방식으로 캐시를 다시 설정하고 이 메서드가 원격 서비스에 액세스하도록 강제 지정하려면 <xref:System.Web.ClientServices.Providers.ClientRoleProvider.ResetCache%2A> 메서드를 호출합니다.  
  
5.  **사용자 지정 연결 문자열 사용**을 선택하거나 선택을 취소합니다. 자세한 내용은 다음 절차를 참조하세요.  
  
#### <a name="to-configure-client-application-services-to-use-a-database-for-the-local-cache"></a>로컬 캐시에 대해 데이터베이스를 사용하도록 클라이언트 응용 프로그램 서비스를 구성하려면  
  
1.  **프로젝트 디자이너**의 **서비스** 페이지에서 **고급**을 클릭합니다.  
  
     **서비스의 고급 설정** 대화 상자가 나타납니다.  
  
2.  **사용자 지정 연결 문자열 사용**을 선택합니다.  
  
     기본값인 `Data Source = |SQL/CE|`가 텍스트 상자에 나타납니다.  
  
3.  SQL Server Compact 데이터베이스를 생성 및 사용하려면 기본 연결 문자열 값을 유지합니다. Visual Studio에서 데이터베이스 파일을 생성하고 <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=nameWithType> 속성에 지정된 디렉터리에 넣습니다.  
  
4.  암호화된 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 데이터베이스를 생성 및 사용하려면 다음 예제에 나와 있는 것처럼 `password` 및 `encrypt database` 값을 연결 문자열에 추가합니다.  
  
    > [!NOTE]
    >  강력한 암호를 지정해야 합니다. 데이터베이스가 생성된 후에는 암호를 변경할 수 없습니다.  
  
    ```  
    Data Source = |SQL/CE|;password=<password>;encrypt database=true  
    ```  
  
5.  고유한 SQL Server 데이터베이스를 사용하려면 연결 문자열을 직접 지정합니다. 유효한 연결 문자열 형식에 대한 자세한 내용은 SQL Server 설명서를 참조하세요. 이 데이터베이스는 자동으로 생성되지 않습니다. 연결 문자열은 다음 SQL 문을 사용하여 만들 수 있는 기존 데이터베이스를 참조해야 합니다.  
  
    ```  
    CREATE TABLE ApplicationProperties (PropertyName nvarchar(256),  
        PropertyValue nvarchar(256))  
    CREATE TABLE UserProperties (PropertyName nvarchar(256),  
        PropertyValue nvarchar(256))  
    CREATE TABLE Roles (UserName nvarchar(256),   
        RoleName nvarchar(256))  
    CREATE TABLE Settings (PropertyName nvarchar(256),   
        PropertyStoredAs nvarchar(1), PropertyValue nvarchar(2048))  
    ```  
  
## <a name="using-custom-providers"></a>사용자 지정 공급자 사용  
 기본적으로 클라이언트 응용 프로그램 서비스 기능은 <xref:System.Web.ClientServices.Providers?displayProperty=nameWithType> 네임스페이스의 공급자를 사용합니다. **프로젝트 디자이너**의 **서비스** 페이지를 사용하여 응용 프로그램을 구성할 때는 이러한 공급자에 대한 참조가 App.config 파일에 추가됩니다. 이러한 기본 공급자는 서버의 해당 공급자에 액세스합니다. 웹 서비스는 <xref:System.Web.Security.SqlMembershipProvider>, <xref:System.Web.Security.SqlRoleProvider> 등의 공급자를 통해 사용자 데이터에 액세스하도록 구성되는 경우가 많습니다.  
  
 사용자 지정 서비스 공급자를 사용하려면 일반적으로 서버에 액세스하는 모든 클라이언트 응용 프로그램에 변경 내용이 적용되도록 서버 쪽에서 공급자를 변경합니다. 그러나 클라이언트 쪽에서 기본값이 아닌 공급자를 사용하는 옵션도 있습니다. 다음 절차에 나와 있는 대로 프로젝트의 App.config 파일에서 사용자 지정 인증 또는 역할 공급자를 지정할 수 있습니다. 사용자 지정 인증 및 역할 공급자를 만드는 방법에 대한 자세한 내용은 [멤버 자격 공급자 구현](https://msdn.microsoft.com/library/d8658b8e-c962-4f64-95e1-4acce35e4582) 및 [역할 공급자 구현](https://msdn.microsoft.com/library/851671ce-bf9b-43f2-aba4-bc9d28b11c7d)을 참조하세요. 프로젝트의 `Settings` 클래스(C#에서는 `Properties.Settings.Default`로, Visual Basic에서는 `My.Settings`로 액세스함)를 수정하여 사용자 지정 설정 공급자를 사용할 수도 있습니다. 자세한 내용은 [응용 프로그램 설정 아키텍처](../../../docs/framework/winforms/advanced/application-settings-architecture.md)를 참조하세요.  
  
#### <a name="to-configure-client-application-services-to-use-non-default-providers"></a>기본값이 아닌 공급자를 사용하여 클라이언트 응용 프로그램 서비스를 구성하려면  
  
1.  기본값이 아닌 인증 또는 역할 서비스 공급자를 사용하려면 먼저 **서비스** 페이지를 통해 기타 모든 구성 설정을 완료합니다.  
  
2.  **프로젝트 디자이너**를 닫습니다. 설정을 수정하지 않더라도 **서비스** 페이지에서는 App.config 파일이 자동으로 업데이트되기 때문입니다. 이 절차에서 설명하는 대로 App.config 파일을 수동으로 수정한 후 **서비스** 페이지로 돌아가면 수정 내용이 다시 설정됩니다.  
  
3.  **솔루션 탐색기**에서 App.config를 두 번 클릭합니다.  
  
     응용 프로그램 구성 파일이 텍스트 편집기에서 열립니다.  
  
4.  `<providers>` 또는 `<membership>` 요소 내에서 `<roleManager>` 요소를 찾습니다. 이러한 요소는 `<system.web>` 요소의 자식입니다. `<membership>` 요소는 인증 공급자를 지정하는 데 사용되고 `<roleManager>` 요소는 역할 공급자를 지정하는 데 사용됩니다.  
  
5.  `<add>` 요소를 `<providers>` 요소의 자식으로 추가합니다. 다음 예제에 나와 있는 대로 `name` 및 `type` 특성을 지정해야 합니다. `type` 특성 값은 정규화된 어셈블리 형식 이름이어야 합니다. 자세한 내용은 <xref:System.Type.AssemblyQualifiedName%2A?displayProperty=nameWithType> 및 [어셈블리 이름](../../../docs/framework/app-domains/assembly-names.md)을 참조하세요.  
  
    ```xml  
    <add name="MyCustomRoleProvider" type="MyNamespace.MyRoleProvider, MyAssembly" />  
    ```  
  
6.  `defaultProvider` 또는 `<membership>` 요소의 `<roleManager>` 특성을 수정하여 이전 단계에서 추가한 `<add>` 요소에서 이름 값을 지정합니다.  
  
    ```xml  
    <roleManager enabled="true" defaultProvider="MyCustomRoleProvider">  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 응용 프로그램 서비스](../../../docs/framework/common-client-technologies/client-application-services.md)  
 [클라이언트 응용 프로그램 서비스 개요](../../../docs/framework/common-client-technologies/client-application-services-overview.md)  
 [프로젝트 디자이너, 서비스 페이지](/visualstudio/ide/reference/services-page-project-designer)  
 [서비스의 고급 설정 대화 상자](/visualstudio/ide/reference/advanced-settings-for-services-dialog-box)  
 [방법: 클라이언트 응용 프로그램 서비스에서 사용자 로그인 구현](../../../docs/framework/common-client-technologies/how-to-implement-user-login-with-client-application-services.md)  
 [연습: 클라이언트 응용 프로그램 서비스 사용](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md)  
 [멤버 자격 공급자 구현](https://msdn.microsoft.com/library/d8658b8e-c962-4f64-95e1-4acce35e4582)  
 [역할 공급자 구현](https://msdn.microsoft.com/library/851671ce-bf9b-43f2-aba4-bc9d28b11c7d)  
 [응용 프로그램 설정 아키텍처](../../../docs/framework/winforms/advanced/application-settings-architecture.md)  
 [SQL Server에 대한 응용 프로그램 서비스 데이터베이스 만들기 및 구성](https://msdn.microsoft.com/library/ab894e83-7e2f-4af8-a116-b1bff8f815b2)
