---
title: Visual Basic에서 My 네임스페이스 확장
ms.date: 07/20/2015
f1_keywords:
- vb.AddingMyExtensions
helpviewer_keywords:
- My namespace [Visual Basic], customizing
- My namespace
- My namespace [Visual Basic], extending
ms.assetid: 808e8617-b01c-4135-8b21-babe87389e8e
ms.openlocfilehash: 31593fa8b0cc2670b9d59b8cd61ae66efd219269
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64659768"
---
# <a name="extending-the-my-namespace-in-visual-basic"></a>Visual Basic에서 My 네임스페이스 확장
`My` Visual Basic의 네임 스페이스의.NET Framework의 강력한 쉽게 활용할 수 있도록 하는 메서드와 속성을 노출 합니다. `My` 네임 스페이스 코드 한 줄으로 어려운 작업이 줄어들 일반적인 프로그래밍 문제를 단순화 합니다. 또한를 `My` 의 동작을 사용자 지정할 수 있도록 네임 스페이스는 완벽 한 확장성 `My` 특정 응용 프로그램 요구에 맞게 해당 계층에 새 서비스를 추가 합니다. 이 항목에서는의 기존 멤버를 사용자 지정 하는 방법을 `My` 네임 스페이스 및 사용자 고유의 사용자 지정 클래스를 추가 하는 방법의 `My` 네임 스페이스입니다.  
  
 **항목 내용**  
  
