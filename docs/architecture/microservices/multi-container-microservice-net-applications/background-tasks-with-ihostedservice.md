---
title: IHostedService 및 BackgroundService 클래스를 사용하여 마이크로 서비스에서 백그라운드 작업 구현
description: 컨테이너화된 .NET 애플리케이션용 .NET 마이크로 서비스 아키텍처 | IHostedService 및 BackgroundService를 사용하여 마이크로 서비스 .NET Core에서 백그라운드 작업을 구현하는 새 옵션을 이해합니다.
ms.date: 01/07/2019
ms.openlocfilehash: ff263212536233bef85e9517442b4d7ed9eff115
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71039880"
---
# <a name="implement-background-tasks-in-microservices-with-ihostedservice-and-the-backgroundservice-class"></a>IHostedService 및 BackgroundService 클래스를 사용하여 마이크로 서비스에서 백그라운드 작업 구현

백그라운드 작업 및 예약된 작업은 마이크로 서비스 기반 애플리케이션 또는 모든 종류의 애플리케이션에서 결국 구현해야 하는 것입니다. 마이크로 서비스 아키텍처를 사용하는 경우 차이점은 이러한 백그라운드 작업을 호스팅하기 위한 단일 마이크로 서비스 프로세스/컨테이너를 구현할 수 있으므로 필요에 따라 축소/확대하거나 해당 마이크로 서비스 프로세스/컨테이너의 단일 인스턴스를 실행하는지 확인할 수도 있다는 점입니다.

일반 관점에서 호스트/애플리케이션/마이크로 서비스 내에서 호스팅하는 서비스/논리이기 때문에 .NET Core에서 이러한 유형의 작업 *호스팅 서비스*를 호출했습니다. 이 경우 호스팅 서비스는 단순히 백그라운드 작업 논리가 있는 클래스를 의미합니다.

.NET Core 2.0부터 프레임워크는 호스팅 서비스를 쉽게 구현할 수 있도록 돕는 <xref:Microsoft.Extensions.Hosting.IHostedService>라는 새 인터페이스를 제공합니다. 기본적인 개념은 이미지 6-26에 나와 있는 것처럼 웹 호스트 또는 호스트를 실행하는 동안 백그라운드에서 실행하는 여러 백그라운드 작업(호스팅 서비스)을 등록할 수 있다는 것입니다.

![ASP.NET Core 1.x 및 2.x는 웹앱의 백그라운드 프로세스용 IWebHost를 지원하며, .NET Core 2.1은 일반 콘솔 앱으로 백그라운드 프로세스용 IHost를 지원합니다.](./media/image26.png)

**그림 6-26**. WebHost 및 Host에서 IHostedService 사용 비교

`WebHost`와 `Host` 사이에서 만들어진 차이점입니다.

ASP.NET Core 2.0의 `WebHost`(`IWebHost`를 구현하는 기본 클래스)는 MVC 웹앱 또는 Web API 서비스를 구현하는 경우와 같이 프로세스에 HTTP 서버 기능을 제공하는 데 사용하는 인프라 아티팩트입니다. 종속성 주입을 사용하고 요청 파이프라인 등에 미들웨어를 넣고 백그라운드 작업에 대해 이러한 `IHostedServices`를 정확하게 사용할 수 있도록 하는 ASP.NET Core의 새로운 모든 인프라 장점을 제공합니다.

`Host`(`IHost`를 구현하는 기본 클래스)는 .NET Core 2.1에서 도입되었습니다. 기본적으로 `Host`를 통해 `WebHost`(종속성 주입, 호스팅 서비스 등)를 사용하여 가진 것보다 유사한 인프라를 가질 수 있지만 이 경우 MVC, Web API 또는 HTTP 서버 기능과 관련이 없는 호스트로 간단하고 쉬운 프로세스를 갖길 원합니다.

따라서 `IHostedServices`를 호스트하기 위해 만들어진 마이크로 서비스와 같은 호스팅 서비스 및 그 밖의 것을 처리하도록 IHost로 특수화된 호스트 프로세스를 선택하고 만들 수 있거나 기존 ASP.NET Core Web API 또는 MVC 앱과 같이 기존 ASP.NET Core `WebHost`를 대안으로 확장할 수 있습니다.

