---
title: 이식 가능한 클래스 라이브러리로 크로스 플랫폼 개발
ms.date: 09/17/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- Portable Class Library [.NET Framework]
- targeting multiple platforms
- multiple platforms, targeting
ms.assetid: c31e1663-c164-4e65-b66d-d3aa8750a154
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e5b6a32aa465700fb316bf2269c4d057ff823443
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64590343"
---
# <a name="cross-platform-development-with-the-portable-class-library"></a>이식 가능한 클래스 라이브러리를 사용 하 여 플랫폼 간 개발

Visual Studio에서 이식 가능한 클래스 라이브러리 프로젝트 형식을 쉽고 빠르게 플랫폼 간 앱 및 Microsoft 플랫폼에 대 한 라이브러리를 구축 하도록 도와줍니다.

[!INCLUDE[standard](../../../includes/pcl-to-standard.md)]

이식 가능한 클래스 라이브러리를 사용하면 코드 개발 및 테스트에 드는 시간과 비용을 줄일 수 있습니다. 이 프로젝트 형식을 사용 하 여 작성 하 고 이식 가능한.NET Framework 어셈블리를 빌드할 및.NET Framework, iOS 또는 Mac.과 같은 여러 플랫폼을 대상으로 하는 앱에서 해당 어셈블리를 참조 한 다음

Visual Studio에서 이식 가능한 클래스 라이브러리 프로젝트를 만든 다음 해당 프로젝트 개발을 시작한 후에도 대상 플랫폼을 변경할 수 있습니다. Visual Studio 코드에서 해야 할 변경 내용을 식별할 수 있는 새 어셈블리로 라이브러리를 컴파일합니다.

## <a name="create-a-portable-class-library-project"></a>이식 가능한 클래스 라이브러리 프로젝트 만들기

