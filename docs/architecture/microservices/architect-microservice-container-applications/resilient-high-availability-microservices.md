---
title: 마이크로 서비스의 복원력 및 고가용성
description: 마이크로 서비스는 고가용성을 달성하기 위해 복원력이 있어야 하므로 일시적인 네트워크 및 종속성 오류를 견디도록 설계되어야 합니다.
ms.date: 09/20/2018
ms.openlocfilehash: 6c110b0fe7a80842f12779494e5b0bdd29c5fb64
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834345"
---
# <a name="resiliency-and-high-availability-in-microservices"></a>마이크로 서비스의 복원력 및 고가용성

예기치 않은 오류를 처리하는 것은 특히 분산 시스템에서 해결하기 가장 어려운 문제 중 하나입니다. 개발자가 작성하는 대부분의 코드에는 예외 처리가 포함되어 있으며 테스트하는 데 가장 많은 시간이 소요되는 부분이기도 합니다. 코드를 작성하여 오류를 처리하는 것보다 문제가 더 복잡합니다. 마이크로 서비스를 실행 중인 컴퓨터에 오류가 발생하면 어떻게 되나요? 이 마이크로 서비스 오류를 감지해야 할 뿐만 아니라(자체적으로 어려운 문제) 마이크로 서비스를 다시 시작해야 합니다.

마이크로 서비스는 오류에 대해 복원력이 있어야 하고 가용성을 위해 다른 컴퓨터에서 자주 다시 시작할 수 있어야 합니다. 이 복원력은 또한 마이크로 서비스가 이 상태를 복구할 수 있도록 마이크로 서비스를 대신하여 미리 저장된 상태와 마이크로 서비스를 성공적으로 다시 시작할 수 있는지 여부에 달려 있습니다. 즉, 상태 또는 데이터의 복원력(데이터 손실 없음, 데이터 일관성 유지)뿐만 아니라 컴퓨팅 기능(프로세스가 언제든지 다시 시작할 수 있음)에도 복원력이 있어야 합니다.

복원력 문제는 애플리케이션 업그레이드 중에 오류가 발생하는 경우와 같이 다른 시나리오 중에 발생합니다. 배포 시스템을 사용하는 마이크로 서비스는 최신 버전으로 계속 전환할지 또는 일관된 상태를 유지하기 위해 이전 버전으로 롤백할지를 결정해야 합니다. 계속 전환할 수 있을 만큼 충분한 컴퓨터가 있는지 여부, 이전 버전의 마이크로 서비스를 복구하는 방법에 대한 질문을 고려해야 합니다. 전체 애플리케이션 및 오케스트레이터에서 이러한 결정을 내릴 수 있도록 마이크로 서비스에서 상태 정보를 내보내야 합니다.

