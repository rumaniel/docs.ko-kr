---
title: WCF 테스트 클라이언트(WcfTestClient.exe)
ms.date: 03/30/2017
ms.assetid: d4302855-677f-4640-aa90-c5d785d72fb7
ms.openlocfilehash: e637a2bb26bd0cc4bea653155c2a85ef5af19fd9
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038346"
---
# <a name="wcf-test-client-wcftestclientexe"></a>WCF 테스트 클라이언트(WcfTestClient.exe)
WCF (Windows Communication Foundation) 테스트 클라이언트 (Wcftestclient.exe)는 사용자가 테스트 매개 변수를 입력 하 고, 해당 입력을 서비스에 제출 하 고, 서비스가 다시 전송 하는 응답을 볼 수 있는 GUI 도구입니다. WCF 서비스 호스트와 결합 될 때 원활한 서비스 테스트 환경을 제공 합니다.

일반적으로 다음 위치에서 WCF 테스트 클라이언트 (wcftestclient.exe)를 찾을 수 있습니다. `C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE` -Community는 설치 된 Visual Studio의 수준에 따라 "Enterprise", "Professional" 또는 "Community" 중 하나일 수 있습니다.

## <a name="scenarios-for-using-test-client"></a>테스트 클라이언트 사용 시나리오

다음 섹션에서는 WCF 테스트 클라이언트를 사용 하 여 개발 프로세스를 간소화할 수 있는 가장 일반적인 시나리오에 대해 설명 합니다.

### <a name="inside-visual-studio"></a>Visual Studio의 경우

#### <a name="wcf-service-host-starts-wcf-test-client-with-a-single-service"></a>WCF 서비스 호스트가 단일 서비스에서 WCF 테스트 클라이언트 시작

새 WCF 서비스 프로젝트를 만들고 F5 키를 눌러 디버거를 시작 하면 WCF 서비스 호스트가 프로젝트에서 서비스를 호스트 하기 시작 합니다. 그런 다음 WCF Test Client가 열리고 구성 파일에 정의 된 서비스 끝점의 목록이 표시 됩니다. 그러면 매개 변수를 테스트하고, 서비스를 호출하며, 이 프로세스를 반복하여 테스트를 계속하고 서비스의 유효성을 검사할 수 있습니다.

#### <a name="wcf-service-host-starts-wcf-test-client-with-multiple-services"></a>WCF 서비스 호스트가 여러 서비스에서 WCF 테스트 클라이언트 시작

WCF 테스트 클라이언트를 사용 하 여 여러 서비스를 포함 하는 서비스 프로젝트를 디버그할 수도 있습니다. WCF 테스트 클라이언트가 열리면 프로젝트의 서비스 목록을 자동으로 반복 하 여 테스트를 위해 엽니다.

### <a name="outside-visual-studio"></a>Visual Studio 외부

Visual Studio 외부에서 WCF 테스트 클라이언트 (Wcftestclient.exe)를 호출 하 여 인터넷에서 임의의 서비스를 테스트할 수도 있습니다. 도구를 찾으려면 다음 위치로 이동합니다.

`C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE`(여기서 community는 컴퓨터에 설치 된 Visual Studio의 수준에 따라 "엔터프라이즈", "전문가" 또는 "커뮤니티" 중 하나일 수 있습니다.)

도구를 사용하려면 파일 이름을 두 번 클릭하여 이 위치에서 열거나 명령줄에서 시작합니다.

WCF 테스트 클라이언트는 명령줄 인수로 임의의 개수의 Uri를 사용 합니다.  이들은 테스트할 수 있는 서비스의 URI입니다.

`wcfTestClient.exe URI1 URI2 …`

WCF 테스트 클라이언트 창이 열리면 **파일**->**서비스 추가**를 클릭 하 고 열려는 서비스의 끝점 주소를 입력 합니다.

## <a name="wcf-test-client-user-interface"></a>WCF 테스트 클라이언트 사용자 인터페이스

WCF 테스트 클라이언트는 단일 서비스 또는 여러 서비스와 함께 사용할 수 있습니다.

### <a name="service-operations"></a>서비스 작업

WCF 테스트 클라이언트 주 창의 왼쪽 창에는 사용 가능한 모든 서비스와 해당 끝점 및 작업이 나열 됩니다.

작업을 두 번 클릭하면 작업 이름이 표시된 새 탭 내의 오른쪽 창에서 해당 내용을 볼 수 있습니다.

