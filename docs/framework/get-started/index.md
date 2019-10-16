---
title: .NET Framework 시작
ms.custom: updateeachrelease
ms.date: 04/02/2019
helpviewer_keywords:
- .NET Framework, getting started
- getting started [.NET Framework]
ms.assetid: c693fd34-88fe-4d90-b332-19eeadf3b7e7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 16e20214981bb5c0f96b26f34be99026aac19266
ms.sourcegitcommit: d8ebe0ee198f5d38387a80ba50f395386779334f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66690195"
---
# <a name="get-started-with-the-net-framework"></a>.NET Framework 시작

.NET Framework는 .NET Framework를 대상으로 하는 앱을 관리하는 런타임 실행 환경입니다. .NET Framework는 메모리 관리 및 기타 시스템 서비스를 제공하는 공용 언어 런타임과 프로그래머가 모든 주요 앱 개발 영역에서 강력하고 신뢰할 수 있는 코드를 활용할 수 있게 하는 광범위한 클래스 라이브러리로 구성됩니다.

> [!NOTE] 
> .NET Framework는 Windows 시스템에서만 사용할 수 있습니다. [.NET Core](../../core/index.md)를 사용하여 Windows, MacOS 및 Linux에서 앱을 실행할 수 있습니다. 

## <a name="Introducing"></a> .NET Framework란?

.NET Framework는 실행 중인 앱에 다양한 서비스를 제공하는 Windows용 관리되는 실행 환경으로, 다음 두 가지 주요 구성 요소로 구성됩니다. 하나는 실행 중인 앱을 처리하는 실행 엔진인 CLR(공용 언어 런타임)이고, 다른 하나는 개발자가 자신의 앱에서 호출할 수 있도록 테스트되고 재사용 가능한 코드로 구성된 .NET Framework 클래스 라이브러리입니다. .NET Framework가 실행 중인 앱에 제공하는 서비스는 다음과 같습니다.

- 메모리 관리. 많은 프로그래밍 언어에서 프로그래머는 메모리를 할당하고 해제하며 개체 수명을 처리하는 일을 담당합니다. .NET Framework 앱에서 CLR은 앱을 대신하여 이러한 서비스를 제공합니다.

- 공용 형식 시스템. 일반적인 프로그래밍 언어에서 기본 형식은 컴파일러에 의해 정의되므로 언어 간 상호 운용성을 까다롭게 합니다. .NET Framework에서 기본 형식은 .NET Framework 형식 시스템에 의해 정의되며 .NET Framework를 대상으로 하는 모든 언어에 공통적입니다.

- 광범위한 클래스 라이브러리. 프로그래머는 낮은 수준의 일반적인 프로그래밍 작업을 처리하는 방대한 양의 코드를 작성하는 대신 .NET Framework 클래스 라이브러리에서 쉽게 액세스할 수 있는 형식 및 해당 멤버로 구성된 라이브러리를 사용합니다.

- 개발 프레임워크 및 기술. .NET Framework에는 웹앱용 ASP.NET, 데이터 액세스용 ADO.NET, 서비스 지향 앱용 Windows Communication Foundation, Windows 데스크톱 앱용 Windows Presentation Foundation과 같은 앱을 개발하는 특정 영역에 대한 라이브러리가 포함됩니다.

- 언어 상호 운용성. .NET Framework를 대상으로 하는 언어 컴파일러에서 CIL(공용 중간 언어)이라는 중간 코드를 내보내면 이 코드는 런타임 시 공용 언어 런타임에 의해 컴파일됩니다. 이 기능을 사용하면 하나의 언어로 작성된 루틴은 다른 언어로 액세스하고 프로그래머는 기본 설정 언어로 앱을 만드는 데 집중할 수 있습니다.

- 버전 호환성. 거의 예외 없이 .NET Framework의 특정 버전을 사용하여 개발한 앱은 이후 버전에서 수정하지 않고 실행할 수 있습니다.

