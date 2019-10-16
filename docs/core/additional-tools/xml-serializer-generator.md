---
title: Microsoft XML Serializer Generator
description: Microsoft XML Serializer Generator에 대한 개요입니다. XML Serializer Generator를 사용하여 프로젝트에 포함된 형식에 대한 XML serialization 어셈블리를 생성합니다.
author: mlacouture
ms.date: 01/19/2017
ms.topic: tutorial
ms.custom: mvc, seodec18
ms.openlocfilehash: 4a9c24455136fe4ccd13379d05c16d6b7cbf85de
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117018"
---
# <a name="using-microsoft-xml-serializer-generator-on-net-core"></a>.NET Core에서 Microsoft XML Serializer Generator 사용

이 자습서에서는 C# .NET Core 애플리케이션에서 Microsoft XML Serializer Generator를 사용하는 방법을 배웁니다. 이 자습서를 진행하면서 다음을 익히게 됩니다.

> [!div class="checklist"]
>
> * .NET Core 앱을 만드는 방법
> * Microsoft.XmlSerializer.Generator 패키지에 대한 참조를 추가하는 방법
> * MyApp.csproj를 편집하여 종속성을 추가하는 방법
> * 클래스 및 XmlSerializer를 추가하는 방법
> * 애플리케이션을 빌드하고 실행하는 방법

.NET Framework용 [Xml Serializer Generator(sgen.exe)](../../standard/serialization/xml-serializer-generator-tool-sgen-exe.md)와 마찬가지로, [Microsoft.XmlSerializer.Generator NuGet 패키지](https://www.nuget.org/packages/Microsoft.XmlSerializer.Generator)는 .NET Core 및 .NET Standard 프로젝트와 동일합니다. <xref:System.Xml.Serialization.XmlSerializer>를 사용하여 해당 형식의 개체를 직렬화하거나 역직렬화할 때 XML serialization의 시작 성능을 향상시키기 위해 어셈블리에 포함된 형식의 XML serialization 어셈블리를 만듭니다.

## <a name="prerequisites"></a>전제 조건

이 자습서를 완료하려면 다음이 필요합니다.

* [.NET Core 2.1 SDK](https://dotnet.microsoft.com/download) 이상
* 선호하는 코드 편집기

> [!TIP]
> 코드 편집기를 설치해야 하나요? [Visual Studio](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)를 체험해 보세요.

## <a name="use-microsoft-xml-serializer-generator-in-a-net-core-console-application"></a>.NET Core 콘솔 애플리케이션에서 Microsoft XML Serializer Generator 사용

다음 지침은 .NET Core 콘솔 애플리케이션에서 Microsoft XML Serializer Generator를 사용하는 방법을 보여 줍니다.

### <a name="create-a-net-core-console-application"></a>.NET Core 콘솔 애플리케이션 만들기

명령 프롬프트를 열고 *MyApp*이라는 폴더를 만듭니다. 만든 폴더로 이동하고 다음 명령을 입력합니다.

```dotnetcli
dotnet new console
```

### <a name="add-a-reference-to-the-microsoftxmlserializergenerator-package-in-the-myapp-project"></a>MyApp 프로젝트에서 Microsoft.XmlSerializer.Generator 패키지에 대한 참조 추가

[`dotnet add package`](../tools//dotnet-add-package.md) 명령을 사용하여 프로젝트에 참조를 추가합니다.

유형:

```dotnetcli
dotnet add package Microsoft.XmlSerializer.Generator -v 1.0.0
```

### <a name="verify-changes-to-myappcsproj-after-adding-the-package"></a>패키지를 추가한 후 MyApp.csproj 변경 사항 확인

코드 편집기를 열고 시작해 보겠습니다! 앱을 빌드한 *MyApp* 디렉터리에서 계속 작업 중입니다.

텍스트 편집기에서 *MyApp.csproj*를 엽니다.

[`dotnet add package`](../tools//dotnet-add-package.md) 명령을 실행하면 다음 줄이 *MyApp.csproj* 프로젝트 파일에 추가됩니다.

 ```xml
 <ItemGroup>
    <PackageReference Include="Microsoft.XmlSerializer.Generator" Version="1.0.0" />
 </ItemGroup>
 ```

### <a name="add-another-itemgroup-section-for-net-core-cli-tool-support"></a>.NET Core CLI 도구 지원을 위해 다른 ItemGroup 섹션 추가

검사한 `ItemGroup` 섹션 뒤에 다음 줄을 추가합니다.

 ```xml
 <ItemGroup>
    <DotNetCliToolReference Include="Microsoft.XmlSerializer.Generator" Version="1.0.0" />
 </ItemGroup>
 ```

### <a name="add-a-class-in-the-application"></a>애플리케이션에서 클래스 추가

텍스트 편집기에서 *Program.cs*를 엽니다. *Program.cs*에서 *MyClass*라는 클래스를 추가합니다.

```csharp
public class MyClass
{
   public int Value;
}
```

### <a name="create-an-xmlserializer-for-myclass"></a>MyClass에 대한 `XmlSerializer` 만들기

*Main* 내에 다음 줄을 추가하여 MyClass에 대해 `XmlSerializer`를 만듭니다.

```csharp
var serializer = new System.Xml.Serialization.XmlSerializer(typeof(MyClass));
```

### <a name="build-and-run-the-application"></a>애플리케이션 빌드 및 실행

*MyApp* 폴더 내에서 [`dotnet run`](../tools/dotnet-run.md)을(를) 통해 애플리케이션을 실행하면 런타임에 미리 생성된 serializer가 자동으로 로드되어 사용됩니다.

콘솔 창에 다음 명령을 입력합니다.

```dotnetcli
dotnet run
```

> [!NOTE]
> [`dotnet run`](../tools/dotnet-run.md)은 [`dotnet build`](../tools/dotnet-build.md)를 호출하여 빌드 대상이 빌드되었는지를 확인하고 `dotnet <assembly.dll>`을 호출하여 대상 애플리케이션을 실행합니다.

> [!IMPORTANT]
> 이 자습서에 나와 있는 애플리케이션 실행을 위한 명령과 단계는 개발하는 동안에만 사용됩니다. 앱을 배포할 준비가 되면 .NET Core 앱에 대한 여러 [배포 전략](../deploying/index.md) 및 [`dotnet publish`](../tools/dotnet-publish.md) 명령을 살펴보세요.

모든 항목이 성공하면 *MyApp.XmlSerializers.dll*이라는 어셈블리가 출력 폴더에 생성됩니다.

지금까지 다음 작업을 수행했습니다.
> [!div class="checklist"]
>
> * .NET Core 앱을 생성했습니다.
> * Microsoft.XmlSerializer.Generator 패키지에 대한 참조를 추가했습니다.
> * MyApp.csproj를 편집하여 종속성을 추가했습니다.
> * 클래스 및 XmlSerializer를 추가했습니다.
> * 애플리케이션을 빌드하고 실행했습니다.

## <a name="related-resources"></a>관련 참고 자료

* [XML serialization 소개](../../standard/serialization/introducing-xml-serialization.md)
* [방법: XmlSerializer를 사용하여 serialize(C#)](../../csharp/programming-guide/concepts/linq/how-to-serialize-using-xmlserializer.md)
* [방법: XmlSerializer를 사용하여 serialize(Visual Basic)](../../visual-basic/programming-guide/concepts/linq/how-to-serialize-using-xmlserializer.md)
