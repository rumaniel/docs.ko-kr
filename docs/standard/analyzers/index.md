---
title: Roslyn 기반 분석기 - .NET
description: 문제를 찾고 해당 문제에 대한 수정 사항을 제안하는 Roslyn 기반 분석기에 대해 알아봅니다.
author: billwagner
ms.author: wiwagn
ms.date: 01/24/2018
ms.technology: dotnet-standard
ms.openlocfilehash: 436cfb3904f0891f8c18bb5890563a13d65e2d1c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62003056"
---
# <a name="the-roslyn-based-analyzers"></a>Roslyn 기반 분석기

Roslyn 기반 분석기는 .NET Compiler SDK(Roslyn API)를 사용해 프로젝트의 소스 코드를 분석하여 문제를 찾고 수정을 제안합니다. 분석기에 따라 버그를 일으킬 수 있는 사례에서 보안 문제, API 호환성 등에 이르는 다양한 종류의 문제를 찾습니다.

Roslyn 기반 분석기는 대화식으로도 사용할 수 있고 빌드 중에도 작동합니다. Visual Studio를 사용할 때나 명령줄 빌드 중에 서로 다른 지침을 제공합니다.

Visual Studio에서 코드를 편집하는 동안에는 변경 작업을 하면 분석기가 실행되어 문제를 트리거하는 코드를 작성하는 즉시 발생할 수 있는 문제를 포착합니다. 모든 문제는 아래에 물결선을 사용하여 강조 표시됩니다. Visual Studio에서는 전구를 표시하고 이 전구를 클릭하면 분석기에서 해당 문제에 대한 가능한 수정을 제안합니다. Visual Studio 또는 명령줄에서 프로젝트를 빌드할 때는 모든 소스 코드가 분석되며 분석기는 잠재적 문제의 전체 목록을 제공합니다. 다음 그림에서는 한 가지 예를 보여줍니다.

![프레임워크 분석기에서 보고한 문제](./media/framework-analyzers-2.png)

Roslyn 기반 분석기에서는 잠재적 문제를 문제의 심각도에 따라 오류, 경고 또는 정보로 보고합니다.

Roslyn 기반 분석기는 프로젝트에서 NuGet 패키지로 설치합니다. 구성된 분석기와 각 분석기의 설정은 모든 개발자의 컴퓨터에서 해당 프로젝트에 대해 복원되고 실행됩니다.

> [!NOTE]
> Roslyn 기반 분석기의 사용자 환경은 이전 버전의 FxCop 및 보안 분석 도구와 같은 코드 분석 라이브러리와 다릅니다.  Roslyn 기반 분석기는 명시적으로 실행할 필요가 없습니다. Visual Studio의 “분석” 메뉴에서 “코드 분석 실행” 메뉴 항목을 사용할 필요가 없습니다. Roslyn 기반 분석기는 작업하는 과정에 비동기적으로 실행됩니다.

## <a name="more-information-on-specific-analyzers"></a>특정 분석기에 대한 자세한 정보

이 섹션에서는 다음과 같은 분석기를 다룹니다.

* [API 분석기](api-analyzer.md): 이 분석기는 코드에서 잠재적인 호환성 위험이나 더 이상 사용되지 않는 API의 사용이 있는지 검사합니다.
* [프레임워크 분석기](framework-analyzer.md): 이 분석기는 코드가 .NET Framework 애플리케이션에 대한 지침을 따르는지 검사합니다. 이러한 규칙에는 여러 보안 기반 권장 사항이 포함됩니다.
* [.NET 이식성 분석기](portability-analyzer.md): 이 분석기는 코드를 검사하여 애플리케이션이 iOS, Android 및 Mac용 .NET Core, .NET 표준, UWP 및 Xamarin을 비롯한 다른 .NET 구현 및 프로필과 호환되도록 하는 데 필요한 작업량을 확인합니다.
