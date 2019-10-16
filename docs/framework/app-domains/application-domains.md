---
title: 애플리케이션 도메인
ms.date: 03/30/2017
helpviewer_keywords:
- process boundaries for isolation
- application isolation
- application domains, about
- common language runtime, application domains
- application domains
- runtime, application domains
- isolation between applications
- code, verification process
- verification testing code
ms.assetid: 113a8bbf-6875-4a72-a49d-ca2d92e19cc8
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0ce9d5f706a473d64e97fb02e0426060878d9c75
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834025"
---
# <a name="application-domains"></a>애플리케이션 도메인

운영 체제와 런타임 환경은 일반적으로 애플리케이션 간에 몇 가지 형식의 격리를 제공합니다. 예를 들어 Windows에서는 프로세스를 사용하여 애플리케이션을 격리합니다. 격리는 한 애플리케이션에서 실행 중인 코드가 서로 관련 없는 다른 애플리케이션에 나쁜 영향을 주지 않도록 하기 위해 필요합니다.  
  
 애플리케이션 도메인은 보안, 안정성, 버전 관리, 어셈블리 언로드를 위해 격리 경계를 제공합니다. 애플리케이션 도메인은 일반적으로 애플리케이션이 실행되기 전에 공용 언어 런타임을 부트스트래핑해야 하는 런타임 호스트에 의해 만들어집니다.  
  
## <a name="the-benefits-of-isolating-applications"></a>애플리케이션 격리의 장점

 지금까지는 동일한 컴퓨터에서 실행 중인 여러 애플리케이션을 격리시키기 위해 프로세스 경계를 사용했습니다. 각 애플리케이션은 독립된 프로세스에 로드되어 동일한 컴퓨터에서 실행 중인 다른 컴퓨터와 격리됩니다.  
  
 메모리 주소는 프로세스에 상대적이고 한 프로세스에서 다른 프로세스로 전달된 메모리 포인터는 대상 프로세스에서 의미 있는 방식으로 사용될 수 없으므로 애플리케이션이 격리됩니다. 또한 두 프로세스를 서로 직접 호출할 수 없습니다. 대신 간접 참조 수준을 제공하는 프록시를 사용해야 합니다.  
  
 관리 코드는 확인 프로세스를 통과해야 실행할 수 있습니다. 단, 관리자가 이 프로세스를 건너 뛸 수 있는 권한을 부여한 경우는 예외입니다. 확인 프로세스는 해당 코드가 잘못된 메모리 주소에 액세스할 수 있는지 또는 실행 중인 프로세스를 정상적으로 작동할 수 없게 하는 일부 다른 작업을 수행할 수 있는지 등을 확인합니다. 확인 테스트를 통과하는 코드를 형식이 안전한 코드라고 합니다. 코드를 형식에 안전하다고 확인하는 기능을 통해 공용 언어 런타임에서는 성능상의 손실을 낮추고 프로세스 경계 만큼의 높은 격리 수준을 제공합니다.  
  
 애플리케이션 도메인은 공용 언어 런타임에서 애플리케이션 간에 격리를 제공하기 위해 사용할 수 있는 더욱 안전한 다용도의 처리 단위를 제공합니다. 사용자는 여러 애플리케이션 도메인을 하나의 프로세스에서 실행할 때, 별개의 프로세스에 존재하도록 동일한 격리 수준을 유지하면서도 프로세스 간에 크로스 프로세스 호출 또는 전환으로 인한 추가 오버헤드가 발생하지 않도록 할 수 있습니다. 단일 프로세스에서 여러 애플리케이션을 실행할 수 있는 기능을 통해 서버 확장성이 상당히 증가합니다.  
  
 또한 애플리케이션 격리는 애플리케이션 보안 측면에서도 중요합니다. 예를 들면 각 컨트롤이 서로의 데이터와 리소스에 액세스할 수 없는 방식으로 여러 웹 애플리케이션의 컨트롤을 단일 브라우저 프로세스에서 실행할 수 있습니다.  
  
 애플리케이션 도메인에서 제공하는 격리에는 다음과 같은 몇 가지 이점이 있습니다.  
  
- 한 애플리케이션에서 발생한 오류가 다른 애플리케이션에 영향을 주지 않습니다. 형식이 안전한 코드는 메모리 오류를 일으킬 수 없으므로 애플리케이션 도메인을 사용하면 한 도메인에서 실행 중인 코드가 프로세스의 다른 애플리케이션에 영향을 줄 수 없습니다.  
  