- Side-by-Side 실행. .NET Framework를 사용하면 동일한 컴퓨터에 여러 버전의 공용 언어 런타임이 존재하도록 허용함으로써 버전 충돌을 해결할 수 있습니다. 즉, 여러 버전의 앱이 공존할 수 있으며 앱이 해당 앱을 빌드한 .NET Framework 버전에서 실행될 수 있습니다. Side-by-Side 실행은 .NET Framework 버전 그룹 1.0/1.1, 2.0/3.0/3.5 및 4/4.5.x/4.6.x/4.7.x/4.8에 적용됩니다.

- 멀티 타기팅. 개발자는 [.NET Standard](../../standard/net-standard.md)를 대상으로 지정하여 표준 버전에서 지원하는 여러 .NET Framework 플랫폼에서 작동하는 클래스 라이브러리를 만듭니다. 예를 들어 .NET Framework 4.6.1, .NET Core 2.0 및 UWP 10.0.16299를 대상으로 하는 앱은 .NET Standard 2.0을 대상으로 하는 라이브러리를 사용할 수 있습니다. 

<a name="ForUsers"></a>
## <a name="the-net-framework-for-users"></a>사용자용 .NET Framework

.NET Framework 앱을 개발하지는 않지만 이를 사용하는 경우에는 .NET Framework 또는 해당 작업에 대한 특정 지식이 필요하지 않습니다. 대부분의 경우 .NET Framework는 사용자에게 완전히 투명하게 공개됩니다.

Windows 운영 체제를 사용하는 경우 .NET Framework가 이미 컴퓨터에 설치되었을 수 있습니다. 또한 .NET Framework가 필요한 앱을 설치하는 경우에는 앱의 설치 프로그램에서 특정 버전의 .NET Framework를 컴퓨터에 설치할 수 있습니다. 경우에 따라 .NET Framework를 설치하도록 요구하는 대화 상자가 나타날 수 있습니다. 이 대화 상자가 표시되었을 때 앱을 실행하려고 하고 컴퓨터가 인터넷에 연결되어 있는 경우 .NET Framework의 누락된 버전을 설치하기 위한 웹 페이지로 이동할 수 있습니다. 자세한 내용은 [설치 가이드](../install/index.md)를 참조하세요.

일반적으로는 컴퓨터에 설치되어 있는 .NET Framework 버전을 제거해서는 안 됩니다. 여기에는 두 가지 이유가 있습니다.

- 사용 중인 앱이 특정 .NET Framework 버전을 사용하는 경우 해당 버전을 제거하면 앱이 손상될 수 있습니다.

- 일부 .NET Framework 버전은 이전 버전의 내부 업데이트입니다. 예를 들어 .NET Framework 3.5는 버전 2.0의 내부 업데이트이고 .NET Framework 4.8은 버전 4~4.7.2의 내부 업데이트입니다. 자세한 내용은 [.NET Framework 버전 및 종속성](../migration-guide/versions-and-dependencies.md)을 참조하십시오.

Windows 8 이전 버전에서 .NET Framework를 제거하려는 경우에는 항상 제어판의 **프로그램 및 기능**을 사용하여 제거합니다. .NET Framework 버전을 수동으로 제거해서는 안 됩니다. Windows 8 이상에서 .NET Framework는 운영 체제 구성 요소이며 독립적으로 제거할 수 없습니다.

여러 버전의 .NET Framework는 동시에 단일 컴퓨터에 존재할 수 있습니다. 즉, 최신 버전을 설치하기 위해 이전 버전을 제거하지 않아도 됩니다.

## <a name="ForDevelopers"></a> 개발자용 .NET Framework

개발자의 경우 앱을 만들기 위해 .NET Framework를 지원하는 모든 프로그래밍 언어를 선택할 수 있습니다. .NET Framework는 언어 독립성과 상호 운용성을 제공하므로 개발된 언어에 관계없이 다른 .NET Framework 앱 및 구성 요소와 상호 작용할 수 있습니다.

