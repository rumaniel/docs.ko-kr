---
title: Docker를 사용하여 앱 컨테이너화 자습서
description: 이 자습서에서는 Docker를 사용하여 .NET Core 애플리케이션을 컨테이너화하는 방법을 알아봅니다.
ms.date: 06/26/2019
ms.topic: tutorial
ms.custom: mvc, seodec18
ms.openlocfilehash: 5e05fd2a38770ce348fbbfcfaa88267217b806bf
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71116554"
---
# <a name="tutorial-containerize-a-net-core-app"></a>자습서: .NET Core 앱 컨테이너화

이 자습서에서는 .NET Core 애플리케이션을 포함하는 Docker 이미지를 빌드하는 방법에 대해 설명합니다. 이미지를 사용하여 로컬 개발 환경이나 프라이빗 클라우드 또는 퍼블릭 클라우드용 컨테이너를 생성할 수 있습니다.

다음을 배울 수 있습니다.

> [!div class="checklist"]
>
> * 간단한 .NET Core 앱 만들기 및 게시
> * .NET Core용 Dockerfile 만들기 및 구성
> * Docker 이미지 빌드
> * Docker 컨테이너 만들기 및 실행

.NET Core 애플리케이션용 Docker 컨테이너 빌드 및 배포 작업을 알아봅니다. Docker 플랫폼은 Docker 엔진을 사용하여 Docker 이미지로 앱을 신속하게 빌드하고 패키지합니다.    이 이미지는 계층화된 컨테이너에서 배포되고 실행되도록 *Dockerfile* 형식으로 작성됩니다.

## <a name="prerequisites"></a>전제 조건

다음 필수 구성 요소를 설치합니다.