- [기존 Namespace 멤버 내 사용자 지정](#customizing)  
  
- [내 개체에 멤버 추가](#addingtoobjects)  
  
- [사용자 지정 개체를 추가 합니다 내 Namespace](#addingcustom)  
  
- [멤버를 추가할는 My Namespace](#addingtonamespace)  
  
- [사용자 지정 개체에 이벤트 추가](#addingevents)  
  
- [디자인 지침](#design)  
  
- [에 대 한 클래스 라이브러리 디자인 내](#designing)  
  
- [패키징 및 배포 확장](#packaging)  
  
## <a name="customizing"></a> 기존 Namespace 멤버 내 사용자 지정  
 `My` 자주 사용 하는 응용 프로그램, 컴퓨터 등에 대 한 정보는 Visual Basic의에서 네임 스페이스입니다. 개체의 전체 목록은 합니다 `My` 네임 스페이스를 참조 하세요 [내 참조](../../../visual-basic/language-reference/keywords/my-reference.md). 기존 멤버를 사용자 지정 해야 할 수 있습니다는 `My` 네임 스페이스는 이러한 향상 된 응용 프로그램의 요구와 일치 합니다. 개체의 속성을 `My` 읽기 전용이 아닌지는 네임 스페이스 사용자 지정 값으로 설정할 수 있습니다.  
  
 예를 들어, 자주 사용 하는 것으로 가정 합니다 `My.User` 응용 프로그램을 실행 하는 사용자에 대 한 현재 보안 컨텍스트에 액세스 하는 개체입니다. 그러나 회사는 추가 정보 및 회사 내에서 사용자를 위한 기능을 노출 하는 사용자 개체를 사용 합니다. 이 시나리오에서의 기본값을 대체할 수 있습니다는 `My.User.CurrentPrincipal` 다음 예와에서 같이 사용자 고유의 사용자 지정 보안 주체 개체의 인스턴스를 사용 하 여 속성입니다.  
  
 [!code-vb[VbVbcnExtendingMy#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnExtendingMy/VB/Class1.vb#1)]  
  
 설정 합니다 `CurrentPrincipal` 속성에는 `My.User` 개체 응용 프로그램이 실행 되는 id를 변경 합니다. `My.User` 개체를 새로 지정 된 사용자에 대 한 정보를 반환 합니다.  
  
## <a name="addingtoobjects"></a> 내 개체에 멤버 추가  
 반환 된 형식은 `My.Application` 하 고 `My.Computer` 로 정의 된 `Partial` 클래스입니다. 따라서 확장할 수 있습니다는 `My.Application` 하 고 `My.Computer` 만들어 개체를 `Partial` 라는 클래스 `MyApplication` 또는 `MyComputer`합니다. 클래스 수 없습니다는 `Private` 클래스입니다. 일부로 클래스를 지정 하는 경우는 `My` 네임 스페이스에 포함 되는 메서드와 속성을 추가할 수 없다 합니다 `My.Application` 또는 `My.Computer` 개체입니다.  
  
 다음 예제에서는 라는 속성을 추가 하는 예를 들어 `DnsServerIPAddresses` 에 `My.Computer` 개체입니다.  
  
 [!code-vb[VbVbcnExtendingMy#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnExtendingMy/VB/Class2.vb#2)]  
  
## <a name="addingcustom"></a> 사용자 지정 개체를 추가 합니다 내 Namespace  
 하지만 합니다 `My` 네임 스페이스는 여러 가지 일반적인 프로그래밍 작업에 대 한 솔루션을 제공, 작업이 있을 수 있습니다는 `My` 네임 스페이스를 다루지 않습니다. 예를 들어 응용 프로그램이 사용자 데이터에 대 한 사용자 지정 디렉터리 서비스에 액세스할 수 있습니다 또는 응용 프로그램에서 Visual Basic을 사용 하 여 기본적으로 설치 되지 않은 어셈블리를 사용할 수 있습니다. 확장할 수 있습니다는 `My` 환경과 관련 된 일반적인 작업에 대 한 사용자 지정 솔루션을 포함 하도록 네임 스페이스입니다. `My` 네임 스페이스 증가 하는 응용 프로그램 요구를 충족 하기 위해 새 멤버를 추가 하도록 쉽게 확장할 수 있습니다. 또한, 배포할 수 있습니다 프로그램 `My` 다른 개발자에 게 Visual Basic 템플릿으로 네임 스페이스 확장 합니다.  
  
### <a name="addingtonamespace"></a> 멤버를 추가할는 My Namespace  
 때문에 `My` 네임 스페이스는 같은 다른 네임 스페이스를 추가할 수 있습니다 최상위 속성에는 모듈을 추가 하 고 지정 하 여는 `Namespace` 의 `My`합니다. 주석을 사용 하 여 모듈을 `HideModuleName` 다음 예제에서와 같이 특성입니다. 합니다 `HideModuleName` 특성 하면 IntelliSense의 멤버를 표시 하는 경우 모듈 이름이 표시 되지 것입니다는 `My` 네임 스페이스입니다.  
  
 [!code-vb[VbVbcnExtendingMy#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnExtendingMy/VB/Class1.vb#3)]  
  
 멤버를 추가 하는 `My` 네임 스페이스, 모듈에 필요에 따라 속성을 추가 합니다. 추가할 각 속성에 대 한 합니다 `My` 네임 스페이스 형식의 private 필드를 추가 `ThreadSafeObjectProvider(Of T)`형식이 사용자 지정 속성에서 반환 되는 형식, 합니다. 이 필드는 호출 하 여 속성에 의해 반환 될 스레드로부터 안전한 개체 인스턴스를 만드는 데는 `GetInstance` 메서드. 결과적으로, 확장된 속성에 액세스 하는 각 스레드는 반환 된 형식의 고유 인스턴스를 받습니다. 다음 예제에서는 라는 속성을 추가 `SampleExtension` 형식의 `SampleExtension` 에 `My` 네임 스페이스:  
  
 [!code-vb[VbVbcnExtendingMy#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnExtendingMy/VB/Class1.vb#4)]  
  
## <a name="addingevents"></a> 사용자 지정 개체에 이벤트 추가  
 사용할 수는 `My.Application` 사용자에 대 한 이벤트를 노출 하는 개체 `My` 확장 하 여 개체를 `MyApplication` partial 클래스에는 `My` 네임 스페이스. Windows 기반 프로젝트를 두 번 클릭 합니다 **My Project** 에서 프로젝트의 노드 **솔루션 탐색기**합니다. Visual Basic의 **프로젝트 디자이너**를 클릭 합니다 `Application` 탭을 클릭 한 다음를 `View Application Events` 단추. ApplicationEvents.vb 라는 새 파일이 생성 됩니다. 확장에 대 한 다음 코드를 포함 합니다 `MyApplication` 클래스입니다.  
  
 [!code-vb[VbVbcnExtendingMy#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnExtendingMy/VB/Class1.vb#5)]  
  
 사용자 지정에 대 한 이벤트 처리기를 추가할 수 있습니다 `My` 사용자 지정 이벤트 처리기를 추가 하 여 개체를 `MyApplication` 클래스입니다. 사용자 지정 이벤트를 사용 하는 이벤트 처리기를 추가, 제거 또는 이벤트가 발생할 때 실행 하는 코드를 추가할 수 있습니다. `AddHandler` 코드 사용자 지정 이벤트를 이벤트를 처리 하는 사용자가 코드를 추가한 경우에 실행 합니다. 예를 들어, 다음을 고려해 야 합니다 `SampleExtension` 이전 섹션에서 개체에는 `Load` 이벤트에 대 한 사용자 지정 이벤트 처리기를 추가 하려는 합니다. 다음 코드 예제에서는 라는 사용자 지정 이벤트 처리기를 보여 줍니다 `SampleExtensionLoad` 될 때 호출는 `My.SampleExtension.Load` 이벤트가 발생 합니다. 새 처리에 코드를 추가한 하는 경우 `My.SampleExtensionLoad` 이벤트는 `AddHandler` 이 사용자 지정 이벤트 코드의 일부가 실행 됩니다. 합니다 `MyApplication_SampleExtensionLoad` 메서드를 처리 하는 이벤트 처리기의 예가 나와 코드 예제에 포함 되는 `My.SampleExtensionLoad` 이벤트입니다. 합니다 `SampleExtensionLoad` 선택 하면 이벤트를 사용할 수는 합니다 **내 응용 프로그램 이벤트** 코드 편집기 위의 ApplicationEvents.vb 파일을 편집 하는 경우 왼쪽된 드롭다운 목록에서 옵션입니다.  
  
 [!code-vb[VbVbcnExtendingMy#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnExtendingMy/VB/Class1.vb#6)]  
  
## <a name="design"></a> 디자인 지침  
 에 대 한 확장을 개발 하는 경우는 `My` 네임 스페이스 확장 구성 요소의 유지 관리 비용을 최소화 하려면 다음 지침을 따르세요.  
  
- **확장 논리만을 포함 됩니다.** 에 포함 된 논리를 `My` 네임 스페이스 확장에 필요한 기능을 노출 하는 데 필요한 코드만 포함 해야 합니다 `My` 네임 스페이스입니다. 확장 사용자 프로젝트에서 소스 코드로 상주할 때문에 높은 유지 관리 비용을 발생 시킵니다 확장 구성 요소 업데이트 및 가능 하면 피해 야 합니다.  
  
- **프로젝트 가정을 최소화 합니다.** 확장을 만들 때 합니다 `My` 네임 스페이스 참조, 프로젝트 수준의 imports 또는 특정 컴파일러 설정 집합을 가정 하지 마세요 (예를 들어 `Option Strict` 해제) 합니다. 대신 종속성을 최소화 하 고 사용 하 여 형식에 대 한 모든 참조를 정규화 합니다 `Global` 키워드입니다. 또한 확장을 사용 하 여 컴파일되는지 확인 `Option Strict` 확장에서 오류를 최소화 하에 있습니다.  
  
- **확장 코드를 격리 합니다.** 단일 파일에 코드를 배치 하면 확장 Visual Studio 항목 템플릿을 형태로 쉽게 배포 가능 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "패키징 및 배포 확장"을 참조 하세요. 모든 배치를 `My` 네임 스페이스 확장 코드를 단일 파일 또는 프로젝트에서 별도 폴더에도 도움이 됩니다 찾을 사용자는 `My` 네임 스페이스 확장 합니다.  
  
## <a name="designing"></a> 에 대 한 클래스 라이브러리 디자인 내  
 대부분의 개체 모델이 있는 경우 몇 가지 디자인 패턴에서 잘 작동 합니다 `My` 네임 스페이스 및 기타 하지 않습니다. 확장을 디자인할 때를 `My` 네임 스페이스 원칙은 다음과:  
  
- **상태 비저장 메서드입니다.** 메서드를 `My` 네임 스페이스에는 특정 작업에 전체 솔루션을 제공 해야 합니다. 메서드에 전달 되는 매개 변수 값을 특정 작업을 완료 하는 데 필요한 모든 입력을 제공 하는지 확인 합니다. 리소스에 연결 등의 이전 상태를 사용 하는 메서드를 만들지 마세요.  
  
- **전역 인스턴스입니다.** 유지 관리 되는 유일한 상태 이기 때문은 `My` 네임 스페이스 전체 프로젝트에 적용 됩니다. 예를 들어 `My.Application.Info` 응용 프로그램 전체에서 공유 되는 상태를 캡슐화 합니다.  
  
- **단순한 매개 변수 형식입니다.** 간단 하 게 복잡 한 매개 변수 형식을 사용 하지 않음으로써 합니다. 입력 매개 변수가 하나는 메서드를 만들거나 단순 입력된 형식 문자열, 기본 형식 등을 수행 하는 대신 합니다.  
  
- **팩터리 메서드입니다.** 일부 형식은 인스턴스화가 까다롭습니다. 팩터리 메서드에 대 한 확장으로 제공 하는 `My` 네임 스페이스를 사용 하면 보다 쉽게 검색 하 고이 범주에 속하는 형식을 사용할 수 있습니다. 잘 작동 하는 팩터리 메서드의 예로 `My.Computer.FileSystem.OpenTextFileReader`합니다. .NET Framework에서 사용할 수는 몇 가지 stream 유형이 있습니다. 특히, 텍스트 파일을 지정 하 여는 `OpenTextFileReader` 는 사용자를 사용 하는 스트림을 이해 하는 데 도움이 됩니다.  
  
 이러한 지침 클래스 라이브러리에 대 한 일반적인 디자인 원칙을 방해 하지 않습니다. 하는 Visual Basic을 사용 하는 개발자를 위한 최적화 된 권장 사항 및 `My` 네임 스페이스입니다. 클래스 라이브러리를 만들기 위한 일반적인 디자인 원칙을 참조 하세요 [프레임 워크 디자인 지침](../../../standard/design-guidelines/index.md)합니다.  
  
## <a name="packaging"></a> 패키징 및 배포 확장  
 포함할 수 있습니다 `My` 네임 스페이스 확장의 Visual Studio 프로젝트 템플릿을 확장 패키지를 Visual Studio 항목 템플릿을로 배포할 수 있습니다. 패키지 있습니다 프로그램 `My` Visual Studio 항목 템플릿 네임 스페이스 확장을 Visual Basic에서 제공 하는 추가 기능 활용을 걸릴 수 있습니다. 이러한 기능을 프로젝트는 특정 어셈블리를 참조 하는 경우 확장을 포함 하거나 사용자가 명시적으로 추가할 하 `My` 를 사용 하 여 네임 스페이스 확장을 **My 확장** Visual Basic의 페이지 프로젝트 디자이너입니다.  
  
 배포 하는 방법에 대 한 자세한 내용은 `My` 네임 스페이스 확장을 참조 하세요 [패키징 및 배포 사용자 지정 내 확장](../../../visual-basic/developing-apps/customizing-extending-my/packaging-and-deploying-custom-my-extensions.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [사용자 지정 My 확장명 패키징 및 배포](../../../visual-basic/developing-apps/customizing-extending-my/packaging-and-deploying-custom-my-extensions.md)
- [Visual Basic 애플리케이션 모델 확장](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)
- [My에 사용할 수 있는 개체 사용자 지정](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)
- [내 확장명 페이지, 프로젝트 디자이너](/visualstudio/ide/reference/my-extensions-page-project-designer-visual-basic)
- [프로젝트 디자이너, 응용 프로그램 페이지(Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)
- [부분](../../../visual-basic/language-reference/modifiers/partial.md)
