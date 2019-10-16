---
title: 스레드 및 스레딩
ms.date: 11/08/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- multiple threads
- threading [.NET]
- threading [.NET], multiple threads
ms.assetid: 5baac3aa-e603-4fa6-9f89-0f2c1084e6b1
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: efbca8177c74fdee635b52294944df23e5aca24f
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65638787"
---
# <a name="threads-and-threading"></a>스레드 및 스레딩

다중 스레딩을 사용하면 애플리케이션의 응답성을 높이고, 다중 프로세서 또는 다중 코어 시스템에서 애플리케이션을 실행하는 경우 해당 처리량을 늘릴 수 있습니다.

## <a name="processes-and-threads"></a>프로세스 및 스레드

*프로세스*는 실행 중인 프로그램입니다. 운영 체제는 프로세스를 사용하여 실행 중인 애플리케이션을 분리합니다. *스레드*는 운영 체제가 프로세서 시간을 할당하는 기본 단위입니다. 각 스레드에는 [예약 우선 순위](scheduling-threads.md)가 있어서 스레드 실행이 일시 중지될 때 스레드 컨텍스트를 저장하는 데 시스템에서 사용하는 일련의 구조를 유지 관리합니다. 스레드 컨텍스트에는 스레드의 CPU 레지스터 및 스택 세트를 포함하여 스레드가 실행을 원활하게 재개하는 데 필요한 모든 정보가 포함됩니다. 다중 스레드는 프로세스의 컨텍스트에서 실행될 수 있습니다. 프로세스의 모든 스레드는 해당 가상 주소 공간을 공유합니다. 스레드는 다른 스레드에 의해 현재 실행 중인 부분을 포함한 프로그램 코드의 일부를 실행할 수 있습니다.

> [!NOTE]
> .NET Framework에서는 *애플리케이션 도메인*을 사용하여 프로세스 내에서 애플리케이션을 격리하는 방법을 제공합니다. (애플리케이션 도메인은 .NET Core에서 사용할 수 없습니다.) 자세한 내용은 [애플리케이션 도메인](../../framework/app-domains/application-domains.md) 문서의 [애플리케이션 도메인 및 스레드](../../framework/app-domains/application-domains.md#application-domains-and-threads) 섹션을 참조하세요.

기본적으로 .NET 프로그램은 *주* 스레드라고도 하는 단일 스레드에서 시작됩니다. 그러나 추가 스레드를 만들어서 기본 스레드에서 병렬로 또는 동시에 코드를 실행할 수 있습니다. 이러한 스레드를 일반적으로 *작업자* 스레드라고 합니다.

## <a name="when-to-use-multiple-threads"></a>다중 스레드 사용 시기

다중 스레딩을 사용하여 애플리케이션의 응답성을 높이고, 다중 프로세서 또는 다중 코어 시스템을 활용하여 애플리케이션의 처리량을 늘릴 수 있습니다.

기본 스레드가 사용자 인터페이스 요소에 대한 책임이 있고 사용자 작업에 응답하는 데 데스크톱 애플리케이션을 사용하는 것이 좋습니다. 작업자 스레드를 사용하여 시간이 많이 걸리는 작업을 수행합니다. 그렇지 않으면 기본 스레드를 점유하고 사용자 인터페이스가 응답하지 않게 됩니다. 네트워크 또는 디바이스 통신을 위한 전용 스레드를 사용하여 들어오는 메시지 또는 이벤트에 대한 응답을 향상시킬 수도 있습니다.

프로그램에서 병렬로 수행될 수 있는 작업을 수행하는 경우 별도 스레드에서 해당 작업을 수행하고 다중 프로세서 또는 다중 코어 시스템에서 프로그램을 실행하여 총 실행 시간을 줄일 수 있습니다. 이러한 시스템에서 다중 스레드를 사용하면 응답성이 함께 증가하며 처리량도 증가할 수 있습니다.

## <a name="how-to-use-multithreading-in-net"></a>.NET에서 다중 스레드를 사용하는 방법

.NET Framework 4부터 다중 스레딩을 사용하는 권장 방법은 [TPL(작업 병렬 라이브러리)](../parallel-programming/task-parallel-library-tpl.md) 및 [PLINQ(병렬 LINQ)](../parallel-programming/parallel-linq-plinq.md)를 사용하는 것입니다. 자세한 내용은 [병렬 프로그래밍](../parallel-programming/index.md)을 참조하세요.

TPL 및 PLINQ는 <xref:System.Threading.ThreadPool> 스레드를 사용합니다. <xref:System.Threading.ThreadPool?displayProperty=nameWithType> 클래스는 작업자 스레드 풀을 포함한 .NET 애플리케이션을 제공합니다. 스레드 풀 스레드를 사용할 수도 있습니다. 자세한 내용은 [관리 스레드 풀](the-managed-thread-pool.md)을 참조하세요.

마지막으로 관리 스레드를 나타내는 <xref:System.Threading.Thread?displayProperty=nameWithType> 클래스를 사용할 수 있습니다. 자세한 내용은 [스레드 및 스레딩 사용](using-threads-and-threading.md)을 참조하세요.

다중 스레드는 공유 리소스에 액세스해야 합니다. 리소스를 손상되지 않도록 유지하고 경합 상태를 방지하기 위해 스레드 액세스를 여기에 동기화해야 합니다. 또한 다중 스레드의 상호 작용을 조정할 수도 있습니다. .NET은 공유 리소스에 대한 액세스를 동기화하거나 스레드 상호 작용을 조정하는 데 사용할 수 있는 다양한 형식을 제공합니다. 자세한 내용은 [동기화 기본 형식 개요](overview-of-synchronization-primitives.md)를 참조하세요.

스레드에서 예외를 처리합니다. 스레드에서 처리되지 않은 예외가 있으면 일반적으로 프로세스가 종료됩니다. 자세한 내용은 [관리 스레드의 예외](exceptions-in-managed-threads.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [스레딩 개체 및 기능](threading-objects-and-features.md)
- [관리 스레딩을 구현하는 최선의 방법](managed-threading-best-practices.md)
- [.NET의 병렬 처리, 동시성 및 비동기 프로그래밍](../parallel-processing-and-concurrency.md)
- [프로세스 및 스레드 정보](/windows/desktop/procthread/about-processes-and-threads)
