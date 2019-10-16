---
title: 디버깅 인터페이스
ms.date: 02/07/2019
helpviewer_keywords:
- unmanaged interfaces [.NET Framework], debugging
- debugging interfaces [.NET Framework]
- interfaces [.NET Framework debugging]
ms.assetid: b6297c26-7624-4431-8af4-14112d07bcd5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ff589285d81a3febf887bba976b62a9ae4a573c8
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2019
ms.locfileid: "67025936"
---
# <a name="debugging-interfaces"></a>디버깅 인터페이스
이 단원에서는 CLR(공용 언어 런타임)에서 실행되는 프로그램의 디버깅을 처리하는 관리되지 않는 인터페이스에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [ICLRDataEnumMemoryRegions 인터페이스](iclrdataenummemoryregions-interface.md)\
 호출자가 지정하는 메모리 영역을 열거하는 메서드를 제공합니다.  
  
 [ICLRDataEnumMemoryRegionsCallback 인터페이스](iclrdataenummemoryregionscallback-interface.md)\
 지정된 메모리 영역을 열거하려고 시도한 결과를 디버거에 보고하는 콜백 메서드를 `EnumMemoryRegions`에 제공합니다.  
  
 [ICLRDataTarget 인터페이스](iclrdatatarget-interface.md)\
 대상 CLR 프로세스와 상호 작용하기 위한 메서드를 제공합니다.  
  
 [ICLRDataTarget2 인터페이스](iclrdatatarget2-interface.md)\
 데이터 액세스 서비스 계층에서 대상 프로세스의 가상 메모리 영역을 조작하는 데 사용하는 `ICLRDataTarget`의 서브클래스입니다.  
  
 [ICLRDataTarget3 인터페이스](iclrdatatarget3-interface.md)\
 서브 클래스 [ICLRDataTarget2](iclrdatatarget2-interface.md) 예외 정보에 대 한 액세스를 제공 하는 합니다.  
  
 [ICLRDebugging 인터페이스](iclrdebugging-interface.md)\
 디버깅을 위해 모듈을 로드 및 언로드하는 작업을 처리하는 메서드를 제공합니다.  
  
 [ICLRDebuggingLibraryProvider 인터페이스](iclrdebugginglibraryprovider-interface.md)\
 포함 된 [ProvideLibrary 메서드](iclrdebugginglibraryprovider-providelibrary-method.md) 메서드 라이브러리 공급자 콜백 인터페이스 공용 언어 런타임 버전별 디버깅 라이브러리 있고에 로드 된 요청 수를 가져옵니다.  
  
 [ICLRMetadataLocator 인터페이스](iclrmetadatalocator-interface.md)\
 데이터 액세스 서비스 계층에서 대상 프로세스의 어셈블리 메타데이터를 찾는 데 사용되는 인터페이스입니다.  
  
 [ICorDebug 인터페이스](icordebug-interface.md)\
 개발자가 CLR 환경에서 애플리케이션을 디버깅하는 데 사용할 수 있는 메서드를 제공합니다.  
  
 [ICorDebugAppDomain 인터페이스](icordebugappdomain-interface.md)\
 애플리케이션 도메인 디버깅에 사용하는 메서드를 제공합니다.  
  
 [ICorDebugAppDomain2 인터페이스](icordebugappdomain2-interface.md)\
 배열, 포인터, 함수 포인터 및 ByRef 형식에 사용할 수 있는 메서드를 제공합니다. 이 인터페이스는 `ICorDebugAppDomain` 인터페이스의 확장입니다.  
  
 [ICorDebugAppDomain3 인터페이스](icordebugappdomain3-interface.md)\
 응용 프로그램 도메인에서 Windows 런타임 형식을 사용 하는 방법을 제공 합니다. 이 인터페이스는 `ICorDebugAppDomain` 및 `ICorDebugAppDomain2` 인터페이스의 확장입니다.  
  
 [ICorDebugAppDomain4 인터페이스](icordebugappdomain4-interface.md)\
 논리적으로 확장 합니다 [ICorDebugAppDomain](icordebugappdomain-interface.md) 인터페이스를 COM 호출 가능 래퍼를에서 관리 되는 개체를 가져옵니다.  
  
 [ICorDebugAppDomainEnum 인터페이스](icordebugappdomainenum-interface.md)\
 열거형의 다음 위치에서 시작하여 지정된 수만큼 `ICorDebugAppDomain` 값을 반환하는 메서드를 제공합니다.  
  
 [ICorDebugArrayValue 인터페이스](icordebugarrayvalue-interface.md)\
 1차원 배열이나 다차원 배열을 나타내는 `ICorDebugHeapValue`의 서브클래스입니다.  
  
 [ICorDebugAssembly 인터페이스](icordebugassembly-interface.md)\
 어셈블리를 나타냅니다.  
  
 [ICorDebugAssembly2 인터페이스](icordebugassembly2-interface.md)\
 어셈블리를 나타냅니다. 이 인터페이스는 `ICorDebugAssembly` 인터페이스의 확장입니다.  
  
 [ICorDebugAssembly3 인터페이스](icordebugassembly3-interface.md)\
 논리적으로 확장 합니다 [ICorDebugAssembly](icordebugassembly-interface.md) 컨테이너 어셈블리 및 포함 된 어셈블리에 대 한 지원을 제공 하는 인터페이스입니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugAssemblyEnum 인터페이스](icordebugassemblyenum-interface.md)\
 `ICorDebugEnum` 메서드를 구현하고 `ICorDebugAssembly` 배열을 열거합니다.  
  
 [ICorDebugBlockingObjectEnum 인터페이스](icordebugblockingobjectenum-interface.md)\
 목록에 대 한 열거자를 제공 [CorDebugBlockingObject](cordebugblockingobject-structure.md) 구조입니다.  
  
 [ICorDebugBoxValue 인터페이스](icordebugboxvalue-interface.md)\
 boxed 값 클래스 개체를 나타내는 `ICorDebugHeapValue`의 서브클래스입니다.  
  
 [ICorDebugBreakpoint 인터페이스](icordebugbreakpoint-interface.md)\
 함수의 중단점 또는 값에 대한 조사식 위치를 나타냅니다.  
  
 [ICorDebugBreakpointEnum 인터페이스](icordebugbreakpointenum-interface.md)\
 `ICorDebugEnum` 메서드를 구현하고 `ICorDebugBreakpoint` 배열을 열거합니다.  
  
 [ICorDebugChain 인터페이스](icordebugchain-interface.md)\
 실제 또는 논리 호출 스택의 세그먼트를 나타냅니다.  
  
 [ICorDebugChainEnum 인터페이스](icordebugchainenum-interface.md)\
 `ICorDebugEnum` 메서드를 구현하고 `ICorDebugChain` 배열을 열거합니다.  
  
 [ICorDebugClass 인터페이스](icordebugclass-interface.md)\
 기본 또는 복합(즉, 사용자 정의) 형식을 나타냅니다. 형식이 제네릭이면 `ICorDebugClass`는 인스턴스화되지 않은 제네릭 형식을 나타냅니다.  
  
 [ICorDebugClass2 인터페이스](icordebugclass2-interface.md)\
 제네릭 클래스나 <xref:System.Type> 형식의 메서드 매개 변수를 사용하는 클래스를 나타냅니다. 이 인터페이스는 `ICorDebugClass`를 확장한 것입니다.  
  
 [ICorDebugCode 인터페이스](icordebugcode-interface1.md)\
 MSIL(Microsoft Intermediate Language) 코드나 네이티브 코드의 세그먼트를 나타냅니다.  
  
 [ICorDebugCode2 인터페이스](icordebugcode2-interface.md)\
 `ICorDebugCode`의 기능을 확장하는 메서드를 제공합니다.  
  
 [ICorDebugCode3 인터페이스](icordebugcode3-interface.md)\
 확장 하는 메서드를 제공 [ICorDebugCode](icordebugcode-interface1.md) 하 고 [ICorDebugCode2](icordebugcode2-interface.md) 관리 되는 반환 값에 대 한 정보를 제공 합니다.  
  
 [ICorDebugCode4 인터페이스](icordebugcode4-interface.md)\
 지역 변수 및 함수에 인수를 열거 하는 디버거를 사용 하도록 설정 하는 메서드를 제공 합니다.  
  
 [ICorDebugCodeEnum 인터페이스](icordebugcodeenum-interface.md)\
 `ICorDebugEnum` 메서드를 구현하고 `ICorDebugCode` 배열을 열거합니다.  
  
 [ICorDebugComObjectValue 인터페이스](icordebugcomobjectvalue-interface.md)\
 캐시된 인터페이스 개체를 검색하는 메서드를 제공합니다.  
  
 [ICorDebugContext 인터페이스](icordebugcontext-interface.md)\
 컨텍스트 개체를 나타냅니다. 이 인터페이스는 아직 구현되지 않았습니다.  
  
 [ICorDebugController 인터페이스](icordebugcontroller-interface.md)\
 <xref:System.Diagnostics.Process>나 <xref:System.AppDomain> 같이 코드 실행 컨텍스트를 제어할 수 있는 범위를 나타냅니다.  
  
 [ICorDebugDataTarget 인터페이스](icordebugdatatarget-interface.md)\
 특정 대상 프로세스에 대한 액세스를 제공하는 콜백 인터페이스를 제공합니다.  
  
 [ICorDebugDataTarget2 인터페이스](icordebugdatatarget2-interface.md)\
 논리적으로 확장 합니다 [ICorDebugDataTarget](icordebugdatatarget-interface.md) 인터페이스입니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugDataTarget3 인터페이스](icordebugdatatarget3-interface.md)\
 논리적으로 확장 합니다 [ICorDebugDataTarget](icordebugdatatarget-interface.md) 로드 된 모듈에 대 한 정보를 제공 하는 인터페이스입니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugDebugEvent 인터페이스](icordebugdebugevent-interface.md)\
 모든 `ICorDebug` 디버그 이벤트가 파생되는 기본 인터페이스를 정의합니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugEditAndContinueErrorInfo 인터페이스](icordebugeditandcontinueerrorinfo-interface.md)\
 사용되지 않습니다. 이 인터페이스를 사용하지 마십시오.  
  
 [ICorDebugEditAndContinueSnapshot 인터페이스](icordebugeditandcontinuesnapshot-interface.md)\
 사용되지 않습니다. 이 인터페이스를 사용하지 마십시오.  
  
 [ICorDebugEnum 인터페이스](icordebugenum-interface1.md)\
 열거자를 디버깅할 수 있는 추상 기본 인터페이스로 사용합니다.  
  
 [ICorDebugErrorInfoEnum 인터페이스](icordebugerrorinfoenum-interface.md)\
 사용되지 않습니다. 이 인터페이스를 사용하지 마십시오.  
  
 [ICorDebugEval 인터페이스](icordebugeval-interface.md)\
 디버깅 중인 코드의 컨텍스트 내에서 디버거가 코드를 실행할 수 있도록 하는 메서드를 제공합니다.  
  
 [ICorDebugEval2 인터페이스](icordebugeval2-interface.md)\
 제네릭 형식을 지원하도록 `ICorDebugEval`을 확장합니다.  
  
 [ICorDebugExceptionDebugEvent 인터페이스](icordebugexceptiondebugevent-interface.md)\
 확장 된 [ICorDebugDebugEvent](icordebugdebugevent-interface.md) 예외 이벤트를 지 원하는 인터페이스입니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugExceptionObjectCallStackEnum 인터페이스](icordebugexceptionobjectcallstackenum-interface.md)\
 예외 개체에 포함된 호출 스택 정보에 대한 열거자를 제공합니다.  
  
 [ICorDebugExceptionObjectValue 인터페이스](icordebugexceptionobjectvalue-interface.md)\
 확장 된 [ICorDebugObjectValue](icordebugobjectvalue-interface.md) 관리 되는 예외 개체에서 스택 추적 정보를 제공 하는 인터페이스입니다.  
  
 [ICorDebugFrame 인터페이스](icordebugframe-interface.md)\
 현재 스택의 프레임을 나타냅니다.  
  
 [ICorDebugFrameEnum 인터페이스](icordebugframeenum-interface.md)\
 `ICorDebugEnum` 메서드를 구현하고 `ICorDebugFrame` 배열을 열거합니다.  
  
 [ICorDebugFunction 인터페이스](icordebugfunction-interface1.md)\
 관리되는 함수 또는 메서드를 나타냅니다.  
  
 [ICorDebugFunction2 인터페이스](icordebugfunction2-interface.md)\
 `ICorDebugFunction`의 기능을 논리적으로 확장하여 "내 코드만" 단계별 실행 디버깅을 지원합니다.  
  
 [ICorDebugFunction3 인터페이스](icordebugfunction3-interface.md)\
 논리적으로 확장 합니다 [ICorDebugFunction](icordebugfunction-interface1.md) ReJIT 요청의 코드에 대 한 액세스를 제공 하는 인터페이스입니다.  
  
 [ICorDebugFunctionBreakpoint 인터페이스](icordebugfunctionbreakpoint-interface.md)\
 함수에서 중단점을 지원하기 위해 `ICorDebugBreakpoint`를 확장합니다.  
  
 [ICorDebugGCReferenceEnum 인터페이스](icordebuggcreferenceenum-interface.md)\
 가비지 수집되는 개체에 대한 열거자를 제공합니다.  
  
 [ICorDebugGenericValue 인터페이스](icordebuggenericvalue-interface.md)\
 모든 값에 적용되는 `ICorDebugValue`의 서브클래스입니다. 이 인터페이스에서는 값의 Get 및 Set 메서드를 제공합니다.  
  
 [ICorDebugGuidToTypeEnum 인터페이스](icordebugguidtotypeenum-interface.md)\
 GUID를 매핑하는 개체와 그에 해당하는 `ICorDebugType` 개체에 대한 열거자를 제공합니다.  
  
 [ICorDebugHandleValue 인터페이스](icordebughandlevalue-interface.md)\
 디버거에서 가비지 수집을 위해 핸들을 만든 대상 참조 값을 나타내는 `ICorDebugReferenceValue`의 서브클래스입니다.  
  
 [ICorDebugHeapEnum 인터페이스](icordebugheapenum-interface.md)\
 관리되는 힙의 개체에 대한 열거자를 제공합니다.  
  
 [ICorDebugHeapSegmentEnum 인터페이스](icordebugheapsegmentenum-interface.md)\
 관리되는 힙 메모리 영역에 대한 열거자를 제공합니다.  
  
 [ICorDebugHeapValue 인터페이스](icordebugheapvalue-interface.md)\
 CLR 가비지 수집기에서 수집한 개체를 나타내는 `ICorDebugValue`의 서브클래스입니다.  
  
 [ICorDebugHeapValue2 인터페이스](icordebugheapvalue2-interface1.md)\
 런타임 핸들에 대한 지원을 제공하는 `ICorDebugHeapValue`의 확장입니다.  
  
 [ICorDebugHeapValue3 인터페이스](icordebugheapvalue3-interface.md)\
 개체의 모니터 잠금 속성을 노출합니다.  
  
 [ICorDebugILCode 인터페이스](icordebugilcode-interface.md)\
 IL(중간 언어) 코드 세그먼트를 나타냅니다.  
  
 [ICorDebugILCode2 인터페이스](icordebugilcode2-interface.md)\
 논리적으로 확장 합니다 [ICorDebugILCode](icordebugilcode-interface.md) 인터페이스 함수의 로컬 변수 서명에 대 한 토큰을 반환 하 고 프로파일러의 계측 된 IL (중간 언어)을 매핑하는 방법을 제공 하기 위해 원래 메서드 IL 오프셋 오프셋 합니다.  
  
 [ICorDebugILFrame 인터페이스](icordebugilframe-interface.md)\
 MSIL 코드의 스택 프레임을 나타냅니다.  
  
 [ICorDebugILFrame2 인터페이스](icordebugilframe2-interface.md)\
 `ICorDebugILFrame`에서 논리적으로 확장된 버전입니다.  
  
 [ICorDebugILFrame3 인터페이스](icordebugilframe3-interface.md)\
 함수의 반환 값을 캡슐화하는 메서드를 제공합니다.  
  
 [ICorDebugILFrame4 인터페이스](icordebugilframe4-interface.md)\
 IL(중간 언어) 코드의 스택 프레임에서 로컬 변수 및 코드에 액세스하는 데 사용할 수 있는 메서드를 제공합니다. 디버거가 프로파일러 ReJIT 계측에 추가된 변수와 코드에 액세스할 수 있는지는 매개 변수를 통해 지정됩니다.  
  
 [ICorDebugInstanceFieldSymbol 인터페이스](icordebuginstancefieldsymbol-interface.md)\
 인스턴스 필드에 대한 디버그 기호 정보를 나타냅니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugInternalFrame 인터페이스](icordebuginternalframe-interface.md)\
 디버거의 프레임 형식을 식별합니다.  
  
 [ICorDebugInternalFrame2 인터페이스](icordebuginternalframe2-interface.md)\
 스택 주소에 상대적인 위치를 포함 하 여 내부 프레임에 대 한 정보를 제공 [ICorDebugFrame](icordebugframe-interface.md) 개체입니다.  
  
 [ICorDebugLoadedModule 인터페이스](icordebugloadedmodule-interface.md)\
 로드된 모듈에 대한 정보를 제공합니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugManagedCallback 인터페이스](icordebugmanagedcallback-interface.md)\
 디버거 콜백을 처리하는 메서드를 제공합니다.  
  
 [ICorDebugManagedCallback2 인터페이스](icordebugmanagedcallback2-interface.md)\
 디버거 예외 처리 및 MDA(관리 디버깅 도우미)를 지원하기 위한 메서드를 제공합니다. `ICorDebugManagedCallback2`은 `ICorDebugManagedCallback`에서 논리적으로 확장된 버전입니다.  
  
 [ICorDebugManagedCallback3 인터페이스](icordebugmanagedcallback3-interface.md)\
 활성화된 사용자 지정 디버거 알림이 발생했음을 나타내는 콜백 메서드를 제공합니다.  
  
 [ICorDebugMDA 인터페이스](icordebugmda-interface.md)\
 MDA(관리 디버깅 도우미) 메시지를 나타냅니다.  
  
 [ICorDebugMemoryBuffer 인터페이스](icordebugmemorybuffer-interface.md)\
 메모리 내 버퍼를 나타냅니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugMergedAssemblyRecord 인터페이스](icordebugmergedassemblyrecord-interface.md)\
 병합된 어셈블리에 대한 정보를 제공합니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugMetaDataLocator 인터페이스](icordebugmetadatalocator-interface.md)\
 디버거에 메타데이터 정보를 제공합니다.  
  
 [ICorDebugModule 인터페이스](icordebugmodule-interface.md)\
 실행 파일이나 DLL(동적 연결 라이브러리)인 CLR 모듈을 나타냅니다.  
  
 [ICorDebugModule2 인터페이스](icordebugmodule2-interface.md)\
 `ICorDebugModule`에서 논리적으로 확장된 버전입니다.  
  
 [ICorDebugModule3 인터페이스](icordebugmodule3-interface.md)\
 동적 모듈에 대한 기호 판독기를 만듭니다.  
  
 [ICorDebugModuleBreakpoint 인터페이스](icordebugmodulebreakpoint-interface.md)\
 특정 모듈에 액세스할 수 있도록 `ICorDebugBreakpoint`를 확장합니다.  
  
 [ICorDebugModuleDebugEvent 인터페이스](icordebugmoduledebugevent-interface.md)\
 확장 된 [ICorDebugDebugEvent](icordebugdebugevent-interface.md) 모듈 수준 이벤트를 지 원하는 인터페이스입니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugModuleEnum 인터페이스](icordebugmoduleenum-interface.md)\
 `ICorDebugEnum` 메서드를 구현하고 `ICorDebugModule` 배열을 열거합니다.  
  
 [ICorDebugMutableDataTarget 인터페이스](icordebugmutabledatatarget-interface.md)\
 확장 된 [ICorDebugDataTarget](icordebugdatatarget-interface.md) 인터페이스를 변경할 수 있는 데이터 대상을 지원 합니다.  
  
 [ICorDebugNativeFrame 인터페이스](icordebugnativeframe-interface.md)\
 네이티브 프레임에 사용되는 특수화된 `ICorDebugFrame` 구현입니다.  
  
 [ICorDebugNativeFrame2 인터페이스](icordebugnativeframe2-interface.md)\
 자식 및 부모 프레임 관계를 테스트하는 메서드를 제공합니다.  
  
 [ICorDebugObjectEnum 인터페이스](icordebugobjectenum-interface.md)\
 `ICorDebugEnum` 메서드를 구현하고 RVA(Relative Virtual Address)로 개체의 배열을 열거합니다.  
  
 [ICorDebugObjectValue 인터페이스](icordebugobjectvalue-interface.md)\
 개체가 들어 있는 값을 나타내는 `ICorDebugValue`의 서브클래스입니다.  
  
 [ICorDebugObjectValue2 인터페이스](icordebugobjectvalue2-interface.md)\
 상속 및 재정의 기능을 지원하도록 `ICorDebugObjectValue`를 확장합니다.  
  
 [ICorDebugProcess 인터페이스](icordebugprocess-interface.md)\
 관리 코드를 실행하는 프로세스를 나타냅니다.  
  
 [ICorDebugProcess2 인터페이스](icordebugprocess2-interface1.md)\
 `ICorDebugProcess`에서 논리적으로 확장된 버전입니다.  
  
 [ICorDebugProcess3 인터페이스](icordebugprocess3-interface.md)\
 사용자 지정 디버거 알림을 제어합니다.

 [ICorDebugProcess4 인터페이스](icordebugprocess4-interface.md)\
 프로세스 실행 제어가 부족에 대 한 지원을 제공합니다.
  
 [ICorDebugProcess5 인터페이스](icordebugprocess5-interface.md)\
 확장 된 [ICorDebugProcess](icordebugprocess-interface.md) 관리 되는 개체의 가비지 수집에 대 한 정보를 제공 하 고 디버거가 응용 프로그램에서 이미지를 로드 하는지 여부를 확인 하려면 관리 되는 힙에 대 한 액세스를 지 원하는 인터페이스의 로컬 네이티브 이미지 캐시 합니다.  
  
 [ICorDebugProcess6 인터페이스](icordebugprocess6-interface.md)\
 논리적으로 확장 합니다 [ICorDebugProcess](icordebugprocess-interface.md) 인터페이스 네이티브 예외 디버그 이벤트, 가상 모듈 분할에서 인코딩 되는 관리 되는 디버그 이벤트 디코딩 등의 기능을 사용 하도록 설정 합니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugProcess7 인터페이스](icordebugprocess7-interface.md)\
 대상 프로세스에서 디버거가 메모리 내 메타데이터 업데이트를 처리하도록 구성하는 메서드를 제공합니다.  
  
 [ICorDebugProcess8 인터페이스](icordebugprocess8-interface.md)\
 논리적으로 확장 합니다 [ICorDebugProcess](icordebugprocess-interface.md) 인터페이스를 사용 하도록 설정 하거나 특정 유형의 사용 하지 않도록 [ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md) 예외 콜백을 합니다.  
  
 [ICorDebugProcessEnum 인터페이스](icordebugprocessenum-interface.md)\
 `ICorDebugEnum` 메서드를 구현하고 `ICorDebugProcess` 배열을 열거합니다.  
  
 [ICorDebugReferenceValue 인터페이스](icordebugreferencevalue-interface.md)\
 참조 형식을 지원하는 `ICorDebugValue`의 서브클래스입니다.  
  
 [ICorDebugRegisterSet 인터페이스](icordebugregisterset-interface.md)\
 코드가 실행되고 있는 컴퓨터에서 사용할 수 있는 레지스터 집합을 나타냅니다.  
  
 [ICorDebugRegisterSet2 인터페이스](icordebugregisterset2-interface.md)\
 64개 이상의 레지스터가 있는 하드웨어 플랫폼의 `ICorDebugRegisterSet` 기능을 확장합니다.  
  
 [ICorDebugRemote 인터페이스](icordebugremote-interface.md)\
 시작할 수 있거나 원격 대상 프로세스에 관리되는 디버거를 연결할 수 있는 기능을 제공합니다.  
  
 [ICorDebugRemoteTarget 인터페이스](icordebugremotetarget-interface.md)\
 CLR 환경에서 Silverlight 기반 애플리케이션을 디버깅하는 데 사용할 수 있는 메서드를 제공합니다.  
  
 [ICorDebugRuntimeUnwindableFrame 인터페이스](icordebugruntimeunwindableframe-interface.md)\
 프레임을 해제하는 데 CLR(공용 언어 런타임)을 필요로 하는 관리되지 않는 메서드에 대한 지원을 제공합니다.  
  
 [ICorDebugStackWalk 인터페이스](icordebugstackwalk-interface.md)\
 스레드 스택에서 관리되는 메서드나 프레임을 가져오기 위한 메서드를 제공합니다.  
  
 [ICorDebugStaticFieldSymbol 인터페이스](icordebugstaticfieldsymbol-interface.md)\
 정적 필드에 대한 디버그 기호 정보를 나타냅니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugStepper 인터페이스](icordebugstepper-interface.md)\
 디버거에서 수행하는 코드 실행 단계를 나타내며, 명령의 실행/완료를 구분하는 식별자로 사용되고, 단계를 취소하는 방법을 제공합니다.  
  
 [ICorDebugStepper2 인터페이스](icordebugstepper2-interface1.md)\
 JMC(내 코드만) 디버깅을 지원합니다.  
  
 [ICorDebugStepperEnum 인터페이스](icordebugstepperenum-interface.md)\
 `ICorDebugEnum` 메서드를 구현하고 `ICorDebugStepper` 배열을 열거합니다.  
  
 [ICorDebugStringValue 인터페이스](icordebugstringvalue-interface.md)\
 문자열 값에 적용되는 `ICorDebugHeapValue`의 서브클래스입니다.  
  
 [ICorDebugSymbolProvider 인터페이스](icordebugsymbolprovider-interface.md)\
 디버그 기호 정보를 검색하는 데 사용할 수 있는 메서드를 제공합니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugSymbolProvider2 인터페이스](icordebugsymbolprovider2-interface.md)\
 논리적으로 확장 합니다 [ICorDebugSymbolProvider](icordebugsymbolprovider-interface.md) 추가 디버그 기호 정보를 검색 하는 인터페이스입니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugThread 인터페이스](icordebugthread-interface.md)\
 프로세스의 스레드를 나타냅니다. `ICorDebugThread` 인스턴스의 수명은 이 인스턴스가 나타내는 스레드의 수명과 같습니다.  
  
 [ICorDebugThread2 인터페이스](icordebugthread2-interface.md)\
 `ICorDebugThread`에서 논리적으로 확장된 버전입니다.  
  
 [ICorDebugThread3 인터페이스](icordebugthread3-interface.md)\
 진입점을 제공 합니다 [ICorDebugStackWalk](icordebugstackwalk-interface.md) 및 해당 인터페이스입니다.  
  
 [ICorDebugThread4 인터페이스](icordebugthread4-interface.md)\
 스레드 차단 정보를 제공합니다.  
  
 [ICorDebugThreadEnum 인터페이스](icordebugthreadenum-interface1.md)\
 `ICorDebugEnum` 메서드를 구현하고 `ICorDebugThread` 배열을 열거합니다.  
  
 [ICorDebugType 인터페이스](icordebugtype-interface.md)\
 기본 또는 복합(즉, 사용자 정의) 형식을 나타냅니다. 형식이 제네릭이면 `ICorDebugType`는 인스턴스화된 제네릭 형식을 나타냅니다.  
  
 [ICorDebugType2 인터페이스](icordebugtype2-interface.md)\
 확장 된 [ICorDebugType](icordebugtype-interface.md) 기본 형식 또는 복합 (사용자 정의 됨) 형식의 형식 식별자를 검색 하는 인터페이스입니다.  
  
 [ICorDebugTypeEnum 인터페이스](icordebugtypeenum-interface.md)\
 `ICorDebugEnum` 메서드를 구현하고 `ICorDebugType` 배열을 열거합니다.  
  
 [ICorDebugUnmanagedCallback 인터페이스](icordebugunmanagedcallback-interface.md)\
 CLR에 직접적으로 관련되지 않은 네이티브 이벤트에 대한 알림을 제공합니다.  
  
 [ICorDebugValue](icordebugvalue-interface.md)\
 디버깅 중인 프로세스의 읽기 또는 쓰기 값을 나타냅니다.  
  
 [ICorDebugValue2](icordebugvalue2-interface.md)\
 `ICorDebugValue`을 지원하기 위해 `ICorDebugType`에서 확장된 버전입니다.  
  
 [ICorDebugValue3 인터페이스](icordebugvalue3-interface.md)\
 2GB 보다 큰 배열 지원 하기 위해 "ICorDebugValue" 및 "ICorDebugValue2" 인터페이스를 확장 합니다.  
  
 [ICorDebugValueBreakpoint](icordebugvaluebreakpoint-interface.md)\
 특정 값에 액세스할 수 있도록 `ICorDebugBreakpoint`를 확장합니다.  
  
 [ICorDebugValueEnum](icordebugvalueenum-interface.md)\
 `ICorDebugEnum` 메서드를 구현하고 `ICorDebugValue` 배열을 열거합니다.  
  
 [ICorDebugVariableHome 인터페이스](icordebugvariablehome-interface.md)\
 지역 변수 또는 함수의 인수를 나타냅니다.  
  
 [ICorDebugVariableHomeEnum 인터페이스](icordebugvariablehomeenum-interface.md)\
 지역 변수 및 함수에 인수 하는 열거자를 제공합니다.  
  
 [ICorDebugVariableSymbol 인터페이스](icordebugvariablesymbol-interface.md)\
 변수에 대한 디버그 기호 정보를 검색합니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorDebugVirtualUnwinder 인터페이스](icordebugvirtualunwinder-interface.md)\
 스택 해제에 도움이 되는 메서드를 제공합니다. **.NET 네이티브 에서만 사용할 수 있습니다.**  
  
 [ICorPublish 인터페이스](icorpublish-interface.md)\
 게시 프로세스에 대한 일반적인 인터페이스로 사용합니다.  
  
 [ICorPublishAppDomain 인터페이스](icorpublishappdomain-interface.md)\
 애플리케이션 도메인을 나타내고 애플리케이션 도메인에 대한 정보를 제공합니다.  
  
 [ICorPublishAppDomainEnum 인터페이스](icorpublishappdomainenum-interface.md)\
 프로세스 내에 현재 있는 `ICorPublishAppDomain` 개체의 컬렉션을 이동하는 메서드를 제공합니다.  
  
 [ICorPublishEnum 인터페이스](icorpublishenum-interface.md)\
 열거자를 게시하기 위한 추상 기본 열거형으로 사용됩니다.  
  
 [ICorPublishProcess 인터페이스](icorpublishprocess-interface.md)\
 프로세스에 대한 정보에 액세스하는 메서드를 제공합니다.  
  
 [ICorPublishProcessEnum 인터페이스](icorpublishprocessenum-interface.md)\
 `ICorPublishProcess` 개체의 컬렉션을 이동하는 메서드를 제공합니다.  

 [ISOSDacInterface 인터페이스](isosdacinterface-interface.md)\
 데이터에 액세스할 도우미 메서드를 제공 `SOS`합니다.

 [IXCLRDataMethodDefinition 인터페이스](ixclrdatamethoddefinition-interface.md)\
 메서드 정의 대 한 정보를 쿼리 하기 위한 메서드를 제공 합니다.
 
 [IXCLRDataMethodInstance 인터페이스](ixclrdatamethodinstance-interface.md)\
 메서드 인스턴스에 대 한 정보를 쿼리 하기 위한 메서드를 제공 합니다.
 
 [IXCLRDataModule 인터페이스](ixclrdatamodule-interface.md)\
 로드 된 모듈에 대 한 정보를 쿼리 하기 위한 메서드를 제공 합니다.
 
 [IXCLRDataProcess 인터페이스](ixclrdataprocess-interface.md)\
 프로세스에 대 한 정보를 쿼리 하기 위한 메서드를 제공 합니다.
  
## <a name="related-sections"></a>관련 단원  
 [디버깅 Coclass](debugging-coclasses.md)\
 [디버깅 전역 정적 함수](debugging-global-static-functions.md)\
 [디버깅 열거형](debugging-enumerations.md)\
 [디버깅 구조체](debugging-structures.md)\
