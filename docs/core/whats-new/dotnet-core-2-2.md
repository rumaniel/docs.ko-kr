---
title: .NET Core 2.2의 새로운 기능
description: .NET Core 2.2에 있는 새로운 기능에 대해 알아봅니다.
dev_langs:
- csharp
- vb
author: rpetrusha
ms.author: ronpet
ms.date: 12/04/2018
ms.openlocfilehash: 49a65dd44159e9800f7cf50a1edaa3d9e9b82e47
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57677268"
---
# <a name="whats-new-in-net-core-22"></a>.NET Core 2.2의 새로운 기능

.NET Core 2.2에는 애플리케이션 배포, 런타임 서비스에 대한 이벤트 처리, Azure SQL 데이터베이스에 인증, JIT 컴파일러 성능 및 `Main` 메서드 실행 전에 코드 삽입 개선 사항이 포함되어 있습니다.

## <a name="new-deployment-mode"></a>새 배포 모드

.NET Core 2.2부터 **.dll** 파일 대신 **.exe** 파일인 [프레임워크 종속 실행 파일](../deploying/index.md#framework-dependent-executables-fde)을 배포할 수 있습니다. 프레임워크 종속 배포와 기능이 유사한 FDE(프레임워크 종속 실행 파일)를 실행하려면 여전히 공유 시스템 수준의 .NET Core 버전이 있어야 합니다. 앱에는 코드와 타사 종속성만 포함됩니다. 프레임워크 종속 배포와 달리 FDE는 플랫폼에 따라 다릅니다.

이 새로운 배포 모드는 라이브러리 대신 실행 파일을 빌드하는 고유한 장점이 있으므로, `dotnet`을 먼저 호출하지 않고 앱을 직접 실행할 수 있습니다.

## <a name="core"></a>코어

**런타임 서비스에서 이벤트 처리**

GC, JIT, ThreadPool 등의 런타임 서비스에 대한 애플리케이션 사용을 자주 모니터링하여 해당 서비스가 애플리케이션에 미치는 영향을 파악하고 싶을 수 있습니다. Windows 시스템에서 이 작업은 일반적으로 현재 프로세스의 ETW 이벤트를 모니터링하여 수행됩니다. 이 방법을 계속 사용할 수도 있지만, 낮은 권한 환경이나 Linux 또는 macOS에서 실행하는 경우 항상 ETW를 사용할 수 있는 것은 아닙니다. 

.NET Core 2.2부터 이제 <xref:System.Diagnostics.Tracing.EventListener?displayProperty=nameWithType> 클래스를 사용하여 CoreCLR 이벤트를 사용할 수 있습니다. 이러한 이벤트는 GC, JIT, ThreadPool 및 interop와 같은 런타임 서비스의 동작을 설명합니다. 이는 CoreCLR ETW 공급자의 일부로 공개되는 동일한 이벤트입니다.  이 공급자를 통해 애플리케이션은 이러한 이벤트를 이용하거나, 전송 메커니즘을 사용하여 원격 분석 집계 서비스에 보낼 수 있습니다. 다음 코드 샘플에서 이벤트 구독 방법을 확인할 수 있습니다.

```csharp
internal sealed class SimpleEventListener : EventListener
{
    // Called whenever an EventSource is created.
    protected override void OnEventSourceCreated(EventSource eventSource)
    {
        // Watch for the .NET runtime EventSource and enable all of its events.
        if (eventSource.Name.Equals("Microsoft-Windows-DotNETRuntime"))
        {
            EnableEvents(eventSource, EventLevel.Verbose, (EventKeywords)(-1));
        }
    }

    // Called whenever an event is written.
    protected override void OnEventWritten(EventWrittenEventArgs eventData)
    {
        // Write the contents of the event to the console.
        Console.WriteLine($"ThreadID = {eventData.OSThreadId} ID = {eventData.EventId} Name = {eventData.EventName}");
        for (int i = 0; i < eventData.Payload.Count; i++)
        {
            string payloadString = eventData.Payload[i]?.ToString() ?? string.Empty;
            Console.WriteLine($"\tName = \"{eventData.PayloadNames[i]}\" Value = \"{payloadString}\"");
        }
        Console.WriteLine("\n");
    }
}
```

또한 .NET Core 2.2에서는 ETW 이벤트에 대한 추가 정보를 제공하기 위해 <xref:System.Diagnostics.Tracing.EventWrittenEventArgs> 클래스에 다음 두 가지 속성이 추가되었습니다.

- <xref:System.Diagnostics.Tracing.EventWrittenEventArgs.OSThreadId?displayProperty=nameWithType>

- <xref:System.Diagnostics.Tracing.EventWrittenEventArgs.TimeStamp?displayProperty=nameWithType>

## <a name="data"></a>데이터

**SqlConnection.AccessToken 속성이 있는 Azure SQL 데이터베이스에 대한 AAD 인증**

.NET Core 2.2부터 Azure Active Directory에서 발급된 액세스 토큰을 사용하여 Azure SQL 데이터베이스에 인증할 수 있습니다. 액세스 토큰을 지원하기 위해 <xref:System.Data.SqlClient.SqlConnection.AccessToken> 속성이 <xref:System.Data.SqlClient.SqlConnection> 클래스에 추가되었습니다. AAD 인증을 활용하려면 System.Data.SqlClient NuGet 패키지 버전 4.6을 다운로드합니다. 이 기능을 사용하려면 [`Microsoft.IdentityModel.Clients.ActiveDirectory`](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) NuGet 패키지에 포함된 [.NET용 Active Directory 인증 라이브러리](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)를 통해 액세스 토큰 값을 얻을 수 있습니다.

## <a name="jit-compiler-improvements"></a>JIT 컴파일러 개선

**계층화된 컴파일은 옵트인 기능으로 유지됨**

.NET Core 2.1에서 JIT 컴파일러는 새로운 컴파일러 기술인 ‘계층화된 컴파일’을 옵트인 기능으로 구현했습니다. 계층화된 컴파일의 목표는 성능 향상입니다. JIT 컴파일러가 수행하는 중요한 작업 중 하나는 코드 실행을 최적화하는 것입니다. 그러나 자주 사용되지 않는 코드 경로의 경우 컴파일러가 코드 최적화에 사용하는 시간이 런타임이 최적화되지 않은 코드 실행에 사용하는 시간보다 길 수 있습니다. 계층화된 컴파일은 JIT 컴파일에 다음과 같은 두 단계를 도입합니다.

- 가능한 한 빨리 코드를 생성하는 **첫 번째 계층**.

- 자주 실행되는 메서드에 대한 최적화된 코드를 생성하는 **두 번째 계층**. 컴파일의 두 번째 계층은 성능 향상을 위해 병렬로 수행됩니다.

계층화된 컴파일을 통한 성능 향상에 대한 자세한 내용은 [.NET Core 2.2 Preview 2 알림](https://devblogs.microsoft.com/dotnet/announcing-net-core-2-2-preview-2/)을 참조하세요.

.NET Core 2.2 Preview 2에서는 계층화된 컴파일을 기본적으로 사용할 수 있었습니다. 그러나 계층화된 컴파일을 기본적으로 사용할 준비가 되지 않았다고 결정하여, .NET Core 2.2에서도 계층화된 컴파일이 계속 옵트인 기능으로 유지되었습니다. 계층화된 컴파일을 옵트인하는 방법에 대한 자세한 내용은 [.NET Core 2.1의 새로운 기능](dotnet-core-2-1.md)에서 [JIT 컴파일러 개선](dotnet-core-2-1.md#jit-compiler-improvements)을 참조하세요.

## <a name="runtime"></a>런타임

**Main 메서드 실행 전에 코드 삽입**

.NET Core 2.2부터 시작 후크를 사용하여 애플리케이션의 Main 메서드를 실행하기 전에 코드를 삽입할 수 있습니다. 시작 후크를 사용하면 호스트가 애플리케이션을 다시 컴파일하거나 변경하지 않고도 배포된 후 애플리케이션의 동작을 사용자 지정할 수 있습니다.

호스팅 공급자는 <xref:System.Runtime.Loader.AssemblyLoadContext?displayProperty=nameWithType> 동작과 같은 주 진입점의 로드 동작에 영향을 미칠 수 있는 설정을 포함하여 사용자 지정 구성 및 정책을 정의해야 합니다. 후크를 사용하여 추적 또는 원격 분석 삽입을 설정하거나, 처리할 콜백을 설정하거나, 기타 환경 종속 동작을 정의할 수 있습니다. 후크는 진입점과 별개이므로 사용자 코드를 수정할 필요가 없습니다.

자세한 내용은 [호스트 시작 후크](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/host-startup-hook.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [.NET Core의 새로운 기능](index.md)
- [ASP.NET Core 2.2의 새로운 기능](/aspnet/core/release-notes/aspnetcore-2.2)
- [EF Core 2.2의 새로운 기능](/ef/core/what-is-new/ef-core-2.2)