각 방식은 비즈니스 및 확장성 요구에 따라 장점과 단점을 갖습니다. 요점은 기본적으로 백그라운드 작업에 HTTP(IWebHost)와 아무 관련이 없다면 IHost를 사용해야 합니다.

## <a name="registering-hosted-services-in-your-webhost-or-host"></a>WebHost 또는 Host에서 호스팅 서비스 등록

사용 방법은 `WebHost` 또는 `Host`에서 매우 유사하므로 `IHostedService` 인터페이스에서 자세히 살펴보도록 하겠습니다.

SignalR은 호스팅 서비스를 사용하는 아티팩트의 한 가지 예이지만 다음과 같이 훨씬 간단한 작업에 사용할 수도 있습니다.

- 변경 내용을 찾는 데이터베이스를 폴링하는 백그라운드 작업
- 주기적으로 일부 캐시를 업데이트하는 예약된 작업
- 백그라운드 스레드에서 작업이 실행되도록 허용하는 QueueBackgroundWorkItem의 구현
- `ILogger`와 같은 공통 서비스를 공유하는 동안 웹앱의 백그라운드에서 메시지 큐의 메시지 처리
- `Task.Run()`으로 시작한 백그라운드 작업

기본적으로 IHostedService에 따라 백그라운드 작업에 이러한 작업을 오프로드할 수 있습니다.

하나 또는 여러 `IHostedServices`를 `WebHost` 또는 `Host`에 추가하는 방법은 ASP.NET Core `WebHost`(또는 .NET Core 2.1 이상의 `Host`에서)에서 표준 DI(종속성 주입)를 통해 등록하는 것입니다. 기본적으로 ASP.NET WebHost의 다음 코드에서처럼 `Startup` 클래스의 친숙한 `ConfigureServices()` 메서드 내에서 호스팅 서비스를 등록해야 합니다.

```csharp
public IServiceProvider ConfigureServices(IServiceCollection services)
{
    //Other DI registrations;

    // Register Hosted Services
    services.AddSingleton<IHostedService, GracePeriodManagerService>();
    services.AddSingleton<IHostedService, MyHostedServiceB>();
    services.AddSingleton<IHostedService, MyHostedServiceC>();
    //...
}
```

해당 코드에서 `GracePeriodManagerService` 호스팅 서비스는 eShopOnContainers에서 순서 지정 비즈니스 마이크로 서비스의 실제 코드인 반면 다른 두 가지는 두 개의 추가 샘플입니다.

`IHostedService` 백그라운드 작업 실행은 애플리케이션의 수명에 맞게 조정됩니다(해당하는 경우 호스트 또는 마이크로 서비스). 애플리케이션이 시작할 때 작업을 등록하고 애플리케이션이 종료될 때 일부 정상적인 작업 또는 정리를 수행할 기회를 갖습니다.

`IHostedService`를 사용하지 않고 항상 백그라운드 스레드를 시작하여 작업을 실행할 수 있습니다. 차이점은 정상적인 정리 작업을 실행할 기회를 갖지 않고 해당 스레드가 그냥 제거되는 경우 정확하게 앱의 종료 시간에 있습니다.

## <a name="the-ihostedservice-interface"></a>IHostedService 인터페이스

`IHostedService`를 등록할 때 .NET Core는 애플리케이션 시작 및 중지 중에 각각 `IHostedService` 유형의 `StartAsync()` 및 `StopAsync()` 메서드를 호출합니다. 특히 서버가 시작되고 `IApplicationLifetime.ApplicationStarted`가 트리거된 후 시작이 호출됩니다.

.NET Core에 정의된 대로 `IHostedService`는 다음과 같습니다.

```csharp
namespace Microsoft.Extensions.Hosting
{
    //
    // Summary:
    //     Defines methods for objects that are managed by the host.
    public interface IHostedService
    {
        //
        // Summary:
        // Triggered when the application host is ready to start the service.
        Task StartAsync(CancellationToken cancellationToken);
        //
        // Summary:
        // Triggered when the application host is performing a graceful shutdown.
        Task StopAsync(CancellationToken cancellationToken);
    }
}
```