또한 왼쪽 창에는 클라이언트 구성 파일이 나열됩니다. 이 항목 중 하나를 두 번 클릭하면 오른쪽 창의 새 탭 창에 파일 내용이 표시됩니다.

### <a name="entering-test-parameters"></a>테스트 매개 변수 입력

테스트 매개 변수를 보려면 작업을 두 번 클릭하여 오른쪽 창에서 엽니다. 매개 변수는 기본적으로 **서식이 지정** 된 보기에 표시 되며, 매개 변수에 대해 임의의 값을 입력 하 여 서비스를 테스트할 수 있습니다.

메시지의 XML을 보려면 **xml**을 클릭 합니다. 이를 서비스로 보내려면 **호출**을 클릭 합니다.

데이터 집합 매개 변수의 경우 ... **편집** ... 옆의 단추 를 편집 하 여 DataGrid를 표시 하는 새 창에서 편집 합니다. **데이터 집합 복사** 및 **데이터 집합 붙여넣기** 단추의 모양을 확인 합니다. 처음 편집할 때 DataSet 개체의 스키마를 알 수 없는 경우 DataGrid는 비어 있습니다. DataSet 개체는 같은 스키마를 사용하여 DataGrid의 현재 개체에 붙여 넣어야 합니다. 붙여넣기 작업 전에 다른 위치에서 스키마를 복사해야 합니다. **데이터 집합 복사** 단추를 클릭 하 여 나중에 사용 하기 위해 데이터 집합 개체를 복사할 수도 있습니다.

서비스의 응답은 테스트 매개 변수 아래에 표시됩니다.

> [!NOTE]
> 예상 반환 값이 문자열이면 제공된 입력 값이 따옴표 안에 들어 있지 않은 경우에도 결과는 따옴표로 묶인 문자열로 표시됩니다.

서비스의 계약을 만들 때 특정 작업을 단방향으로 지정한 경우 서비스 응답이 표시되지 않습니다. 메시지가 배달을 위해 대기 중이면 대화 상자가 표시되어 메시지를 보냈음을 알립니다.

### <a name="session-support"></a>세션 지원

서비스 작업의 탭에서 **새 프록시 시작** 확인란을 사용 하 여 세션 지원을 설정/해제할 수 있습니다. 이 상자는 기본적으로 선택되어 있지 않습니다.

특정 작업 (또는 동일한 서비스 끝점의 다른 작업)에 대 한 테스트 매개 변수를 입력 하 고 확인란의 선택을 취소 하 여 여러 번 **호출** 을 클릭 하는 경우 이러한 작업은 하나의 프록시를 공유 하 고 서비스 상태는 여러 개에서 지속 됩니다. 작업도.

**새 프록시 시작** 확인란을 선택 하면 각 **호출**에 대해 새 프록시가 시작 되 고, 이전 세션 시나리오가 종료 되 고, 서비스 상태가 다시 설정 됩니다.

### <a name="editing-client-configuration"></a>클라이언트 구성 편집

WCF 테스트 클라이언트 주 창의 왼쪽 창에는 클라이언트 구성 파일이 나열 됩니다. 이 항목 중 하나를 두 번 클릭하면 오른쪽 창에 파일 내용이 표시됩니다.

#### <a name="edit-with-service-configuration-editor"></a>서비스 구성 편집기로 편집

왼쪽 창에서 **구성 파일** 을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴 **SvcConfigEditor를 사용 하 여 편집**을 선택 합니다. 서비스 구성 편집기가 시작되어 클라이언트 구성 내용이 표시됩니다. 이 도구 내에서 구성을 편집하고 저장할 수 있습니다.

서비스 구성 편집기에서 파일을 저장 한 후 WCF 테스트 클라이언트는 파일이 외부에서 수정 되었음을 알리는 경고 메시지를 표시 하 고 해당 파일을 다시 로드할지 여부를 묻는 메시지를 표시 합니다.

**예**를 선택 하면 "client.msi" 탭의 구성 콘텐츠가 편집기에서 변경한 내용을 반영 합니다.

**아니요**를 선택 하면 "client.msi" 탭의 구성 콘텐츠가 변경 되지 않은 상태로 유지 되 고 수정 된 내용이 원본 파일에 자동으로 저장 됩니다.

#### <a name="restore-to-default-configuration"></a>기본 구성으로 복원

모든 변경 내용을 취소 하 고 기본 클라이언트 구성으로 복원 하려면 왼쪽 창에서 **구성 파일** 을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴 **기본 구성으로 복원**을 선택 합니다. 기본 구성 값이 로드 되 고 "client.msi" 탭의 내용이 복원 됩니다.