.NET Framework 앱 또는 구성 요소를 개발하려면 다음과 같이 하세요.

1. 운영 체제에 사전 설치되지 않은 경우, 앱의 대상이 되는 .NET Framework 버전을 설치합니다. 최신 프로덕션 버전은 .NET Framework 4.8입니다. Windows 10 2019년 5월 업데이트에 사전 설치되어 있으며, 이전 버전의 Windows 운영 체제에서 다운로드할 수 있습니다. .NET Framework 시스템 요구 사항은 [시스템 요구 사항](system-requirements.md)을 참조하십시오. 다른 버전의 .NET Framework 설치에 대한 자세한 내용은 [설치 가이드](../install/guide-for-developers.md)를 참조하십시오. 추가 .NET Framework 패키지는 대역 외로 릴리스됩니다. 즉, 모든 일반 또는 예약된 릴리스 주기를 벗어난 롤링 방식으로 릴리스됩니다. 이러한 패키지에 대한 자세한 내용은 [.NET Framework 및 번외 릴리스](the-net-framework-and-out-of-band-releases.md)를 참조하십시오.

2. 앱을 개발하는 데 사용하는 .NET Framework에서 지원하는 언어를 선택합니다. Microsoft의 [Visual Basic](../../visual-basic/index.md), [C#](../../csharp/index.md), [F#](../../fsharp/index.md) 및 [C++/CLI](/cpp/dotnet/dotnet-programming-with-cpp-cli-visual-cpp)를 포함한 많은 언어를 사용할 수 있습니다. (.NET Framework용 앱을 개발할 수 있는 프로그래밍 언어는 [CLI(공용 언어 인프라) 사양](https://visualstudio.microsoft.com/license-terms/ecma-c-common-language-infrastructure-standards/)을 준수합니다.)

3. 앱을 만드는 데 사용되며 선택된 프로그래밍 언어를 지원하는 개발 환경을 선택하고 설치합니다. .NET Framework 앱의 Microsoft IDE(통합 개발 환경)은 [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)입니다. 많은 버전을 사용 가능합니다.

.NET Framework를 대상으로 하는 앱 개발 방법에 대한 자세한 내용은 [개발 가이드](../development-guide.md)를 참조하십시오.

## <a name="related-articles"></a>관련 문서

| 제목 | 설명 |
| ----- |------------ |
| [개요](overview.md) | .NET Framework를 대상으로 하는 앱을 빌드하는 개발자를 위한 자세한 정보를 제공합니다. |
| [설치 가이드](../install/index.md) | .NET Framework 설치 방법에 대한 정보를 제공합니다. |  
| [.NET Framework 및 번외 릴리스](the-net-framework-and-out-of-band-releases.md) | .NET Framework 대역 외 릴리스 및 이러한 릴리스를 앱에서 사용하는 방법에 대해 설명합니다. |
| [시스템 요구 사항](system-requirements.md) | .NET Framework를 실행하기 위한 하드웨어 및 소프트웨어 요구 사항이 나와 있습니다. |
| [.NET Core 및 오픈 소스](net-core-and-open-source.md) | .NET Core와 .NET Framework 간의 관계 및 오픈 소스 .NET Core 프로젝트에 액세스하는 방법에 대해 설명합니다. |
| [.NET Core 설명서](../../core/index.md) | .NET Core에 대한 개념 및 API 참조 설명서를 제공합니다. |
| [.NET Standard](../../standard/net-standard.md) | 여러 플랫폼에서 일관된 API 집합을 사용할 수 있도록 보장해 주는, 개별 .NET 구현에서 지원하는 버전 사양인 .NET Standard를 설명합니다.

## <a name="see-also"></a>참고 항목

- [.NET Framework 가이드](../index.md)
- [새로운 기능](../whats-new/index.md)
- [.NET API 브라우저](../../../api/index.md)
- [개발 가이드](../development-guide.md)