- 전체 프로세스를 중지하지 않고 개별 애플리케이션만 중지할 수 있습니다. 애플리케이션 도메인을 사용하면 단일 애플리케이션에서 실행 중인 코드를 언로드할 수 있습니다.  
  
    > [!NOTE]
    > 개별 어셈블리 또는 형식은 언로드할 수 없습니다. 전체 도메인만 언로드할 수 있습니다.  
  
- 한 애플리케이션에서 실행 중인 코드가 다른 애플리케이션의 코드 또는 리소스에 직접 액세스할 수 없습니다. 공용 언어 런타임은 다른 애플리케이션 도메인의 개체를 서로 직접 호출할 수 없도록 하여 이러한 격리를 적용합니다. 도메인 사이를 통과하는 개체는 복사되거나 프록시에 의해 액세스됩니다. 개체가 복사되는 경우 해당 개체에 대한 호출은 로컬입니다. 즉, 참조되는 개체와 호출자 둘 다 같은 애플리케이션 도메인에 있습니다. 프록시를 통해 개체가 액세스되는 경우 해당 개체에 대한 호출은 원격입니다. 이 경우 참조되는 개체와 호출자는 서로 다른 애플리케이션 도메인에 있습니다. 크로스 도메인 호출은 두 프로세스 또는 두 컴퓨터 사이의 호출과 동일한 원격 호출 인프라를 사용합니다. 따라서 메서드 호출을 올바르게 JIT로 컴파일할 수 있도록 하기 위해 참조되는 개체의 메타데이터를 두 애플리케이션 도메인에서 모두 사용할 수 있어야 합니다. 호출하는 도메인이 호출되는 개체의 메타데이터에 액세스할 수 없는 경우 <xref:System.IO.FileNotFoundException> 형식의 예외가 발생하여 컴파일할 수 없습니다. 자세한 내용은 [Remote Objects](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))을 참조하세요. 도메인 사이에서 개체에 액세스할 수 있는 방법을 결정하는 메커니즘은 개체에 의해 결정됩니다. 자세한 내용은 <xref:System.MarshalByRefObject?displayProperty=nameWithType>을 참조하세요.  
  
- 코드의 동작 범위는 해당 코드가 실행되는 애플리케이션에 의해 지정됩니다. 즉, 애플리케이션 도메인은 애플리케이션 버전 정책, 액세스하는 원격 어셈블리의 위치, 도메인으로 로드하는 어셈블리를 찾을 위치 관련 정보 등의 구성 설정을 제공합니다.  
  
- 코드에 부여된 권한은 해당 코드가 실행 중인 애플리케이션 도메인에서 제어할 수 있습니다.  
  
## <a name="application-domains-and-assemblies"></a>애플리케이션 도메인 및 어셈블리

 이 섹션에서는 애플리케이션 도메인과 어셈블리 사이의 관계에 대해 설명합니다. 어셈블리에 포함되어 있는 코드를 실행하려면 먼저 해당 어셈블리를 애플리케이션 도메인에 로드해야 합니다. 일반적으로 애플리케이션을 실행하면 여러 어셈블리가 애플리케이션 도메인에 로드됩니다.  
  
 어셈블리가 로드되는 방식에 따라 프로세스에서 여러 애플리케이션 도메인이 해당 어셈블리의 JIT(Just-In-Time) 컴파일된 코드를 공유할 수 있는지 여부와 어셈블리를 프로세스에서 언로드할 수 있는지 여부가 결정됩니다.  
  
- 어셈블리가 도메인 중립적으로 로드된 경우 동일한 보안 권한 부여 집합을 공유하는 모든 애플리케이션 도메인에서 동일한 JIT 컴파일된 코드를 공유할 수 있으므로 애플리케이션에 필요한 메모리가 줄어듭니다. 그러나 어셈블리를 프로세스에서 언로드할 수는 없습니다.  
  
- 어셈블리가 도메인 중립적으로 로드되지 않은 경우 해당 어셈블리가 로드된 모든 애플리케이션 도메인에서 어셈블리를 JIT 컴파일해야 합니다. 그러나 어셈블리가 로드된 모든 애플리케이션 도메인을 언로드하여 프로세스에서 어셈블리를 언로드할 수는 있습니다.  
  
 런타임 호스트는 런타임을 프로세스로 로드하는 경우 도메인 중립적으로 어셈블리를 로드할지 여부를 결정합니다. 관리되는 애플리케이션의 경우 프로세스의 진입점 메서드에 <xref:System.LoaderOptimizationAttribute> 특성을 적용하고 연관된 <xref:System.LoaderOptimization> 열거형의 값을 지정합니다. 공용 언어 런타임을 호스팅하는 관리되지 않는 애플리케이션의 경우 [CorBindToRuntimeEx 함수](../unmanaged-api/hosting/corbindtoruntimeex-function.md) 메서드를 호출할 때 적절한 플래그를 지정합니다.  
  
 도메인 중립 어셈블리를 로드할 수 있는 다음과 같은 세 가지 옵션이 있습니다.  
  
