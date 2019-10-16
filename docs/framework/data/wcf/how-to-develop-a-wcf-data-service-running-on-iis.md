---
title: '방법: IIS에서 실행되는 WCF Data Service 개발'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, developing
- WCF Data Services, deploying
- WCF Data Services, hosting
ms.assetid: f6f768c5-4989-49e3-a36f-896ab4ded86e
ms.openlocfilehash: 89be7aa8339a4edf6d6ab9c0c243e4320d2fdfa8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052968"
---
# <a name="how-to-develop-a-wcf-data-service-running-on-iis"></a>방법: IIS에서 실행 되는 WCF 데이터 서비스 개발

이 항목에서는 WCF Data Services를 사용 하 여 인터넷 정보 서비스 (IIS)에서 실행 되는 ASP.NET 웹 응용 프로그램에서 호스트 되는 Northwind 샘플 데이터베이스를 기반으로 하는 데이터 서비스를 만드는 방법을 보여 줍니다. ASP.NET 개발 서버에서 실행 되는 ASP.NET 웹 응용 프로그램으로 동일한 Northwind 데이터 서비스를 만드는 방법에 대 한 예제는 [WCF Data Services 빠른](quickstart-wcf-data-services.md)시작을 참조 하세요.

> [!NOTE]
> Northwind 데이터 서비스를 만들려면 로컬 컴퓨터에 Northwind 샘플 데이터베이스를 설치해야 합니다. 이 샘플 데이터베이스를 다운로드하려면 [SQL Server용 샘플 데이터베이스](https://go.microsoft.com/fwlink/?linkid=24758)다운로드 페이지를 참조하세요.

이 항목에서는 Entity Framework 공급자를 사용하여 데이터 서비스를 만드는 방법을 보여 줍니다. 다른 데이터 서비스 공급자를 사용할 수 있습니다. 자세한 내용은 [데이터 서비스 공급자](data-services-providers-wcf-data-services.md)합니다.

서비스를 만든 후 데이터 서비스 리소스에 대한 액세스 권한을 명시적으로 부여해야 합니다. 자세한 내용은 [방법: 데이터 서비스](how-to-enable-access-to-the-data-service-wcf-data-services.md)에 대 한 액세스를 사용 하도록 설정 합니다.

## <a name="create-the-aspnet-web-application-that-runs-on-iis"></a>IIS에서 실행 되는 ASP.NET 웹 응용 프로그램 만들기

1. Visual Studio의 **파일** 메뉴에서 **새** > **프로젝트**를 선택 합니다.

2. **새 프로젝트** 대화 상자에서 **설치** 된 > [ **C# Visual** 또는 **Visual Basic**] > **웹** 범주를 선택 합니다.

3. **ASP.NET 웹 응용 프로그램** 템플릿을 선택 합니다.

4. 프로젝트 `NorthwindService` 의 이름으로를 입력 합니다.

5. **확인**을 클릭합니다.

6. **프로젝트** 메뉴에서 **NorthwindService 속성**을 선택 합니다.

7. **웹** 탭을 선택한 다음 **로컬 IIS 웹 서버 사용**을 선택 합니다.

8. **가상 디렉터리 만들기** 를 클릭 한 다음 **확인을**클릭 합니다.

9. 관리자 권한으로 실행되는 명령 프롬프트에서 운영 체제에 따라 다음 명령 중 하나를 실행합니다.

    - 32비트 시스템:

        ```console
        "%windir%\Microsoft.NET\Framework\v3.0\Windows Communication Foundation\ServiceModelReg.exe" -i
        ```

    - 64비트 시스템:

        ```console
        "%windir%\Microsoft.NET\Framework64\v3.0\Windows Communication Foundation\ServiceModelReg.exe" -i
        ```

     이렇게 하면 WCF(Windows Communication Foundation)가 컴퓨터에 등록됩니다.

10. 관리자 권한으로 실행되는 명령 프롬프트에서 운영 체제에 따라 다음 명령 중 하나를 실행합니다.

    - 32비트 시스템:

        ```console
        "%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe" -i -enable
        ```

    - 64비트 시스템:

        ```console
        "%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe" -i -enable
        ```

     이렇게 하면 WCF가 컴퓨터에 설치된 후 IIS가 제대로 실행됩니다. 또한 IIS를 다시 시작해야 할 수도 있습니다.

11. ASP.NET 애플리케이션이 IIS7에서 실행되는 경우 다음 단계도 수행해야 합니다.

    1. IIS 관리자를 열고 **기본 웹 사이트**아래에 있는 사진 서비스 응용 프로그램으로 이동 합니다.

    2. **기능 보기**에서 **인증**을 두 번 클릭 합니다.

    3. **인증** 페이지에서 **익명 인증**을 선택 합니다.

    4. **작업** 창에서 **편집** 을 클릭 하 여 익명 사용자가 사이트에 연결 하는 보안 주체를 설정 합니다.

    5. **익명 인증 자격 증명 편집** 대화 상자에서 **응용 프로그램 풀 id**를 선택 합니다.

    > [!IMPORTANT]
    > Network Service 계정을 사용하는 경우 해당 계정과 연결된 모든 내부 네트워크 액세스 권한이 익명 사용자에게 부여됩니다.

12. SQL Server Management Studio, sqlcmd.exe 유틸리티 또는 Visual Studio의 Transact-SQL 편집기를 사용하여 Northwind 데이터베이스가 연결된 SQL Server 인스턴스에 대해 다음 Transact-SQL 명령을 실행합니다.

    ```sql
    CREATE LOGIN [NT AUTHORITY\NETWORK SERVICE] FROM WINDOWS;
    GO
    ```

    이렇게 하면 IIS를 실행하는 데 사용되는 Windows 계정에 대한 로그인이 SQL Server 인스턴스에서 만들어집니다. 이에 따라 IIS에서 SQL Server 인스턴스에 연결할 수 있습니다.

13. Northwind 데이터베이스가 연결된 상태에서 다음 Transact-SQL 명령을 실행합니다.

    ```sql
    USE Northwind
    GO
    CREATE USER [NT AUTHORITY\NETWORK SERVICE]
    FOR LOGIN [NT AUTHORITY\NETWORK SERVICE] WITH DEFAULT_SCHEMA=[dbo];
    GO
    ALTER LOGIN [NT AUTHORITY\NETWORK SERVICE]
    WITH DEFAULT_DATABASE=[Northwind];
    GO
    EXEC sp_addrolemember 'db_datareader', 'NT AUTHORITY\NETWORK SERVICE'
    GO
    EXEC sp_addrolemember 'db_datawriter', 'NT AUTHORITY\NETWORK SERVICE'
    GO
    ```

    이렇게 하면 새 로그인에 권한이 부여되어 IIS에서 Northwind 데이터베이스에 있는 데이터를 읽고 Northwind 데이터베이스에 데이터를 쓸 수 있습니다.

## <a name="define-the-data-model"></a>데이터 모델 정의

1. **솔루션 탐색기**에서 ASP.NET 프로젝트의 이름을 마우스 오른쪽 단추로 클릭 한 다음**새 항목** **추가** > 를 클릭 합니다.

2. **새 항목 추가** 대화 상자에서 **ADO.NET 엔터티 데이터 모델**를 선택 합니다.

3. 데이터 모델의 이름에을 입력 `Northwind.edmx`합니다.

4. 엔터티 데이터 모델 마법사에서 **데이터베이스에서 생성**을 선택 하 고 **다음**을 클릭 합니다.

5. 다음 단계 중 하나를 수행 하 여 데이터 모델을 데이터베이스에 연결한 **후 다음을 클릭 합니다**.

    - 데이터베이스 연결이 이미 구성 되어 있지 않은 경우 **새 연결** 을 클릭 하 고 새 연결을 만듭니다. 자세한 내용은 [방법: SQL Server 데이터베이스](https://go.microsoft.com/fwlink/?LinkId=123631)에 대 한 연결을 만듭니다. 이 SQL Server 인스턴스에는 Northwind 샘플 데이터베이스가 연결되어 있어야 합니다.

         \- 또는 -

    - Northwind 데이터베이스에 연결할 수 있도록 데이터베이스 연결이 이미 구성되어 있는 경우 연결 목록에서 해당 연결을 선택합니다.

6. 마법사의 마지막 페이지에서 데이터베이스의 모든 테이블에 대한 확인란을 선택하고 뷰 및 저장 프로시저에 대한 확인란의 선택을 취소합니다.

7. **마침** 을 클릭하여 마법사를 닫습니다.

## <a name="create-the-data-service"></a>데이터 서비스 만들기

1. **솔루션 탐색기**에서 ASP.NET 프로젝트의 이름을 마우스 오른쪽 단추로 클릭 한 다음**새 항목** **추가** > 를 클릭 합니다.

2. **새 항목 추가** 대화 상자에서 **WCF Data Service**를 선택 합니다.

   ![Visual Studio 2015의 WCF 데이터 서비스 항목 템플릿](./media/wcf-data-service-item-template.png)

   > [!NOTE]
   > **WCF 데이터 서비스** 템플릿은 visual studio 2015에서 사용할 수 있지만 visual studio 2017에서는 사용할 수 없습니다.

3. 서비스의 이름으로을 입력 `Northwind`합니다.

     Visual Studio에서 새 서비스의 XML 태그 및 코드 파일이 생성됩니다. 기본적으로 코드 편집기 창이 열립니다. **솔루션 탐색기**에서 서비스에는 이름, Northwind 및 확장명이 svc.cs 또는. n b n이 있습니다.

4. 데이터 서비스 코드에서 데이터 서비스를 정의하는 클래스 정의의 `/* TODO: put your data source class name here */` 주석을 데이터 모델의 엔터티 컨테이너인 형식(이 경우 `NorthwindEntities`)으로 바꿉니다. 클래스 정의는 다음과 같이 나타납니다.

     [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_service/cs/northwind.svc.cs#servicedefinition)]
     [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_service/vb/northwind.svc.vb#servicedefinition)]

## <a name="see-also"></a>참고자료

- [서비스로 데이터 노출](exposing-your-data-as-a-service-wcf-data-services.md)
