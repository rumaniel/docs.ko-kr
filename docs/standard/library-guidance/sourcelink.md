---
title: 소스 링크 및 .NET 라이브러리
description: 소스 링크를 사용하여 .NET 라이브러리의 디버깅을 향상시키기 위한 모범 사례 권장 사항입니다.
author: jamesnk
ms.author: mairaw
ms.date: 01/15/2019
ms.openlocfilehash: 7530c984ce4bbe9e40362bd550bec57ac585a550
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928980"
---
# <a name="source-link"></a>소스 링크

소스 링크는 개발자가 NuGet에서 제공하는 .NET 어셈블리의 소스 코드 디버깅을 가능하게 해주는 기술입니다. 소스 링크는 NuGet 패키지를 만들 때 실행되며 어셈블리 및 패키지 내부에 소스 제어 메타데이터를 포함합니다. 패키지를 다운로드하고 Visual Studio에서 소스 링크를 사용하도록 설정한 개발자는 소스 코드를 한 단계씩 실행할 수 있습니다. 소스 링크는 뛰어난 디버깅 환경을 만들기 위해 소스 제어 메타데이터를 제공합니다.

## <a name="source-link-demo"></a>소스 링크 데모

> [!VIDEO https://www.youtube.com/embed/gyRGhCQPkB4?start=61]

## <a name="using-source-link"></a>소스 링크 사용

소스 링크 사용에 대한 지침은 [dotnet/sourcelink](https://github.com/dotnet/sourcelink/blob/master/README.md) GitHub 리포지토리에서 확인할 수 있습니다.

[NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)를 사용하여 소스 링크 메타데이터가 패키지에 성공적으로 포함되었는지 확인할 수 있습니다. 주석 식별자가 포함된 `Repository` 메타데이터가 있는지와 .pdb 파일이 각 대상의 .dll과 함께 있는지 확인합니다.

![NuGet 패키지 탐색기의 소스 링크](./media/sourcelink/nuget-package-explorer-sourcelink.png "NuGet 패키지 탐색기의 소스 링크")

**✔️** 소스 링크를 사용하여 어셈블리 및 NuGet 패키지에 소스 제어 메타데이터를 추가하는 것이 좋습니다.

> [!TIP]
> 사용자 유형에 디버거 특성을 추가하여 개발자의 디버깅 환경을 향상시킬 수 있습니다.
>
> * <xref:System.Diagnostics.DebuggerDisplayAttribute>는 클래스 또는 필드가 디버거 변수 창에 표시되는 방법을 사용자 지정할 수 있습니다.
> * <xref:System.Diagnostics.DebuggerStepThroughAttribute>는 디버거가 코드를 한 단계씩 실행하는 대신 코드를 단계별로 실행하도록 디버거에 지시합니다.
> * <xref:System.Diagnostics.DebuggerBrowsableAttribute>는 멤버가 디버거 변수 창에 표시되는지 여부를 제어합니다.

**✔️** 게시 기호 파일(`*.pdb`)을 고려합니다.

> 최상의 디버깅 환경을 위해서는 라이브러리에서 기호 파일을 게시하고 소스 링크를 사용해야 합니다. 기호 파일 및 기호 패키지에 대한 자세한 내용은 [기호 패키지](./nuget.md#symbol-packages)를 참조하세요.

>[!div class="step-by-step"]
>[이전](dependencies.md)
>[다음](publish-nuget-package.md)
