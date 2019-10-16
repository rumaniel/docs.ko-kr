---
title: CorDebugRegister 열거형
ms.date: 03/30/2017
api_name:
- CorDebugRegister
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugRegister
helpviewer_keywords:
- CorDebugRegister enumeration [.NET Framework debugging]
ms.assetid: 003bb138-7960-4291-ac88-0d87e470ff70
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bed3c461935c5a2bc912ed9ed16d147fddaf8a1a
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67739659"
---
# <a name="cordebugregister-enumeration"></a>CorDebugRegister 열거형
지정한 프로세서 아키텍처에 연결된 레지스터를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorDebugRegister {  
  
    REGISTER_INSTRUCTION_POINTER = 0,  
    REGISTER_STACK_POINTER,  
    REGISTER_FRAME_POINTER,  
  
    REGISTER_X86_EIP = 0,  
    REGISTER_X86_ESP,  
    REGISTER_X86_EBP,  
  
    REGISTER_X86_EAX,  
    REGISTER_X86_ECX,  
    REGISTER_X86_EDX,  
    REGISTER_X86_EBX,  
  
    REGISTER_X86_ESI,  
    REGISTER_X86_EDI,  
  
    REGISTER_X86_FPSTACK_0,  
    REGISTER_X86_FPSTACK_1,  
    REGISTER_X86_FPSTACK_2,  
    REGISTER_X86_FPSTACK_3,  
    REGISTER_X86_FPSTACK_4,  
    REGISTER_X86_FPSTACK_5,  
    REGISTER_X86_FPSTACK_6,  
    REGISTER_X86_FPSTACK_7,  
  
    REGISTER_AMD64_RIP = 0,  
    REGISTER_AMD64_RSP,  
    REGISTER_AMD64_RBP,  
    REGISTER_AMD64_RAX,  
    REGISTER_AMD64_RCX,  
    REGISTER_AMD64_RDX,  
    REGISTER_AMD64_RBX,  
    REGISTER_AMD64_RSI,  
    REGISTER_AMD64_RDI,  
    REGISTER_AMD64_R8,  
    REGISTER_AMD64_R9,  
    REGISTER_AMD64_R10,  
    REGISTER_AMD64_R11,  
    REGISTER_AMD64_R12,  
    REGISTER_AMD64_R13,  
    REGISTER_AMD64_R14,  
    REGISTER_AMD64_R15,  
  
    REGISTER_AMD64_XMM0,  
    REGISTER_AMD64_XMM1,  
    REGISTER_AMD64_XMM2,  
    REGISTER_AMD64_XMM3,  
    REGISTER_AMD64_XMM4,  
    REGISTER_AMD64_XMM5,  
    REGISTER_AMD64_XMM6,  
    REGISTER_AMD64_XMM7,  
    REGISTER_AMD64_XMM8,  
    REGISTER_AMD64_XMM9,  
    REGISTER_AMD64_XMM10,  
    REGISTER_AMD64_XMM11,  
    REGISTER_AMD64_XMM12,  
    REGISTER_AMD64_XMM13,  
    REGISTER_AMD64_XMM14,  
    REGISTER_AMD64_XMM15,  
  
    REGISTER_IA64_BSP = REGISTER_FRAME_POINTER,  
    REGISTER_IA64_R0  = REGISTER_IA64_BSP + 1,  
    REGISTER_IA64_F0  = REGISTER_IA64_R0  + 128,  
    REGISTER_ARM_PC = 0,  
    REGISTER_ARM_SP,  
    REGISTER_ARM_R0,  
    REGISTER_ARM_R1,  
    REGISTER_ARM_R2,  
    REGISTER_ARM_R3,  
    REGISTER_ARM_R4,  
    REGISTER_ARM_R5,  
    REGISTER_ARM_R6,  
    REGISTER_ARM_R7,  
    REGISTER_ARM_R8,  
    REGISTER_ARM_R9,  
    REGISTER_ARM_R10,  
    REGISTER_ARM_R11,  
    REGISTER_ARM_R12,  
    REGISTER_ARM_LR,  
  
} CorDebugRegister;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`REGISTER_INSTRUCTION_POINTER`|프로세서의 명령 포인터 레지스터입니다.|  
|`REGISTER_STACK_POINTER`|프로세서의 스택 포인터 레지스터입니다.|  
|`REGISTER_FRAME_POINTER`|프로세서의 프레임 포인터 레지스터입니다.|  
|`REGISTER_X86_EIP`|x86 프로세서의 명령 포인터 레지스터입니다.|  
|`REGISTER_X86_ESP`|x86 프로세서의 스택 포인터 레지스터입니다.|  
|`REGISTER_X86_EBP`|x86 프로세서의 기본 포인터 레지스터입니다.|  
|`REGISTER_X86_EAX`|x86 프로세서의 A 데이터 레지스터입니다.|  
|`REGISTER_X86_ECX`|x86 프로세서의 C 데이터 레지스터입니다.|  
|`REGISTER_X86_EDX`|x86 프로세서의 D 데이터 레지스터입니다.|  
|`REGISTER_X86_EBX`|x86 프로세서의 B 데이터 레지스터입니다.|  
|`REGISTER_X86_ESI`|x86 프로세서의 소스 인덱스 레지스터입니다.|  
|`REGISTER_X86_EDI`|x86 프로세서의 대상 인덱스 레지스터입니다.|  
|`REGISTER_X86_FPSTACK_0`|x86 FP(부동 소수점) 프로세서의 스택 레지스터 0입니다.|  
|`REGISTER_X86_FPSTACK_1`|x86 FP 프로세서의 1번 스택 레지스터입니다.|  
|`REGISTER_X86_FPSTACK_2`|x86 FP 프로세서의 2번 스택 레지스터입니다.|  
|`REGISTER_X86_FPSTACK_3`|x86 FP 프로세서의 3번 스택 레지스터입니다.|  
|`REGISTER_X86_FPSTACK_4`|x86 FP 프로세서의 4번 스택 레지스터입니다.|  
|`REGISTER_X86_FPSTACK_5`|x86 FP 프로세서의 5번 스택 레지스터입니다.|  
|`REGISTER_X86_FPSTACK_6`|x86 FP 프로세서의 6번 스택 레지스터입니다.|  
|`REGISTER_X86_FPSTACK_7`|x86 FP 프로세서의 7번 스택 레지스터입니다.|  
|`REGISTER_AMD64_RIP`|AMD64 프로세서의 명령 포인터 레지스터입니다.|  
|`REGISTER_AMD64_RSP`|AMD64 프로세서의 스택 포인터 레지스터입니다.|  
|`REGISTER_AMD64_RBP`|AMD64 프로세서의 기본 포인터 레지스터입니다.|  
|`REGISTER_AMD64_RAX`|AMD64 프로세서의 A 데이터 레지스터입니다.|  
|`REGISTER_AMD64_RCX`|AMD64 프로세서의 C 데이터 레지스터입니다.|  
|`REGISTER_AMD64_RDX`|AMD64 프로세서의 D 데이터 레지스터입니다.|  
|`REGISTER_AMD64_RBX`|AMD64 프로세서의 B 데이터 레지스터입니다.|  
|`REGISTER_AMD64_RSI`|AMD64 프로세서의 소스 인덱스 레지스터입니다.|  
|`REGISTER_AMD64_RDI`|AMD64 프로세서의 대상 인덱스 레지스터입니다.|  
|`REGISTER_AMD64_R8`|AMD64 프로세서의 8번 데이터 레지스터입니다.|  
|`REGISTER_AMD64_R9`|AMD64 프로세서의 9번 데이터 레지스터입니다.|  
|`REGISTER_AMD64_R10`|AMD64 프로세서의 10번 데이터 레지스터입니다.|  
|`REGISTER_AMD64_R11`|AMD64 프로세서의 11번 데이터 레지스터입니다.|  
|`REGISTER_AMD64_R12`|AMD64 프로세서의 12번 데이터 레지스터입니다.|  
|`REGISTER_AMD64_R13`|AMD64 프로세서의 13번 데이터 레지스터입니다.|  
|`REGISTER_AMD64_R14`|AMD64 프로세서의 14번 데이터 레지스터입니다.|  
|`REGISTER_AMD64_R15`|AMD64 프로세서의 15번 데이터 레지스터입니다.|  
|`REGISTER_AMD64_XMM0`|AMD64 프로세서의 0번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM1`|AMD64 프로세서의 1번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM2`|AMD64 프로세서의 2번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM3`|AMD64 프로세서의 3번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM4`|AMD64 프로세서의 4번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM5`|AMD64 프로세서의 5번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM6`|AMD64 프로세서의 6번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM7`|AMD64 프로세서의 7번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM8`|AMD64 프로세서의 8번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM9`|AMD64 프로세서의 9번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM10`|AMD64 프로세서의 10번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM11`|AMD64 프로세서의 11번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM12`|AMD64 프로세서의 12번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM13`|AMD64 프로세서의 13번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM14`|AMD64 프로세서의 14번 멀티미디어 레지스터입니다.|  
|`REGISTER_AMD64_XMM15`|AMD64 프로세서의 15번 멀티미디어 레지스터입니다.|  
|`REGISTER_IA64_BSP`|IA-64 프로세서의 스택 포인터 레지스터입니다.|  
|`REGISTER_IA64_R0`|IA-64 프로세서의 0번 데이터 레지스터입니다.|  
|`REGISTER_IA64_F0`|IA-64 프로세서의 0번 FP 데이터 레지스터입니다.|  
|`REGISTER_ARM_PC`|ARM 프로세서의 프로그램 카운터 레지스터(R15)입니다.|  
|`REGISTER_ARM_SP`|ARM 프로세서의 스택 포인터 레지스터(R13)입니다.|  
|`REGISTER_ARM_R0`|ARM 프로세서의 데이터 레지스터 R0입니다.|  
|`REGISTER_ARM_R1`|ARM 프로세서의 데이터 레지스터 R1입니다.|  
|`REGISTER_ARM_R2`|ARM 프로세서의 데이터 레지스터 R2입니다.|  
|`REGISTER_ARM_R3`|ARM 프로세서의 데이터 레지스터 R3입니다.|  
|`REGISTER_ARM_R4`|ARM 프로세서의 레지스터 R4입니다.|  
|`REGISTER_ARM_R5`|ARM 프로세서의 레지스터 R5입니다.|  
|`REGISTER_ARM_R6`|ARM 프로세서의 레지스터 R6입니다.|  
|`REGISTER_ARM_R7`|ARM 프로세서의 레지스터 R7(THUMB 프레임 포인터)입니다.|  
|`REGISTER_ARM_R8`|ARM 프로세서의 레지스터 R8입니다.|  
|`REGISTER_ARM_R9`|ARM 프로세서의 레지스터 R9입니다.|  
|`REGISTER_ARM_R10`|ARM 프로세서의 레지스터 R10입니다.|  
|`REGISTER_ARM_R11`|ARM 프로세서의 프레임 포인터입니다.|  
|`REGISTER_ARM_R12`|ARM 프로세서의 레지스터 R12입니다.|  
|`REGISTER_ARM_LR`|ARM 프로세서의 링크 레지스터(R14)입니다.|  
  
## <a name="remarks"></a>설명  
 IA-64 프로세서에는 범용 데이터 레지스터와 부동 소수점 데이터 레지스터가 각각 128개씩 있지만 `REGISTER_IA64_R0` 및 `REGISTER_IA64_F0` 값만 제공됩니다. 나머지 값은 다음과 같이 결정할 수 있습니다.  
  
- `REGISTER_IA64_R0`~`REGISTER_IA64_R1` 값의 경우 레지스터 번호를 `REGISTER_IA64_R127`에 더합니다. 그러면 IA-64 프로세서에서 1번~127번 데이터 레지스터에 해당하는 값이 생성됩니다.  
  
- `REGISTER_IA64_F0`~`REGISTER_IA64_F1` 값의 경우 레지스터 번호를 `REGISTER_IA64_F127`에 더합니다. 그러면 IA-64 프로세서에서 1번~127번 FP 데이터 레지스터에 해당하는 값이 생성됩니다.  
  
 예를 들어 IA-64 프로세서의 83번 데이터 레지스터를 지정해야 한다면 `REGISTER_IA64_R0` + 83을 사용합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 열거형](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)
