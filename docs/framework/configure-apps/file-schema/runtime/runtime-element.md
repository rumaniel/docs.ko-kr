---
title: <runtime> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#runtime
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime
helpviewer_keywords:
- <runtime> element
- runtime element
- container tags, <runtime> element
ms.assetid: 1eb2fae3-de4b-45b6-852f-517c39b751bd
ms.openlocfilehash: e703b9739ea93d3c7bf08371bc264bbdcb05b716
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252323"
---
# <a name="runtime-element"></a>\<런타임 > 요소

공용 언어 런타임에서 응용 프로그램을 구성 하는 데 사용 되는 정보를 제공 합니다.

[ **\<configuration>** ](../configuration-element.md)  
&nbsp;&nbsp; **\<runtime>**  

## <a name="syntax"></a>구문

```xml
<runtime>
</runtime>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 자식 요소 및 부모 요소에 대해 설명 합니다.

### <a name="attributes"></a>특성

없음

### <a name="child-elements"></a>자식 요소

|요소|설명|
|-------------|-----------------|
|[\<alwaysFlowImpersonationPolicy>](alwaysflowimpersonationpolicy-element.md)|가장을 수행하는 방법과 관계없이 Windows ID가 항상 비동기 지점 간을 흐르도록 지정합니다.|
|[\<AppContextSwitchOverrides>](appcontextswitchoverrides-element.md)|<xref:System.AppContext> 클래스에 사용되는 스위치를 하나 이상 정의하여 새 기능의 옵트아웃 메커니즘을 제공합니다.|
|[\<appDomainManagerAssembly>](appdomainmanagerassembly-element.md)|프로세스의 기본 애플리케이션 도메인용 애플리케이션 도메인 관리자를 제공하는 어셈블리를 지정합니다.|
|[\<appDomainManagerType>](appdomainmanagertype-element.md)|기본 애플리케이션 도메인용 애플리케이션 도메인 관리자로 사용되는 유형을 지정합니다.|
|[\<appDomainResourceMonitoring>](appdomainresourcemonitoring-element.md)|프로세스의 수명 동안 프로세스의 모든 애플리케이션 도메인에서 통계를 수집하도록 런타임에 명령합니다.|
|[\<assemblyBinding>](assemblybinding-element-for-runtime.md)|어셈블리 버전 리디렉션 및 어셈블리 위치에 대한 정보를 포함합니다.|
|[\<bypassTrustedAppStrongNames>](bypasstrustedappstrongnames-element.md)|신뢰할 수 있는 어셈블리에 대한 강력한 이름 확인을 바이패스할지를 지정합니다.|
|[\<CompatSortNLSVersion>](compatsortnlsversion-element.md)|런타임에 문자열 비교를 수행할 때 레거시 정렬 동작을 사용 하도록 지정 합니다.|
|[\<developmentMode>](developmentmode-element.md)|런타임이 DEVPATH 환경 변수로 지정된 디렉터리에서 어셈블리를 검색할지를 지정합니다.|
|[\<disableCachingBindingFailures>](disablecachingbindingfailures-element.md)|.NET Framework 버전 2.0의 기본 동작인 바인딩 실패의 캐싱을 사용 하지 않도록 설정할지 여부를 지정 합니다.|
|[\<disableCommitThreadStack>](disablecommitthreadstack-element.md)|스레드가 시작될 때 전체 스레드 스택을 커밋할지 여부를 지정합니다.|
|[\<disableFusionUpdatesFromADManager>](disablefusionupdatesfromadmanager-element.md)|런타임 호스트가 애플리케이션 도메인에 대한 구성 설정을 재정의할 수 있도록 허용하는 기본 동작을 사용하지 않도록 설정할지를 지정합니다.|
|[\<EnableAmPmParseAdjustment>](enableampmparseadjustment-element.md)|날짜 및 시간 구문 분석 메서드가 조정된 규칙 집합을 사용하여 일, 월, 시간 및 오전/오후 지정자만 포함하는 날짜 문자열을 구문 분석할지를 결정합니다.|
|[\<enforceFIPSPolicy>](enforcefipspolicy-element.md)|암호화 알고리즘이 FIPS(Federal Information Processing Standards)를 준수해야 하는 컴퓨터 구성 요구 사항을 적용할지를 지정합니다.|
|[\<etwEnable>](etwenable-element.md)|공용 언어 런타임 이벤트에 대해 ETW(Windows용 이벤트 추적)를 사용하도록 설정할지를 지정합니다.|
|[\<forcePerformanceCounterUniqueSharedMemoryReads>](forceperformancecounteruniquesharedmemoryreads-element.md)|PerfCounter.dll이 .NET Framework 버전 1.1 애플리케이션에서 CategoryOptions 레지스트리 설정을 사용하여 성능 카운터 데이터를 범주별 공유 메모리에서 로드할지 또는 전역 메모리에서 로드할지를 결정하도록 지정합니다.|
|[\<gcAllowVeryLargeObjects>](gcallowverylargeobjects-element.md)|64비트 플랫폼에서 총 크기가 2GB보다 큰 배열을 사용하도록 설정합니다.|
|[\<gcConcurrent>](gcconcurrent-element.md)|공용 언어 런타임이 동시에 가비지 수집을 실행 하는지 여부를 지정 합니다.|
|[\<GCCpuGroup>](gccpugroup-element.md)|가비지 수집에서 여러 CPU 그룹을 지원할지를 지정합니다.|
|[\<gcServer>](gcserver-element.md)|공용 언어 런타임이 서버 가비지 컬렉션을 실행하는지 여부를 지정합니다.|
|[\<generatePublisherEvidence>](generatepublisherevidence-element.md)|런타임이 CAS(코드 액세스 보안) 게시자 정책을 사용할지를 지정합니다.|
|[\<legacyCorruptedStateExceptionsPolicy>](legacycorruptedstateexceptionspolicy-element.md)|런타임에서 관리 코드가 액세스 위반 및 기타 손상된 상태 예외를 catch하도록 허용하는지를 지정합니다.|
|[\<legacyImpersonationPolicy>](legacyimpersonationpolicy-element.md)|현재 스레드의 실행 컨텍스트 흐름 설정과 관계없이 Windows ID가 비동기 지점 간을 흐르지 않도록 지정합니다.|
|[\<loadfromRemoteSources>](loadfromremotesources-element.md)|원격 소스의 어셈블리를 완전 신뢰로 로드할지를 지정합니다.|
|[\<NetFx40_LegacySecurityPolicy>](netfx40-legacysecuritypolicy-element.md)|런타임이 레거시 CAS(코드 액세스 보안) 정책을 사용할지를 지정합니다.|
|[\<NetFx40_PInvokeStackResilience>](netfx40-pinvokestackresilience-element.md)|런타임이 잘못된 플랫폼 호출 선언을 실행 시간에 자동으로 수정할지를 지정합니다. 자동 수정을 수행하는 경우 관리 코드와 비관리 코드 간 전환 속도가 느려집니다.|
|[\<NetFx45_CultureAwareComparerGetHashCode_LongStrings>](netfx45-cultureawarecomparergethashcode-longstrings-element.md)|런타임이 <xref:System.StringComparer.GetHashCode%2A?displayProperty=nameWithType> 메서드에 대한 해시 코드를 계산하기 위해 고정된 양의 메모리를 사용할지 여부를 지정합니다.|
|[\<PreferComInsteadOfRemoting>](prefercominsteadofmanagedremoting-element.md)|런타임이 애플리케이션 도메인 경계 간에 원격 모드가 아닌 COM interop를 사용하도록 지정합니다.|
|[\<relativeBindForResources>](relativebindforresources-element.md)|위성 어셈블리에 대한 프로브를 최적화합니다.|
|[\<shadowCopyVerifyByTimeStamp>](shadowcopyverifybytimestamp-element.md)|섀도 복사가 .NET Framework 4에서 도입 된 기본 시작 동작을 사용 하는지 아니면 이전 버전의 .NET Framework의 시작 동작으로 돌아가는지를 지정 합니다.|
|[\<supportPortability>](supportportability-element.md)|애플리케이션 이식성을 위해 어셈블리를 동일하게 간주하는 기본 동작을 사용하지 않도록 설정함으로써, 애플리케이션이 .NET Framework의 서로 다른 두 구현에서 같은 어셈블리를 참조할 수 있도록 지정합니다.|
|[\<system.runtime.caching>](system-runtime-caching-element-cache-settings.md)|기본 메모리 내 개체 캐시에 대한 구성 정보를 제공합니다.|
|[\<Thread_UseAllCpuGroups>](thread-useallcpugroups-element.md)|런타임이 모든 CPU 그룹에 관리되는 스레드를 배포할지를 지정합니다.|
|[\<ThrowUnobservedTaskExceptions>](throwunobservedtaskexceptions-element.md)|작업 예외가 처리되지 않으면 실행 중인 프로세스를 종료할지를 지정합니다.|
|[\<TimeSpan_LegacyFormatMode>](timespan-legacyformatmode-element.md)|런타임이 <xref:System.TimeSpan> 값에 대해 레거시 서식을 사용할지를 지정합니다.|
|[\<useLegacyJit>](uselegacyjit-element.md)|공용 언어 런타임이 Just-In-Time 컴파일에 레거시 64비트 JIT 컴파일러를 사용할지를 결정합니다.|
|[\<UseRandomizedStringHashAlgorithm>](userandomizedstringhashalgorithm-element.md)|런타임이 애플리케이션 도메인별로 문자열의 해시 코드를 계산할지를 지정합니다.|
|[\<UseSmallInternalThreadStacks>](usesmallinternalthreadstacks-element.md)|런타임이 내부적으로 사용하는 특정 스레드를 만들 때 기본 스택 크기가 아닌 명시적 스택 크기를 사용하도록 요청합니다.|

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|

## <a name="remarks"></a>설명

구성 파일의 [ \<런타임 >](runtime-element.md) 섹션에 있는 자식 요소는 응용 프로그램이 실행 되는 방법을 구성 하기 위해 공용 언어 런타임에서 사용 됩니다. 예를 들어 [ \<gcServer >](gcserver-element.md) 요소는 가비지 수집기가 워크스테이션 가비지 컬렉션을 사용 하는지 아니면 서버 [ \<](userandomizedstringhashalgorithm-element.md) 가비지 컬렉션을 사용 하는지 여부를 결정 합니다. UseRandomizedStringHashAlgorithm > 요소 공용 언어 런타임이 응용 프로그램별 또는 응용 프로그램당 도메인 별로 문자열의 해시 코드를 계산할지 여부를 결정 하 고, 요소를 `AppContextSwitchOverrides` 사용 하면 라이브러리 사용자가 라이브러리에서 제공 하는 변경 된 기능을 옵트인 또는 옵트아웃 (opt out) 할 수 있습니다.

런타임 > 섹션의 [ \<](runtime-element.md) 요소는 응용 프로그램 시작 시 공용 언어 런타임에 의해 자동으로 읽힙니다. <xref:System.AppDomainSetup.ConfigurationFile%2A?displayProperty=nameWithType> 속성에 해당 이름을 제공 하 여 기본이 아닌 응용 프로그램 도메인에 대 한 구성 파일을 정의할 수도 있습니다 .이 경우 응용 프로그램 도메인이 로드 될 때 해당 설정이 자동으로 읽힙니다. 응용 프로그램의 구성 파일에서 [ \<런타임 >](runtime-element.md) 섹션의 설정을 직접 읽어야 하는 경우는 거의 없습니다.

## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
