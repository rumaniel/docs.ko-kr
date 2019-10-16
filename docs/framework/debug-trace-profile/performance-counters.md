---
title: .NET Framework의 성능 카운터
ms.date: 03/30/2017
helpviewer_keywords:
- performance, .NET Framework applications
- performance counters
- performance monitoring, counters
ms.assetid: 06a4ae8c-eeb2-4d5a-817e-b1b95c0653e1
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: eafbd5b1dfa8eeee386cdcf49652aeeee9d635a8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052390"
---
# <a name="performance-counters-in-the-net-framework"></a>.NET Framework의 성능 카운터
이 항목에서는 [Windows 성능 모니터](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc749249%28v=ws.11%29)에서 확인할 수 있는 성능 카운터 목록을 제공 합니다.  
  
- [예외 성능 카운터](#exception)  
  
- [interop 성능 카운터](#interop)  
  
- [JIT 성능 카운터](#jit)  
  
- [로드 성능 카운터](#loading)  
  
- [잠금 및 스레드 성능 카운터](#lockthread)  
  
- [메모리 성능 카운터](#memory)  
  
- [네트워킹 성능 카운터](#networking)  
  
- [보안 성능 카운터](#security)  
  
<a name="exception"></a>   
## <a name="exception-performance-counters"></a>예외 성능 카운터  
 성능 콘솔 .NET CLR 예외 범주에는 응용 프로그램에서 발생한 예외에 대한 정보를 제공하는 카운터가 포함됩니다. 다음 표에서는 이러한 성능 카운터에 대해 설명합니다.  
  
|성능 카운터|설명|  
|-------------------------|-----------------|  
|**# of Exceps Thrown**|응용 프로그램이 시작된 이후 발생한 예외의 총수를 표시합니다. .NET 예외 및 .NET 예외로 변환된 관리되지 않는 예외를 모두 포함합니다. 예를 들어 비관리 코드에서 반환된 HRESULT는 관리 코드에서 예외로 변환됩니다.<br /><br /> 이 카운터는 처리된 예외와 처리되지 않은 예외를 모두 포함합니다. 다시 발생한 예외는 다시 계산됩니다.|  
|**# of Exceps Thrown / Sec**|초당 발생한 예외 수를 표시합니다. .NET 예외 및 .NET 예외로 변환된 관리되지 않는 예외를 모두 포함합니다. 예를 들어 비관리 코드에서 반환된 HRESULT는 관리 코드에서 예외로 변환됩니다.<br /><br /> 이 카운터는 처리된 예외와 처리되지 않은 예외를 모두 포함합니다. 시간별 평균이 아니라 마지막 두 샘플에서 관찰된 값의 차이를 샘플 간격 기간으로 나눈 값을 표시합니다. 이 카운터는 100개를 초과(>100)하는 수의 예외가 throw된 경우 잠재적 성능 문제를 표시합니다.|  
|**# of Filters / Sec**|초당 실행된 .NET 예외 필터 수를 표시합니다. 예외가 처리되었는지 여부에 관계없이 예외 필터가 평가됩니다.<br /><br /> 이 카운터는 평균 초과 시간이 아니며, 샘플 간격으로 나뉜 마지막 두 개의 샘플에서 관찰된 값의 차이를 표시합니다.|  
|**# of Finallys / Sec**|초당 실행된 finally 블록 수를 표시합니다. finally 블록은 try 블록이 종료된 방식에 관계없이 실행됩니다.  예외에 대해 실행된 finally 블록만 계산됩니다. 정상적인 코드 경로의 finally 블록은 이 카운터에서 계산되지 않습니다.<br /><br /> 이 카운터는 평균 초과 시간이 아니며, 샘플 간격으로 나뉜 마지막 두 개의 샘플에서 관찰된 값의 차이를 표시합니다.|  
|**Throw to Catch Depth / Sec**|예외가 발생한 프레임에서 예외를 처리한 프레임으로 트래버스된 초당 스택 프레임 수를 표시합니다. 예외 처리기를 실행하면 이 카운터가 0으로 다시 설정되므로 중첩된 예외는 처리기 간의 스택 깊이를 나타냅니다.<br /><br /> 이 카운터는 평균 초과 시간이 아니며, 샘플 간격으로 나뉜 마지막 두 개의 샘플에서 관찰된 값의 차이를 표시합니다.|  
  
<a name="interop"></a>   
## <a name="interop-performance-counters"></a>interop 성능 카운터  
 성능 콘솔 .NET CLR Interop 범주에는 응용 프로그램과 COM 구성 요소, COM+ 서비스 및 외부 형식 라이브러리의 상호 작용에 대한 정보를 제공하는 카운터가 포함됩니다. 다음 표에서는 이러한 성능 카운터에 대해 설명합니다.  
  
|성능 카운터|설명|  
|-------------------------|-----------------|  
|**# of CCWs**|현재 CCW(COM 호출 가능 래퍼) 수를 표시합니다. CCW는 관리되지 않는 COM 클라이언트에서 참조되는 관리되는 개체에 대한 프록시입니다. 이 카운터는 관리되지 않는 COM 코드에서 참조되는 관리되는 개체 수를 나타냅니다.|  
|**# of marshaling**|응용 프로그램이 시작된 이후 인수 및 반환 값을 관리 코드에서 비관리 코드로 마샬링하거나 그 반대로 마샬링한 총 횟수를 표시합니다. 이 카운터는 스텁이 인라인인 경우에는 증가하지 않습니다. 스텁은 인수 및 반환 값을 마샬링합니다. 일반적으로 스텁은 마샬링 오버헤드가 적을 때 인라인됩니다.|  
|**# of Stubs**|공용 언어 런타임에서 만든 현재 스텁 수를 표시합니다. 스텁은 COM interop 호출이나 플랫폼 호출 중에 인수 및 반환 값을 관리 코드에서 비관리 코드로 마샬링하거나 그 반대로 마샬링합니다.|  
|**# of TLB exports / sec**|나중에 사용하기 위해 예약되어 있습니다.|  
|**# of TLB imports / sec**|나중에 사용하기 위해 예약되어 있습니다.|  
  
<a name="jit"></a>   
## <a name="jit-performance-counters"></a>JIT 성능 카운터  
 성능 콘솔 .NET CLR JIT 범주에는 JIT 컴파일된 코드에 대한 정보를 제공하는 카운터가 포함됩니다. 다음 표에서는 이러한 성능 카운터에 대해 설명합니다.  
  
|성능 카운터|설명|  
|-------------------------|-----------------|  
|**# of IL Bytes JITted**|응용 프로그램이 시작된 이후 JIT(Just-In-Time) 컴파일러에서 컴파일된 MSIL(Microsoft Intermediate Language) 바이트의 총수를 표시합니다. 이 카운터는 **Total # of IL Bytes Jitted** 카운터에 해당합니다.|  
|**# of Methods JITted**|응용 프로그램이 시작된 이후 JIT 컴파일된 메서드의 총수를 표시합니다. 이 카운터는 사전 JIT 컴파일된 메서드를 포함하지 않습니다.|  
|**% Time in Jit**|마지막 JIT 컴파일 단계 이후 JIT 컴파일에 소요된 경과 시간의 백분율을 표시합니다. 이 카운터는 JIT 컴파일 단계가 끝날 때마다 업데이트됩니다. JIT 컴파일 단계는 메서드 및 해당 종속성이 컴파일될 때 발생합니다.|  
|**IL Bytes Jitted / sec**|초당 JIT 컴파일되는 MSIL 바이트 수를 표시합니다. 이 카운터는 평균 초과 시간이 아니며, 샘플 간격으로 나뉜 마지막 두 개의 샘플에서 관찰된 값의 차이를 표시합니다.|  
|**Standard Jit Failures**|응용 프로그램이 시작된 이후 JIT 컴파일러에서 컴파일하지 못한 메서드의 최대 개수를 표시합니다. 이 오류는 MSIL을 확인할 수 없거나 JIT 컴파일러에 내부 오류가 있는 경우에 발생할 수 있습니다.|  
|**Total # of IL Bytes Jitted**|응용 프로그램이 시작된 이후 JIT 컴파일된 MSIL 바이트의 총수를 표시합니다. 이 카운터는 **# of IL Bytes Jitted** 카운터에 해당합니다.|  
  
<a name="loading"></a>   
## <a name="loading-performance-counters"></a>로드 성능 카운터  
 성능 콘솔 .NET CLR 로드 범주에는 로드된 어셈블리, 클래스 및 응용 프로그램 도메인에 대한 정보를 제공하는 카운터가 포함됩니다. 다음 표에서는 이러한 성능 카운터에 대해 설명합니다.  
  
|성능 카운터|설명|  
|-------------------------|-----------------|  
|**% Time Loading**|나중에 사용하기 위해 예약되어 있습니다.|  
|**Assembly Search Length**|나중에 사용하기 위해 예약되어 있습니다.|  
|**Bytes in Loader Heap**|모든 응용 프로그램 도메인에 클래스 로더가 커밋된 메모리의 현재 크기(바이트)를 표시합니다. 커밋된 메모리는 디스크 페이징 파일에 예약된 실제 공간입니다.|  
|**Current appdomains**|이 응용 프로그램에 로드된 응용 프로그램 도메인의 현재 개수를 표시합니다.|  
|**Current Assemblies**|현재 실행 중인 응용 프로그램에서 모든 응용 프로그램 도메인에 로드된 어셈블리의 현재 개수를 표시합니다. 어셈블리가 여러 응용 프로그램 도메인에서 도메인 중립적으로 로드되는 경우 이 카운터는 한 번만 증가됩니다.|  
|**Current Classes Loaded**|모든 어셈블리에 로드된 클래스의 현재 개수를 표시합니다.|  
|**Rate of appdomains**|초당 로드된 응용 프로그램 도메인 수를 표시합니다. 이 카운터는 평균 초과 시간이 아니며, 샘플 간격으로 나뉜 마지막 두 개의 샘플에서 관찰된 값의 차이를 표시합니다.|  
|**Rate of appdomains unloaded**|초당 언로드된 응용 프로그램 도메인 수를 표시합니다. 이 카운터는 평균 초과 시간이 아니며, 샘플 간격으로 나뉜 마지막 두 개의 샘플에서 관찰된 값의 차이를 표시합니다.|  
|**Rate of Assemblies**|모든 응용 프로그램 도메인에 초당 로드된 어셈블리 수를 표시합니다. 어셈블리가 여러 응용 프로그램 도메인에서 도메인 중립적으로 로드되는 경우 이 카운터는 한 번만 증가됩니다.<br /><br /> 이 카운터는 평균 초과 시간이 아니며, 샘플 간격으로 나뉜 마지막 두 개의 샘플에서 관찰된 값의 차이를 표시합니다.|  
|**Rate of Classes Loaded**|모든 어셈블리에 초당 로드된 클래스 수를 표시합니다. 이 카운터는 평균 초과 시간이 아니며, 샘플 간격으로 나뉜 마지막 두 개의 샘플에서 관찰된 값의 차이를 표시합니다.|  
|**Rate of Load Failures**|초당 로드하지 못한 클래스 수를 표시합니다. 이 카운터는 평균 초과 시간이 아니며, 샘플 간격으로 나뉜 마지막 두 개의 샘플에서 관찰된 값의 차이를 표시합니다.<br /><br /> 로드 실패는 부적절한 보안이나 잘못된 형식과 같은 다양한 이유로 발생할 수 있습니다. 자세한 내용은 프로파일링 서비스 도움말을 참조하세요.|  
|**Total # of Load Failures**|응용 프로그램이 시작된 이후 로드하지 못한 클래스의 최대 개수를 표시합니다.<br /><br /> 로드 실패는 부적절한 보안이나 잘못된 형식과 같은 다양한 이유로 발생할 수 있습니다. 자세한 내용은 프로파일링 서비스 도움말을 참조하세요.|  
|**Total Appdomains**|응용 프로그램이 시작된 이후 로드된 응용 프로그램 도메인의 최대 개수를 표시합니다.|  
|**Total appdomains unloaded**|응용 프로그램이 시작된 이후 언로드된 응용 프로그램 도메인의 총수를 표시합니다. 응용 프로그램 도메인이 여러 번 로드 및 언로드되는 경우 이 카운터는 응용 프로그램 도메인이 언로드될 때마다 증가합니다.|  
|**Total Assemblies**|응용 프로그램이 시작된 이후 로드된 어셈블리의 총수를 표시합니다. 어셈블리가 여러 응용 프로그램 도메인에서 도메인 중립적으로 로드되는 경우 이 카운터는 한 번만 증가됩니다.|  
|**Total Classes Loaded**|응용 프로그램이 시작된 이후 모든 어셈블리에 로드된 클래스의 누적 개수를 표시합니다.|  
  
<a name="lockthread"></a>   
## <a name="lock-and-thread-performance-counters"></a>잠금 및 스레드 성능 카운터  
 성능 콘솔 .NET CLR LocksAndThreads 범주에는 응용 프로그램에서 사용하는 관리되는 잠금 및 스레드에 대한 정보를 제공하는 카운터가 포함됩니다. 다음 표에서는 이러한 성능 카운터에 대해 설명합니다.  
  
|성능 카운터|설명|  
|-------------------------|-----------------|  
|**# of current logical Threads**|응용 프로그램에서 현재 관리 되는 스레드 개체 수를 표시합니다. 이 카운터는 실행 중인 스레드와 중지된 스레드 둘 다의 개수를 유지 관리합니다. 이 카운터는 시간별 평균이 아니라 마지막으로 관찰된 값만 표시합니다.|  
|**# of current physical Threads**|공용 언어 런타임에서 관리되는 스레드 개체에 대한 기본 스레드로 사용하기 위해 만들고  소유한 네이티브 운영 체제 스레드 수를 표시합니다. 런타임에서 내부 작업에 사용하는 스레드는 이 카운터 값에 포함되지 않고 운영 체제 프로세스의 스레드 하위 집합입니다.|  
|**# of current recognized threads**|현재 런타임에서 인식된 스레드 수를 표시합니다. 이 스레드는 해당하는 관리되는 스레드 개체와 연결됩니다. 런타임에서 이 스레드를 만들지는 않지만 런타임 내에서 한 번 이상 실행되었습니다.<br /><br /> 고유한 스레드만 추적됩니다. 런타임에 다시 실행되거나 스레드가 종료된 후 다시 만들어진 동일한 스레드 ID를 가진 스레드는 두 번 계산되지 않습니다.|  
|**# of total recognized Threads**|응용 프로그램이 시작된 이후 런타임에서 인식된 스레드의 총수를 표시합니다. 이 스레드는 해당하는 관리되는 스레드 개체와 연결됩니다. 런타임에서 이 스레드를 만들지는 않지만 런타임 내에서 한 번 이상 실행되었습니다.<br /><br /> 고유한 스레드만 추적됩니다. 런타임에 다시 실행되거나 스레드가 종료된 후 다시 만들어진 동일한 스레드 ID를 가진 스레드는 두 번 계산되지 않습니다.|  
|**Contention Rate / Sec**|런타임에서 관리되는 잠금을 얻는 데 실패한 스레드의 비율을 표시합니다.|  
|**Current Queue Length**|응용 프로그램에서 현재 관리되는 잠금을 얻기 위해 대기 중인 스레드의 총수를 표시합니다. 이 카운터는 시간별 평균이 아니라 마지막으로 관찰된 값을 표시합니다.|  
|**Queue Length / sec**|응용 프로그램에서 잠금을 얻기 위해 대기 중인 초당 스레드 수를 표시합니다. 이 카운터는 평균 초과 시간이 아니며, 샘플 간격으로 나뉜 마지막 두 개의 샘플에서 관찰된 값의 차이를 표시합니다.|  
|**Queue Length Peak**|응용 프로그램이 시작된 이후 관리되는 잠금을 얻기 위해 대기한 스레드의 총수를 표시합니다.|  
|**rate of recognized threads / sec**|런타임에서 인식된 초당 스레드 수를 표시합니다. 이 스레드는 해당하는 관리되는 스레드 개체와 연결됩니다. 런타임에서 이 스레드를 만들지는 않지만 런타임 내에서 한 번 이상 실행되었습니다.<br /><br /> 고유한 스레드만 추적됩니다. 런타임에 다시 실행되거나 스레드가 종료된 후 다시 만들어진 동일한 스레드 ID를 가진 스레드는 두 번 계산되지 않습니다.<br /><br /> 이 카운터는 평균 초과 시간이 아니며, 샘플 간격으로 나뉜 마지막 두 개의 샘플에서 관찰된 값의 차이를 표시합니다.|  
|**Total # of Contentions**|런타임의 스레드가 관리되는 잠금을 얻는 데 실패한 총 횟수를 표시합니다.|  
  
<a name="memory"></a>   
## <a name="memory-performance-counters"></a>메모리 성능 카운터  
 성능 콘솔 .NET CLR 메모리 범주에는 가비지 수집기에 대한 정보를 제공하는 카운터가 포함됩니다. 다음 표에서는 이러한 성능 카운터에 대해 설명합니다.  
  
|성능 카운터|설명|  
|-------------------------|-----------------|  
|**# Bytes in all Heaps**|**Gen 1 Heap Size**, **Gen 2 Heap Size** 및 **Large Object Heap Size** 카운터의 합계를 표시합니다. 이 카운터는 가비지 컬렉션 힙에 할당된 현재 메모리 크기(바이트)를 나타냅니다.|  
|**# GC Handles**|사용 중인 가비지 컬렉션 핸들의 현재 개수를 표시합니다. 가비지 컬렉션 핸들은 공용 언어 런타임 및 관리되는 환경의 외부 리소스에 대한 핸들입니다.|  
|**# Gen 0 Collections**|응용 프로그램이 시작된 이후 0세대 개체(즉, 가장 최근에 할당된 개체)가 가비지 수집된 횟수를 표시합니다.<br /><br /> 0세대 가비지 수집은 0세대에서 사용 가능한 메모리가 할당 요청을 충족하기에 충분하지 않을 때 발생합니다. 이 카운터는 0세대 가비지 수집이 끝날 때 증가됩니다. 상위 세대 가비지 수집에는 하위 세대 수집이 모두 포함됩니다. 이 카운터는 상위 세대(1세대 또는 2세대) 가비지 수집이 발생할 때 명시적으로 증가됩니다.<br /><br /> 이 카운터는 마지막으로 관찰된 값을 표시합니다. **_Global\_** 카운터 값은 정확하지 않으며 무시해야 합니다.|  
|**# Gen 1 Collections**|응용 프로그램이 시작된 이후 1세대 개체가 가비지 수집된 횟수를 표시합니다.<br /><br /> 이 카운터는 1세대 가비지 수집이 끝날 때 증가됩니다. 상위 세대 가비지 수집에는 하위 세대 수집이 모두 포함됩니다. 이 카운터는 상위 세대(2세대) 가비지 수집이 발생할 때 명시적으로 증가됩니다.<br /><br /> 이 카운터는 마지막으로 관찰된 값을 표시합니다. **_Global\_** 카운터 값은 정확하지 않으며 무시해야 합니다.|  
|**# Gen 2 Collections**|응용 프로그램이 시작된 이후 2세대 개체가 가비지 수집된 횟수를 표시합니다. 이 카운터는 2세대 가비지 수집(전체 가비지 수집이라고도 함)이 끝날 때 증가됩니다.<br /><br /> 이 카운터는 마지막으로 관찰된 값을 표시합니다. **_Global\_** 카운터 값은 정확하지 않으며 무시해야 합니다.|  
|**# Induced GC**|명시적 <xref:System.GC.Collect%2A?displayProperty=nameWithType> 호출로 인해 가비지 컬렉션이 수행된 최대 횟수를 표시합니다. 가비지 수집기가 컬렉션 빈도를 조정하도록 하는 것이 좋습니다.|  
|**# of Pinned Objects**|마지막 가비지 컬렉션에서 발생한 고정된 개체 수를 표시합니다. 고정된 개체는 가비지 수집기가 메모리에서 이동할 수 없는 개체입니다. 이 카운터는 가비지 수집된 힙에서만 고정된 개체를 추적합니다. 예를 들어 0세대 가비지 컬렉션에서는 0세대 힙의 고정된 개체만 열거됩니다.|  
|**# of Sink Blocks in use**|사용 중인 동기화 블록의 수를 나타냅니다. 동기화 블록은 동기화 정보를 저장하는 데 할당된 개체별 데이터 구조입니다. 동기화 블록은 관리되는 개체에 대한 약한 참조를 가지며 가비지 수집기에 의해 스캔됩니다. 동기화 블록에 동기화 정보뿐 아니라 COM interop 메타데이터를 저장할 수도 있습니다. 이 카운터는 동기화 기본 형식을 많이 사용할 때 발생하는 성능 문제를 나타냅니다.|  
|**# Total committed Bytes**|가비지 컬렉션기에서 현재 커밋된 가상 메모리 크기(바이트)를 표시합니다. 커밋된 메모리는 디스크 페이징 파일에 공간이 예약된 실제 메모리입니다.|  
|**# Total reserved Bytes**|가비지 수집기에서 현재 예약한 가상 메모리의 양을 바이트 단위로 표시합니다. 예약한 메모리는 디스크 또는 주 메모리 페이지가 아직 사용되지 않았을 때 응용 프로그램에 예약된 가상 메모리 공간입니다.|  
|**% Time in GC**|마지막 가비지 컬렉션 주기 이후 가비지 컬렉션을 수행하는 데 소요된 경과 시간의 백분율을 표시합니다. 이 카운터는 일반적으로 가비지 수집기에서 응용 프로그램을 대신하여 메모리를 수집 및 압축하기 위해 수행한 작업을 나타냅니다. 이 카운터는 각 가비지 수집이 끝날 때만 업데이트됩니다. 이 카운터는 평균이 아니며 마지막으로 관찰된 값이 카운터 값에 반영됩니다.|  
|**Allocated Bytes/second**|가비지 컬렉션 힙에 할당된 초당 바이트 수를 표시합니다. 이 카운터는 각 할당이 아니라 가비지 수집이 끝날 때마다 업데이트됩니다. 이 카운터는 평균 초과 시간이 아니며, 샘플 간격으로 나뉜 마지막 두 개의 샘플에서 관찰된 값의 차이를 표시합니다.|  
|**Finalization Survivors**|종료 대기 중이므로 컬렉션 후에 유지되는 가비지 수집된 개체 수를 표시합니다. 이 개체가 다른 개체에 대한 참조를 포함하는 경우 해당 개체도 유지되지만 이 카운터에서 계산되지는 않습니다. **Promoted Finalization-Memory from Gen 0** 카운터는 종료로 인해 남아 있는 모든 메모리를 표시합니다.<br /><br /> 이 카운터는 누적되지 않으며, 가비지 컬렉션이 끝날 때마다 해당 컬렉션 중에 유지된 항목 수로 업데이트됩니다. 이 카운터는 종료로 인해 응용 프로그램에서 발생할 수 있는 추가 오버헤드를 나타냅니다.|  
|**Gen 0 heap size**|0세대에 할당할 수 있는 최대 바이트 수를 표시합니다. 0세대에 할당된 현재 바이트 수를 나타내지 않습니다.<br /><br /> 0세대 가비지 수집은 마지막 수집 이후의 할당이 이 크기를 초과할 때 발생합니다. 0세대 크기는 가비지 수집기에서 조정되며 응용 프로그램 실행 중에 변경될 수 있습니다. 0세대 수집이 끝나면 0세대 힙 크기가 0바이트가 됩니다. 이 카운터는 다음 0세대 가비지 수집을 호출하는 할당 크기(바이트)를 표시합니다.<br /><br /> 이 카운터는 각 할당이 아니라 가비지 컬렉션이 끝날 때 업데이트됩니다.|  
|**Gen 0 Promoted Bytes/Sec**|0세대에서 1세대로 수준이 올려진 초당 바이트 수를 표시합니다. 메모리는 가비지 수집 후에 유지될 때 수준이 올려집니다. 이 카운터는 초당 만들어지는 비교적 수명이 긴 개체 수를 나타냅니다.<br /><br /> 이 카운터는 마지막 두 샘플에서 관찰된 값의 차이를 샘플 간격 기간으로 나눈 값을 표시합니다.|  
|**Gen 1 heap size**|1세대의 현재 바이트 수를 표시합니다. 이 카운터는 1세대의 최대 크기를 표시하지 않습니다. 개체는 이 세대에 직접 할당되지 않고 이전 0세대 가비지 수집에서 수준이 올려집니다. 이 카운터는 각 할당이 아니라 가비지 컬렉션이 끝날 때 업데이트됩니다.|  
|**Gen 1 Promoted Bytes/Sec**|1세대에서 2세대로 수준이 올려진 초당 바이트 수를 표시합니다. 단지 종료 대기 중이므로 수준이 올려진 개체는 이 카운터에 포함되지 않습니다.<br /><br /> 메모리는 가비지 수집 후에 유지될 때 수준이 올려집니다. 최상위 세대이므로 2세대에서 수준이 올려지는 항목은 없습니다. 이 카운터는 초당 만들어지는 매우 수명이 긴 개체 수를 나타냅니다.<br /><br /> 이 카운터는 마지막 두 샘플에서 관찰된 값의 차이를 샘플 간격 기간으로 나눈 값을 표시합니다.|  
|**Gen 2 heap size**|2세대의 현재 바이트 수를 표시합니다. 개체는 이 세대에 직접 할당되지 않고 이전 1세대 가비지 수집 중 1세대에서 수준이 올려집니다. 이 카운터는 각 할당이 아니라 가비지 컬렉션이 끝날 때 업데이트됩니다.|  
|**Large Object Heap size**|대형 개체 힙의 현재 크기(바이트)를 표시합니다. 85,000바이트보다 큰 개체는 가비지 수집기에서 대형 개체로 처리되며, 특별한 힙에 직접 할당하기 때문에 이 개체는 세대 간에 수준이 오르지 않습니다. 이 카운터는 각 할당이 아니라 가비지 컬렉션이 끝날 때 업데이트됩니다.|  
|**프로세스 ID**|모니터링 중인 CLR 프로세스 인스턴스의 프로세스 ID를 표시합니다.|  
|**Promoted Finalization-Memory from Gen 0**|단지 종료 대기 중이므로 0세대에서 1세대로 수준이 올려진 메모리 크기(바이트)를 표시합니다. 이 카운터는 누적되지 않으며, 마지막 가비지 컬렉션이 끝날 때 관찰된 값을 표시합니다.|  
|**Promoted Memory from Gen 0**|가비지 컬렉션 후에 유지되고 0세대에서 1세대로 수준이 올려진 메모리 크기(바이트)를 표시합니다. 단지 종료 대기 중이므로 수준이 올려진 개체는 이 카운터에 포함되지 않습니다. 이 카운터는 누적되지 않으며, 마지막 가비지 컬렉션이 끝날 때 관찰된 값을 표시합니다.|  
|**Promoted Memory from Gen 1**|가비지 컬렉션 후에 유지되고 1세대에서 2세대로 수준이 올려진 메모리 크기(바이트)를 표시합니다. 단지 종료 대기 중이므로 수준이 올려진 개체는 이 카운터에 포함되지 않습니다. 이 카운터는 누적되지 않으며, 마지막 가비지 수집이 끝날 때 관찰된 값을 표시합니다. 마지막 가비지 수집이 0세대만 수집하는 경우 이 카운터는 0으로 다시 설정됩니다.|  
  
<a name="networking"></a>   
## <a name="networking-performance-counters"></a>네트워킹 성능 카운터  
 성능 콘솔 .NET CLR 네트워킹 범주에는 응용 프로그램이 네트워크를 통해 보내고 받는 데이터에 대한 정보를 제공하는 카운터가 포함됩니다. 다음 표에서는 이러한 성능 카운터에 대해 설명합니다.  
  
|성능 카운터|설명|  
|-------------------------|-----------------|  
|**Bytes Received**|프로세스가 시작된 이후 <xref:System.AppDomain> 내의 모든 <xref:System.Net.Sockets.Socket> 개체가 받은 바이트 수의 누적 합계입니다. 이 개수에는 TCP/IP에서 정의되지 않은 데이터 및 프로토콜 정보가 포함됩니다.|  
|**Bytes Sent**|프로세스가 시작된 이후 <xref:System.AppDomain> 내의 모든 <xref:System.Net.Sockets.Socket> 개체가 보낸 바이트 수의 누적 합계입니다. 이 개수에는 TCP/IP에서 정의되지 않은 데이터 및 프로토콜 정보가 포함됩니다.|  
|**Connections Established**|프로세스가 시작된 이후 <xref:System.AppDomain> 내에서 연결된 스트림 소켓에 대한 <xref:System.Net.Sockets.Socket> 개체 수의 누적 합계입니다.|  
|**Datagrams Received**|프로세스가 시작된 이후 <xref:System.AppDomain> 내의 모든 <xref:System.Net.Sockets.Socket> 개체가 받은 데이터그램 패킷 수의 누적 합계입니다.|  
|**Datagrams Sent**|프로세스가 시작된 이후 <xref:System.AppDomain> 내의 모든 <xref:System.Net.Sockets.Socket> 개체가 보낸 데이터그램 패킷 수의 누적 합계입니다.|  
|**HttpWebRequest Average Lifetime**|프로세스가 시작된 이후 <xref:System.AppDomain> 내에서 마지막 간격에 끝난 모든 <xref:System.Net.HttpWebRequest> 개체의 평균 완료 시간입니다.|  
|**HttpWebRequest Average Queue Time**|프로세스가 시작된 이후 <xref:System.AppDomain> 내에서 마지막 간격에 큐에서 제거된 모든 <xref:System.Net.HttpWebRequest> 개체의 평균 큐 대기 시간입니다.|  
|**HttpWebRequests Created/sec**|<xref:System.AppDomain> 내에서 초당 만들어진 <xref:System.Net.HttpWebRequest> 개체 수입니다.|  
|**HttpWebRequests Queued/sec**|<xref:System.AppDomain> 내에서 초당 큐에 추가된 <xref:System.Net.HttpWebRequest> 개체 수입니다.|  
|**HttpWebRequests Aborted/sec**|<xref:System.AppDomain> 내에서 초당 응용 프로그램이 <xref:System.Net.HttpWebRequest.Abort%2A> 메서드를 호출한 <xref:System.Net.HttpWebRequest> 개체 수입니다.|  
|**HttpWebRequests Failed/sec**|<xref:System.AppDomain> 내에서 초당 서버로부터 실패 상태 코드를 받은 <xref:System.Net.HttpWebRequest> 개체 수입니다.|  
  
 지원되는 네트워킹 성능 카운터의 클래스는 다음과 같습니다.  
  
- 일부 이벤트가 발생한 횟수를 측정하는 이벤트 카운터  
  
- 보내거나 받은 데이터 수량을 측정하는 데이터 카운터  
  
- 각 프로세스의 소요 시간을 측정하는 기간 카운터 개체가 다른 상태에서 전환된 후 각 간격(일반적으로 초 단위)마다 개체에서 시간을 측정합니다.  
  
- 간격당(일반적으로 초당) 특정 전환을 수행하는 개체 수를 측정하는 간격당 카운터  
  
 이벤트에 대한 네트워킹 성능 카운터는 다음과 같습니다.  
  
- **Connections Established**  
  
- **Datagrams Received**  
  
- **Datagrams Sent**  
  
 이러한 성능 카운터는 프로세스가 시작된 이후의 개수를 제공합니다. 설정된 <xref:System.Net.Sockets.Socket> 연결 수에는 설정된 스트림 소켓 연결에 대한 응용 프로그램의 명시적 <xref:System.Net.Sockets.Socket> 메서드 호출 및 <xref:System.Net.Sockets.Socket> 클래스에 대한 다른 클래스(예: <xref:System.Net.HttpWebRequest>, <xref:System.Net.FtpWebRequest>, <xref:System.Net.WebClient> 및 <xref:System.Net.Sockets.TcpClient>)의 내부 호출이 포함됩니다.  
  
 **Datagrams Received** 및 **Datagrams Sent** 개수에는 응용 프로그램의 명시적 <xref:System.Net.Sockets.Socket> 메서드 호출 및 <xref:System.Net.Sockets.Socket> 클래스에 대한 다른 클래스(예: <xref:System.Net.Sockets.UdpClient>)의 내부 호출을 사용하여 보냈거나 받은 데이터그램 패킷이 포함됩니다. **Datagrams Received** 및 **Datagrams Sent** 개수를 통해 데이터그램의 평균 크기를 가정하여 데이터그램으로 보냈거나 받은 바이트 수의 대략적인 측정값을 제공할 수도 있습니다.  
  
 데이터에 대한 네트워킹 성능 카운터는 다음과 같습니다.  
  
- **Bytes Received**  
  
- **Bytes Sent**  
  
 위 카운터는 프로세스가 시작된 이후의 바이트 수를 제공합니다.  
  
 <xref:System.Net.HttpWebRequest> 개체가 전체 수명 주기나 일부만 통과하는 데 소요된 시간을 측정하는 다음 두 개의 기간 카운터가 있습니다.  
  
- **HttpWebRequest Average Lifetime**  
  
- **HttpWebRequest Average Queue Time**  
  
 **HttpWebRequest Average Lifetime** 카운터의 경우 대부분의 <xref:System.Net.HttpWebRequest> 개체 수명은 항상 개체를 만든 시간부터 응용 프로그램이 응답 스트림을 닫은 시간까지입니다. 두 가지 특수한 경우는 다음과 같습니다.  
  
- 응용 프로그램이 <xref:System.Net.HttpWebRequest.GetResponse%2A> 또는 <xref:System.Net.HttpWebRequest.BeginGetResponse%2A> 메서드를 호출하지 않는 경우 <xref:System.Net.HttpWebRequest> 개체의 수명은 무시됩니다.  
  
- <xref:System.Net.HttpWebRequest> 개체가 <xref:System.Net.HttpWebRequest.GetResponse%2A> 또는 <xref:System.Net.HttpWebRequest.EndGetResponse%2A> 메서드를 호출할 때 <xref:System.Net.WebException>이 발생하는 경우 수명은 예외가 발생할 때 종료됩니다. 기술적으로, 기본 응답 스트림도 해당 시점에 닫힙니다(사용자에게 반환되는 응답 스트림은 실제로 응답 스트림의 복사본을 포함하는 메모리 스트림임).  
  
 간격당 특정 <xref:System.Net.HttpWebRequest> 개체 문제를 추적하는 4개의 카운터가 있습니다. 이러한 성능 카운터는 응용 프로그램 개발자, 관리자 및 지원 담당자가 <xref:System.Net.HttpWebRequest> 개체의 성능을 파악하는 데 도움이 됩니다. 해당 카운터는 다음과 같습니다.  
  
- **HttpWebRequests Created/sec**  
  
- **HttpWebRequests Queued/sec**  
  
- **HttpWebRequests Aborted/sec**  
  
- **HttpWebRequests Failed/sec**  
  
 **HttpWebRequests Aborted/sec** 카운터의 경우 <xref:System.Net.HttpWebRequest.Abort%2A>에 대한 내부 호출도 계산됩니다. 이러한 내부 호출은 일반적으로 응용 프로그램이 측정하려는 시간 제한에 의해 발생합니다.  
  
 **HttpWebRequests Failed/sec** 카운터에는 초당 서버로부터 실패 상태 코드를 받은 <xref:System.Net.HttpWebRequest> 개체 수가 포함됩니다. 이는 요청이 끝날 때 HTTP 서버로부터 받은 상태 코드가 200에서 299 사이의 범위에 없음을 의미합니다. 처리된 후 새 요청을 생성하는 상태 코드(예: 대부분의 401 권한이 없음 상태 코드)는 다시 시도 결과에 따라 실패 여부가 결정됩니다. 다시 시도에 따라 응용 프로그램에 오류가 표시되는 경우 이 카운터가 증가합니다.  
  
 네트워킹 성능 카운터는 <xref:System.Diagnostics> 네임스페이스의 <xref:System.Diagnostics.PerformanceCounter> 및 관련 클래스를 통해 액세스하고 관리할 수 있습니다. Windows 성능 모니터 콘솔을 통해 네트워킹 성능 카운터를 볼 수도 있습니다.  
  
 네트워킹 성능 카운터를 사용하려면 구성 파일에서 사용하도록 설정해야 합니다. 구성 파일의 단일 설정을 통해 모든 네트워킹 성능 카운터를 사용하거나 사용하지 않도록 설정합니다. 개별 네트워킹 성능 카운터를 사용하거나 사용하지 않도록 설정할 수는 없습니다. 자세한 내용은 [\<performanceCounter> 요소(네트워크 설정)](../configure-apps/file-schema/network/performancecounter-element-network-settings.md)를 참조하세요.  
  
 네트워킹 카운터를 사용하도록 설정하면 AppDomain별 성능 카운터와 전역 성능 카운터가 모두 생성 및 업데이트됩니다. 사용하지 않도록 설정하면 응용 프로그램이 네트워킹 성능 카운터 데이터를 제공하지 않습니다.  
  
 성능 카운터는 범주로 그룹화되어 있습니다. 다음 예제 코드를 사용하여 응용 프로그램에 모든 범주를 나열할 수 있습니다.  
  
```csharp
PerformanceCounterCategory[] Array = PerformanceCounterCategory.GetCategories();  
for (int i = 0; i < Array.Length; i++)  
{  
    Console.Out.WriteLine("{0}. Name={1} Help={2}", i, Array[i].CategoryName, Array[i].CategoryHelp);  
}  
```  
  
 네트워킹 성능 카운터는 다음 두 가지 범주에 나열됩니다.  
  
- ".NET CLR 네트워킹" - .NET Framework 버전 2에서 도입되었으며 .NET Framework 버전 2 이상에서 지원되는 원래 성능 카운터  
  
- ".NET CLR 네트워킹 4.0.0.0" - 위의 모든 소켓 카운터 및 .NET Framework 버전 4 이상에서 지원되는 새 성능 카운터 이러한 새 카운터는 <xref:System.Net.HttpWebRequest> 개체에 대한 성능 정보를 제공합니다.  
  
 애플리케이션에서 성능 카운터에 액세스하고 관리하는 방법에 대한 자세한 내용은 [성능 카운터](performance-counters.md)를 참조하세요.  
  
<a name="security"></a>   
## <a name="security-performance-counters"></a>보안 성능 카운터  
 성능 콘솔 .NET CLR 보안 범주에는 공용 언어 런타임이 응용 프로그램에 대해 수행하는 보안 검사에 대한 정보를 제공하는 카운터가 포함됩니다. 다음 표에서는 이러한 성능 카운터에 대해 설명합니다.  
  
|성능 카운터|설명|  
|-------------------------|-----------------|  
|**# Link Time Checks**|응용 프로그램이 시작된 이후 링크 타임 코드 액세스 보안 검사의 총수를 표시합니다. 링크 타임 코드 액세스 보안 검사는 호출자가 JIT(Just-In-Time) 컴파일 타임에 특정 권한을 요구하는 경우에 수행됩니다. 링크 타임 검사는 호출자당 한 번 수행됩니다. 이 개수는 심각한 성능 문제가 아니라 단순히 보안 시스템 동작을 나타냅니다.|  
|**% Time in RT checks**|마지막 샘플 이후 런타임 코드 액세스 보안 검사를 수행하는 데 소요된 경과 시간의 백분율을 표시합니다. 이 카운터는 .NET Framework 보안 검사가 끝날 때 업데이트됩니다. 평균이 아니라 마지막으로 관찰된 값을 나타냅니다.|  
|**% Time Sig Authenticating**|나중에 사용하기 위해 예약되어 있습니다.|  
|**Stack Walk Depth**|마지막 런타임 코드 액세스 보안 검사 중 스택의 깊이를 표시합니다. 런타임 코드 액세스 보안 검사는 스택을 따라 수행됩니다. 이 카운터는 평균이 아니라 마지막으로 관찰된 값만 표시합니다.|  
|**Total Runtime Checks**|응용 프로그램이 시작된 이후 수행된 런타임 코드 액세스 보안 검사의 총수를 표시합니다. 런타임 코드 액세스 보안 검사는 호출자가 특정 권한을 요구하는 경우에 수행됩니다. 런타임 검사는 호출자에 의해 각 호출에서 수행되고 호출자의 현재 스레드 스택을 검사합니다. **Stack Walk Depth** 카운터와 함께 사용할 경우 이 카운터는 보안 검사에 대해 발생하는 성능 저하를 나타냅니다.|  
  
## <a name="see-also"></a>참고자료

- [성능 카운터](performance-counters.md)
- [런타임 프로파일링](runtime-profiling.md)