- <xref:System.LoaderOptimization.SingleDomain?displayProperty=nameWithType>에서는 어셈블리를 도메인 중립적으로 로드하지 않습니다. 단, 항상 도메인 중립적으로 로드되는 Mscorlib는 예외입니다. 이 설정은 일반적으로 호스트가 프로세스에서 단일 애플리케이션을 실행 중인 경우에만 사용되므로 단일 도메인이라고 합니다.

- <xref:System.LoaderOptimization.MultiDomain?displayProperty=nameWithType>에서는 모든 어셈블리를 도메인 중립적으로 로드합니다. 프로세스에 여러 애플리케이션 도메인이 있고 모두 동일한 코드를 실행하는 경우 이 설정을 사용합니다.

- <xref:System.LoaderOptimization.MultiDomainHost?displayProperty=nameWithType>에서는 강력한 이름의 어셈블리와 이 어셈블리의 모든 종속 어셈블리가 전역 어셈블리 캐시에 설치되어 있는 경우 강력한 이름의 어셈블리를 도메인 중립적으로 로드합니다. 다른 어셈블리는 해당 어셈블리가 로드되는 각 애플리케이션 도메인에 대해 개별적으로 로드되고 JIT 컴파일되므로 프로세스에서 언로드할 수 있습니다. 동일한 프로세스에서 둘 이상의 애플리케이션을 실행할 경우나 여러 애플리케이션 도메인에서 공유되는 어셈블리와 프로세스에서 언로드해야 하는 어셈블리가 혼합된 경우 이 설정을 사용합니다.
  
 <xref:System.Reflection.Assembly.LoadFrom%2A> 클래스의 <xref:System.Reflection.Assembly> 메서드를 사용하여 로드 컨텍스트로 로드한 어셈블리나 바이트 배열을 지정하는 <xref:System.Reflection.Assembly.Load%2A> 메서드의 오버로드를 사용하여 이미지에서 로드한 어셈블리의 경우 JIT 컴파일된 코드를 공유할 수 없습니다.  
  
 [Ngen.exe(네이티브 이미지 생성기)](../tools/ngen-exe-native-image-generator.md)를 사용하여 네이티브 코드로 컴파일된 어셈블리는 프로세스에 처음 로드될 때 도메인 중립적으로 로드되는 경우 애플리케이션 도메인 간에 공유할 수 있습니다.  
  
 애플리케이션 진입점이 포함된 어셈블리의 JIT 컴파일된 코드는 모든 종속 어셈블리를 공유할 수 있는 경우에만 공유됩니다.  
  
 도메인 중립 어셈블리는 두 번 이상 JIT 컴파일할 수 있습니다. 예를 들어, 보안 권한 부여 집합이 각기 다른 두 애플리케이션 도메인에서 동일한 JIT 컴파일된 코드를 공유할 수 없습니다. 그러나 JIT 컴파일된 어셈블리의 각 복사본은 동일한 권한 부여 집합이 있는 다른 애플리케이션 도메인과 공유할 수 있습니다.  
  
 어셈블리를 도메인 중립적으로 로드할지 여부를 결정할 때는 메모리 사용량 감소와 기타 성능 요인 간의 균형을 조절해야 합니다.  
  
- 도메인 중립 어셈블리의 경우 어셈블리를 격리시켜야 하므로 정적 데이터 및 메서드에 액세스하는 속도가 느립니다. 어셈블리에 액세스하는 각 애플리케이션 도메인은 정적 필드의 개체에 대한 참조가 도메인 경계를 지나지 않도록 정적 데이터의 개별 복사본을 가지고 있어야 합니다. 결과적으로 런타임은 호출자에 추가 논리를 포함시켜서 정적 데이터 또는 메서드의 적절한 복사본으로 사용합니다. 이 추가 논리는 호출 속도를 늦춥니다.  
  
- 어셈블리에 도메인 중립적으로 로드할 수 없는 종속 어셈블리가 있으면 해당 어셈블리가 도메인 중립적으로 로드되지 않으므로 어셈블리를 도메인 중립적으로 로드할 때는 해당 어셈블리의 모든 종속 어셈블리를 찾아서 로드해야 합니다.  
  
