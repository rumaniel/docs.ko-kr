---
title: External RuleSet Toolkit
ms.date: 03/30/2017
ms.assetid: a306d283-a031-475e-aa01-9ae86e7adcb0
ms.openlocfilehash: c453c6137beeae8eee0e356734a1f9cdf8d8568b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62005487"
---
# <a name="external-ruleset-toolkit"></a>External RuleSet Toolkit

일반적으로 워크플로 애플리케이션 내에서 규칙이 사용될 경우 해당 규칙은 어셈블리의 일부입니다. 일부 시나리오에서는 워크플로 어셈블리를 다시 빌드하고 배포하지 않고도 RuleSet을 업데이트할 수 있도록 어셈블리와 별도로 RuleSet을 유지할 수 있습니다. 이 샘플에서는 데이터베이스에 있는 RuleSet을 관리하고 편집하며 런타임에 워크플로에서 이러한 RuleSet에 액세스할 수 있습니다. 따라서 워크플로 인스턴스를 실행하여 RuleSet 변경 내용을 자동으로 통합할 수 있습니다.

External RuleSet Toolkit 샘플에는 데이터베이스에서 RuleSet 버전을 관리하고 편집하는 데 사용할 수 있는 Windows Forms 기반 도구가 포함되어 있으며, 해당 규칙을 실행하는 호스트 서비스 및 활동도 포함되어 있습니다.

> [!NOTE]
> 이 샘플에 필요 [Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=96181)합니다.

Visual Studio는 Windows Workflow Foundation (WF)의 일부로 규칙 집합 편집기를 제공합니다. 이 편집기는 워크플로의 `Policy` 활동을 두 번 클릭하여 시작할 수 있으며 정의된 RuleSet 개체를 워크플로와 연결된 .rules 파일로 serialize합니다. `Policy` 활동은 워크플로에 대해 RuleSet 인스턴스를 실행합니다. .rules 파일은 워크플로 프로젝트를 빌드할 때 리소스로 어셈블리에 컴파일됩니다.

이 샘플의 구성 요소는 다음과 같습니다.

- 데이터베이스에서 RuleSet 버전을 편집하고 관리하는 데 사용할 수 있는 RuleSet 그래픽 사용자 인터페이스

- 호스트 애플리케이션에서 구성되고 데이터베이스에서 RuleSet에 액세스하는 RuleSet 서비스

- RuleSet 서비스에서 RuleSet을 요청하고 워크플로에 대해 RuleSet을 실행하는 `ExternalPolicy` 활동

구성 요소의 상호 작용은 다음 이미지에 표시 됩니다. 그 뒤에 나오는 단원에서는 각 구성 요소에 대해 설명합니다.