#### <a name="validate-changes"></a>변경 내용 확인

WCF 테스트 클라이언트에 저장 된 변경 내용이 로드 되는 경우 WCF 스키마에 대 한 구성의 유효성을 검사 합니다. 오류가 발견되면 오류 정보를 보여 주는 대화 상자가 표시됩니다.

프록시 생성, 이진 컴파일 또는 서비스 호출 중에는 편집을 지 원하는 메뉴 항목 (즉, "편집 ...", "복원 ..." 등)을 사용할 수 없습니다. 업데이트 된 구성을 WCF 테스트 클라이언트에 로드할 때도 서비스 호출을 사용할 수 없습니다.

#### <a name="persist-client-configuration"></a>클라이언트 구성 유지

**도구**->**옵션** 클라이언트 구성 탭에는 기본적으로 사용 하도록 설정 된 서비스를 시작할 때 항상 구성 다시 생성 옵션이 포함 되어 있습니다.-> 이 옵션은 WCF 테스트 클라이언트에서 서비스를 로드할 때마다 최신 서비스 계약 및 서비스 App.config 파일을 기반으로 구성 파일을 다시 생성 하도록 지정 합니다.

WCF 서비스에 대 한 클라이언트 구성을 편집 하 고 항상이 업데이트 된 파일을 사용 하 여 서비스를 디버깅 하려면 **다시 생성** 옵션을 선택 취소 하면 됩니다. 이렇게 하면 서비스를 업데이트 하 고 WCF 테스트 클라이언트를 다시 여는 경우에도 업데이트 된 서비스를 기반으로 하 여 다시 생성 되는 것이 아니라 이전에 업데이트 한 파일을 사용 합니다.

그러나 다시 생성된 프록시와 일치하도록 구성 파일을 편집해야 할 수 있습니다. 다시 생성된 프록시와 구성 파일이 업데이트된 서비스로 인해 일치하지 않으면 서비스를 호출할 때 오류가 발생합니다.

> [!CAUTION]
> 클라이언트 구성 파일을 수정한 후 나중에 다시 사용하기 위해 선택하는 경우 파일이 다음 위치에 있습니다.
>
> \Documents 및 설정\\[사용자 계정] \My documents\test Client Projects.
>
> 클라이언트 구성 파일에 저장된 업데이트된 자격 증명 정보는 ACL(Access Control 목록)을 통해 보호됩니다.

### <a name="adding-removing-and-refreshing-services"></a>서비스 추가, 제거 및 새로 고침

#### <a name="add-service"></a>서비스 추가

**파일**->**서비스 추가** 를 클릭 하 여 WCF 테스트 클라이언트에 서비스를 추가 합니다. 그런 다음 추가할 서비스의 URI(엔드포인트 주소)를 입력해야 합니다. 서비스 주소는 mex 주소나 WSDL 주소일 수 있습니다.

**최근 서비스** 하위 메뉴에서 최근에 추가 된 서비스의 10 개 목록을 찾을 수도 있습니다. 하나를 선택 하면 지정 된 서비스가 WCF 테스트 클라이언트에 추가 됩니다.

서비스 트리 **내 서비스 프로젝트**의 루트를 마우스 오른쪽 단추로 클릭 하 고 **서비스 추가** 를 선택 하 여 동일한 결과를 얻을 수도 있습니다.

프록시 생성, 이진 컴파일 또는 서비스 호출 도중에는 서비스 편집을 지원하는 메뉴 항목을 사용할 수 없습니다. 서비스 호출도 비활성화됩니다.

#### <a name="remove-service"></a>서비스 제거

제거할 서비스의 서비스 루트를 마우스 오른쪽 단추로 클릭 하 고 **서비스 제거** 를 선택 하 여 WCF 테스트 클라이언트에서 서비스를 제거 합니다.

프록시 생성, 이진 컴파일 또는 서비스 호출 도중에는 서비스 제거를 지원하는 메뉴 항목을 사용할 수 없습니다. 서비스 호출도 비활성화됩니다.

#### <a name="refresh-service"></a>서비스 새로 고침

WCF 테스트 클라이언트가 실행 되는 동안 서비스를 변경 하 고 해당 서비스에 대 한 WCF 테스트 클라이언트 구현이 최신 상태 인지 확인 하려면 서비스의 서비스 루트를 마우스 오른쪽 단추로 클릭 하 고 **서비스 새로 고침**을 선택 합니다. 서비스를 새로 고친 한 서비스 상태는 다시 설정됩니다.

