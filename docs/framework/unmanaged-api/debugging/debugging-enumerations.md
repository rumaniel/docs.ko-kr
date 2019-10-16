---
title: 디버깅 열거형
ms.date: 03/30/2017
helpviewer_keywords:
- debugging enumerations [.NET Framework]
- unmanaged enumerations [.NET Framework], debugging
- enumerations [.NET Framework debugging]
ms.assetid: 3af9f584-f1b4-4154-aeaa-8fce7c9f8b50
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5edd6dfb3dac05ce4614c43949f2ec4c19b5f742
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61698514"
---
# <a name="debugging-enumerations"></a>디버깅 열거형
이 섹션에서는 디버깅 API에서 사용하는 관리되지 않는 열거형에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [CLR_DEBUGGING_PROCESS_FLAGS 열거형](../../../../docs/framework/unmanaged-api/debugging/clr-debugging-process-flags-enumeration.md)  
 사용 되는 값을 제공 합니다 [iclrdebugging:: Openvirtualprocess](../../../../docs/framework/unmanaged-api/debugging/iclrdebugging-openvirtualprocess-method.md) 메서드.  
  
 [CLRDataEnumMemoryFlags 열거형](../../../../docs/framework/unmanaged-api/debugging/clrdataenummemoryflags-enumeration.md)  
 메모리 영역에 대 한 호출을 나타내는 합니다 [iclrdataenummemoryregions:: Enummemoryregions](../../../../docs/framework/unmanaged-api/debugging/iclrdataenummemoryregions-enummemoryregions-method.md) 메서드를 포함 해야 합니다.  
  
 [COR_PUB_ENUMPROCESS 열거형](../../../../docs/framework/unmanaged-api/debugging/cor-pub-enumprocess-enumeration.md)  
 열거할 프로세스 형식을 식별합니다.  
  
 [CorDebugBlockingReason 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugblockingreason-enumeration.md)  
 지정된 개체에서 스레드가 차단될 수 있는 이유를 지정합니다.  
  
 CorDebugChainReason  
 호출 체인의 시작 이유를 하나 이상 나타냅니다.  
  
 [CorDebugCodeInvokeKind 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugcodeinvokekind-enumeration.md)  
 내보낸 함수가 관리 코드를 호출하는 방법을 설명합니다.  
  
 [CorDebugCodeInvokePurpose 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugcodeinvokepurpose-enumeration.md)  
 내보낸 함수가 관리 코드를 호출하는 이유를 설명합니다.  
  
 CorDebugCreateProcessFlags  
 에 대 한 호출에서 사용할 수 있는 추가 디버깅 옵션을 제공 합니다 [icordebug:: Createprocess](../../../../docs/framework/unmanaged-api/debugging/icordebug-createprocess-method.md) 메서드.  
  
 [CorDebugDebugEventKind 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugdebugeventkind-enumeration.md)  
 정보를 가져올 디코딩되는 이벤트의 형식을 나타내는 합니다 [DecodeEvent](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess6-decodeevent-method.md) 메서드.  
  
 [CorDebugDecodeEventFlagsWindows 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugdecodeeventflagswindows-enumeration.md)  
 Windows 플랫폼에서 디버그 이벤트에 대한 추가 정보를 제공합니다.  
  
 CorDebugExceptionCallbackType  
 수행 되는 콜백의 형식을 나타냅니다는 [ICorDebugManagedCallback2::Exception](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-exception-method.md) 이벤트입니다.  
  
 [CorDebugExceptionFlags 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugexceptionflags-enumeration.md)  
 예외에 대한 추가 정보를 제공합니다.  
  
 CorDebugExceptionUnwindCallbackType  
 해제 단계 중에 콜백에서 신호를 보내는 이벤트를 나타냅니다.  
  
 [CorDebugGCType 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebuggctype-enumeration.md)  
 가비지 수집기가 실행되고 있는 위치(워크스테이션 또는 서버)를 나타냅니다.  
  
 [CorDebugGenerationTypes 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebuggenerationtypes-enumeration.md)  
 관리되는 힙에 대한 메모리 영역 생성을 지정합니다.  
  
 CorDebugHandleType  
 핸들 형식을 나타냅니다.  
  
 [CorDebugIlToNativeMappingTypes 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugiltonativemappingtypes-enumeration.md)  
 기본 명령의 특정 범위가 특수 코드 영역에 해당하는지 여부를 나타냅니다.  
  
 CorDebugIntercept  
 한 단계씩 실행할 수 있는 코드 형식을 나타냅니다.  
  
 [CorDebugInterfaceVersion 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebuginterfaceversion-enumeration.md)  
 특정 .NET Framework 버전 또는 인터페이스가 적용된 .NET Framework 버전을 지정합니다.  
  
 CorDebugInternalFrameType  
 스택 프레임 형식을 식별합니다.  
  
 [CorDebugJITCompilerFlags 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugjitcompilerflags-enumeration.md)  
 관리되는 JIT(Just-In-Time) 컴파일러의 동작에 영향을 주는 값을 포함합니다.  
  
 [CorDebugJITCompilerFlagsDeprecated 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugjitcompilerflagsdeprecated-enumeration.md)  
 사용되지 않습니다. 사용 합니다 `CORDEBUG_JIT_DEFAULT` 의 멤버는 [CorDebugJITCompilerFlags](../../../../docs/framework/unmanaged-api/debugging/cordebugjitcompilerflags-enumeration.md) 열거형 대신 합니다.  
  
 CorDebugMappingResult  
 IP(명령 포인터)의 값을 가져온 방법에 대한 세부 정보를 제공합니다.  
  
 [CorDebugMDAFlags 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugmdaflags-enumeration.md)  
 MDA(관리 디버깅 도우미)가 실행된 스레드의 상태를 지정합니다.  
  
 [CorDebugNGenPolicy 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugngenpolicy-enumeration.md)  
 디버거가 네이티브 이미지 캐시에서 네이티브(NGen) 이미지를 로드하는지 여부를 결정하는 값을 제공합니다.  
  
 [CorDebugPlatform 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugplatform-enumeration.md)  
 사용 되는 대상 플랫폼 값을 제공 합니다 [icordebugdatatarget:: Getplatform](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-getplatform-method.md) 메서드.  
  
 [CorDebugRecordFormat 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugrecordformat-enumeration.md)  
 네이티브 예외 디버그 이벤트에 대한 정보가 포함된 바이트 배열의 데이터 형식을 설명합니다.  
  
 CorDebugRegister  
 지정한 프로세서 아키텍처에 연결된 레지스터를 지정합니다.  
  
 [CorDebugSetContextFlag 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugsetcontextflag-enumeration.md)  
 컨텍스트가 스택의 활성(리프) 프레임에서 가져온 것인지 아니면 다른 프레임에서 해제하여 계산되었는지를 나타냅니다.  
  
 [CorDebugStateChange 열거형](../../../../docs/framework/unmanaged-api/debugging/cordebugstatechange-enumeration.md)  
 프로세스에 대한 변경 내용을 기반으로 삭제해야 하는 캐시된 데이터의 양을 설명합니다.  
  
 CorDebugStepReason  
 개별 단계의 결과를 나타냅니다.  
  
 CorDebugThreadState  
 디버깅을 위한 스레드 상태를 지정합니다.  
  
 \>CorDebugUnmappedStop  
 스텝퍼에 의해 코드 실행에서 중지를 트리거할 수 있는 매핑되지 않은 코드 형식을 지정합니다.  
  
 CorDebugUserState  
 스레드의 사용자 상태를 나타냅니다.  
  
 [CorGCReferenceType 열거형](../../../../docs/framework/unmanaged-api/debugging/corgcreferencetype-enumeration.md)  
 가비지가 수집될 개체의 소스를 식별합니다.  
  
 [ILCodeKind 열거형](../../../../docs/framework/unmanaged-api/debugging/ilcodekind-enumeration.md)  
 디버거가 프로파일러 ReJIT 계측에 추가된 로컬 변수나 코드에 액세스할 수 있는지 여부를 지정하는 값을 제공합니다.  
  
 [LoggingLevelEnum 열거형](../../../../docs/framework/unmanaged-api/debugging/logginglevelenum-enumeration.md)  
 관리되는 스레드가 이벤트를 기록할 때 이벤트 로그에 기록되는 설명 메시지의 보안 수준을 나타냅니다.  
  
 [LogSwitchCallReason 열거형](../../../../docs/framework/unmanaged-api/debugging/logswitchcallreason-enumeration.md)  
 디버깅/추적 스위치에 대해 수행된 작업을 나타냅니다.  
  
 [VariableLocationType 열거형](../../../../docs/framework/unmanaged-api/debugging/variablelocationtype-enumeration.md)  
 변수의 네이티브 위치 유형을 나타냅니다.  
  
 [WriteableMetadataUpdateMode 열거형](../../../../docs/framework/unmanaged-api/debugging/writeablemetadataupdatemode-enumeration.md)  
 메타데이터에 대한 메모리 내 업데이트가 디버거에 표시되는지 여부를 지정하는 값을 제공합니다. 

 [ClrDataSourceType 열거형](../../../../docs/framework/unmanaged-api/debugging/clrdatasourcetype-enumeration.md) CLRDATA_IL_ADDRESS_MAP 구조에서 사용 되는 값을 제공 합니다.

## <a name="related-sections"></a>관련 단원  
 [디버깅 Coclass](../../../../docs/framework/unmanaged-api/debugging/debugging-coclasses.md)  
  
 [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
  
 [디버깅 전역 정적 함수](../../../../docs/framework/unmanaged-api/debugging/debugging-global-static-functions.md)  
  
 [디버깅 구조체](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
