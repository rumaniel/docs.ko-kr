---
title: .NET Core 2.1의 새로운 기능
description: .NET Core 2.1에서 볼 수 있는 새로운 기능에 대해 알아봅니다.
dev_langs:
- csharp
- vb
author: rpetrusha
ms.author: ronpet
ms.date: 10/10/2018
ms.openlocfilehash: 18c8d566c3b79c131a3d031e5bdf3b37996d9115
ms.sourcegitcommit: 10db6551ea3c971470cf5d2cc21ba1cbcefe5c55
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72031855"
---
# <a name="whats-new-in-net-core-21"></a>.NET Core 2.1의 새로운 기능

.NET Core 2.1은 다음 영역에서 향상된 기능 및 새로운 기능을 포함합니다.

- [도구](#tooling)
- [롤포워드](#roll-forward)
- [배포](#deployment)
- [Windows 호환 기능 팩](#windows-compatibility-pack)
- [JIT 컴파일 개선](#jit-compiler-improvements)
- [API 변경 내용](#api-changes)

## <a name="tooling"></a>도구

.NET Core 2.1에 포함된 도구인 .NET Core 2.1 SDK(v 2.1.300)에는 다음과 같은 변경 내용과 향상된 기능이 포함됩니다.

### <a name="build-performance-improvements"></a>빌드 성능 개선

.NET Core 2.1은 특히 증분 빌드의 빌드 시간 성능을 개선하는 데 주로 초점을 맞춥니다. 이러한 성능 개선은 `dotnet build`를 사용하는 명령줄 빌드와 Visual Studio의 빌드에 모두 적용됩니다. 개선된 일부 개별 영역은 다음과 같습니다.

- 패키지 자산 해결의 경우 모든 자산이 아닌 빌드에 사용되는 자산만 해결.

- 어셈블리 참조의 캐싱.

- 여러 개별 `dotnet build` 호출에서 사용되는 프로세스인 장기 실행 SDK 빌드 서버의 사용. `dotnet build`가 실행될 때마다 코드의 큰 블록을 JIT 컴파일할 필요가 없습니다. 다음 명령을 사용하여 빌드 서버 프로세스를 자동으로 종료할 수 있습니다.

   ```dotnetcli
   dotnet buildserver shutdown
   ```

### <a name="new-cli-commands"></a>새 CLI 명령

[`DotnetCliToolReference`](../tools/extensibility.md)를 사용하여 프로젝트별로 사용할 수 있었던 많은 도구를 이제 .NET Core SDK의 일부로 사용할 수 있습니다. 사용 가능한 도구는 다음과 같습니다.

- `dotnet watch`는 지정된 명령 집합을 실행하기 전에 파일이 변경될 때까지 대기하는 파일 시스템 감시자를 제공합니다. 예를 들어 다음 명령은 자동으로 현재 프로젝트를 다시 빌드하고 파일이 변경될 때마다 자세한 정보 출력을 생성합니다.

   ```dotnetcli
   dotnet watch -- --verbose build
   ```

   `--verbose` 옵션 앞에 있는 `--` 옵션에 주목하세요. 이 옵션은 `dotnet watch` 명령으로 직접 전달되는 옵션을 자식 `dotnet` 프로세스에 전달되는 인수와 구분합니다. 이 옵션을 사용하지 않으면 `--verbose` 옵션이 `dotnet build` 명령 대신 `dotnet watch` 명령에 적용됩니다.
  
   자세한 내용은 [dotnet watch를 사용한 ASP.NET Core 앱 개발](/aspnet/core/tutorials/dotnet-watch)을 참조하세요.

- `dotnet dev-certs`는 ASP.NET Core 애플리케이션에서 개발하는 동안 사용되는 인증서를 생성하고 관리합니다.

- `dotnet user-secrets`는 ASP.NET Core 애플리케이션의 사용자 비밀 저장소에서 비밀을 관리합니다.

- `dotnet sql-cache`는 분산 캐싱에 사용할 Microsoft SQL Server 데이터베이스에 테이블 및 인덱스를 만듭니다.

- `dotnet ef`는 Entity Framework Core 애플리케이션에서 데이터베이스, <xref:Microsoft.EntityFrameworkCore.DbContext> 개체 및 마이그레이션을 관리하기 위한 도구입니다. 자세한 내용은 [EF Core .NET 명령줄 도구](/ef/core/miscellaneous/cli/dotnet)를 참조하세요.

### <a name="global-tools"></a>전역 도구

.NET Core 2.1은 명령줄에서 전역으로 사용할 수 있는 사용자 지정 도구인 ‘전역 도구’를 지원합니다.  이전 버전 .NET Core의 확장성 모델은 [`DotnetCliToolReference`](../tools/extensibility.md#consuming-per-project-tools)를 사용하여 프로젝트별로만 사용 가능한 사용자 지정 도구를 만들었습니다.

전역 도구를 설치하려면 [dotnet tool install](../tools/dotnet-tool-install.md) 명령을 사용합니다. 예:

```dotnetcli
dotnet tool install -g dotnetsay
```

설치된 도구는 도구 이름을 지정하여 명령줄에서 실행할 수 있습니다. 자세한 내용은 [.NET Core 전역 도구 개요](../tools/global-tools.md)를 참조하세요.

### <a name="tool-management-with-the-dotnet-tool-command"></a>`dotnet tool` 명령을 사용한 도구 관리

.NET Core 2.1 SDK에서 모든 도구 작업은 `dotnet tool` 명령을 사용합니다. 다음 옵션을 사용할 수 있습니다.

- [`dotnet tool install`](../tools/dotnet-tool-install.md) - 도구를 설치합니다.

- [`dotnet tool update`](../tools/dotnet-tool-update.md) - 도구를 제거하고 다시 설치하여 효과적으로 업데이트합니다.

- [`dotnet tool list`](../tools/dotnet-tool-list.md) - 현재 설치된 도구를 나열합니다.

- [`dotnet tool uninstall`](../tools/dotnet-tool-uninstall.md) - 현재 설치된 도구를 제거합니다.

## <a name="roll-forward"></a>롤포워드

.NET Core 2.0부터 모든 .NET Core 애플리케이션은 시스템에 설치된 최신 *부 버전*으로 자동으로 롤포워드됩니다.

.NET Core 2.0부터 애플리케이션 빌드에 사용된 .NET Core 버전이 런타임에 없는 경우에는 애플리케이션이 .NET Core의 설치된 최신 *부 버전*에 대해 자동으로 실행됩니다. 즉, 애플리케이션이 .NET Core 2.0을 사용하여 빌드되고 .NET Core 2.0이 호스트 시스템에 없지만 .NET Core 2.1이 있는 경우 애플리케이션은 .NET Core 2.1을 사용하여 실행됩니다.

> [!IMPORTANT]
> 이 롤포워드 동작은 미리 보기 릴리스에는 적용되지 않습니다. 기본적으로 주요 릴리스에도 적용되지 않지만 아래 설정으로 변경할 수 있습니다.

후보 공유 프레임워크에서 롤포워드 설정을 변경하여 이 동작을 수정할 수 있습니다. 사용 가능한 설정은 다음과 같습니다.

- `0` - 부 버전 롤포워드 동작을 비활성화합니다. 이 설정을 사용하면 .NET Core 2.0.0용으로 빌드된 애플리케이션이 .NET Core 2.0.1 롤포워드되지만 .NET Core 2.2.0 또는 .NET Core 3.0.0에서는 롤포워드되지 않습니다.
- `1` - 부 버전 롤포워드 동작을 활성화합니다. 이는 설정의 기본값입니다. 이 설정을 사용하면 .NET Core 2.0.0용으로 빌드된 애플리케이션은 설치된 .NET Core 2.0.1 또는 .NET Core 2.2.0에 따라 하나를 롤포워드하지만 .NET Core 3.0.0으로 롤포워드되지 않습니다.
- `2` - 부 버전 및 주 버전 롤포워드 동작을 활성화합니다. 설정한 경우 다른 주 버전도 고려되므로 .NET Core 2.0.0용으로 빌드된 애플리케이션은 NET Core 3.0.0으로 롤포워드됩니다.

다음 세 가지 방법 중 하나로 이 설정을 수정할 수 있습니다.

- `DOTNET_ROLL_FORWARD_ON_NO_CANDIDATE_FX` 환경 변수를 원하는 값으로 설정합니다.

- 원하는 값이 포함된 다음 줄을 *.runtimeconfig.json* 파일에 추가합니다.

   ```json
   "rollForwardOnNoCandidateFx" : 0
   ```

- [.NET Core CLI 도구](../tools/index.md)를 사용하는 경우 `run`과 같은 .NET Core 명령에 원하는 값을 포함하여 다음 옵션을 추가합니다.

   ```dotnetcli
   dotnet run --rollForwardOnNoCandidateFx=0
   ```

패치 버전 롤포워드는 이 설정과는 무관하며 잠재적인 부 버전 롤포워드가 적용된 후에 수행됩니다.

## <a name="deployment"></a>배포

### <a name="self-contained-application-servicing"></a>자체 포함 애플리케이션 제공

`dotnet publish`는 이제 서비스 런타임 버전이 포함된 자체 포함 애플리케이션을 게시합니다. .NET Core 2.1 SDK(v 2.1.300)를 사용하여 자체 포함 애플리케이션을 게시하면 애플리케이션에는 해당 SDK가 인식하는 최신 서비스 런타임 버전이 포함됩니다. 최신 SDK로 업그레이드하면 최신 .NET Core 런타임 버전으로 게시됩니다. 이는 .NET Core 1.0 런타임 이상에 적용됩니다.

자체 포함 게시에는 NuGet.org의 런타임 버전을 사용합니다. 컴퓨터에 서비스 런타임이 있어야 할 필요는 없습니다.

.NET Core 2.0 SDK를 사용하면 `RuntimeFrameworkVersion` 속성을 통해 다른 버전이 지정되지 않는 한 자체 포함 애플리케이션은 .NET Core 2.0.0 런타임으로 게시됩니다. 이 새 동작을 사용하면 더 이상 자체 포함 애플리케이션의 상위 런타임 버전을 선택하기 위해 이 속성을 설정할 필요가 없습니다. 앞으로 가장 쉬운 방법은 항상 .NET Core 2.1 SDK(v 2.1.300)로 게시하는 것입니다.

자세한 내용은 [자체 포함 배포 런타임 롤포워드](../deploying/runtime-patch-selection.md)를 참조하세요.
## <a name="windows-compatibility-pack"></a>Windows 호환 기능 팩

.NET Framework에서 .NET Core로 기존 코드를 포팅할 경우 [Windows 호환 기능 팩](https://www.nuget.org/packages/Microsoft.Windows.Compatibility)을 사용할 수 있습니다. .NET Core에서 사용할 수 있는 것보다 20,000개 많은 API에 대한 액세스를 제공합니다. 이러한 API에는 <xref:System.Drawing?displayProperty=nameWithType> 네임스페이스, <xref:System.Diagnostics.EventLog> 클래스, WMI, 성능 카운터, Windows 서비스 및 Windows 레지스트리 형식/멤버의 형식이 포함됩니다.

## <a name="jit-compiler-improvements"></a>JIT 컴파일러 개선

.NET Core는 성능을 상당히 개선할 수 있는 ‘계층화된 컴파일’(‘적응형 최적화’라고도 함)이라는 새로운 JIT 컴파일러 기술을 통합합니다.   계층화된 컴파일은 옵트인 설정입니다.

JIT 컴파일러가 수행하는 중요한 작업 중 하나는 코드 실행을 최적화하는 것입니다. 그러나 자주 사용되지 않는 코드 경로의 경우 컴파일러가 코드 최적화에 사용하는 시간이 런타임이 최적화되지 않은 코드 실행에 사용하는 시간보다 길 수 있습니다. 계층화된 컴파일은 JIT 컴파일에 다음과 같은 두 단계를 도입합니다.

- 가능한 한 빨리 코드를 생성하는 **첫 번째 계층**.

- 자주 실행되는 메서드에 대한 최적화된 코드를 생성하는 **두 번째 계층**. 컴파일의 두 번째 계층은 성능 향상을 위해 병렬로 수행됩니다.

두 가지 방법 중 하나로 계층화된 컴파일을 옵트인할 수 있습니다.

- .NET Core 2.1 SDK를 사용하는 모든 프로젝트에서 계층화된 컴파일을 사용하려면 다음 환경 변수를 설정합니다.

  ```console
  COMPlus_TieredCompilation="1"
  ```

- 프로젝트별로 계층화된 컴파일을 사용하려면 다음 예제처럼 MSBuild 프로젝트 파일의 `<PropertyGroup>` 섹션에 `<TieredCompilation>` 속성을 추가합니다.

   ```xml
   <PropertyGroup>
      <!-- other property definitions -->

      <TieredCompilation>true</TieredCompilation>
   </PropertyGroup>
   ```

## <a name="api-changes"></a>API 변경 내용

### <a name="spant-and-memoryt"></a>`Span<T>` 및 `Memory<T>`

.NET Core 2.1에는 배열 및 다른 유형의 메모리 관련 작업을 훨씬 더 효율적으로 만드는 몇 가지 새로운 형식이 포함됩니다. 새 형식은 다음과 같습니다.

- <xref:System.Span%601?displayProperty=nameWithType>와 <xref:System.ReadOnlySpan%601?displayProperty=nameWithType>을 참조하세요.

- <xref:System.Memory%601?displayProperty=nameWithType>와 <xref:System.ReadOnlyMemory%601?displayProperty=nameWithType>을 참조하세요.

이러한 형식이 없다면 배열의 일부 또는 메모리 버퍼의 섹션과 같은 항목을 전달할 경우 데이터의 일부를 복사한 다음, 메서드에 전달해야 합니다. 이러한 형식은 추가 메모리 할당 및 복사 작업이 없어도 해당 데이터의 가상 보기를 제공합니다.

다음 예제에서는 <xref:System.Span%601> 및 <xref:System.Memory%601> 인스턴스를 사용하여 배열의 10개 요소에 대한 가상 보기를 제공합니다.

[!code-csharp[Span\<T>](~/samples/core/whats-new/whats-new-in-21/cs/program.cs)]

[!code-vb[Memory\<T>](~/samples/core/whats-new/whats-new-in-21/vb/program.vb)]

### <a name="brotli-compression"></a>Brotli 압축

.NET Core 2.1은 Brotli 압축 및 압축 풀기에 대한 지원을 추가합니다. Brotli는 [RFC 7932](https://www.ietf.org/rfc/rfc7932.txt)에 정의되어 있고 대부분의 웹 브라우저와 주요 웹 서버에서 지원되는 범용 무손실 압축 알고리즘입니다. 스트림 기반 <xref:System.IO.Compression.BrotliStream?displayProperty=nameWithType> 클래스 또는 고성능 범위 기반 <xref:System.IO.Compression.BrotliEncoder?displayProperty=nameWithType> 및 <xref:System.IO.Compression.BrotliDecoder?displayProperty=nameWithType> 클래스를 사용할 수 있습니다. 다음 예제는 <xref:System.IO.Compression.BrotliStream> 클래스를 사용한 압축을 보여 줍니다.

[!code-csharp[Brotli compression](~/samples/core/whats-new/whats-new-in-21/cs/brotli.cs#1)]

[!code-vb[Brotli compression](~/samples/core/whats-new/whats-new-in-21/vb/brotli.vb#1)]

<xref:System.IO.Compression.BrotliStream> 동작은 <xref:System.IO.Compression.DeflateStream> 및 <xref:System.IO.Compression.GZipStream>과 동일하므로, 이러한 API를 호출하는 코드를 <xref:System.IO.Compression.BrotliStream>으로 쉽게 변환할 수 있습니다.

### <a name="new-cryptography-apis-and-cryptography-improvements"></a>새 암호화 API 및 암호화 개선

.NET Core 2.1에는 암호화 API에 대한 다양한 개선 사항이 포함되어 있습니다.

- <xref:System.Security.Cryptography.Pkcs.SignedCms?displayProperty=nameWithType>는 System.Security.Cryptography.Pkcs 패키지에서 사용할 수 있습니다. 구현은 .NET Framework의 <xref:System.Security.Cryptography.Pkcs.SignedCms> 클래스와 동일합니다.

- <xref:System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHash%2A?displayProperty=nameWithType> 및 <xref:System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHashString%2A?displayProperty=nameWithType> 메서드의 새 오버로드는 해시 알고리즘 식별자를 허용하므로 호출자가 SHA-1 이외의 알고리즘을 사용하여 인증서 지문 값을 가져올 수 있습니다.

- 새 <xref:System.Span%601> 기반 암호화 API는 해시, HMAC, 암호화 난수 생성, 비대칭 시그니처 생성, 비대칭 시그니처 처리 및 RSA 암호화에 사용할 수 있습니다.

- <xref:System.Security.Cryptography.Rfc2898DeriveBytes?displayProperty=nameWithType> 성능은 <xref:System.Span%601> 기반 구현을 사용함으로써 15% 정도 향상되었습니다.

- 새 <xref:System.Security.Cryptography.CryptographicOperations?displayProperty=nameWithType> 클래스에는 다음 두 가지 새 메서드가 포함됩니다.

  - <xref:System.Security.Cryptography.CryptographicOperations.FixedTimeEquals%2A>는 동일한 길이의 두 입력에 대해 반환하는 데 고정된 시간을 사용하므로, 타이밍 부채널 정보에 영향을 주지 않기 위해 암호화 확인에 사용하기에 적합합니다.

  - <xref:System.Security.Cryptography.CryptographicOperations.ZeroMemory%2A>는 최적화할 수 없는 메모리 정리 루틴입니다.

- <xref:System.Security.Cryptography.RandomNumberGenerator.Fill%2A?displayProperty=nameWithType> 정적 메서드는 <xref:System.Span%601>를 임의 값으로 채웁니다.

- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms?displayProperty=nameWithType>는 이제 Linux 및 macOS에서 지원됩니다.

- ECDH(타원 곡선 Diffie-Hellman)는 이제 <xref:System.Security.Cryptography.ECDiffieHellman?displayProperty=nameWithType> 클래스 제품군에서 사용할 수 있습니다. 노출 영역은 .NET Framework의 것과 같습니다.

- <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType>에서 반환된 인스턴스는 SHA-2 다이제스트를 사용하여 OAEP에서 암호화 또는 암호 해독되고 RSA-PSS를 사용하여 시그니처를 생성하거나 유효성 검사할 수 있습니다.

### <a name="sockets-improvements"></a>소켓 개선

.NET Core에는 더 높은 수준의 네트워킹 API 기반을 형성하는 새 형식 <xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType> 및 다시 작성된 <xref:System.Net.Http.HttpMessageHandler?displayProperty=nameWithType>가 포함됩니다.  예를 들어 <xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType>는 <xref:System.Net.Http.HttpClient> 구현의 기반입니다. 이전 버전의 .NET Core에서 더 높은 수준의 API는 기본 네트워킹 구현을 기반으로 했습니다.

.NET Core 2.1에 도입된 소켓 구현에는 다음과 같은 여러 가지 이점이 있습니다.

- 이전 구현보다 월등히 향상된 성능.

- 배포 및 서비스를 단순화하는 플랫폼 종속성 제거.

- 모든 .NET Core 플랫폼에서 일관된 동작.

<xref:System.Net.Http.SocketsHttpHandler>는 .NET Core 2.1의 기본 구현입니다. 그러나 <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> 메서드를 호출하여 이전 <xref:System.Net.Http.HttpClientHandler> 클래스를 사용하도록 애플리케이션을 구성할 수 있습니다.

```csharp
AppContext.SetSwitch("System.Net.Http.UseSocketsHttpHandler", false);
```

```vb
AppContext.SetSwitch("System.Net.Http.UseSocketsHttpHandler", False)
```

환경 변수를 사용하여 <xref:System.Net.Http.SocketsHttpHandler>를 기반으로 한 소켓 구현 사용을 옵트아웃할 수도 있습니다. 이를 수행하려면 `DOTNET_SYSTEM_NET_HTTP_USESOCKETSHTTPHANDLER`를 `false` 또는 0으로 설정합니다.

Windows에서는 네이티브 구현을 사용하는 <xref:System.Net.Http.WinHttpHandler?displayProperty=nameWithType>을 사용하거나 클래스의 인스턴스를 <xref:System.Net.Http.HttpClient> 생성자에 전달하여 <xref:System.Net.Http.SocketsHttpHandler> 클래스를 사용하도록 선택할 수도 있습니다.

Linux 및 macOS에서는 프로세스별로 <xref:System.Net.Http.HttpClient>만 구성할 수 있습니다. Linux에서 이전 <xref:System.Net.Http.HttpClient> 구현을 사용하려면 [libcurl](https://curl.haxx.se/libcurl/)을 배포해야 합니다. (.NET Core 2.0과 함께 설치됩니다.)

## <a name="see-also"></a>참고 항목

- [.NET Core의 새로운 기능](index.md)
- [EF Core 2.1의 새로운 기능](/ef/core/what-is-new/ef-core-2.1)
- [ASP.NET Core 2.1의 새로운 기능](/aspnet/core/aspnetcore-2.1)
