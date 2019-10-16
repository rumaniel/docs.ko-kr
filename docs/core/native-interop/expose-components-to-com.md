---
title: COM에 .NET Core 구성 요소 공개
ms.date: 07/12/2019
helpviewer_keywords:
- exposing .NET Core components to COM
- interoperation with unmanaged code, exposing .NET Core components
- COM interop, exposing COM components
ms.assetid: 21271167-fe7f-46ba-a81f-a6812ea649d4
author: jkoritzinsky
ms.author: jekoritz
ms.openlocfilehash: 8f9624414a2b423bd43e8790d11b70ae1ca6286d
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216234"
---
# <a name="exposing-net-core-components-to-com"></a>COM에 .NET Core 구성 요소 공개

.NET Core에서는 COM에 .NET 개체를 공개하는 절차가 .NET Framework에 비해 크게 간소화되었습니다. 다음 절차에서는 클래스를 COM에 공개하는 방법을 안내합니다. 이 자습서에서는 다음을 수행하는 방법을 보여 줍니다.

- .NET Core에서 COM에 클래스를 공개합니다.
- .NET Core 라이브러리를 빌드하는 동안 COM 서버를 생성합니다.
- 레지스트리 없는 COM을 위한 병렬 서버 매니페스트를 자동으로 생성합니다.

## <a name="prerequisites"></a>전제 조건

- [.NET Core 3.0 SDK](https://dotnet.microsoft.com/download) 또는 최신 버전을 설치합니다.

## <a name="create-the-library"></a>라이브러리 만들기

첫 번째 단계는 라이브러리를 만드는 것입니다.

1. 새 폴더를 만든 다음, 해당 폴더에서 다음 명령을 실행합니다.
    
    ```dotnetcli
    dotnet new classlib
    ```

2. `Class1.cs`를 엽니다.
3. `using System.Runtime.InteropServices;`를 파일의 맨 위에 추가합니다.
4. `IServer` 인터페이스를 만듭니다. 예:

   [!code-csharp[The IServer interface](~/samples/core/extensions/COMServerDemo/COMContract/IServer.cs)]

5. 구현 중인 COM 인터페이스의 인터페이스 GUID를 사용하여 `[Guid("<IID>")]` 특성을 인터페이스에 추가합니다. 예: `[Guid("fe103d6e-e71b-414c-80bf-982f18f6c1c7")]`. 이 GUID는 이 COM용 인터페이스의 유일한 식별자이므로 고유해야 합니다. Visual Studio에서 [도구] > [GUID 만들기]로 이동하여 GUID 만들기 도구를 열고 GUID를 생성할 수 있습니다.
6. `[InterfaceType]` 특성을 인터페이스에 추가하고 이 인터페이스에서 구현해야 하는 기본 COM 인터페이스를 지정합니다.
7. `IServer`를 구현하는 `Server`라는 클래스를 만듭니다.
8. 구현 중인 COM 클래스의 클래스 식별자 GUID를 사용하여 `[Guid("<CLSID>")]` 특성을 클래스에 추가합니다. 예: `[Guid("9f35b6f5-2c05-4e7f-93aa-ee087f6e7ab6")]`. 인터페이스 GUID와 마찬가지로 이 GUID는 이 COM용 인터페이스의 유일한 식별자이므로 고유해야 합니다.
9. 인터페이스 및 클래스에 모두 `[ComVisible(true)]` 특성을 추가합니다.

> [!IMPORTANT]
> .NET Framework와 달리 .NET Core에서는 COM을 통해 활성화하려는 클래스의 CLSID를 지정해야 합니다.

## <a name="generate-the-com-host"></a>COM 호스트 생성

1. `.csproj` 프로젝트 파일을 열고 `<PropertyGroup></PropertyGroup>` 태그 안에 `<EnableComHosting>true</EnableComHosting>`을 추가합니다.
2. 프로젝트를 빌드합니다.

결과 출력에는 `ProjectName.dll`, `ProjectName.deps.json`, `ProjectName.runtimeconfig.json` 및 `ProjectName.comhost.dll` 파일이 포함됩니다.

## <a name="register-the-com-host-for-com"></a>COM용 COM 호스트 등록

관리자 권한 명령 프롬프트를 열고 `regsvr32 ProjectName.comhost.dll`을 실행합니다. 이렇게 하면 공개된 모든 .NET 개체가 COM에 등록됩니다.

## <a name="enabling-regfree-com"></a>RegFree COM 사용

1. `.csproj` 프로젝트 파일을 열고 `<PropertyGroup></PropertyGroup>` 태그 안에 `<EnableRegFreeCom>true</EnableRegFreeCom>`을 추가합니다.
2. 프로젝트를 빌드합니다.

이제 결과 출력에는 `ProjectName.X.manifest` 파일도 포함됩니다. 이 파일은 레지스트리 없는 COM과 함께 사용할 병렬 매니페스트입니다.

## <a name="sample"></a>예제

GitHub의 dotnet/samples 리포지토리에는 완벽하게 작동하는 [COM 서버 샘플](https://github.com/dotnet/samples/tree/master/core/extensions/COMServerDemo)이 있습니다.

## <a name="additional-notes"></a>추가 참고 사항

.NET Framework와 달리 .NET Core에서는 .NET Core 어셈블리에서 COM 형식 라이브러리(TLB)를 생성하는 기능을 지원하지 않습니다. 인터페이스의 기본 선언을 위한 IDL 파일 또는 C++ 헤더를 수동으로 작성해야 합니다.

또한 .NET Framework와 .NET Core를 동일한 프로세스에 로드하는 기능은 지원되지 않으므로, .NET Core COM 서버를 .NET Framework COM 클라이언트 프로세스에 로드하거나 그 반대로 로드할 수는 없습니다.