상상할 수 있듯이 IHostedService의 여러 구현을 만들고 이전에 표시된 것처럼 `ConfigureService()` 메서드에서 DI 컨테이너로 등록할 수 있습니다. 이러한 모든 호스팅 서비스는 애플리케이션/마이크로 서비스와 함께 시작되고 중지됩니다.

개발자는 `StopAsync()` 메서드가 호스트에 의해 트리거될 때 서비스의 중지 작업을 처리할 책임이 있습니다.

## <a name="implementing-ihostedservice-with-a-custom-hosted-service-class-deriving-from-the-backgroundservice-base-class"></a>BackgroundService 기본 클래스에서 파생되는 사용자 지정 호스팅 서비스 클래스로 IHostedService 구현

.NET Core 2.0을 사용할 때 수행해야 하므로 계속 진행하고 처음부터 사용자 지정 호스팅 서비스 클래스를 만들고 `IHostedService`를 구현할 수 있습니다.

그러나 대부분의 백그라운드 작업은 취소 토큰 관리 및 기타 일반적인 작업과 관련하여 비슷한 요구 사항이 있으므로 `BackgroundService`라는(.NET Core 2.1부터 사용 가능) 파생시킬 수 있는 매우 편리한 추상 기본 클래스가 있습니다.

해당 클래스는 백그라운드 작업을 설정하는 데 필요한 주요 작업을 제공합니다.

다음 코드는 .NET Core에서 구현되는 추상 BackgroundService 기본 클래스입니다.

```csharp
// Copyright (c) .NET Foundation. Licensed under the Apache License, Version 2.0.
/// <summary>
/// Base class for implementing a long running <see cref="IHostedService"/>.
/// </summary>
public abstract class BackgroundService : IHostedService, IDisposable
{
    private Task _executingTask;
    private readonly CancellationTokenSource _stoppingCts =
                                                   new CancellationTokenSource();

    protected abstract Task ExecuteAsync(CancellationToken stoppingToken);

    public virtual Task StartAsync(CancellationToken cancellationToken)
    {
        // Store the task we're executing
        _executingTask = ExecuteAsync(_stoppingCts.Token);

        // If the task is completed then return it,
        // this will bubble cancellation and failure to the caller
        if (_executingTask.IsCompleted)
        {
            return _executingTask;
        }

        // Otherwise it's running
        return Task.CompletedTask;
    }

    public virtual async Task StopAsync(CancellationToken cancellationToken)
    {
        // Stop called without start
        if (_executingTask == null)
        {
            return;
        }

        try
        {
            // Signal cancellation to the executing method
            _stoppingCts.Cancel();
        }
        finally
        {
            // Wait until the task completes or the stop token triggers
            await Task.WhenAny(_executingTask, Task.Delay(Timeout.Infinite,
                                                          cancellationToken));
        }

    }

    public virtual void Dispose()
    {
        _stoppingCts.Cancel();
    }
}
```

이전 추상 기본 클래스에서 파생될 때 상속된 해당 구현 덕분에 데이터베이스를 폴링하고 필요한 경우 통합 이벤트를 이벤트 버스로 게시하는 eShopOnContainers의 다음 단순화된 코드에서처럼 사용자 고유의 사용자 지정 호스팅 서비스 클래스에서 `ExecuteAsync()` 메서드를 구현해야 합니다.

```csharp
public class GracePeriodManagerService : BackgroundService
{
    private readonly ILogger<GracePeriodManagerService> _logger;
    private readonly OrderingBackgroundSettings _settings;

    private readonly IEventBus _eventBus;

    public GracePeriodManagerService(IOptions<OrderingBackgroundSettings> settings,
                                     IEventBus eventBus,
                                     ILogger<GracePeriodManagerService> logger)
    {
        //Constructor’s parameters validations...
    }

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        _logger.LogDebug($"GracePeriodManagerService is starting.");

        stoppingToken.Register(() =>
            _logger.LogDebug($" GracePeriod background task is stopping."));

        while (!stoppingToken.IsCancellationRequested)
        {
            _logger.LogDebug($"GracePeriod task doing background work.");

            // This eShopOnContainers method is querying a database table
            // and publishing events into the Event Bus (RabbitMQ / ServiceBus)
            CheckConfirmedGracePeriodOrders();

            await Task.Delay(_settings.CheckUpdateTime, stoppingToken);
        }

        _logger.LogDebug($"GracePeriod background task is stopping.");
    }

    .../...
}
```