* [.NET Core 2.2 SDK](https://dotnet.microsoft.com/download)\
.NET Core가 설치되어 있는 경우 `dotnet --info` 명령을 사용하여 사용 중인 SDK를 확인합니다.

* [Docker Community Edition](https://www.docker.com/products/docker-desktop)

* *Dockerfile* 및 .NET Core 예제 앱의 임시 작업 폴더입니다. 이 자습서에서는 이름 `docker-working`이 작업 폴더로 사용됩니다.

### <a name="use-sdk-version-22"></a>SDK 버전 2.2 사용

3\.0 같은 최신 SDK를 사용하는 경우 앱에서 2.2 SDK를 사용해야 하는지 확인합니다. 작업 폴더에 `global.json`이라는 파일을 만들고 다음 json 코드를 붙여넣습니다.

```json
{
  "sdk": {
    "version": "2.2.100"
  }
}
```

이 파일을 저장합니다. 파일이 존재하면 .NET Core에서는 이 폴더 및 아래에서 호출된 모든 `dotnet` 명령에 버전 2.2를 사용해야 합니다.

## <a name="create-net-core-app"></a>.NET Core 앱 만들기

Docker 컨테이너가 실행되는 .NET Core 앱이 필요합니다. 아직 없는 경우, 터미널을 열고 작업 폴더를 만든 후 입력합니다. 작업 폴더에서 다음 명령을 실행하여 app이라는 하위 디렉터리에서 새 프로젝트를 만듭니다.

```dotnetcli
dotnet new console -o app -n myapp
```

폴더 트리는 다음과 같이 나타납니다.

```
docker-working
│   global.json
│
└───app
    │   myapp.csproj
    │   Program.cs
    │
    └───obj
            myapp.csproj.nuget.cache
            myapp.csproj.nuget.g.props
            myapp.csproj.nuget.g.targets
            project.assets.json
```

`dotnet new` 명령은 *app*이라는 새 폴더를 만들고 “Hello World” 앱을 생성합니다. *app* 폴더를 입력하고 `dotnet run` 명령을 실행합니다. 다음 출력이 표시됩니다.

```console
> dotnet run
Hello World!
```

기본 템플릿은 터미널에 인쇄한 후 종료되는 앱을 만듭니다. 이 자습서에서는 무한 반복되는 앱을 사용합니다. 텍스트 편집기에서 **Program.cs** 파일을 엽니다. 현재는 다음 코드와 같이 표시됩니다.

```csharp
using System;

namespace myapp
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

1초마다 숫자를 계산하는 다음 코드로 파일을 바꿉니다.

```csharp
using System;

namespace myapp
{
    class Program
    {
        static void Main(string[] args)
        {
            var counter = 0;
            var max = args.Length != 0 ? Convert.ToInt32(args[0]) : -1;
            while(max == -1 || counter < max)
            {
                counter++;
                Console.WriteLine($"Counter: {counter}");
                System.Threading.Tasks.Task.Delay(1000).Wait();
            }
        }
    }
}
```

파일을 저장하고 `dotnet run`을 사용하여 프로그램을 다시 테스트합니다. 이 앱은 무한 실행된다는 점을 명심하세요. 취소 명령 <kbd>CTRL+C</kbd>를 사용하여 앱을 중지합니다. 다음 출력이 표시됩니다.

```console
> dotnet run
Counter: 1
Counter: 2
Counter: 3
Counter: 4
^C
```

명령줄의 숫자를 앱에 전달하면 해당 양까지만 계산되고 종료됩니다. 앱에서 `dotnet run -- 5`를 사용하여 5까지 계산해 보세요.

> [!NOTE]
> `--` 이후 매개 변수는 `dotnet run` 명령에 전달되지 않고 대신 애플리케이션에 전달됩니다.

## <a name="publish-net-core-app"></a>.NET Core 앱 게시

Docker 이미지에 .NET Core 앱을 추가하기 전에 해당 앱을 게시합니다. 앱이 시작될 때 컨테이너가 게시된 버전의 앱을 실행하는지 확인하려고 합니다.

작업 폴더에서 예제 소스 코드가 있는 **app** 폴더를 입력하고 다음 명령을 실행합니다.

```dotnetcli
dotnet publish -c Release
```

이 명령은 앱을 **publish** 폴더로 컴파일합니다. 작업 폴더에서 **publish** 폴더의 경로는 `.\app\bin\Release\netcoreapp2.2\publish\`이어야 합니다.

publish 폴더의 디렉터리 목록을 가져오고 **myapp.dll**이 생성되었는지 확인합니다. **app** 폴더에서 다음 명령 중 하나를 실행합니다.

```console
> dir bin\Release\netcoreapp2.2\publish
 Directory of C:\docker-working\app\bin\Release\netcoreapp2.2\publish

04/05/2019  11:00 AM    <DIR>          .
04/05/2019  11:00 AM    <DIR>          ..
04/05/2019  11:00 AM               447 myapp.deps.json
04/05/2019  11:00 AM             4,608 myapp.dll
04/05/2019  11:00 AM               448 myapp.pdb
04/05/2019  11:00 AM               154 myapp.runtimeconfig.json
```

```bash
me@DESKTOP:/docker-working/app$ ls bin/Release/netcoreapp2.2/publish
myapp.deps.json  myapp.dll  myapp.pdb  myapp.runtimeconfig.json
```

## <a name="create-the-dockerfile"></a>Dockerfile 만들기

*Dockerfile* 파일은 `docker build` 명령에서 컨테이너 이미지를 만드는 데 사용됩니다. 이 파일은 확장명이 없는 *Dockerfile*이라는 일반 텍스트 파일입니다.

터미널에서 시작 시에 생성한 작업 폴더로 디렉터리를 위쪽으로 이동합니다. 작업 폴더에 *Dockerfile*이라는 파일을 만들고 텍스트 편집기에서 엽니다. 다음 명령을 파일의 첫 줄로 추가합니다.

```dockerfile
FROM mcr.microsoft.com/dotnet/core/runtime:2.2
```

`FROM` 명령은 **mcr.microsoft.com/dotnet/core/runtime** 리포지토리에서 **2.2** 태그가 지정된 이미지를 풀하도록 Docker에 지시합니다. SDK에서 대상으로 지정된 런타임과 일치하는 .NET Core 런타임을 풀해야 합니다. 예를 들어 이전 섹션에서 만든 앱은 .NET Core 2.2 SDK를 사용하고 .NET Core 2.2를 대상으로 하는 앱을 만들었습니다. 따라서 *Dockerfile*에서 참조되는 기본 이미지에는 **2.2** 태그가 지정됩니다.

*Dockerfile* 파일을 저장합니다. 작업 폴더의 디렉터리 구조는 다음과 같이 표시됩니다. 문서에서 공간을 절약하기 위해 더 깊은 수준의 파일과 폴더의 일부가 잘렸습니다.

```
docker-working
│   Dockerfile
│   global.json
│
└───app
    │   myapp.csproj
    │   Program.cs
    │
    ├───bin
    │   └───Release
    │       └───netcoreapp2.2
    │           └───publish
    │                   myapp.deps.json
    │                   myapp.dll
    │                   myapp.pdb
    │                   myapp.runtimeconfig.json
    │
    └───obj
```

터미널에서 다음 명령을 실행합니다.

```console
docker build -t myimage -f Dockerfile .
```

Docker가 *Dockerfile*에서 각 줄을 처리합니다. `docker build` 명령의 `.`는 *Dockerfile*을 찾는 데 현재 폴더를 사용하도록 Docker에 지시합니다. 이 명령은 이미지를 빌드하고 해당 이미지를 가리키는 **myimage**라는 로컬 리포지토리를 만듭니다. 이 명령이 완료된 후 `docker images`를 실행하여 설치된 이미지 목록을 확인합니다.

```console
> docker images
REPOSITORY                              TAG                 IMAGE ID            CREATED             SIZE
mcr.microsoft.com/dotnet/core/runtime   2.2                 d51bb4452469        2 days ago          314MB
myimage                                 latest              d51bb4452469        2 days ago          314MB
```

두 이미지가 동일한 **IMAGE ID** 값을 공유함을 알 수 있습니다. *Dockerfile*의 유일한 명령은 기존 이미지를 기반으로 새 이미지를 만드는 것이므로 두 이미지에서 해당 값이 동일합니다. *Dockerfile*에 두 개의 명령을 추가하겠습니다. 각 명령은 **myimage** 리포지토리가 가리키는 이미지를 나타내는 마지막 명령으로 새 이미지 계층을 만듭니다.

```dockerfile
COPY app/bin/Release/netcoreapp2.2/publish/ app/

ENTRYPOINT ["dotnet", "app/myapp.dll"]
```

`COPY` 명령은 컴퓨터의 지정된 폴더를 컨테이너의 폴더에 복사하도록 Docker에 지시합니다. 이 예제에서 **publish** 폴더는 컨테이너의 **app** 폴더에 복사됩니다.

다음 명령인 `ENTRYPOINT`는 컨테이너가 실행 파일로 실행되게 컨테이너를 구성하도록 Docker에 지시합니다. 컨테이너가 시작되면 `ENTRYPOINT` 명령이 실행됩니다. 이 명령이 종료되면 컨테이너가 자동으로 중지됩니다.

터미널에서 `docker build -t myimage -f Dockerfile .`를 실행하고 명령이 완료되면 `docker images`를 실행합니다.

```console
> docker build -t myimage -f Dockerfile .
Sending build context to Docker daemon  819.7kB
Step 1/3 : FROM mcr.microsoft.com/dotnet/core/runtime:2.2
 ---> d51bb4452469
Step 2/3 : COPY app/bin/Release/netcoreapp2.2/publish/ app/
 ---> a1e98ac62017
Step 3/3 : ENTRYPOINT ["dotnet", "app/myapp.dll"]
 ---> Running in f34da5c18e7c
Removing intermediate container f34da5c18e7c
 ---> ddcc6646461b
Successfully built ddcc6646461b
Successfully tagged myimage:latest

> docker images
REPOSITORY                              TAG                 IMAGE ID            CREATED             SIZE
myimage                                 latest              ddcc6646461b        10 seconds ago      314MB
mcr.microsoft.com/dotnet/core/runtime   2.2                 d51bb4452469        2 days ago          314MB
```

*Dockerfile*의 각 명령이 계층을 생성하고 **IMAGE ID**를 만들었습니다. 마지막 **IMAGE ID**(사용자에 따라 다름)는 **ddcc6646461b**이고 다음에 이 이미지를 기반으로 컨테이너를 만듭니다.

## <a name="create-a-container"></a>컨테이너 만들기

이제 앱을 포함하는 이미지가 있으므로 컨테이너를 만들 수 있습니다. 두 가지 방법으로 컨테이너를 만들 수 있습니다. 먼저 중지된 새 컨테이너를 만듭니다.

```console
> docker create myimage
0e8f3c2ca32ce773712a5cca38750f41259a4e54e04bdf0946087e230ad7066c
```

위에서 `docker create` 명령은 **myimage** 이미지를 기반으로 컨테이너를 만듭니다. 해당 명령의 출력은 생성된 컨테이너의 **CONTAINER ID**(사용자에 따라 다름)를 표시합니다. 모든 컨테이너 목록을 보려면 `docker ps -a` 명령을 사용합니다. 

```console
> docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS        PORTS   NAMES
0e8f3c2ca32c        myimage             "dotnet app/myapp.dll"   4 seconds ago       Created               boring_matsumoto
```

### <a name="manage-the-container"></a>컨테이너 관리

각 컨테이너에는 해당 컨테이너 인스턴스를 참조하는 데 사용할 수 있는 임의 이름이 할당됩니다. 예를 들어 자동으로 생성된 컨테이너에 **boring_matsumoto**(사용자에 따라 다름) 이름이 선택되면 해당 이름을 사용하여 컨테이너를 시작할 수 있습니다. `docker create --name` 매개 변수를 사용하여 특정 이름으로 자동 이름을 재정의합니다.

다음 예제에서는 `docker start` 명령을 사용하여 컨테이너를 시작한 후 `docker ps` 명령을 사용하여 실행 중인 컨테이너만 표시합니다.

```console
> docker start boring_matsumoto
boring_matsumoto

> docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS         PORTS   NAMES
0e8f3c2ca32c        myimage             "dotnet app/myapp.dll"   7 minutes ago       Up 8 seconds           boring_matsumoto
```

마찬가지로 `docker stop` 명령은 컨테이너를 중지합니다. 다음 예제에서는 `docker stop` 명령을 사용하여 컨테이너를 중지한 후 `docker ps` 명령을 사용하여 컨테이너가 실행 중이지 않음을 보여 줍니다.

```console
> docker stop boring_matsumoto
boring_matsumoto

> docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS     PORTS   NAMES
```

### <a name="connect-to-a-container"></a>컨테이너에 연결

컨테이너가 실행된 후 컨테이너에 연결하여 출력을 볼 수 있습니다. `docker start` 및 `docker attach` 명령을 사용하여 컨테이너를 시작하고 출력 스트림을 피킹합니다. 이 예제에서는 <kbd>CTRL+C</kbd> 명령을 사용하여 실행 중인 컨테이너에서 분리합니다. 이렇게 하면 실제로 컨테이너에서 프로세스가 종료되어 컨테이너가 중지될 수 있습니다. `--sig-proxy=false` 매개 변수는 <kbd>CTRL + C</kbd>가 컨테이너에서 프로세스를 중지하지 않도록 합니다.

컨테이너에서 분리한 후 다시 연결하여 계속 실행 및 계산 중인지 확인합니다.

```console
> docker start boring_matsumoto
boring_matsumoto

> docker attach --sig-proxy=false boring_matsumoto
Counter: 7
Counter: 8
Counter: 9
^C

> docker attach --sig-proxy=false boring_matsumoto
Counter: 17
Counter: 18
Counter: 19
^C
```

### <a name="delete-a-container"></a>컨테이너 삭제

이 문서의 목적이 아무 작업도 수행하지 않는 컨테이너를 만드는 것은 아닙니다. 이전에 만든 컨테이너를 삭제합니다. 컨테이너가 실행 중이면 중지합니다.

```console
> docker stop boring_matsumoto
```

다음 예제에는 모든 컨테이너가 나와 있습니다. `docker rm` 명령을 사용하여 컨테이너를 삭제한 후 실행 중인 컨테이너가 있는지 다시 확인합니다.

```console
> docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS     PORTS   NAMES
0e8f3c2ca32c        myimage             "dotnet app/myapp.dll"   19 minutes ago      Exited             boring_matsumoto

> docker rm boring_matsumoto
boring_matsumoto

> docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS     PORTS    NAMES
```

### <a name="single-run"></a>단일 실행

Docker는 단일 명령으로 컨테이너를 만들고 실행할 수 있는 `docker run` 명령을 제공합니다. 이 명령을 사용하면 `docker create`를 실행한 후 `docker start`를 실행할 필요가 없습니다. 컨테이너가 중지될 때 컨테이너를 자동으로 삭제하도록 이 명령을 설정할 수도 있습니다. 예를 들어 `docker run -it --rm`을 사용하여 두 가지 작업을 수행합니다. 먼저 현재 터미널을 사용하여 컨테이너에 연결한 후 컨테이너가 완료되면 컨테이너를 제거합니다.

```console
> docker run -it --rm myimage
Counter: 1
Counter: 2
Counter: 3
Counter: 4
Counter: 5
^C
```

`docker run -it`을 사용하면 <kbd>CTRL+C</kbd> 명령이 컨테이너에서 실행 중인 프로세스를 중지하고, 이에 따라 컨테이너가 중지됩니다. `--rm` 매개 변수가 제공되었으므로 프로세스가 중지되면 컨테이너가 자동으로 삭제됩니다. 컨테이너가 존재하지 않는지 확인합니다.

```console
> docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS    PORTS   NAMES
```

### <a name="change-the-entrypoint"></a>ENTRYPOINT 변경

`docker run` 명령을 사용하면 *Dockerfile*에서 `ENTRYPOINT` 명령을 수정하고 해당 컨테이너에만 해당하는 다른 작업을 실행할 수 있습니다. 예를 들어 다음 명령을 사용하여 `bash` 또는 `cmd.exe`를 실행합니다. 필요에 따라 명령을 편집합니다.

#### <a name="windows"></a>Windows
이 예제에서 `ENTRYPOINT`는 `cmd.exe`로 변경됩니다. <kbd>Ctrl+C</kbd>를 눌러 프로세스를 종료하고 컨테이너를 중지합니다.

```console
> docker run -it --rm --entrypoint "cmd.exe" myimage

Microsoft Windows [Version 10.0.17763.379]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\>dir
 Volume in drive C has no label.
 Volume Serial Number is 3005-1E84

 Directory of C:\

04/09/2019  08:46 AM    <DIR>          app
03/07/2019  10:25 AM             5,510 License.txt
04/02/2019  01:35 PM    <DIR>          Program Files
04/09/2019  01:06 PM    <DIR>          Users
04/02/2019  01:35 PM    <DIR>          Windows
               1 File(s)          5,510 bytes
               4 Dir(s)  21,246,517,248 bytes free

C:\>^C
```

#### <a name="linux"></a>Linux

이 예제에서 `ENTRYPOINT`는 `bash`로 변경됩니다. `quit` 명령이 실행되면 프로세스가 종료되고 컨테이너가 중지됩니다.

```bash
root@user:~# docker run -it --rm --entrypoint "bash" myimage
root@8515e897c893:/# ls app
myapp.deps.json  myapp.dll  myapp.pdb  myapp.runtimeconfig.json
root@8515e897c893:/# exit
exit
```

## <a name="essential-commands"></a>필수 명령

Docker에는 컨테이너 및 이미지로 수행할 작업을 다루는 다른 명령이 있습니다. 이 Docker 명령은 컨테이너 관리에 필수적입니다.

* [docker build](https://docs.docker.com/engine/reference/commandline/build/)
* [docker run](https://docs.docker.com/engine/reference/commandline/run/)
* [docker ps](https://docs.docker.com/engine/reference/commandline/ps/)
* [docker stop](https://docs.docker.com/engine/reference/commandline/stop/)
* [docker rm](https://docs.docker.com/engine/reference/commandline/rm/)
* [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/)
* [docker image](https://docs.docker.com/engine/reference/commandline/image/)

## <a name="clean-up-resources"></a>리소스 정리

이 자습서에서는 컨테이너 및 이미지를 만들었습니다. 원하는 경우 이 리소스를 삭제합니다. 다음 명령을 사용하여 다음을 수행합니다.

01. 모든 컨테이너 나열

    ```console
    > docker ps -a
    ```

02. 실행 중인 컨테이너 중지 `CONTAINER_NAME`은 컨테이너에 자동으로 할당된 이름을 나타냅니다.

    ```console
    > docker stop CONTAINER_NAME
    ```

03. 컨테이너 삭제

    ```console
    > docker rm CONTAINER_NAME
    ```

그런 다음, 머신에서 더 이상 사용하지 않을 이미지를 삭제합니다. *Dockerfile*에서 만든 이미지를 삭제한 후 *Dockerfile*이 기반으로 하는 .NET Core 이미지를 삭제합니다. **IMAGE ID** 또는 **REPOSITORY:TAG** 형식 문자열을 사용할 수 있습니다.

```console
docker rmi myimage:latest
docker rmi mcr.microsoft.com/dotnet/core/runtime:2.2
```

`docker images` 명령을 사용하여 설치된 이미지 목록을 확인합니다.

> [!NOTE]
> 이미지 파일이 클 수 있습니다. 일반적으로 앱을 테스트하고 개발하는 동안 만든 임시 컨테이너를 제거합니다. 일반적으로 해당 런타임을 기반으로 다른 이미지를 빌드할 계획인 경우에는 설치된 런타임과 함께 기본 이미지를 유지합니다.

## <a name="next-steps"></a>다음 단계

* [ASP.NET Core 마이크로 서비스 자습서 확인 보기](https://dotnet.microsoft.com/learn/web/aspnet-microservice-tutorial/intro)
* [컨테이너를 지원하는 Azure 서비스 검토](https://azure.microsoft.com/overview/containers/)
* [Dockerfile 명령에 대해 읽어 보기](https://docs.docker.com/engine/reference/builder/)
* [Visual studio용 컨테이너 도구 살펴보기](/visualstudio/containers/overview)