프록시 생성, 이진 컴파일 또는 서비스 호출 도중에는 서비스 새로 고침을 지원하는 메뉴 항목을 사용할 수 없습니다. 서비스 호출도 비활성화됩니다.

## <a name="location-of-files-generated-by-the-test-client"></a>테스트 클라이언트에서 생성한 파일의 위치

기본적으로 WCF 테스트 클라이언트는 생성 된 클라이언트 코드와 구성 파일을 "%Appdata%\local\temp\test client projects Client Projects" 폴더에 저장 합니다. 이 폴더는 WCF 테스트 클라이언트가 종료 된 후 삭제 됩니다. WCF 테스트 클라이언트에서 구성 파일이 수정 되 고 **서비스를 시작할 때 항상 구성 다시 생성** 옵션을 사용 하지 않도록 설정 하면 수정 된 파일이 매핑을 사용 하 여 "My Documents\Test Client Projects" 아래의 "cachedconfig" 폴더로 복사 됩니다. 메타 데이터-파일 이름-파일 이름) XML 파일을 인덱스로 처리 합니다.

명령줄에서 WCF 테스트 클라이언트를 시작 하 고, `/ProjectPath` 스위치를 사용 하 여 생성 된 파일을 저장 하는 데 필요한 새 경로를 지정 하거나, `/RestoreProjectPath` 스위치를 사용 하 여 기본 위치를 복원할 수도 있습니다. 구문은 다음과 같습니다.

`wcfTestClient.exe /ProjectPath [desired location]`

이 명령을 실행 해도 WCF 테스트 클라이언트는 열리지 않습니다. 폴더 위치만 변경됩니다. WCF 테스트 클라이언트가 실행 중인지 여부에 관계 없이이 명령을 실행할 수 있습니다. WCF 테스트 클라이언트를 다시 시작할 때 새 위치가 적용 됩니다. 위치 정보는 레지스트리 또는 "%Appdata%\local\temp\test client projects Client Projects" 폴더의 Wcftestclient.exe 파일에 저장할 수 있습니다.

## <a name="features-supported-by-wcf-test-client"></a>WCF 테스트 클라이언트에서 지원되는 기능

다음은 WCF 테스트 클라이언트에서 지원 되는 기능의 목록입니다.

- 서비스 호출: 요청/응답과 단방향 메시지입니다.

- 바인딩: Svcutil.exe에서 지원되는 모든 바인딩.

- 세션 제어

- 메시지 계약

- XML 직렬화

다음은 WCF 테스트 클라이언트에서 지원 되지 않는 기능 목록입니다.

- 형식: <xref:System.IO.Stream>, <xref:System.ServiceModel.Channels.Message>, <xref:System.Xml.XmlElement>, <xref:System.Xml.XmlAttribute>, <xref:System.Xml.XmlNode>, <xref:System.Xml.Serialization.IXmlSerializable> 인터페이스를 구현하는 형식(관련 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 특성 포함), <xref:System.Xml.Linq.XDocument> 및 <xref:System.Xml.Linq.XElement> 형식, ADO.NET <xref:System.Data.DataTable> 형식

- 이중 계약

- 트랜잭션

- 보안: CardSpace, 인증서 및 사용자 이름/암호를 입력 합니다.

- 바인딩하 WSFederationbinding, 모든 컨텍스트 바인딩 및 Https 바인딩, WebHttpbinding (Json 응답 메시지 지원).

## <a name="closing-wcf-test-client"></a>WCF 테스트 클라이언트 닫기

다음과 같은 방법으로 WCF 테스트 클라이언트를 닫을 수 있습니다.

- **파일** 메뉴에서 **끝내기**를 클릭합니다. 또는 WCF 테스트 클라이언트 주 창에서 **닫기**를 클릭 합니다. 이러한 작업은 모두 WCF 서비스 자동 호스트를 종료 하 고 Visual Studio에서 WCF 테스트 클라이언트를 시작 하는 경우 Visual Studio 디버깅 프로세스를 중지 합니다.

- 알림 영역에서 **WCF 서비스 호스트** 아이콘을 마우스 오른쪽 단추로 클릭 한 다음 끝내기를 클릭 **합니다.** 그러면 WCF 서비스 자동 호스트와 WCF 테스트 클라이언트가 모두 종료 되 고 Visual Studio 디버깅 프로세스가 중지 됩니다.

## <a name="see-also"></a>참고자료

- [WCF 서비스 호스트(WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)