eShopOnContainers에 대한 이 특정 경우에 특정 상태로 주문을 조회하는 데이터베이스 테이블을 쿼리하는 애플리케이션 메서드를 실행하고, 변경 내용을 적용하는 경우 이벤트 버스를 통해 통합 이벤트를 게시합니다(아래에서 RabbitMQ 또는 Azure Service Bus를 사용할 수 있음).

물론 다른 비즈니스 백그라운드 작업을 대신 실행할 수 있습니다.

`IWebHostBuilder`의 `UseShutdownTimeout` 확장을 사용하여 `WebHost`를 빌드할 때 해당 값을 변경할 수 있지만 기본적으로 취소 토큰은 5초 시간 제한으로 설정됩니다. 즉, 서비스는 5초 내에 취소될 것으로 예상되며 그렇지 않은 경우 갑자기 종료됩니다.

다음 코드는 해당 시간을 10초로 변경합니다.

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
    ...
```

### <a name="summary-class-diagram"></a>요약 클래스 다이어그램

다음 이미지는 IHostedServices를 구현할 때 관련되는 클래스 및 인터페이스의 시각적 개체 요약을 보여줍니다.

![클래스 다이어그램: IWebHost와 IHost는 IHostedService를 구현하는 BackgroundService에서 상속되는 많은 서비스를 호스트할 수 있습니다.](./media/image27.png)

**그림 6-27**. IHostedService와 관련된 다중 클래스 및 인터페이스를 보여 주는 클래스 다이어그램

### <a name="deployment-considerations-and-takeaways"></a>배포 고려 사항 및 요점

ASP.NET Core `WebHost` 또는 .NET Core `Host`를 배포하는 방법은 최종 솔루션에 영향을 줄 수 있습니다. 예를 들어 IIS에서 `WebHost` 또는 일반 Azure App Service를 배포하는 경우 호스트는 앱 풀 재활용으로 인해 종료될 수 있습니다. 하지만 호스트를 컨테이너로 Kubernetes 또는 Service Fabric과 같은 오케스트레이터에 배포하는 경우 호스트의 실제 인스턴스의 보증된 수를 제어할 수 있습니다. 또한 Azure Functions와 같은 해당 시나리오에 대해 특별히 만들어진 클라우드에서 다른 방법을 고려할 수 있습니다. 마지막으로 서비스가 항상 실행 중이어야 하고 Windows Server에 배포하는 경우 Windows 서비스를 사용할 수 있습니다.

하지만 앱 풀에 배포된 `WebHost`의 경우에도 애플리케이션의 메모리 내 캐시를 다시 채우거나 플러시하는 등의 시나리오가 있습니다. 이는 여전히 해당됩니다.

`IHostedService` 인터페이스는 ASP.NET Core 웹 애플리케이션(.NET Core 2.0에서) 또는 모든 프로세스/호스트(`IHost`로 .NET Core 2.1에서 시작)에서 백그라운드 작업을 시작하는 편리한 방법을 제공합니다. 주요 혜택은 호스트 자체가 종료될 때 백그라운드 작업의 정리 코드에 대한 정상적인 취소를 얻는 기회입니다.

## <a name="additional-resources"></a>추가 자료

- **ASP.NET Core/Standard 2.0에서 예약된 작업 빌드**  
  <https://blog.maartenballiauw.be/post/2017/08/01/building-a-scheduled-cache-updater-in-aspnet-core-2.html>

- **ASP.NET Core 2.0에서 IHostedService 구현**  
  <https://www.stevejgordon.co.uk/asp-net-core-2-ihostedservice>

- **ASP.NET Core 2.1을 사용한 GenericHost 샘플**  
  <https://github.com/aspnet/Hosting/tree/release/2.1/samples/GenericHostSample>

>[!div class="step-by-step"]
>[이전](test-aspnet-core-services-web-apps.md)
>[다음](implement-api-gateways-with-ocelot.md)