## <a name="application-domains-and-threads"></a>애플리케이션 도메인과 스레드

 애플리케이션 도메인은 보안, 버전 관리, 안정성 및 관리 코드 언로드를 위해 격리 경계를 구성합니다. 스레드는 코드를 실행하기 위해 공용 언어 런타임에서 사용하는 운영 체제 구문입니다. 런타임에서 모든 관리 코드는 애플리케이션 도메인에 로드되고 하나 이상의 관리되는 스레드에 의해 실행됩니다.  
  
 애플리케이션 도메인과 스레드 간에는 일대일 상관 관계가 없습니다. 일부 스레드는 어느 시점에서든 단일 애플리케이션 도메인에서 실행될 수 있으며, 특정 스레드는 단일 애플리케이션 도메인으로 제한되지 않습니다. 즉, 스레드는 크로스 애플리케이션 도메인 경계에 종속되지 않고 각 애플리케이션 도메인에 대해 새 스레드가 만들어지지 않습니다.  
  
 어느 시점에서든 모든 스레드는 단일 애플리케이션 도메인에서 실행됩니다. 지정된 애플리케이션 도메인에서 0개, 한 개 또는 여러 개의 스레드가 실행 중일 수 있습니다. 런타임은 애플리케이션 도메인에서 실행 중인 스레드를 추적하므로 사용자는 언제든지 <xref:System.Threading.Thread.GetDomain%2A?displayProperty=nameWithType> 메서드를 호출하여 스레드가 실행되고 있는 도메인을 찾을 수 있습니다.

### <a name="application-domains-and-cultures"></a>애플리케이션 도메인 및 문화권

 스레드와 연결된 <xref:System.Globalization.CultureInfo> 개체로 표현되는 문화권입니다. <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 속성을 사용하여 현재 실행 중인 스레드와 연결된 문화권을 가져오고 <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> 속성을 사용하여 현재 실행 중인 스레드와 연결된 문화권을 가져오거나 설정할 수 있습니다. 스레드와 연결된 문화권을 <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> 속성을 사용하여 명시적으로 설정한 경우, 스레드가 애플리케이션 도메인 경계를 넘나들 때 해당 스레드와 계속해서 연결됩니다. 어느 시점에서 문화권이 스레드와 연결되어 있는지 여부는 스레드가 실행 중인 애플리케이션 도메인의 <xref:System.Globalization.CultureInfo.DefaultThreadCurrentCulture%2A?displayProperty=nameWithType> 속성 값에 의해 결정됩니다.  
  
- 속성 값이 `null`이 아닌 경우, 속성에 의해 반환되는 문화권은 스레드와 연결되어 있습니다. 따라서 <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> 및 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 속성에 의해 반환됩니다.  
  
- 속성 값이 `null`인 경우 현재 시스템 문화권이 스레드와 연결되어 있습니다.  
  
## <a name="programming-with-application-domains"></a>애플리케이션 도메인으로 프로그래밍

 애플리케이션 도메인은 일반적으로 런타임 호스트가 프로그래밍 방식으로 만들고 조작합니다. 그러나 때때로 애플리케이션에서 애플리케이션 도메인을 사용할 수도 있습니다. 예를 들어, 전체 애플리케이션을 중지하지 않고도 도메인과 구성 요소를 언로드할 수 있도록 애플리케이션에서 애플리케이션 구성 요소를 도메인에 로드할 수 있습니다.  
  
 <xref:System.AppDomain>은 애플리케이션 도메인에 대한 프로그래밍 인터페이스입니다. 이 클래스는 도메인을 만들고 언로드하며 도메인에서 형식 인스턴스를 만들고 애플리케이션 도메인 언로드와 같이 다양한 알림을 등록할 수 있는 메서드를 포함합니다. 다음 표에는 자주 사용되는 <xref:System.AppDomain> 메서드가 나열되어 있습니다.  
  