이식 가능한 클래스 라이브러리를 만들려면 Visual Studio에서 제공 하는 템플릿을 사용 합니다. 새 프로젝트를 만듭니다 (**파일** > **새 프로젝트**), 및를 **새 프로젝트** 대화 상자 (Visual C# 또는 Visual Basic) 프로그래밍 언어를 선택 합니다. 다음을 선택 합니다 **클래스 라이브러리 (레거시 이식 가능)** 템플릿. 프로젝트에 대 한 이름을 입력 하 고 선택 **확인**합니다.

합니다 **이식 가능한 클래스 라이브러리 추가** 대화 상자가 나타납니다. 둘 이상의 대상을 선택 하 고 선택한 **확인**합니다.

![Visual Studio에서 이식 가능한 클래스 라이브러리 대상 추가](media/add-portable-class-library.png)

## <a name="change-targets"></a>대상 변경

개발을 시작한 후 만들 때 또는 이식 가능한 클래스 라이브러리 프로젝트의 대상 플랫폼을 변경할 수 있습니다. 프로젝트를 만든 후 대상을 변경 하려면 **솔루션 탐색기**, (솔루션 아님), 이식 가능한 클래스 라이브러리 프로젝트에 대 한 바로 가기 메뉴를 열고 선택한 후 **속성** . 프로젝트 속성 페이지의 **라이브러리** 탭 플랫폼 프로젝트가 현재 대상으로 지정 함을 보여 줍니다.

![Visual Studio에서 이식 가능한 클래스 라이브러리에 대 한 프로젝트 속성](media/pcl-project-properties.png)

대상을 추가 하거나 제거를 선택 합니다 **변경** 단추를 선택 하 고 적절 한 확인란의 선택을 취소 합니다.

대상을 변경하면 프로젝트 개발에 사용할 수 있는 API가 선택에 맞춰 변경됩니다. Visual Studio에서는 대상 변경의 결과로 발생할 수 있는 오류 및 경고를 보고합니다.

Visual Studio에서 변경을 수행 하기 전에 어셈블리의 이식성을 평가 하려는 경우, 사용할 수는 [.NET 이식성 분석기](https://visualstudiogallery.msdn.microsoft.com/1177943e-cfb7-4822-a8a6-e56c7905292b)합니다.

## <a name="supported-types-and-members"></a>지원되는 형식 및 멤버

이식 가능한 클래스 라이브러리 프로젝트에서 사용할 수 있는 형식 및 멤버는 다음과 같이 여러 호환성 요소로 제한됩니다.

- 이들은 선택한 대상 간에 공유되어야 합니다.

- 이들은 이러한 여러 대상에서 유사하게 작동해야 합니다.

- 이들은 사용 중단 후보가 되어서는 안 됩니다.

- 이들은 특히 지원하는 멤버를 이식할 수 없을 때 이식 가능한 환경에서 의미가 있어야 합니다.

멤버가 이식 가능한 클래스 라이브러리에서 그리고 선택한 대상에 대해 지원되는 경우 IntelliSense의 프로젝트에 나타납니다. 그러나 이식 가능한 클래스 라이브러리에서 API가 지원될 수는 있지만 API를 사용할 수 있는지 여부는 선택한 대상에 따라 달라집니다.

## <a name="api-differences-in-the-portable-class-library"></a>이식 가능한 클래스 라이브러리에서의 API 차이점

이식 가능한 클래스 라이브러리 어셈블리가 지원되는 모든 플랫폼에서 호환되도록 하기 위해 이식 가능한 클래스 라이브러리에서 일부 멤버가 약간 변경되었습니다.

## <a name="use-the-portable-class-library"></a>이식 가능한 클래스 라이브러리 사용

이식 가능한 클래스 라이브러리 프로젝트를 빌드한 후에는 다른 프로젝트에서 이 프로젝트를 참조하게 합니다. 액세스하려는 클래스가 포함된 프로젝트 또는 특정 어셈블리를 참조할 수 있습니다.

이식 가능한 클래스 라이브러리 어셈블리를 참조하는 앱을 실행하려면 대상 플랫폼의 필수 버전(또는 이후 버전)이 컴퓨터에 설치되어 있어야 합니다. Visual Studio에는 필요한 모든 프레임워크가 포함되므로 앱을 개발하는 데 사용한 컴퓨터에서 더 이상의 수정 없이 앱을 실행할 수 있습니다.

### <a name="deploy-a-universal-windows-app"></a>유니버설 Windows 앱 배포

유니버설 Windows 앱을 만들 때 이식 가능한 클래스 라이브러리 어셈블리를 참조 하는 앱을 배포 하는 데 필요한 모든 앱 패키지에 포함 되어 및 추가 단계가 필요 하지 않습니다.

### <a name="deploy-a-net-framework-app"></a>배포는.NET Framework 앱

이식 가능한 클래스 라이브러리 어셈블리를 참조하는 .NET Framework 앱을 배포할 때 종속성을 올바른 .NET Framework 버전에 지정해야 합니다. 이 종속성을 지정하여 응용 프로그램에 필수 버전이 설치되도록 해야 합니다.

- ClickOnce 배포를 사용 하 여 종속성을 만들려면: **솔루션 탐색기**를 게시 하려면 프로젝트의 프로젝트 노드를 선택 합니다. 이 프로젝트가 이식 가능한 클래스 라이브러리 프로젝트를 참조할 프로젝트입니다. 메뉴 모음에서 선택 **프로젝트** > **속성**를 선택한 후 합니다 **게시** 탭 합니다. 에 **게시** 페이지에서 **필수 조건**합니다. 필수 .NET Framework 버전을 필수 구성 요소로 선택합니다.

- 설치 프로젝트를 사용 하 여 종속성을 만들려면: **솔루션 탐색기**, 설치 프로젝트를 선택 합니다. 메뉴 모음에서 선택 **프로젝트** > **속성** > **필수 구성 요소**합니다. 필수 .NET Framework 버전을 필수 구성 요소로 선택합니다.

.NET Framework 앱을 배포 하는 방법에 대 한 자세한 내용은 참조 하세요. [개발자를 위한 배포 가이드](../../../docs/framework/deployment/deployment-guide-for-developers.md)합니다.

## <a name="see-also"></a>참고자료

- [MVVM과 함께 이식 가능한 클래스 라이브러리 사용](../../../docs/standard/cross-platform/using-portable-class-library-with-model-view-view-model.md)
- [여러 플랫폼을 대상으로 하는 라이브러리의 앱 리소스](../../../docs/standard/cross-platform/app-resources-for-libraries-that-target-multiple-platforms.md)
- [.NET 이식성 분석기](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)
- [Windows 스토어 앱 및 Windows 런타임에 대한 .NET Framework 지원](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)
- [배포](../../../docs/framework/deployment/net-framework-applications.md)