![External RuleSet Toolkit 샘플 개요를 보여 주는 다이어그램입니다.](./media/external-ruleset-toolkit/ruleset-toolkit-overview.gif)

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ExternalRuleSetToolKit`

## <a name="ruleset-tool"></a>RuleSet 도구

다음 이미지는 RuleSet 도구의 스크린 샷을입니다. **규칙 저장소** 메뉴, 데이터베이스에서 사용 가능한 Ruleset을 로드 하 고 수정 된 Ruleset을 저장소에 다시 저장 합니다. 애플리케이션 구성 파일에서는 RuleSet 데이터베이스에 대한 데이터베이스 연결 문자열을 제공합니다. 도구를 시작하면 구성된 데이터베이스에서 RuleSet이 자동으로 로드됩니다.

![규칙 집합 브라우저를 보여주는 스크린샷.](./media/external-ruleset-toolkit/ruleset-browser-dialog.gif)

RuleSet 도구에서는 RuleSet에 주 버전 및 부 버전 번호를 적용하여 동시에 여러 버전을 유지하고 저장할 수 있게 합니다. 이 도구에서는 버전 관리 기능 이외에 잠금이나 기타 구성 관리 기능을 제공하지 않습니다. 이 도구를 사용하여 새 RuleSet 버전을 만들거나 기존 버전을 삭제할 수 있습니다. 클릭 하면 **새로 만들기**, 도구 새 RuleSet 이름을 만들고 버전 1.0에 적용 합니다. 버전을 복사하면 도구에서 포함된 규칙을 비롯하여 선택한 RuleSet 버전의 복사본을 만들고 고유한 새 버전 번호를 할당합니다. 이러한 버전 번호는 기존 RuleSet의 버전 번호를 기반으로 합니다. 양식에서 연결된 필드를 사용하여 RuleSet 이름 및 버전 번호를 변경할 수 있습니다.

클릭 하면 **규칙 편집**, 다음 이미지에 표시 된 대로 규칙 집합 편집기가 시작 됩니다.

![규칙 집합 편집기를 보여주는 스크린샷.](./media/external-ruleset-toolkit/ruleset-editor-dialog.gif)

Windows Workflow Foundation에 대 한 Visual Studio 추가 기능의 일부인 편집기 대화 상자를 다시 호스트입니다. Intellisense 지원을 비롯하여 편집기 대화 상자와 동일한 기능을 제공합니다. 도구; RuleSet과 연결 된 대상 형식 (예: 워크플로)에 대해 작성 된 규칙 클릭 하면 **찾아보기** 주 도구 대화 상자에는 **워크플로/형식 선택기** 그림 4 에서처럼 대화 상자가 나타납니다.

![워크플로 &#47;입력 선택](./media/71f08d57-e8f2-499e-8151-ece2cbdcabfd.gif "71f08d57-e8f2-499e-8151-ece2cbdcabfd")

그림 4: 워크플로/형식 선택기

사용할 수는 **워크플로/형식 선택기** 어셈블리 및 해당 어셈블리 내의 특정 형식을 지정 하는 대화 상자. 이 형식은 규칙이 제작 및 실행되는 대상 형식입니다. 대부분의 경우 대상 형식은 워크플로나 다른 활동 형식입니다. 그러나 .NET 형식에 대해 RuleSet을 실행할 수 있습니다.

어셈블리 파일 및 형식에 대 한 경로 `name are stored with the` 에서 데이터베이스를 데이터베이스에서 검색 하면 되도록 도구 ruleset을 대상 형식을 자동으로 로드 합니다.

클릭 하면 **확인** 에 **워크플로/형식 선택기** 대화 상자에서 대상 형식에 규칙에서 참조 하는 모든 멤버가 있는지 확인 하는 규칙 집합에 대해 선택한 형식 검사 합니다. 에 오류가 표시 됩니다는 **유효성 검사 오류** 대화 합니다. 오류에도 불구 하 고 변경 내용을 사용 하 여 계속 하도록 선택할 수 있습니다 **취소**합니다. **도구** 주 도구 대화 상자에서 메뉴를 클릭 **유효성 검사** 다시 대상 활동에 대해 RuleSet 버전 유효성 검사를 합니다.

![유효성 검사 오류 대화 상자를 보여주는 스크린샷.](./media/external-ruleset-toolkit/validation-errors-dialog.png)

**데이터** 메뉴 도구에서 가져오기 및 Ruleset을 내보낼 수 있습니다. 클릭 하면 **가져오기**,.rules 파일을 선택할 수 있는, 파일 선택 대화 상자가 나타납니다. 이 수도 있고 처음에 Visual Studio에서 만든 파일 되지 않을 수 있습니다. .rules 파일에는 조건 컬렉션과 RuleSet 컬렉션을 포함하는 serialize된 `RuleDefinitions` 인스턴스가 포함되어야 합니다. 도구에서는 조건 컬렉션을 사용 하지 않지만 사용 된 `RuleDefinitions` .rules 형식을 Visual Studio 환경과 상호 작용을 허용 합니다.

.Rules 파일을 선택한 후는 **RuleSet 선택기** 대화 상자가 나타납니다. 이 대화 상자를 사용하여 파일에서 가져올 RuleSet을 선택할 수 있습니다. 기본적으로 모든 RuleSet으로 지정되어 있습니다. WF 프로젝트 내의 버전 관리는 어셈블리의 버전과 동일하기 때문에 .rules 파일의 RuleSet에는 버전 번호가 없습니다. 가져오기 과정에서 도구를 자동으로 할당 (가져온 후 변경할 수 있습니다)는 다음 사용 가능한 주 버전 번호; 할당 된 버전 번호를 표시 합니다 **RuleSet 선택기** 목록입니다.

도구는 가져오는 각 RuleSet에 대해 RuleSet에 사용된 멤버를 기반으로 .rules 파일(있는 경우)의 위치 아래에 있는 bin\Debug 폴더에서 연결된 형식을 찾으려고 합니다. RuleSet 도구에서 일치하는 형식을 여러 개 찾으면 .rules 파일 이름과 형식 이름이 일치하는 형식을 선택하려고 합니다. 예를 들어 `Workflow1` 형식은 Workflow1.rules에 대응합니다. 일치하는 항목이 여러 개 있으면 형식을 선택하라는 메시지가 표시됩니다. 이 자동 식별 메커니즘을 일치 하는 어셈블리나 형식을 찾지 못하는 경우 가져온 후 클릭할 수 **찾아보기** 연결된 된 형식에 이동 주 도구 대화 상자에서. 다음 이미지에서는 RuleSet 선택기를 보여 줍니다.

![RuleSet 선택기 대화 상자를 보여주는 스크린샷.](./media/external-ruleset-toolkit/ruleset-selector-dialog.gif)

클릭 하면 **데이터 내보내기** 주 도구 메뉴에서를 **RuleSet 선택기** 대화 상자가 다시 나타나 내보내야 하는 데이터베이스에서 Ruleset을 결정할 수 있습니다. 클릭 하면 **확인**, **파일 저장** 이름과 결과.rules 파일의 위치를 지정할 수 있는 대화 상자가 나타납니다. .rules 파일에는 버전 정보가 저장되지 않으므로 지정된 RuleSet 이름을 사용하는 RuleSet 버전을 하나만 선택할 수 있습니다.

## <a name="policyfromservice-activity"></a>PolicyFromService 활동

`PolicyFromService` 활동에 대한 코드는 간단합니다. 이 활동은 WF와 함께 제공되는 `Policy` 활동과 매우 유사하게 작동하지만 .rules 파일에서 대상 RuleSet을 검색하는 대신 호스트 서비스를 호출하여 RuleSet 인스턴스를 가져옵니다. 그런 다음 루트 워크플로 활동 인스턴스에 대해 RuleSet을 실행합니다.

워크플로에서 활동을 사용하려면 워크플로 프로젝트에서 `PolicyActivities` 및 `RuleSetService` 어셈블리에 참조를 추가합니다. 도구 상자에 활동을 추가하는 방법에 대한 자세한 내용은 이 항목의 끝에 나오는 절차를 참조하세요.

워크플로에 활동을 배치한 후에는 실행할 RuleSet의 이름을 제공해야 합니다. 리터럴 값으로 이름을 입력하거나 다른 활동의 워크플로 변수나 속성에 바인딩할 수 있습니다. 선택적으로 실행할 특정 RuleSet의 버전 번호를 입력할 수 있습니다. 주 버전 및 부 버전 번호의 기본값 0을 유지하면 데이터베이스의 최신 버전 번호가 자동으로 활동에 제공됩니다.

## <a name="ruleset-service"></a>RuleSet 서비스

이 서비스는 데이터베이스에서 RuleSet 버전을 검색하고 호출 활동에 반환합니다. 앞에서 설명한 대로 `GetRuleSet` 호출에서 전달된 주 버전 및 부 버전 값이 둘 다 0이면 서비스에서는 최신 버전을 검색합니다. 이때 RuleSet 정의나 인스턴스의 캐시가 없으며 마찬가지로 RuleSet 버전을 "배포됨"으로 표시하여 진행 중인 RuleSet과 구분하는 기능도 없습니다.

서비스에서 액세스할 데이터베이스는 애플리케이션 구성 파일을 사용하여 호스트에서 구성해야 합니다.

#### <a name="to-run-the-tool"></a>도구를 실행하려면

1. 도구 및 서비스에서 사용하는 RuleSet 테이블을 설정하는 폴더에 Setup.sql 파일이 포함되어 있습니다. Setup.cmd 배치 파일을 실행하여 SQL Express에 규칙 데이터베이스를 만들고 RuleSet 테이블을 설정할 수 있습니다.

2. 배치 파일이나 Setup.sql을 편집하고 SQL Express를 사용하지 않거나 `Rules`가 아닌 다른 이름의 데이터베이스에 테이블을 배치하도록 지정할 경우 RuleSet 도구와 `UsageSample` 프로젝트의 애플리케이션 구성 파일을 같은 정보로 편집해야 합니다.

3. Setup.sql 스크립트를 실행한 후에는 `ExternalRuleSetToolkit` 솔루션을 빌드하고 ExternalRuleSetTool 프로젝트에서 RuleSet 도구를 시작할 수 있습니다.

4. `RuleSetToolkitUsageSample` 순차 워크플로 콘솔 애플리케이션에는 샘플 워크플로가 포함되어 있습니다. 워크플로는 대상 RuleSet이 실행되는 `PolicyFromService` 활동 및 두 가지 변수인 `orderValue`와 `discount`로 구성되어 있습니다.

5. 샘플을 사용하려면 `RuleSetToolkitUsageSample` 솔루션을 빌드합니다. RuleSet 도구 주 메뉴에서 클릭 **데이터 가져오기** RuleSetToolkitUsageSample 폴더의 DiscountRuleSet.rules 파일을 가리킵니다. 클릭 합니다 **규칙 저장소-저장** 데이터베이스로 가져온된 RuleSet을 저장 하려면 메뉴 옵션입니다.

6. `PolicyActivities` 어셈블리는 샘플 워크플로 프로젝트에서 참조되므로 `PolicyFromService` 활동이 워크플로에 나타납니다. 그러나 기본적으로 도구 상자에는 나타나지 않습니다. 도구 상자에 추가하려면 다음을 수행합니다.

    - 도구 상자를 마우스 오른쪽 단추로 클릭 **선택 항목** (잠시 걸릴 수 있음).

    - 경우는 **도구 상자 항목 선택** 대화 상자가 나타나면 클릭 합니다 **활동** 탭 합니다.

    - 로 이동 합니다 `PolicyActivities` 어셈블리에는 `ExternalRuleSetToolkit` 솔루션을 클릭 **열기**.

    - 있는지 확인 합니다 `PolicyFromService` 에서 활동이 선택 되었는지는 **도구 상자 항목 선택** 대화 하 고 클릭 한 다음 **확인**합니다.

    - 이제 활동에서 도구 상자에 표시 합니다 **RuleSetToolkitUsageSample 구성 요소** 범주입니다.

7. RuleSet 서비스는 Program.cs에서 다음 문을 사용하여 콘솔 애플리케이션 호스트에 이미 구성되어 있습니다.

    ```csharp
    workflowRuntime.AddService(new RuleSetService());
    ```

8. 구성 파일을 사용하여 호스트에 서비스를 구성할 수도 있습니다. 자세한 내용은 SDK 설명서를 참조하세요.

9. 애플리케이션 구성 파일이 워크플로 프로젝트에 추가되어 서비스에서 사용할 데이터베이스에 대한 연결 문자열을 지정합니다. 이 문자열은 RuleSet 도구에서 사용하는 연결 문자열과 동일해야 합니다. RuleSet 도구에서 사용하는 연결 문자열은 RuleSet 테이블을 포함하는 데이터베이스를 가리킵니다.

10. 이제 다른 모든 워크플로 콘솔 애플리케이션처럼 `RuleSetToolkitUsageSample` 프로젝트를 실행할 수 있습니다. F5 또는 Ctrl + f5를 눌러 Visual Studio 내에서 누르거나 RuleSetToolkitUsageSample.exe 파일을 직접 실행 합니다.

    > [!NOTE]
    > RuleSet 도구에서는 사용 샘플 어셈블리를 로드하므로 사용 샘플을 다시 컴파일하려면 도구를 닫아야 합니다.