|AppDomain 메서드|설명|  
|----------------------|-----------------|  
|<xref:System.AppDomain.CreateDomain%2A>|새 응용 프로그램 도메인을 만듭니다. <xref:System.AppDomainSetup> 개체를 지정하는 이 메서드의 오버로드를 사용하는 것이 좋습니다. 이 메서드는 애플리케이션 기본 디렉터리 또는 애플리케이션의 루트 디렉터리, 도메인의 구성 파일 위치 및 어셈블리를 도메인에 로드하기 위해 공용 언어 런타임에서 사용할 검색 경로 등 새 도메인의 속성을 설정하는 기본적인 방법입니다.|  
|<xref:System.AppDomain.ExecuteAssembly%2A> 및 <xref:System.AppDomain.ExecuteAssemblyByName%2A>|애플리케이션 도메인에서 어셈블리를 실행합니다. 이 메서드는 인스턴스 메서드이므로 참조할 다른 애플리케이션 도메인에서 코드를 실행하는 데 사용할 수 있습니다.|  
|<xref:System.AppDomain.CreateInstanceAndUnwrap%2A>|애플리케이션 도메인에서 지정한 형식의 인스턴스를 만들고 프록시를 반환합니다. 만들어진 형식을 포함하는 어셈블리가 호출 어셈블리에 로드되지 않도록 하려면 이 메서드를 사용합니다.|  
|<xref:System.AppDomain.Unload%2A>|도메인을 완전 종료합니다. 애플리케이션 도메인은 도메인에서 실행 중인 모든 스레드가 중지되거나 더 이상 도메인에 없을 때까지 언로드되지 않습니다.|  
  
> [!NOTE]
> 공용 언어 런타임에서는 전역 메서드의 serialization을 지원하지 않으므로 다른 애플리케이션 도메인에서 대리자를 사용하여 전역 메서드를 실행할 수 없습니다.  
  
 또한 공용 언어 런타임 호스팅 인터페이스 사양에 설명되어 있는 관리되지 않는 인터페이스를 사용하여 애플리케이션 도메인에 액세스할 수도 있습니다. 런타임 호스트는 비관리 코드에서 인터페이스를 사용하여 프로세스 내에서 애플리케이션 도메인을 만들고 액세스할 수 있습니다.  
  
## <a name="the-complus_loaderoptimization-environment-variable"></a>COMPLUS_LoaderOptimization 환경 변수

 실행 가능한 애플리케이션의 기본 로더 최적화 정책을 설정하는 환경 변수입니다.  
  
### <a name="syntax"></a>구문  
  
```env  
COMPLUS_LoaderOptimization = 1  
```  
  
### <a name="remarks"></a>설명

 일반적인 애플리케이션은 포함된 코드를 실행하기 전에 애플리케이션 도메인에 여러 어셈블리를 로드합니다.  
  
 어셈블리가 로드되는 방식에 따라 프로세스에서 여러 애플리케이션 도메인이 해당 어셈블리의 JIT(Just-In-Time) 컴파일된 코드를 공유할 수 있는지 여부가 결정됩니다.  
  
- 어셈블리가 도메인 중립적으로 로드되는 경우 같은 보안 권한 설정을 공유하는 모든 애플리케이션 도메인은 동일한 JIT-컴파일된 코드를 공유할 수 있습니다. 이렇게 하면 애플리케이션에 필요한 메모리가 줄어듭니다.  
  
- 어셈블리가 도메인 중립적으로 로드되지 않은 경우 로드되는 모든 애플리케이션 도메인에서 JIT-컴파일되어야 하며 로더는 애플리케이션 도메인에서 내부 리소스를 공유해서는 안 됩니다.  
  
 COMPLUS_LoaderOptimization 환경 플래그가 1로 설정되면 런타임 호스트가 모든 어셈블리를 SingleDomain이라는 비 도메인 중립 방식으로 로드합니다. SingleDomain은 어셈블리를 도메인 중립적으로 로드하지 않습니다. 단, 항상 도메인 중립적으로 로드되는 Mscorlib는 예외입니다. 이 설정은 일반적으로 호스트가 프로세스에서 단일 애플리케이션을 실행 중인 경우에만 사용되므로 단일 도메인이라고 합니다.  
  
> [!CAUTION]
> COMPLUS_LoaderOptimization 환경 플래그는 진단 및 테스트 시나리오에 사용할 수 있도록 설계되었습니다. 플래그가 설정되어 있으면 속도가 심각하게 느려지고 메모리 사용량이 증가할 수 있습니다.  
  
### <a name="code-example"></a>코드 예제

 모든 어셈블리를 IISADMIN 서비스에 대해 도메인 중립적으로 로드되지 않게 하려면 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\IISADMIN 키에서 Environment의 다중 문자열 값에 `COMPLUS_LoaderOptimization=1`을 추가합니다.  
  
```env  
Key = HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\IISADMIN  
Name = Environment  
Type = REG_MULTI_SZ  
Value (to append) = COMPLUS_LoaderOptimization=1  
```  
  
## <a name="see-also"></a>참조

- <xref:System.AppDomain?displayProperty=nameWithType>
- <xref:System.MarshalByRefObject?displayProperty=nameWithType>
- [애플리케이션 도메인 및 어셈블리를 사용한 프로그래밍](index.md)
- [애플리케이션 도메인 사용](use.md)
