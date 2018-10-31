---
title: .NET Core를 사용하여 REST 클라이언트 만들기
description: 이 자습서에서는 .NET Core 및 C# 언어의 다양한 기능에 대해 설명합니다.
ms.date: 03/06/2017
ms.assetid: 51033ce2-7a53-4cdd-966d-9da15c8204d2
ms.openlocfilehash: 521c6edfa7163219ea86c6fb8444bc95859c9aa1
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50199918"
---
# <a name="rest-client"></a>REST 클라이언트

## <a name="introduction"></a>소개
이 자습서에서는 .NET Core 및 C# 언어의 다양한 기능에 대해 설명합니다. 다음을 배울 수 있습니다.
*   .NET Core CLI(명령줄 인터페이스)의 기본 사항
*   C# 언어 기능의 개요
*   NuGet으로 종속성 관리
*   HTTP 통신
*   JSON 정보 처리
*   특성을 사용하여 구성 관리 

GitHub에서 REST 서비스에 HTTP 요청을 실행하는 응용 프로그램을 빌드합니다. JSON 형식의 정보를 읽은 후 해당 JSON 패킷을 C# 개체로 변환합니다. 마지막으로 C# 개체를 사용하는 방법을 배웁니다.

이 자습서에는 많은 기능이 있습니다. 하나씩 빌드해 보겠습니다.