또한 복원력은 클라우드 기반 시스템의 작동 방식과 관련이 있습니다. 앞서 언급했듯이 클라우드 기반 시스템은 오류에 대응하여 자동으로 복구를 시도해야 합니다. 예를 들어, 네트워크 또는 컨테이너 오류가 발생하는 경우 많은 경우 클라우드의 오류가 부분적이기 때문에 클라이언트 앱 또는 클라이언트 서비스는 메시지 전송을 재시도하거나 요청을 재시도하는 전략을 포함해야 합니다. 이 가이드의 [복원력 있는 애플리케이션 구현](../implement-resilient-applications/index.md) 섹션에서는 부분적인 오류를 처리하는 방법에 대해 설명합니다. 이 주제를 다룰 다양한 정책을 제공하는 [Polly](https://github.com/App-vNext/Polly)와 같은 라이브러리를 사용하여 .NET Core의 회로 차단기 패턴이나 지수 백오프를 통한 재시도 같은 기술을 설명합니다.

## <a name="health-management-and-diagnostics-in-microservices"></a>마이크로 서비스의 상태 관리 및 진단

명백한 것 같으면서도 지나치기 쉽지만 마이크로 서비스는 해당 상태와 진단을 보고해야 합니다. 그렇지 않으면 작업 측면에서 거의 정보를 얻을 수 없습니다. 일련의 독립된 서비스의 진단 이벤트를 상호 연결하고 이벤트 순서를 파악하기 위해 시스템 클록 불일치를 다루는 것은 어려운 문제입니다. 합의된 프로토콜 및 데이터 형식을 통해 마이크로 서비스와 상호 작용하는 것과 같은 방식으로, 궁극적으로 쿼리 및 보기를 위해 이벤트 저장소에 저장되는 상태 및 진단 이벤트를 로깅하는 방법에 대한 표준화가 필요합니다. 마이크로 서비스 접근 방식에서는 서로 다른 팀이 단일 로깅 형식에 동의하는 것이 중요합니다. 애플리케이션에서는 진단 이벤트를 보는 일관된 접근 방식이 필요합니다.

### <a name="health-checks"></a>상태 확인

상태는 진단과 다릅니다. 상태란 적절한 조치를 취하기 위해 현재 상태를 보고하는 마이크로 서비스에 관한 것입니다. 좋은 예로는 가용성을 유지하기 위해 업그레이드 및 배포 메커니즘을 사용하는 것입니다. 서비스가 프로세스 충돌이나 컴퓨터 재부팅으로 인해 현재 상태가 좋지 않을 수도 있지만 서비스는 여전히 작동 중일 수 있습니다. 마지막으로 필요한 것은 업그레이드를 수행하여 이 문제를 악화시키는 것입니다. 가장 좋은 방법은 조사를 먼저 하거나 마이크로 서비스가 복구되는 시간을 허용하는 것입니다. 마이크로 서비스의 상태 이벤트를 통해 합리적인 의사 결정을 수행할 수 있고 실제로 자체 복구 서비스를 만들 수 있습니다.

이 가이드의 [ASP.NET Core 서비스의 상태 검사 구현](../implement-resilient-applications/monitor-app-health.md#implement-health-checks-in-aspnet-core-services) 섹션에서는 모니터링 서비스에 상태를 보고하고 적절한 조치를 취할 수 있도록 마이크로 서비스에서 새 ASP.NET HealthChecks 라이브러리를 사용하는 방법을 설명합니다.

[GitHub](https://github.com/Xabaril/BeatPulse)에서 [NuGet 패키지](https://www.nuget.org/packages/BeatPulse/)로 사용할 수 있는 비트 펄스라는 뛰어난 오픈 소스 라이브러리를 사용하는 옵션도 있습니다. 이 라이브러리에서는 조금 복잡한 상태 검사를 수행하고 두 형식의 검사를 처리합니다.

- **활동성**: 마이크로 서비스가 활성 상태인지, 즉 요청을 수락하고 응답할 수 있는지를 검사합니다. 
- **준비성**: 마이크로 서비스가 의도된 작업을 수행할 수 있도록 마이크로 서비스의 종속성(데이터베이스, 큐 서비스 등)이 자체적으로 준비되었는지를 검사합니다. 

### <a name="using-diagnostics-and-logs-event-streams"></a>진단 및 로그 이벤트 스트림 사용

로그는 예외, 경고 및 간단한 정보 메시지를 포함하여 애플리케이션이나 서비스의 실행 방법에 대한 정보를 제공합니다. 일반적으로 각 로그는 이벤트당 하나의 줄이 있는 텍스트 형식이지만 종종 여러 줄에 걸쳐 스택 추적을 표시하는 경우도 있습니다.

모놀리식 서버 기반 애플리케이션에서는 로그를 디스크의 파일(로그 파일)에 기록한 다음, 모든 도구로 분석할 수 있습니다. 애플리케이션 실행은 고정된 서버 또는 VM으로 제한되므로 일반적으로 이벤트 흐름을 분석하기에는 그다지 복잡하지 않습니다. 그러나 오케스트레이터 클러스터의 여러 노드에서 여러 서비스가 실행되는 분산 애플리케이션에서는 분산된 이벤트를 상호 연결할 수 있습니다.

마이크로 서비스 기반 애플리케이션은 이벤트나 로그 파일의 출력 스트림을 자체적으로 저장하려고 시도해서는 안되며 이벤트 라우팅을 중앙 위치로 관리하려고 시도하지 않아야 합니다. 이 모든 과정은 투명해야 합니다. 즉, 각 프로세스는 실행 중인 실행 환경 인프라에서 수집하는 표준 출력에 해당 이벤트 스트림을 기록해야 합니다. 이러한 이벤트 스트림 라우터의 예로는 [Microsoft.Diagnostic.EventFlow](https://github.com/Azure/diagnostics-eventflow)가 있으며, 여러 소스에서 이벤트 스트림을 수집하여 출력 시스템에 게시합니다. 여기에는 [Azure Monitor](https://azure.microsoft.com/services/monitor//), [Azure Diagnostics](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostics-extension-overview)와 같은 개발 환경 또는 클라우드 시스템을 위한 간단한 표준 출력이 포함될 수 있습니다. [Splunk](https://www.splunk.com/goto/Splunk_Log_Management?ac=ga_usa_log_analysis_phrase_Mar17&_kk=logs%20analysis&gclid=CNzkzIrex9MCFYGHfgodW5YOtA)와 같이 실시간으로도 로그를 검색, 경고, 보고 및 모니터링할 수 있는 타사 로그 분석 플랫폼 및 도구도 제공됩니다.

### <a name="orchestrators-managing-health-and-diagnostics-information"></a>상태 및 진단 정보를 관리하는 오케스트레이터

마이크로 서비스 기반 애플리케이션을 만들 때는 복잡성을 처리해야 합니다. 물론 단일 마이크로 서비스는 다루기가 쉽지만 유형이나 수십 수백 가지 유형의 마이크로 서비스 인스턴스는 복잡한 문제입니다. 안정적이고 응집성 있는 시스템을 갖추기 위해서는 마이크로 서비스 아키텍처를 빌드하는 것뿐만 아니라 고가용성, 주소 지정 기능, 복원력, 상태 및 진단도 필요합니다.

![마이크로 서비스에 대한 지원 플랫폼을 제공하는 클러스터의 다이어그램입니다.](./media/resilient-high-availability-microservices/microservice-platform.png)

**그림 4-22**. 마이크로 서비스 플랫폼은 애플리케이션의 상태 관리를 위한 기본 요소입니다.

그림 4-22의 복잡한 문제는 직접 해결하기가 어렵습니다. 개발 팀은 마이크로 서비스 기반 접근 방식을 사용하여 비즈니스 문제를 해결하고 사용자 지정 애플리케이션을 빌드하는 데 집중해야 합니다. 복잡한 인프라 문제를 해결하는 데 집중해서는 안됩니다. 마이크로 서비스 기반 애플리케이션의 비용이 엄청나게 늘어나기 때문입니다. 따라서 오케스트레이터 또는 마이크로 서비스 클러스터라고 하는 마이크로 서비스 지향 플랫폼이 있어 서비스 구축 및 실행과 인프라 리소스를 효율적으로 사용하는 어려운 문제를 해결하려고 합니다. 이를 통해 마이크로 서비스 접근 방식을 사용하는 애플리케이션 빌드의 복잡성을 줄일 수 있습니다.

서로 다른 오케스트레이터가 비슷한 것처럼 보일 수도 있지만, 다음 섹션에서 설명하는 것처럼 각각 제공되는 진단 및 상태 확인은 OS 플랫폼에 따라 기능 및 성숙도가 다를 수 있습니다.

## <a name="additional-resources"></a>추가 자료

- **The Twelve-Factor App. XI. 로그: 로그를 이벤트 스트림으로 처리** \
  <https://12factor.net/logs>

- **Microsoft 진단 EventFlow 라이브러리** GitHub 리포지토리 \
  <https://github.com/Azure/diagnostics-eventflow>

- **Azure Diagnostics란?**  \
  <https://docs.microsoft.com/azure/azure-diagnostics>

- **Azure Monitor 서비스에 Windows 컴퓨터 연결** \
  <https://docs.microsoft.com/azure/azure-monitor/platform/agent-windows>

- **의도한 내용 로깅: 의미 체계 로깅 애플리케이션 블록 사용** \
  <https://docs.microsoft.com/previous-versions/msp-n-p/dn440729(v=pandp.60)>

- **Splunk** 공식 사이트 \
  <https://www.splunk.com/>

- Windows용 이벤트 추적(ETW)의 **EventSource 클래스** API\
  [https://docs.microsoft.com/dotnet/api/system.diagnostics.tracing.eventsource](xref:System.Diagnostics.Tracing.EventSource)

>[!div class="step-by-step"]
>[이전](microservice-based-composite-ui-shape-layout.md)
>[다음](scalable-available-multi-container-microservice-applications.md)
