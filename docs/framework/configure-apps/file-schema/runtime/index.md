---
title: 런타임 설정 스키마
ms.date: 03/30/2017
helpviewer_keywords:
- schema runtime settings
- configuration schema [.NET Framework], runtime settings
- runtime settings schema
ms.assetid: f04816ab-110d-4e28-9283-845d6d9a4a68
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5b340ef99b489b66c62971cacedccdfe609d0b1a
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252529"
---
# <a name="runtime-settings-schema"></a>런타임 설정 스키마

런타임 설정은 공용 언어 런타임에서 .NET Framework를 대상으로 하는 애플리케이션을 구성하는 데 사용됩니다.

## <a name="the-runtime-section-and-its-parent-and-child-elements"></a>\<런타임 > 섹션과 해당 부모 및 자식 요소

[\<configuration>](../configuration-element.md)\
&nbsp;&nbsp;[\<runtime>](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<alwaysFlowImpersonationPolicy>](alwaysflowimpersonationpolicy-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<AppContextSwitchOverrides>](appcontextswitchoverrides-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<appDomainManagerAssembly>](appdomainmanagerassembly-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<appDomainManagerType>](appdomainmanagertype-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<appDomainResourceMonitoring>](appdomainresourcemonitoring-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<assemblyBinding>](assemblybinding-element-for-runtime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\<dependentAssembly>](dependentassembly-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\<assemblyIdentity>](assemblyidentity-element-for-runtime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\<bindingRedirect>](bindingredirect-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\<codeBase>](codebase-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\<Y apply >](publisherpolicy-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\<probing>](probing-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\<qualifyAssembly>](qualifyassembly-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\<Supportportability> >](supportportability-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<bypassTrustedAppStrongNames>](bypasstrustedappstrongnames-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<CompatSortNLSVersion>](compatsortnlsversion-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<developmentMode>](developmentmode-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<disableCachingBindingFailures>](disablecachingbindingfailures-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<disableCommitThreadStack>](disablecommitthreadstack-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<disableFusionUpdatesFromADManager>](disablefusionupdatesfromadmanager-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<EnableAmPmParseAdjustment>](enableampmparseadjustment-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<enforceFIPSPolicy>](enforcefipspolicy-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<etwEnable>](etwenable-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<forcePerformanceCounterUniqueSharedMemoryReads>](forceperformancecounteruniquesharedmemoryreads-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<gcAllowVeryLargeObjects>](gcconcurrent-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<gcConcurrent>](gcconcurrent-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<GCCpuGroup>](gccpugroup-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<gcServer>](gcserver-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<generatePublisherEvidence>](generatepublisherevidence-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<legacyCorruptedStateExceptionsPolicy>](legacycorruptedstateexceptionspolicy-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<legacyImpersonationPolicy>](legacyimpersonationpolicy-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<loadfromRemoteSources>](loadfromremotesources-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<NetFx40_LegacySecurityPolicy>](netfx40-legacysecuritypolicy-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<NetFx40_PInvokeStackResilience>](netfx40-pinvokestackresilience-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<NetFx45_CultureAwareComparerGetHashCode_LongStrings>](netfx45-cultureawarecomparergethashcode-longstrings-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<PreferComInsteadOfManagedRemoting>](prefercominsteadofmanagedremoting-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<relativeBindForResources>](relativebindforresources-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<shadowCopyVerifyByTimeStamp>](shadowcopyverifybytimestamp-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<Thread_UseAllCpuGroups>](thread-useallcpugroups-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<ThrowUnobservedTaskExceptions>](throwunobservedtaskexceptions-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<TimeSpan_LegacyFormatMode>](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<useLegacyJit>](uselegacyjit-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<UseRandomizedStringHashAlgorithm>](userandomizedstringhashalgorithm-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<UseSmallInternalThreadStacks>](usesmallinternalthreadstacks-element.md)\
&nbsp;&nbsp;[\<>의 런타임 캐싱](system-runtime-caching-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\<memoryCache >](memorycache-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\<namedCaches >](namedcaches-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\<> 추가](add-element-for-namedcaches.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\<> 지우기](clear-element-for-namedcaches.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\<> 제거](remove-element-for-namedcaches.md)  