이 항목에 대한 [최종 샘플](https://github.com/dotnet/samples/tree/master/csharp/getting-started/console-webapiclient)을 따르려는 경우 해당 샘플을 다운로드할 수 있습니다. 다운로드 지침은 [샘플 및 자습서](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)를 참조하세요.

## <a name="prerequisites"></a>전제 조건
.NET Core를 실행하려면 컴퓨터에 설정해야 합니다. [.NET Core](https://www.microsoft.com/net/core) 페이지에서 설치 지침을 확인할 수 있습니다. Windows, Linux, macOS 또는 Docker 컨테이너에서 이 응용 프로그램을 실행할 수 있습니다. 선호하는 코드 편집기를 설치해야 합니다. 아래 설명에서는 오픈 소스 플랫폼 간 편집기인 [Visual Studio Code](https://code.visualstudio.com/)를 사용합니다. 그러나 익숙한 어떤 도구도 사용 가능합니다.
## <a name="create-the-application"></a>응용 프로그램 만들기
첫 번째 단계에서는 새 응용 프로그램을 만듭니다. 명령 프롬프트를 열고 응용 프로그램에 대한 새 디렉터리를 만듭니다. 해당 디렉터리를 현재 디렉터리로 지정합니다. 명령 프롬프트에 명령 `dotnet new console`을 입력합니다. 이렇게 하면 기본 "Hello World" 응용 프로그램에 대한 시작 파일이 만들어집니다.

파일 수정을 시작하기 전에 간단한 Hello World 응용 프로그램을 실행하는 단계를 진행해 보겠습니다. 응용 프로그램을 만든 후에 명령 프롬프트에서 `dotnet restore`([참고 참조](#dotnet-restore-note))를 입력합니다. 이 명령은 NuGet 패키지 복원 프로세스를 실행합니다. NuGet은 .NET 패키지 관리자입니다. 이 명령은 프로젝트에 대한 누락된 종속성 중 하나를 다운로드합니다. 이 프로젝트는 새 프로젝트이므로 어떤 종속성도 없습니다. 따라서 처음 실행하면 .NET Core 프레임워크가 다운로드됩니다. 이 초기 단계 후에 새 종속 패키지를 추가하거나 종속성 버전을 업데이트할 때 `dotnet restore`([참고 참조](#dotnet-restore-note))를 실행하기만 하면 됩니다.  

패키지를 복원한 후 `dotnet build`를 실행합니다. 이렇게 하면 빌드 엔진이 실행되고 응용 프로그램이 만들어집니다. 마지막으로 `dotnet run`을 실행하여 응용 프로그램을 실행합니다.

## <a name="adding-new-dependencies"></a>새 종속성 추가
.NET Core의 주요 디자인 목표 중 하나는 .NET 설치의 크기를 최소화하는 것입니다. 응용 프로그램에 일부 기능을 위해 추가 라이브러리가 필요한 경우 C# 프로젝트(\*.csproj) 파일에 해당 종속성을 추가합니다. 현재 예제에서는 응용 프로그램이 JSON 응답을 처리할 수 있도록 `System.Runtime.Serialization.Json` 패키지를 추가해야 합니다.

`csproj` 프로젝트 파일을 엽니다. 파일의 첫 번째 줄은 다음과 같습니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
```

이 줄 바로 뒤에 다음을 추가합니다. 

```xml
   <ItemGroup>
      <PackageReference Include="System.Runtime.Serialization.Json" Version="4.3.0" />
   </ItemGroup> 
```
대부분의 코드 편집기는 이러한 라이브러리의 완성된 다양한 버전을 제공합니다. 일반적으로 추가하는 모든 패키지의 최신 버전을 사용하려고 할 것입니다. 그러나 모든 패키지의 버전이 일치하는지와 .NET Core 응용 프로그램 프레임워크의 버전도 일치하는지 확인해야 합니다.

이러한 변경을 수행한 후에는 패키지가 시스템에 설치되도록 `dotnet restore`([참고 참조](#dotnet-restore-note))를 다시 실행해야 합니다.

## <a name="making-web-requests"></a>웹 요청 수행
이제 웹에서 데이터 검색을 시작할 준비가 되었습니다. 이 응용 프로그램에서는 [GitHub API](https://developer.github.com/v3/)에서 정보를 읽게 됩니다. [.NET Foundation](https://www.dotnetfoundation.org/) 상위 항목 아래에서 프로젝트에 대한 정보를 읽어 보겠습니다. 먼저 GitHub API에 대해 요청을 수행하여 프로젝트에 대한 정보를 검색합니다. 사용할 엔드포인트는 [https://api.github.com/orgs/dotnet/repos](https://api.github.com/orgs/dotnet/repos)입니다. 이러한 프로젝트에 대해 모든 정보를 검색하려고 하므로 HTTP GET 요청을 사용합니다.
브라우저도 HTTP GET 요청을 사용하므로 해당 URL을 브라우저에 붙여 넣어 수신되고 처리 중인 정보를 볼 수 있습니다.

<xref:System.Net.Http.HttpClient> 클래스를 사용하여 웹 요청을 수행합니다. 모든 최신 .NET API와 마찬가지로 <xref:System.Net.Http.HttpClient> 는 장기 실행되는 API에 대해 비동기 메서드만 지원합니다.
먼저 비동기 메서드를 만들어 보겠습니다. 응용 프로그램의 기능을 빌드할 때 구현을 채웁니다. 먼저 프로젝트 디렉터리에서 `program.cs` 파일을 열고 `Program` 클래스에 다음 메서드를 추가합니다.

```csharp
private static async Task ProcessRepositories()
{
    
}
```

C# 컴파일러에서 <xref:System.Threading.Tasks.Task> 형식을 인식하도록 `using` 문을 `Main` 메서드 맨 위에 추가해야 합니다.

```csharp
using System.Threading.Tasks;
```

이때 프로젝트를 빌드하면 이 메서드에는 `await` 연산자가 없어서 동기적으로 실행되므로 경고가 생성됩니다. 지금은 이 경고를 무시하세요. 메서드를 입력할 때 `await` 연산자를 추가할 것입니다.

다음에는 `namespace` 문에 정의된 네임스페이스의 이름을 기본값인 `ConsoleApp`에서 `WebAPIClient`로 바꿉니다. 나중에 이 네임스페이스에서 `repo` 클래스를 정의할 것입니다.

다음에는 `Main` 메서드를 업데이트하여 이 메서드를 호출합니다. `ProcessRepositories` 메서드는 작업을 반환합니다. 이 작업이 완료되기 전에 프로그램을 종료하지 않아야 합니다. 따라서 `Wait` 메서드를 사용하여 작업이 완료될 때까지 차단하고 기다려야 합니다.

```csharp
static void Main(string[] args)
{
    ProcessRepositories().Wait();
}
```

이제 아무 작업도 수행하지 않지만 비동기적으로는 수행하는 프로그램이 되었습니다. 이것을 개선해보겠습니다.

먼저 웹에서 데이터를 검색할 수 있는 개체가 필요합니다. 이를 위해 <xref:System.Net.Http.HttpClient>를 사용할 수 있습니다. 이 개체는 요청 및 응답을 처리합니다. Program.cs 파일 내의 `Program` 클래스에서 해당 형식의 단일 인스턴스를 인스턴스화합니다.

```csharp
namespace WebAPIClient
{
    class Program
    {
        private static readonly HttpClient client = new HttpClient();

        static void Main(string[] args)
        {
            //...
        }
    }
}
```

 다시 `ProcessRepositories` 메서드로 돌아가 첫 번째 버전을 채워 보겠습니다.

```csharp
private static async Task ProcessRepositories()
{
    client.DefaultRequestHeaders.Accept.Clear();
    client.DefaultRequestHeaders.Accept.Add(
        new MediaTypeWithQualityHeaderValue("application/vnd.github.v3+json"));
    client.DefaultRequestHeaders.Add("User-Agent", ".NET Foundation Repository Reporter");

    var stringTask = client.GetStringAsync("https://api.github.com/orgs/dotnet/repos");

    var msg = await stringTask;
    Console.Write(msg);
}
```

컴파일을 위해 파일 맨 위에 2개의 새 using 문을 추가해야 합니다.

```csharp
using System.Net.Http;
using System.Net.Http.Headers;
```

이 첫 번째 버전은 dotnet foundation 조직의 모든 리포지토리 목록을 읽으라는 웹 요청을 수행합니다. (.NET Foundation의 gitHub ID는 'dotnet'임) 첫 몇 줄은 이 요청에 대해 <xref:System.Net.Http.HttpClient>를 설정합니다. 먼저 GitHub JSON 응답을 수락하도록 구성됩니다.
이 형식은 단순히 JSON입니다. 다음 줄은 이 개체의 모든 요청에 사용자 에이전트 헤더를 추가합니다. 이러한 두 가지 헤더는 GitHub 서버 코드에서 확인되며 GitHub에서 정보를 검색하는 데 필요합니다.

<xref:System.Net.Http.HttpClient> 를 구성한 후에는 웹 요청을 수행하고 응답을 검색합니다. 이 첫 번째 버전에서는 <xref:System.Net.Http.HttpClient.GetStringAsync(System.String)?displayProperty=nameWithType> 편의 메서드를 사용합니다. 이 편의 메서드는 웹 요청을 수행하는 작업을 시작한 다음, 요청이 반환될 때 응답 스트림을 읽고 해당 스트림에서 콘텐츠를 추출합니다. 응답의 본문은 <xref:System.String> 으로 반환됩니다. 작업이 완료되면 이 문자열을 사용할 수 있습니다. 

이 메서드의 마지막 두 줄은 해당 작업을 대기하고 콘솔에 응답을 출력합니다.
앱을 빌드한 다음 실행합니다. `ProcessRepositories`에는 `await` 연산자가 포함되므로 이제 빌드 경고는 사라집니다. 길게 표시되는 JSON 형식 텍스트를 볼 수 있습니다.   

## <a name="processing-the-json-result"></a>JSON 결과 처리

지금까지 웹 서버에서 응답을 검색하고 해당 응답에 포함된 텍스트를 표시하는 코드를 작성했습니다. 다음에는 JSON 응답을 C# 개체로 변환해 보겠습니다.

JSON Serializer는 JSON 데이터를 C# 개체로 변환합니다. 가장 먼저 수행할 작업은 이 응답 중에서 사용하는 정보를 포함하는 C# 클래스 형식을 정의하는 것입니다. 리포지토리 이름을 포함하는 간단한 C# 형식 먼저 시작하여 천천히 빌드해 보겠습니다.

```csharp
using System;

namespace WebAPIClient
{
    public class repo
    {
        public string name;
    }
}
``` 

'repo.cs'라는 새 파일에 위 코드를 넣습니다. 이 버전의 클래스는 JSON 데이터를 처리하는 가장 간단한 경로를 나타냅니다. 클래스 이름 및 멤버 이름은 다음 C# 규칙 대신 JSON 패킷에 사용된 이름과 일치합니다. 나중에 몇 가지 구성 특성을 제공하여 수정할 것입니다. 이 클래스에서는 JSON serialization 및 deserialization의 또 다른 중요한 특징을 보여 줍니다. 즉, JSON 패킷의 모든 필드가 이 클래스에 속하는 것은 아닙니다.
JSON serializer는 사용되는 클래스 형식에 포함되지 않은 정보를 무시합니다.
이 특징 때문에 JSON 패킷의 필드 일부에만 작용하는 형식을 보다 쉽게 만들 수 있습니다.

이제 형식을 만들었으므로 deserialize를 수행해 보겠습니다. <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 개체를 만들어야 합니다. 이 개체는 검색하는 JSON 패킷에 필요한 CLR 형식을 알고 있어야 합니다. GitHub의 패킷에는 리포지토리 시퀀스가 포함되어 있으므로 `List<repo>`가 올바른 형식입니다. `ProcessRepositories` 메서드에 다음 줄을 추가합니다.

```csharp
var serializer = new DataContractJsonSerializer(typeof(List<repo>));
```

두 개의 새 네임스페이스를 사용하고 있으므로 해당 네임스페이스도 추가해야 합니다.

```csharp
using System.Collections.Generic;
using System.Runtime.Serialization.Json;
```

다음으로, serializer를 사용하여 JSON을 C# 개체로 변환합니다. `ProcessRepositories` 메서드의 <xref:System.Net.Http.HttpClient.GetStringAsync(System.String)> 호출을 다음 두 줄로 바꿉니다.

```csharp
var streamTask = client.GetStreamAsync("https://api.github.com/orgs/dotnet/repos");
var repositories = serializer.ReadObject(await streamTask) as List<repo>;
```

현재 <xref:System.Net.Http.HttpClient.GetStringAsync(System.String)> 대신 <xref:System.Net.Http.HttpClient.GetStreamAsync(System.String)>를 사용하고 있습니다. serializer는 해당 소스로 문자열 대신 스트림을 사용합니다. 위의 두 번째 줄에서 사용되는 C# 언어의 몇 가지 기능에 대해 설명해 보겠습니다. <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject(System.IO.Stream)>에 대한 인수는 `await` 식입니다. 지금까지는 대입문의 일부로만 볼 수 있었지만 Await 식은 코드의 거의 모든 위치에 나올 수 있습니다.

둘째로 `as` 연산자는 컴파일 타임 형식 `object`에서 `List<repo>`로 변환합니다. <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject(System.IO.Stream)> 선언은 <xref:System.Object?displayProperty=nameWithType> 형식의 개체로 반환됨을 선언합니다. <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject(System.IO.Stream)>는 사용자가 생성 시에 지정한 형식을 반환합니다(이 자습서에서는 `List<repo>`). 변환이 성공하지 못하면 `as` 연산자는 예외를 throw하는 대신 `null`을 계산합니다.

이 섹션이 거의 완료되었습니다. JSON을 C# 개체로 변환했으므로 각 리포지토리의 이름을 표시해 보겠습니다. 다음 줄을

```csharp
var msg = await stringTask;   //**Deleted this
Console.Write(msg);
```

다음으로 바꿉니다.

```csharp
foreach (var repo in repositories)
    Console.WriteLine(repo.name);
```

응용 프로그램을 컴파일하고 실행합니다. .NET Foundation에 포함된 리포지토리의 이름이 출력됩니다.

## <a name="controlling-serialization"></a>serialization 제어

더 많은 기능을 추가하기 전에 `repo` 형식의 주소를 지정하고 더 많은 표준 C# 규칙을 따르도록 합니다. 이 작업을 위해 JSON Serializer가 작동하는 방식을 제어하는 *특성*을 `repo` 형식에 주석으로 지정합니다. 여기서는 이러한 특성을 사용하여 JSON 키 이름과 C# 클래스 및 멤버 이름 간에 매핑을 정의합니다. 사용되는 2가지 특성은 `DataContract` 특성 및 `DataMember` 특성입니다. 규칙에 따라 모든 Attribute 클래스는 접미사 `Attribute`로 끝납니다. 그러나 특성을 적용할 때 해당 접미사를 사용할 필요는 없습니다. 

`DataContract` 및 `DataMember` 특성은 다른 라이브러리에 포함되므로 해당 라이브러리를 C# 프로젝트 파일에 종속성으로 추가해야 합니다. 다음 줄을 프로젝트 파일의 `<ItemGroup>` 섹션에 추가합니다.

```xml
<PackageReference Include="System.Runtime.Serialization.Primitives" Version="4.3.0" />
```

파일을 저장한 후 `dotnet restore`([참고 참조](#dotnet-restore-note))를 실행하여 이 패키지를 검색합니다.

다음으로 `repo.cs` 파일을 엽니다. 이름을 파스칼식 대/소문자를 사용하도록 이름을 변경하고 `Repository`라고 정확히 입력합니다. 여전히 JSON 'repo' 노드를 이 형식에 매핑하려고 하므로 `DataContract` 특성을 클래스 선언에 추가해야 합니다. 이 특성의 `Name` 속성을 이 형식에 매핑되는 JSON 노드의 이름으로 설정합니다.

```csharp
[DataContract(Name="repo")]
public class Repository
```

<xref:System.Runtime.Serialization.DataContractAttribute> 는  <xref:System.Runtime.Serialization> 네임스페이스의 멤버이므로 파일 맨 위에 해당 `using` 문을 추가해야 합니다.

```csharp
using System.Runtime.Serialization;
```

`repo` 클래스의 이름을 `Repository`로 변경했으므로 Program.cs에서도 동일하게 이름을 변경해야 합니다(일부 편집기에서 이러한 변경을 자동으로 수행하는 이름 바꾸기 리팩터링이 지원될 수 있음).

```csharp
var serializer = new DataContractJsonSerializer(typeof(List<Repository>));

// ...

var repositories = serializer.ReadObject(await streamTask) as List<Repository>;
```

다음으로 <xref:System.Runtime.Serialization.DataMemberAttribute> 클래스를 사용하여 `name` 필드를 동일하게 변경해 보겠습니다. repo.cs에서 `name` 필드의 선언을 다음과 같이 변경합니다.

```csharp
[DataMember(Name="name")]
public string Name;
```

이렇게 변경할 경우 program.cs에서 각 리포지토리의 이름을 쓰는 코드를 변경해야 합니다.

```csharp
Console.WriteLine(repo.Name);
```

`dotnet build` 다음에 `dotnet run`을 수행하여 매핑이 올바르게 수행되었는지 확인합니다. 이전과 동일한 출력이 표시되어야 합니다. 웹 서버의 더 많은 속성을 처리하기 전에 `Repository` 클래스를 한 가지 더 변경해 보겠습니다. `Name` 멤버는 공개적으로 액세스할 수 있는 필드입니다. 그렇지만 적절한 개체 지향 방식은 아니므로 속성으로 변경해 보겠습니다. 이 예제에서는 속성을 가져오거나 설정할 때 특정 코드를 실행할 필요가 없으며 속성을 변경하여 `Repository` 클래스를 사용하는 코드를 중단하지 않고도 나중에 해당 변경 내용을 보다 쉽게 추가할 수 있습니다.

필드 정의를 제거한 후 [자동 구현 속성](../programming-guide/classes-and-structs/auto-implemented-properties.md)으로 바꿉니다.

```csharp
public string Name { get; set; }
```

컴파일러는 `get` 및 `set` 접근자의 본문 뿐만 아니라 이름을 저장하는 private 필드도 생성합니다. 이 작업은 다음 코드를 직접 입력하는 것과 비슷합니다.

```csharp
public string Name 
{ 
    get { return this._name; }
    set { this._name = value; }
}
private string _name;
```

새로운 기능을 추가하기 전에 한 가지 더 변경해 보겠습니다. `ProcessRepositories` 메서드는 비동기 작업을 수행하고 리포지토리 컬렉션을 반환할 수 있습니다. 이 메서드에서 `List<Repository>`로 돌아가 정보를 쓰는 코드를 `Main` 메서드로 이동해 보겠습니다.

`ProcessRepositories`의 시그니처를 변경하여 `Repository` 개체의 목록을 해당 결과로 표시하는 작업을 반환합니다.

```csharp
private static async Task<List<Repository>> ProcessRepositories()
```

다음에는 JSON 응답을 처리한 후 리포지토리를 반환합니다.

```csharp
var repositories = serializer.ReadObject(await streamTask) as List<Repository>;
return repositories;
```

이 개체를 `async`로 표시했으므로 컴파일러는 해당 반환에 대한 `Task<T>` 개체를 생성합니다.
그런 다음 해당 결과를 캡처하고 각 리포지토리 이름을 콘솔에 쓰도록 `Main` 메서드를 수정해 보겠습니다. `Main` 메서드는 이제 다음과 같이 표시됩니다.

```csharp
public static void Main(string[] args)
{
    var repositories = ProcessRepositories().Result;

    foreach (var repo in repositories)
        Console.WriteLine(repo.Name);
}
```

작업이 완료될 때까지 Task의 `Result` 속성에 대한 액세스가 차단됩니다. 일반적으로 `ProcessRepositories` 메서드에서와 같이 작업의 컴파일을 `await`하는 것을 선호하겠지만 `Main` 메서드에서는 허용되지 않습니다.

## <a name="reading-more-information"></a>추가 정보 읽기

GitHub API에서 전송되는 JSON 패킷에 있는 속성을 몇 가지 더 처리하는 것으로 마무리해 보겠습니다. 모든 기능을 알 수는 없겠지만 일부 속성을 추가하면 C# 언어의 몇 가지 기능이 추가로 확인됩니다.

먼저 `Repository` 클래스 정의에 몇 가지 간단한 형식을 더 추가해 보겠습니다. 해당 클래스에 다음 속성을 추가합니다.

```csharp
[DataMember(Name="description")]
public string Description { get; set; }

[DataMember(Name="html_url")]
public Uri GitHubHomeUrl { get; set; }

[DataMember(Name="homepage")]
public Uri Homepage { get; set; }

[DataMember(Name="watchers")]
public int Watchers { get; set; }
```

이러한 속성은 기본적으로 문자열 형식(JSON 패킷에 포함된 형식)을 대상 형식으로 변환합니다. <xref:System.Uri> 형식은 생소할 수 있습니다. 이 형식은 URI 또는 이 경우에는 URL을 나타냅니다. `Uri` 및 `int` 형식의 경우 JSON 패킷에 대상 형식으로 변환되지 않는 데이터가 포함되어 있으면 serialization 작업은 예외를 throw합니다.

이러한 데이터를 추가한 경우에는 해당 요소를 표시하도록 `Main` 메서드를 업데이트합니다.

```csharp
foreach (var repo in repositories)
{
    Console.WriteLine(repo.Name);
    Console.WriteLine(repo.Description);
    Console.WriteLine(repo.GitHubHomeUrl);
    Console.WriteLine(repo.Homepage);
    Console.WriteLine(repo.Watchers);
    Console.WriteLine();
}
```
마지막 단계로, 최종 밀어넣기 작업을 위한 정보를 추가해 보겠습니다. 이 정보는 JSON 응답에서 다음 방식으로 형식이 지정됩니다.

```json
2016-02-08T21:27:00Z
```

해당 형식은 표준 .NET <xref:System.DateTime> 형식을 따르지 않습니다. 따라서 사용자 지정 변환 메서드를 작성해야 합니다. 또한 `Repository` 클래스 사용자에게 원시 문자열이 노출되는 것을 원하지 않을 것입니다. 특성도 이러한 작업을 제어하는 데 도움이 될 수 있습니다. 먼저 `Repository` 클래스에서 날짜/시간에 대한 문자열 표현을 포함할 `private` 속성을 정의합니다.

```csharp
[DataMember(Name="pushed_at")]
private string JsonDate { get; set; }
```

`DataMember` 특성은 공용 멤버가 아니어도 처리되어야 함을 serializer에 알려줍니다. 다음에는 문자열을 유효한 <xref:System.DateTime> 개체로 변환한 후 해당 <xref:System.DateTime>을 반환하는 공용 읽기 전용 속성을 작성해야 합니다.

```csharp
[IgnoreDataMember]
public DateTime LastPush
{
    get
    {
        return DateTime.ParseExact(JsonDate, "yyyy-MM-ddTHH:mm:ssZ", CultureInfo.InvariantCulture);
    }
}
```

위의 새 구문을 살펴 보겠습니다. `IgnoreDataMember` 특성은 이 형식을 임의 JSON 개체에 쓰거나 이 개체에서 읽지 않아야 함을 serializer에 알려줍니다. 이 속성은 `get` 접근자만 포함합니다. `set` 접근자가 없습니다. 바로 C#에서 *읽기 전용* 속성을 정의하는 방식입니다. (C#에서 *쓰기 전용* 속성을 만들 수 있지만 해당 값은 제한됩니다.) <xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)> 메서드는 제공된 날짜 형식을 사용하여 문자열을 구문 분석하고 <xref:System.DateTime> 개체를 만들고, `CultureInfo` 개체를 사용하여 `DateTime`에 메타데이터를 더 추가합니다. 구문 분석 작업이 실패하는 경우 속성 접근자가 예외를 throw합니다.

<xref:System.Globalization.CultureInfo.InvariantCulture> 를 사용하려면 `repo.cs`의 `using` 문에 <xref:System.Globalization> 네임스페이스를 추가해야 합니다.

```csharp
using System.Globalization;
```

마지막으로 콘솔에 output 문을 하나 더 추가하면 이 앱을 빌드하고 다시 실행할 준비가 됩니다.

```csharp
Console.WriteLine(repo.LastPush);
```

이제 해당 버전이 [완성된 샘플](https://github.com/dotnet/samples/tree/master/csharp/getting-started/console-webapiclient)과 일치해야 합니다.
 
## <a name="conclusion"></a>결론

이 자습서에서는 웹 요청을 수행하고, 결과를 구문 분석하고, 해당 결과의 속성을 표시하는 방법을 알아보았습니다. 또한 프로젝트에 종속성으로 새 패키지를 추가했습니다. 개체 지향 기술을 지원하는 C# 언어의 일부 기능을 확인했습니다.

<a name="dotnet-restore-note"></a>
[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]