## <a name="alphabetical-list-of-runtime-elements"></a>\<런타임 > 요소의 사전순 목록

|요소|설명|
|-------------|-----------------|
|[\<add>](add-element-for-namedcaches.md)|메모리 캐시용으로 명명된 캐시를 `namedCaches` 컬렉션에 추가합니다.|
|[\<alwaysFlowImpersonationPolicy>](alwaysflowimpersonationpolicy-element.md)|가장을 수행하는 방법과 관계없이 Windows ID가 항상 비동기 지점 간을 흐르도록 지정합니다.|
|[\<AppContextSwitchOverrides>](appcontextswitchoverrides-element.md)|<xref:System.AppContext> 클래스에 사용되는 스위치를 하나 이상 정의하여 새 기능의 옵트아웃 메커니즘을 제공합니다.|
|[\<appDomainManagerAssembly>](appdomainmanagerassembly-element.md)|프로세스의 기본 애플리케이션 도메인용 애플리케이션 도메인 관리자를 제공하는 어셈블리를 지정합니다.|
|[\<appDomainManagerType>](appdomainmanagertype-element.md)|기본 애플리케이션 도메인용 애플리케이션 도메인 관리자로 사용되는 유형을 지정합니다.|
|[\<appDomainResourceMonitoring>](appdomainresourcemonitoring-element.md)|프로세스의 수명 동안 프로세스의 모든 애플리케이션 도메인에서 통계를 수집하도록 런타임에 명령합니다.|
|[\<assemblyBinding>](assemblybinding-element-for-runtime.md)|어셈블리 버전 리디렉션 및 어셈블리 위치에 대한 정보를 포함합니다.|
|[\<assemblyIdentity>](assemblyidentity-element-for-runtime.md)|어셈블리에 대한 식별 정보를 포함합니다.|
|[\<bindingRedirect>](bindingredirect-element.md)|어셈블리 버전을 다른 버전으로 리디렉션합니다.|
|[\<bypassTrustedAppStrongNames>](bypasstrustedappstrongnames-element.md)|신뢰할 수 있는 어셈블리에 대한 강력한 이름 확인을 바이패스할지를 지정합니다.|
|[\<clear>](clear-element-for-namedcaches.md)|메모리 캐시에 대해 `namedCaches` 컬렉션을 지웁니다.|
|[\<codeBase>](codebase-element.md)|런타임이 어셈블리를 찾을 수 있는 위치를 지정합니다.|
|[\<CompatSortNLSVersion>](compatsortnlsversion-element.md)|Specifies that the runtime should use legacy sorting behavior when performing string comparisons|
|[\<dependentAssembly>](dependentassembly-element.md)|각 어셈블리에 대한 바인딩 정책 및 어셈블리 위치를 캡슐화합니다.|
|[\<developmentMode>](developmentmode-element.md)|런타임이 DEVPATH 환경 변수로 지정된 디렉터리에서 어셈블리를 검색할지를 지정합니다.|
|[\<disableCachingBindingFailures>](disablecachingbindingfailures-element.md)|.NET Framework 2.0의 기본 동작인 바인딩 실패의 캐싱을 사용 하지 않도록 설정할지 여부를 지정 합니다.|
|[\<disableCommitThreadStack>](disablecommitthreadstack-element.md)|스레드가 시작될 때 전체 스레드 스택을 커밋할지를 지정합니다.|
|[\<disableFusionUpdatesFromADManager>](disablefusionupdatesfromadmanager-element.md)|런타임 호스트가 애플리케이션 도메인에 대한 구성 설정을 재정의할 수 있도록 허용하는 기본 동작을 사용하지 않도록 설정할지를 지정합니다.|
|[\<EnableAmPmParseAdjustment>](enableampmparseadjustment-element.md)|날짜 및 시간 구문 분석 메서드가 조정된 규칙 집합을 사용하여 일, 월, 시간 및 오전/오후 지정자만 포함하는 날짜 문자열을 구문 분석할지를 결정합니다.|
|[\<enforceFIPSPolicy>](enforcefipspolicy-element.md)|암호화 알고리즘이 FIPS(Federal Information Processing Standards)를 준수해야 하는 컴퓨터 구성 요구 사항을 적용할지를 지정합니다.|
|[\<etwEnable>](etwenable-element.md)|공용 언어 런타임 이벤트에 대해 ETW(Windows용 이벤트 추적)를 사용하도록 설정할지를 지정합니다.|
|[\<forcePerformanceCounterUniqueSharedMemoryReads>](forceperformancecounteruniquesharedmemoryreads-element.md)|PerfCounter.dll이 .NET Framework 버전 1.1 애플리케이션에서 CategoryOptions 레지스트리 설정을 사용하여 성능 카운터 데이터를 범주별 공유 메모리에서 로드할지 또는 전역 메모리에서 로드할지를 결정하도록 지정합니다.|
|[\<gcAllowVeryLargeObjects>](gcallowverylargeobjects-element.md)|64비트 플랫폼에서 총 크기가 2GB보다 큰 배열을 사용하도록 설정합니다.|
|[\<gcConcurrent>](gcconcurrent-element.md)|런타임이 동시에 가비지 컬렉션을 실행하는지 여부를 지정합니다.|
|[\<GCCpuGroup>](gccpugroup-element.md)|가비지 수집에서 여러 CPU 그룹을 지원할지를 지정합니다.|
|[\<gcServer>](gcserver-element.md)|공용 언어 런타임이 서버 가비지 컬렉션을 실행하는지 여부를 지정합니다.|
|[\<generatePublisherEvidence>](generatepublisherevidence-element.md)|런타임이 CAS(코드 액세스 보안) 게시자 정책을 사용할지를 지정합니다.|
|[\<legacyCorruptedStateExceptionsPolicy>](legacycorruptedstateexceptionspolicy-element.md)|런타임에서 관리 코드가 액세스 위반 및 기타 손상된 상태 예외를 catch하도록 허용하는지를 지정합니다.|
|[\<legacyImpersonationPolicy>](legacyimpersonationpolicy-element.md)|현재 스레드의 실행 컨텍스트 흐름 설정과 관계없이 Windows ID가 비동기 지점 간을 흐르지 않도록 지정합니다.|
|[\<loadfromRemoteSources>](loadfromremotesources-element.md)|원격 소스의 어셈블리를 완전 신뢰로 로드할지를 지정합니다.|
|[\<memoryCache>](memorycache-element-cache-settings.md)|<xref:System.Runtime.Caching.MemoryCache> 클래스를 기반으로 하는 캐시 구성에 사용되는 요소를 정의합니다.|
|[\<namedCaches>](namedcaches-element-cache-settings.md)|`namedCache` 인스턴스에 대한 구성 설정 컬렉션을 포함합니다.|
|[\<NetFx40_LegacySecurityPolicy>](netfx40-legacysecuritypolicy-element.md)|런타임이 레거시 CAS(코드 액세스 보안) 정책을 사용할지를 지정합니다.|
|[\<NetFx40_PInvokeStackResilience>](netfx40-pinvokestackresilience-element.md)|런타임이 잘못된 플랫폼 호출 선언을 실행 시간에 자동으로 수정할지를 지정합니다. 자동 수정을 수행하는 경우 관리 코드와 비관리 코드 간 전환 속도가 느려집니다.|
|[\<NetFx45_CultureAwareComparerGetHashCode_LongStrings>](netfx45-cultureawarecomparergethashcode-longstrings-element.md)|런타임이 <xref:System.StringComparer.GetHashCode%2A?displayProperty=nameWithType> 메서드에 대한 해시 코드를 계산하기 위해 고정된 양의 메모리를 사용할지 여부를 지정합니다.|
|[\<PreferComInsteadOfManagedRemoting>](prefercominsteadofmanagedremoting-element.md)|런타임이 애플리케이션 도메인 경계 간에 원격 모드가 아닌 COM interop를 사용하도록 지정합니다.|
|[\<probing>](probing-element.md)|어셈블리를 로드할 때 런타임이 검색하는 하위 디렉터리를 지정합니다.|
|[\<publisherPolicy>](publisherpolicy-element.md)|런타임이 게시자 정책을 적용할지를 지정합니다.|
|[\<qualifyAssembly>](qualifyassembly-element.md)|부분 이름이 사용될 때 동적으로 로드되어야 하는 어셈블리의 전체 이름을 지정합니다.|
|[\<relativeBindForResources>](relativebindforresources-element.md)|위성 어셈블리에 대한 프로브를 최적화합니다.|
|[\<remove>](remove-element-for-namedcaches.md)|메모리 캐시용으로 명명된 캐시 항목을 `namedCaches` 컬렉션에서 제거합니다.|
|[\<runtime>](runtime-element.md)|어셈블리 바인딩 및 가비지 수집 동작에 대한 정보를 포함합니다.|
|[\<shadowCopyTimeStampVerification>](shadowcopyverifybytimestamp-element.md)|섀도 복사가 .NET Framework 4에서 도입 된 기본 시작 동작을 사용 하는지 아니면 이전 버전의 .NET Framework의 시작 동작으로 돌아가는지를 지정 합니다.|
|[\<supportPortability>](supportportability-element.md)|애플리케이션 이식성을 위해 어셈블리를 동일하게 간주하는 기본 동작을 사용하지 않도록 설정함으로써, 애플리케이션이 .NET Framework의 서로 다른 두 구현에서 같은 어셈블리를 참조할 수 있도록 지정합니다.|
|[\<system.runtime.caching>](system-runtime-caching-element-cache-settings.md)|기본 메모리 내 개체 캐시에 대한 구성 정보를 제공합니다.|
|[\<Thread_UseAllCpuGroups>](thread-useallcpugroups-element.md)|런타임이 모든 CPU 그룹에 관리되는 스레드를 배포할지를 지정합니다.|
|[\<ThrowUnobservedTaskExceptions>](throwunobservedtaskexceptions-element.md)|작업 예외가 처리되지 않으면 실행 중인 프로세스를 종료할지를 지정합니다.|
|[\<TimeSpan_LegacyFormatMode>](runtime-element.md)|런타임이 <xref:System.TimeSpan> 값에 대해 레거시 서식을 사용할지를 지정합니다.|
|[\<useLegacyJit>](uselegacyjit-element.md)|공용 언어 런타임이 Just-In-Time 컴파일에 레거시 64비트 JIT 컴파일러를 사용할지를 결정합니다.|
|[\<UseRandomizedStringHashAlgorithm>](userandomizedstringhashalgorithm-element.md)|런타임이 애플리케이션 도메인별로 문자열의 해시 코드를 계산할지를 지정합니다.|
|[\<UseSmallInternalThreadStacks>](usesmallinternalthreadstacks-element.md)|런타임이 내부적으로 사용하는 특정 스레드를 만들 때 기본 스택 크기가 아닌 명시적 스택 크기를 사용하도록 요청합니다.|

## <a name="see-also"></a>참고자료

- [구성 파일 스키마](../index.md)
- [동시 가비지 수집을 사용 하지 않도록 설정 하려면](gcconcurrent-element.md#to-disable-background-garbage-collection)
- [어셈블리 버전 리디렉션](../../redirect-assembly-versions.md)
