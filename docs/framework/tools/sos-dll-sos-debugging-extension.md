---
title: SOS.dll(SOS 디버깅 확장명)
ms.date: 03/30/2017
helpviewer_keywords:
- debugging extensions
- SOS debugging extensions
- SOS.dll
ms.assetid: 9ac1b522-77ab-4cdc-852a-20fcdc9ae498
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2c6f2d001c6513211cf15993285e3564f7613402
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "47863665"
---
# <a name="sosdll-sos-debugging-extension"></a>SOS.dll(SOS 디버깅 확장)

SOS 디버깅 확장명(SOS.dll)을 사용하면 내부 CLR(공용 언어 런타임) 환경에 대한 정보를 제공하여 관리되는 프로그램을 Windows 디버거(WinDbg.exe)와 Visual Studio에서 쉽게 디버깅할 수 있습니다. 이 도구를 사용하려면 프로젝트에 관리되지 않는 디버깅을 활성화해야 합니다. SOS.dll은 .NET Framework와 함께 자동으로 설치됩니다. Visual Studio에서 SOS.dll을 사용하려면 [WDK(Windows 드라이버 키트)](/windows-hardware/drivers/download-the-wdk)를 설치합니다.

## <a name="syntax"></a>구문

```shell
![command] [options]
```

## <a name="commands"></a>명령

|명령|설명|
|-------------|-----------------|
|**AnalyzeOOM** (**ao**)|가비지 수집 힙에 대한 할당 요청에 발생한 마지막 OOM(메모리 부족)에 대한 정보를 표시합니다. (서버 가비지 컬렉션에서 각 가비지 컬렉션 힙에 OOM(있는 경우)을 표시합니다.)|
|**BPMD** [**-nofuturemodule**] [\<*module name*> \<*method name*>] [**-md** <`MethodDesc`>] **-list** **-clear** \<*pending breakpoint number*> **-clearall**|지정된 모듈의 지정된 메서드에 중단점을 만듭니다.<br /><br /> 지정된 모듈 및 메서드가 로드되지 않은 경우 이 명령은 모듈이 로드되고 JIT(Just-In-Time) 컴파일되었다는 알림을 받을 때까지 기다렸다가 중단점을 만듭니다.<br /><br /> **-list**, **-clear** 및 **-clearall** 옵션을 사용하여 보류 중단점 목록을 관리할 수 있습니다.<br /><br /> **-list** 옵션은 모든 보류 중단점의 목록을 생성합니다. 보류 중인 중단점에 0이 아닌 모듈 ID가 있는 경우 해당 중단점은 로드된 특정 모듈의 함수에 적용됩니다. 보류 중인 중단점에 0인 모듈 ID가 있을 경우 해당 중단점은 아직 로드되지 않은 모듈에 적용됩니다.<br /><br /> **-clear** 또는 **-clearall** 옵션을 사용하여 목록에서 보류 중단점을 제거합니다.|
|**CLRStack** [**-a**] [**-l**] [**-p**] [**-n**]|관리 코드의 스택 추적만 제공합니다.<br /><br /> **-p** 옵션은 관리되는 함수의 인수를 표시합니다.<br /><br /> **-l** 옵션은 프레임의 지역 변수에 대한 정보를 표시합니다. SOS 디버깅 확장에서 로컬 이름을 검색할 수 없으므로 로컬 이름의 출력은 \<*local address*> **=** \<*value*> 형식입니다.<br /><br /> **-a**(all) 옵션은 **-l** 및 **-p** 옵션을 동시에 지정하는 바로 가기입니다.<br /><br /> **-n** 옵션은 소스 파일 이름과 줄 번호의 표시를 사용하지 않도록 설정합니다. 디버거에 옵션 SYMOPT_LOAD_LINES가 지정된 경우 SOS는 관리되는 모든 프레임에 대한 기호를 조회하고, 성공한 경우, 해당 소스 파일 이름과 줄 번호를 표시합니다. 이 동작을 사용하지 않으려면 **-n**(줄 번호 없음) 매개 변수를 지정할 수 있습니다.<br /><br /> SOS 디버깅 확장에서는 x64 및 IA-64 기반 플랫폼에 전환 프레임을 표시하지 않습니다.|
|**COMState**|각 스레드의 COM 아파트 모델과 `Context` 포인터를 나열합니다(사용할 수 있는 경우).|
|**DumpArray** [**-start** \<*startIndex*>] [**-length** \<*length*>] [**-details**] [**-nofields**] \<*array object address*><br /><br /> 또는<br /><br /> **DA** [**-start** \<*startIndex*>] [**-length** \<*length*>] [**-detail**] [**-nofields**] *array object address*>|배열 개체의 요소를 검사합니다.<br /><br /> **-start** 옵션은 요소를 표시할 시작 인덱스를 지정합니다.<br /><br /> **-length** 옵션은 표시할 요소의 수를 지정합니다.<br /><br /> **-details** 옵션은 **DumpObj** 및 **DumpVC** 형식을 사용하여 요소의 세부 정보를 표시합니다.<br /><br /> **-nofields** 옵션은 배열이 표시되지 않도록 합니다. 이 옵션은 **-detail** 옵션을 지정한 경우에만 사용할 수 있습니다.|
|**DumpAssembly** \<*assembly address*>|어셈블리에 대한 정보를 표시합니다.<br /><br /> **DumpAssembly** 명령은 여러 모듈을 나열합니다(있는 경우).<br /><br /> **DumpDomain** 명령을 사용하여 어셈블리 주소를 가져올 수 있습니다.|
|**DumpClass** \<*EEClass address*>|형식과 연관된 `EEClass` 구조체에 대한 정보를 표시합니다.<br /><br /> **DumpClass** 명령은 정적 필드 값을 표시하지만, 비정적 필드 값은 표시하지 않습니다.<br /><br /> `EEClass` 구조체 주소를 가져오려면 **DumpMT**, **DumpObj**, **Name2EE** 또는 **Token2EE** 명령을 사용합니다.|
|**DumpDomain** [\<*domain address*>]|지정된 <xref:System.Reflection.Assembly> 개체 주소 내에 로드된 각 <xref:System.AppDomain> 개체를 열거합니다.  매개 변수 없이 호출된 경우 **DumpDomain** 명령은 프로세스의 모든 <xref:System.AppDomain> 개체를 나열합니다.|
|**DumpHeap** [**-stat**] [**-strings**] [**-short**] [**-min** \<*size*>] [**-max** \<*size*>] [**-thinlock**] [**-startAtLowerBound**] [**-mt** \<*MethodTable address*>] [**-type** \<*partial type name*>][*start* [*end*]]|가비지 컬렉션된 힙에 대한 정보와 개체에 대한 컬렉션 통계를 표시합니다.<br /><br /> **DumpHeap** 명령은 가비지 수집기 힙에서 과도한 조각화를 감지하면 경고를 표시합니다.<br /><br /> **-stat** 옵션은 출력을 통계 형식 요약으로 제한합니다.<br /><br /> **-strings** 옵션은 출력을 통계 형식 문자열 값 요약으로 제한합니다.<br /><br /> **-short** 옵션은 출력을 각 개체의 주소로 제한합니다. 이 명령의 출력을 자동화를 위해 다른 디버거 명령에 쉽게 파이프할 수 있습니다.<br /><br /> **-min** 옵션은 바이트로 지정된 `size` 매개 변수보다 작은 개체를 무시합니다.<br /><br /> **-max** 옵션은 바이트로 지정된 `size` 매개 변수보다 큰 개체를 무시합니다.<br /><br /> **-thinlock** 옵션은 ThinLocks를 보고합니다.  자세한 내용은 **SyncBlk** 명령을 참조하세요.<br /><br /> `-startAtLowerBound` 옵션은 제공된 주소 범위의 하한에서 힙 워크가 시작되도록 만듭니다. 계획 단계 동안에는 개체가 이동 중이기 때문에 종종 힙을 움직일 수 없습니다. 이 옵션은 **DumpHeap**이 지정된 하한에서 Walk를 시작하도록 합니다. 이 옵션이 작동하려면 유효한 개체의 주소를 하한으로 제공해야 합니다. 다음 메서드 테이블을 수동으로 찾기 위해 잘못된 개체의 주소에서 메모리를 표시할 수 있습니다. 가비지 수집이 현재 `memcopy`에 대한 호출에 있는 경우 크기를 매개 변수로 제공되는 시작 주소에 추가하여 다음 개체의 주소를 찾을 수도 있습니다.<br /><br /> **-mt** 옵션은 지정된 `MethodTable` 구조체에 해당하는 개체만 나열합니다.<br /><br /> **-type** 옵션은 형식 이름이 지정된 문자열의 부분 문자열과 일치하는 개체만 나열합니다.<br /><br /> `start` 매개 변수는 지정된 주소부터 나열을 시작합니다.<br /><br /> `end` 매개 변수는 지정된 주소에서 나열을 중지합니다.|
|**DumpIL** \<*Managed DynamicMethod object*> |       \<*DynamicMethodDesc pointer*> |        \<*MethodDesc pointer*>|관리되는 메서드와 연관된 MSIL(Microsoft intermediate language)을 표시합니다.<br /><br /> 동적 MSIL은 어셈블리에서 로드된 MSIL과는 다르게 내보내집니다. 동적 MSIL은 메타데이터 토큰 대신 관리되는 개체 배열의 개체를 참조합니다.|
|**DumpLog** [**-addr** \<*addressOfStressLog*>] [<*Filenam*`e`>]|메모리 내 스트레스 로그의 내용을 지정된 파일에 씁니다. 이름을 지정하지 않으면 이 명령은 현재 디렉터리에 StressLog.txt라는 파일을 만듭니다.<br /><br /> 메모리 내 스트레스 로그는 잠금 또는 I/O를 사용하지 않고 진단 스트레스 오류에 도움을 줍니다. 스트레스 로그를 사용하려면 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework에서 다음 레지스트리 키를 설정합니다.<br /><br /> (DWORD) StressLog = 1<br /><br /> (DWORD) LogFacility = 0xffffffff<br /><br /> (DWORD) StressLogSize = 65536<br /><br /> 선택적 `-addr` 옵션을 사용하면 기본 로그 외에 다른 스트레스 로그를 지정할 수 있습니다.|
|**DumpMD** \<*MethodDesc address*>|지정된 주소의 `MethodDesc` 구조체에 대한 정보를 표시합니다.<br /><br /> **IP2MD** 명령을 사용하여 관리되는 함수에서 `MethodDesc` 구조체 주소를 가져올 수 있습니다.|
|**DumpMT** [**-MD**] \<*MethodTable address*>|지정된 주소의 메서드 테이블에 대한 정보를 표시합니다. **-MD** 옵션을 지정하면 개체와 함께 정의된 모든 메서드의 목록을 표시합니다.<br /><br /> 관리되는 각 개체에는 메서드 테이블 포인터가 들어 있습니다.|
|**DumpMethodSig** \<*sigaddr*> <*moduleadd*`r`>|지정된 주소의 `MethodSig` 구조체에 대한 정보를 표시합니다.|
|**DumpModule** [**-mt**] \<*Module address*>|지정된 주소의 모듈에 대한 정보를 표시합니다. **-mt** 옵션은 모듈에 정의된 형식과 모듈에서 참조하는 형식을 표시합니다.<br /><br /> **DumpDomain** 또는 **DumpAssembly** 명령을 사용하여 모듈의 주소를 검색할 수 있습니다.|
|**DumpObj** [**-nofields**] \<*object address*><br /><br /> 또는<br /><br /> **DO** \<*object address*>|지정된 주소의 개체에 대한 정보를 표시합니다. **DumpObj** 명령은 필드, `EEClass` 구조체 정보, 메서드 테이블 및 개체 크기를 표시합니다.<br /><br /> **DumpStackObjects** 명령을 사용하여 개체의 주소를 검색할 수 있습니다.<br /><br /> `CLASS` 형식의 필드도 개체이므로 이러한 필드에서 **DumpObj** 명령을 실행할 수 있습니다.<br /><br /> `-`**nofields** 옵션은 개체의 필드가 표시되지 않도록 방지하며, String과 같은 개체에 유용합니다.|
|**DumpRuntimeTypes**|가비지 수집기 힙에 있는 런타임 형식 개체를 표시하고 해당 개체에 연관된 형식 이름과 메서드 테이블을 나열합니다.|
|**DumpStack** [**-EE**] [**-n**] [`top` *stack* [`bottom` *stac*`k`]]|스택 추적을 표시합니다.<br /><br /> **-EE** 옵션을 사용하면 **DumpStack** 명령이 관리되는 함수만 표시합니다. x86 플랫폼에 표시되는 스택 프레임을 제한하려면 `top` 및 `bottom` 매개 변수를 사용합니다.<br /><br /> **-n** 옵션은 소스 파일 이름과 줄 번호의 표시를 사용하지 않도록 설정합니다. 디버거에 옵션 SYMOPT_LOAD_LINES가 지정된 경우 SOS는 관리되는 모든 프레임에 대한 기호를 조회하고, 성공한 경우, 해당 소스 파일 이름과 줄 번호를 표시합니다. 이 동작을 사용하지 않으려면 **-n**(줄 번호 없음) 매개 변수를 지정할 수 있습니다.<br /><br /> x86 및 x64 플랫폼에서 **DumpStack** 명령은 자세한 스택 추적을 만듭니다.<br /><br /> IA-64 기반 플랫폼에서 **DumpStack** 명령은 디버거의 **K** 명령과 비슷하게 작동합니다. `top` 및 `bottom` 매개 변수는 IA-64 기반 플랫폼에서 무시됩니다.|
|**DumpSig** \<*sigaddr*> \<*moduleaddr*>|지정된 주소의 `Sig` 구조체에 대한 정보를 표시합니다.|
|**DumpSigElem** \<*sigaddr*> \<*moduleaddr*>|서명 개체의 단일 요소를 표시합니다. 대부분의 경우 개별 서명 개체를 보려면 **DumpSig**를 사용해야 합니다. 그러나 어떤 방식으로든 서명이 손상된 경우 **DumpSigElem**을 사용하여 유효한 부분을 읽을 수 있습니다.|
|**DumpStackObjects** [**-verify**] [`top` *stack* [`bottom` *stack*]]<br /><br /> 또는<br /><br /> **DSO** [**-verify**] [`top` *stack* [`bottom` *stack*]]|현재 스택의 범위 내에 있는 관리되는 모든 개체를 표시합니다.<br /><br /> **-verify** 옵션은 개체 필드의 비정적 `CLASS` 필드 각각의 유효성을 검사합니다.<br /><br /> 지역 변수 및 매개 변수의 값을 확인하려면 스택 추적 명령(예: **K** 명령 및 **CLRStack** 명령)과 함께 **DumpStackObject** 명령을 사용합니다.|
|**DumpVC** \<*MethodTable address*> \<*Address*>|지정된 주소에 있는 값 클래스의 필드에 대한 정보를 표시합니다.<br /><br /> **MethodTable** 매개 변수를 사용하면 **DumpVC** 명령이 필드를 올바르게 해석할 수 있습니다. 값 클래스에는 첫 번째 필드로 메서드 테이블이 포함되지 않습니다.|
|**EEHeap** [**-gc**] [**-loader**]|내부 CLR 데이터 구조에서 사용되는 프로세스 메모리에 대한 정보를 표시합니다.<br /><br /> **-gc** 및 **-loader** 옵션은 이 명령의 출력을 가비지 수집기 또는 로더 데이터 구조로 제한합니다.<br /><br /> 가비지 컬렉션기에 대한 정보에는 관리되는 힙의 각 세그먼트 범위가 나열됩니다.  포인터가 **-gc**로 지정된 세그먼트 범위 내에 있으면 해당 포인터는 개체 포인터입니다.|
|**EEStack** [**-short**] [**-EE**]|프로세스의 모든 스레드에서 **DumpStack** 명령을 실행합니다.<br /><br /> **-EE** 옵션은 **DumpStack** 명령에 직접 전달됩니다. **-short** 매개 변수는 출력을 다음과 같은 종류의 스레드로 제한합니다.<br /><br /> 잠긴 스레드<br /><br /> 가비지 수집을 위해 중단된 스레드<br /><br /> 현재 관리 코드에 있는 스레드|
|**EEVersion**|CLR 버전을 표시합니다.|
|**EHInfo** [\<*MethodDesc address*>] [\<*Code address*>]|지정된 메서드의 예외 처리 블록을 표시합니다.  이 명령은 절 블록(`try` 블록) 및 처리기 블록(`catch` 블록)의 코드 주소와 오프셋을 표시합니다.|
|**FAQ**|FAQ(질문과 대답)를 표시합니다.|
|**FinalizeQueue** [**-detail**] | [**-allReady**] [**-short**]|종료하도록 등록된 모든 개체를 표시합니다.<br /><br /> **-detail** 옵션은 정리해야 하는 모든 `SyncBlocks`와 정리를 기다리는 모든 `RuntimeCallableWrappers`(RCWs)에 대한 추가 정보를 표시합니다. 이러한 두 데이터 구조는 실행할 때 모두 종료자 스레드에서 캐시되고 정리됩니다.<br /><br /> `-allReady` 옵션은 가비지 컬렉션에 의해 이미 표시되거나 다음 가비지 컬렉션에 의해 표시될지 여부에 관계없이 종료할 준비가 된 모든 개체를 표시합니다. "종료 준비" 목록에 있는 개체는 더 이상 루트에 있지 않은 종료할 수 있는 개체입니다. 종료 가능한 큐에 있는 모든 개체가 여전히 루트인지 여부를 확인하기 때문에 이 옵션은 매우 많은 비용이 소요될 수 있습니다.<br /><br /> `-short` 옵션은 각 개체의 주소로 출력을 제한합니다. **-allReady**와 함께 사용하면 더 이상 루트가 아닌 종료자가 있는 개체를 모두 열거합니다. 독립적으로 사용되는 경우 종료 가능 및 "종료 준비" 큐에 모든 개체를 나열합니다.|
|**FindAppDomain** \<*Object address*>|지정된 주소에 있는 개체의 응용 프로그램 도메인을 확인합니다.|
|**FindRoots** **-gen** \<*N*> | **-gen any** |\<*object address*>|디버거가 지정된 생성의 다음 컬렉션에서 디버기를 중단하도록 합니다. 효과는 중단이 발생하는 즉시 다시 설정됩니다. 다음 컬렉션에서 중단하려면 명령을 다시 실행해야 합니다. 이 명령의 *\<object address>* 양식은 **-gen** 또는 **-gen any**로 인한 중단이 발생한 후에 사용됩니다. 중단 발생 시점에서 디버기가 현재 문제가 되는 생성의 개체에 대한 루트를 **FindRoots**에서 식별하는 올바른 상태에 있습니다.|
|**GCHandles** [**-perdomain**]|프로세스의 가비지 수집기 핸들에 대한 통계를 표시합니다.<br /><br /> **-perdomain** 옵션은 통계를 응용 프로그램 도메인별로 정렬합니다.<br /><br /> 가비지 수집기 핸들 누수로 인한 메모리 누수를 확인하려면 **GCHandles** 명령을 사용합니다. 예를 들어, 강력한 가비지 수집기 핸들이 코드에서 큰 배열을 가리키고 있어서 아직 배열이 해제되지 않은 상태로 핸들을 삭제하면 메모리 누수가 발생합니다.|
|**GCHandleLeaks**|메모리에서 프로세스의 강력하고 고정된 가비지 수집기 핸들에 대한 참조를 검색하여 결과를 표시합니다. 핸들이 있으면 **GCHandleLeaks** 명령은 참조의 주소를 표시합니다. 메모리에 핸들이 없으면 이 명령은 알림을 표시합니다.|
|**GCInfo** \<*MethodDesc address*>\<*Code address*>|레지스터 또는 스택 위치에 관리되는 개체가 포함되는 시기를 나타내는 데이터를 표시합니다. 가비지 컬렉션이 수행될 때 수집기에서는 개체에 대한 참조의 위치를 알고 있어야 새 개체 포인터 값으로 업데이트할 수 있습니다.|
|**GCRoot** [**-nostacks**] \<*Object address*>|지정된 주소의 개체에 대한 참조(또는 루트)와 관련된 정보를 표시합니다.<br /><br /> **GCRoot** 명령은 관리되는 전체 힙 및 스택의 다른 개체와 핸들 내에 있는 핸들에 대한 핸들 테이블을 검사합니다. 그런 다음 각 스택에서 개체에 대한 포인터를 검색하고 종료자 큐도 검색합니다.<br /><br /> 이 명령은 스택 루트가 유효하거나 삭제되었는지는 확인하지 않습니다. 스택 루트가 여전히 사용 중인지 확인하기 위해 로컬 또는 인수 값이 속한 프레임을 디스어셈블하려면 **CLRStack** 및 **U** 명령을 사용합니다.<br /><br /> **-nostacks** 옵션은 검색을 가비지 수집기 핸들 및 종료-도달(freachable) 개체로 제한합니다.|
|**GCWhere**  *\<object address>*|가비지 수집 힙에서 전달된 인수의 위치와 크기를 표시합니다. 인수가 관리되는 힙에 있지만 유효한 개체 주소가 아니면 크기는 0(영)으로 표시됩니다.|
|**help** [\<*command*>] [`faq`]|매개 변수가 지정되지 않은 경우 사용할 수 있는 모든 명령을 표시하거나, 지정된 명령에 대한 자세한 도움말 정보를 표시합니다.<br /><br /> `faq` 매개 변수는 질문과 대답을 표시합니다.|
|**HeapStat** [**-inclUnrooted** | **-iu**]|각 힙의 생성 크기와 각 힙의 각 세대에 있는 총 여유 공간을 표시합니다. -**inclUnrooted** 옵션을 지정하면 더 이상 루트가 아닌 가비지 수집 힙의 관리되는 개체에 대한 정보가 보고서에 포함됩니다.|
|**HistClear**|`Hist` 명령의 패밀리에서 사용하는 모든 리소스를 해제합니다.<br /><br /> 일반적으로 각 `HistClear`가 이전 리소스를 정리하기 때문에 `HistInit`를 명시적으로 호출할 필요가 없습니다.|
|**HistInit**|디버기에 저장된 스트레스 로그에서 SOS 구조를 초기화합니다.|
|**HistObj** *<obj_address>*|모든 스트레스 로그 재배치 레코드를 검사하여 인수로 전달된 주소로 연결될 수 있는 가비지 수집 재배치의 체인을 표시합니다.|
|**HistObjFind**  *<obj_address>*|지정된 주소의 개체를 참조하는 모든 로그 항목을 표시합니다.|
|**HistRoot** *\<root>*|지정된 루트의 승격 및 재배치와 관련된 정보를 표시합니다.<br /><br /> 루트 값은 가비지 컬렉션을 통해 개체의 움직임을 추적하는 데 사용할 수 있습니다.|
|**IP2MD** \<*Code address*>|JIT 컴파일된 코드의 지정된 주소에 있는 `MethodDesc` 구조체를 표시합니다.|
|`ListNearObj` (`lno`) *<obj_address>*|지정된 주소 앞에 오거나 뒤에 오는 개체를 표시합니다. 명령은 관리되는 개체(유효한 메서드 테이블을 기준으로 함)와 인수 주소 다음에 있는 개체의 유효한 시작처럼 보이는 가비지 수집 힙에서 주소를 찾습니다.|
|**MinidumpMode** [**0**] [**1**]|미니덤프를 사용할 때 안전하지 않은 명령이 실행되지 않도록 합니다.<br /><br /> 이 기능을 해제하려면 **0**을 전달하고, 설정하려면 **1**을 전달합니다. 기본적으로 **MinidumpMode** 값은 **0**으로 설정됩니다.<br /><br /> **.dump /m** 명령 또는 **.dump** 명령으로 만들어진 미니덤프에는 제한된 CLR 관련 데이터가 있으며, 이 미니덤프를 사용하면 SOS 명령의 하위 집합만 올바르게 실행할 수 있습니다. 일부 명령은 필요한 메모리 영역이 매핑되지 않거나 부분적으로만 매핑되었기 때문에 예기치 않은 오류와 함께 실패할 수 있습니다. 이 옵션은 미니덤프에 대해 안전하지 않은 명령이 실행되지 않도록 합니다.|
|**Name2EE** \<*module name*> \<*type or method name*><br /><br /> 또는<br /><br /> **Name2EE** \<*module name*>**!**\<*type or method name*>|지정된 모듈에 있는 지정된 형식 또는 메서드의 `MethodTable` 구조체와 `EEClass` 구조체를 표시합니다.<br /><br /> 지정된 모듈은 프로세스에 로드되어 있어야 합니다.<br /><br /> 올바른 형식 이름을 가져오려면 [Ildasm.exe(IL 디스어셈블러)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)를 사용하여 모듈을 찾아봅니다. `*`를 module name 매개 변수로 전달하여 로드된 모든 관리되는 모듈을 검색할 수도 있습니다. *module name* 매개 변수는 모듈의 디버거 이름(예: `mscorlib` 또는 `image00400000`)일 수도 있습니다.<br /><br /> 이 명령은 <`module`>`!`<`type`>의 Windows 디버거 구문을 지원합니다. 해당 형식은 정규화된 형식이어야 합니다.|
|**ObjSize** [\<*Object address*>] | [**-aggregate**] [**-stat**]|지정된 개체의 크기를 표시합니다. 매개 변수를 지정하지 않으면 **ObjSize** 명령은 관리되는 스레드에 있는 모든 개체의 크기를 표시하고, 프로세스의 모든 가비지 수집기 핸들 및 이러한 핸들이 가리키는 모든 개체의 총 크기를 표시합니다. **ObjSize** 명령은 부모 개체뿐만 아니라 모든 자식 개체의 크기도 포함합니다.<br /><br /> **-aggregate** 옵션은 **-stat** 인수와 함께 사용하여 여전히 루트인 형식의 자세한 보기를 얻을 수 있습니다. **!dumpheap -stat** 및 **!objsize -aggregate -stat**를 사용하면 더 이상 루트가 아닌 개체를 확인하고 다양한 메모리 문제를 진단할 수 있습니다.|
|**PrintException** [**-nested**] [**-lines**] [\<*Exception object address*>]<br /><br /> 또는<br /><br /> **PE** [**-nested**] [\<*Exception object address*>]|지정된 주소의 <xref:System.Exception> 클래스에서 파생된 개체 필드를 표시하고 필드의 형식을 지정합니다. 주소를 지정하지 않으면 **PrintException** 명령은 현재 스레드에서 마지막으로 throw된 예외를 표시합니다.<br /><br /> **-nested** 옵션은 중첩된 예외 개체에 대한 자세한 정보를 표시합니다.<br /><br /> **-lines** 옵션은 가능한 경우 소스 정보를 표시합니다.<br /><br /> 이 명령을 사용하여 이진 배열인 `_stackTrace` 필드의 형식을 지정하고 해당 필드를 볼 수 있습니다.|
|**ProcInfo** [**-env**] [**-time**] [**-mem**]|프로세스의 환경 변수, 커널 CPU 시간 및 메모리 사용 통계를 표시합니다.|
|**RCWCleanupList** \<*RCWCleanupList address*>|지정된 주소에서 정리를 기다리는 런타임 호출 가능 래퍼의 목록을 표시합니다.|
|**SaveModule** \<*Base address*> \<*Filename*>|지정된 주소의 메모리에 로드된 이미지를 지정된 파일에 씁니다.|
|**SOSFlush**|내부 SOS 캐시를 플러시합니다.|
|**StopOnException** [**-derived**] [**-create** | **-create2**] \<*Exception*> \<*Pseudo-register number*>|지정된 예외가 throw되면 디버거가 중지되고 다른 예외가 throw되면 계속 실행되도록 합니다.<br /><br /> **-derived** 옵션은 지정된 예외와 지정된 예외에서 파생되는 모든 예외를 catch합니다.|
|**SyncBlk** [**-all** | \<*syncblk number*>]|지정된 `SyncBlock` 구조체나 모든 `SyncBlock` 구조체를 표시합니다.  인수를 전달하지 않으면 **SyncBlk** 명령은 스레드에서 소유하는 개체에 해당하는 `SyncBlock` 구조체를 표시합니다.<br /><br /> `SyncBlock` 구조체는 모든 개체에 대해 만들 필요가 없는 추가 정보를 포함하기 위한 컨테이너입니다. 이 구조체는 COM interop 데이터, 해시 코드 및 스레드로부터 안전한 작업에 대한 잠금 정보를 포함할 수 있습니다.|
|**ThreadPool**|큐에 대기 중인 작업 요청 수, 완료 포트 스레드 수 및 타이머 수를 비롯하여 관리되는 스레드 풀에 대한 정보를 표시합니다.|
|**Token2EE** \<*module name*> \<*token*>|지정된 모듈의 지정된 메타데이터 토큰을 `MethodTable` 구조체나 `MethodDesc` 구조체로 전환합니다.<br /><br /> module name 매개 변수에 `*`를 전달하면 로드된 모든 관리되는 모듈에서 해당 토큰이 매핑되는 대상을 확인할 수 있습니다. `mscorlib` 또는 `image00400000`과 같이 모듈의 디버거 이름을 전달할 수도 있습니다.|
|**Threads** [**-live**] [**-special**]|프로세스의 관리되는 모든 스레드를 표시합니다.<br /><br /> **Threads** 명령은 디버거 약식 ID, CLR 스레드 ID 및 운영 체제 스레드 ID를 표시합니다.  또한 **Threads** 명령은 스레드가 실행 중인 응용 프로그램 도메인을 나타내는 Domain 열, COM 아파트 모드를 표시하는 APT 열 및 스레드에서 마지막으로 throw된 예외를 표시하는 Exception 열을 표시합니다.<br /><br /> **-live** 옵션은 라이브 스레드와 연결된 스레드를 표시합니다.<br /><br /> **-special** 옵션은 CLR에서 만들어진 모든 특수 스레드를 표시합니다. 특수 스레드에는 가비지 수집 스레드(동시 및 서버 가비지 수집), 디버거 도우미 스레드, 종료자 스레드, <xref:System.AppDomain> 언로드 스레드 및 스레드 풀 타이머 스레드가 포함됩니다.|
|**ThreadState \<** *State value field* **>**|스레드의 현재 상태를 표시합니다. `value` 매개 변수는 **Threads** 보고서 출력의 `State` 필드 값입니다.<br /><br /> 예제:<br /><br /> `0:003> !Threads     ThreadCount:      2     UnstartedThread:  0     BackgroundThread: 1     PendingThread:    0     DeadThread:       0     Hosted Runtime:   no                                           PreEmptive   GC Alloc           Lock            ID OSID ThreadOBJ    State     GC       Context       Domain   Count APT Exception        0    1  250 0019b068      a020 Disabled 02349668:02349fe8 0015def0     0 MTA        2    2  944 001a6020      b220 Enabled  00000000:00000000 0015def0     0 MTA (Finalizer)     0:003> !ThreadState b220         Legal to Join         Background         CLR Owns         CoInitialized         In Multi Threaded Apartment`|
|**TraverseHeap** [**-xml**] \<*filename*>|힙 정보를 CLR 프로파일러에서 인식할 수 있는 형식으로 지정된 파일에 씁니다. **-xml** 옵션을 사용하면 **TraverseHeap** 명령은 파일을 XML 형식으로 지정합니다.<br /><br /> CLR 프로파일러는 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?LinkID=67325)에서 다운로드할 수 있습니다.|
|**U** [**-gcinfo**] [**-ehinfo**] [**-n**] \<*MethodDesc address*> | \<*Code address*>|메서드의 `MethodDesc` 구조체 포인터나 메서드 본문 내의 코드 주소로 지정된 관리되는 메서드에 대해 주석이 지정된 디스어셈블리를 표시합니다. **U** 명령은 메타데이터 토큰을 이름으로 변환하는 주석과 함께 전체 메서드를 처음부터 끝까지 표시합니다.<br /><br /> **-gcinfo** 옵션을 사용하면 **U** 명령은 메서드의 `GCInfo` 구조체를 표시합니다.<br /><br /> **-ehinfo** 옵션은 메서드에 대한 예외 정보를 표시합니다. **EHInfo** 명령을 사용하여 이 정보를 얻을 수도 있습니다.<br /><br /> **-n** 옵션은 소스 파일 이름과 줄 번호의 표시를 사용하지 않도록 설정합니다. 디버거에 옵션 SYMOPT_LOAD_LINES가 지정된 경우 SOS는 관리되는 모든 프레임에 대한 기호를 조회하고, 성공한 경우, 해당 소스 파일 이름과 줄 번호를 표시합니다. 이 동작을 사용하지 않으려면 **-n** 옵션을 지정할 수 있습니다.|
|**VerifyHeap**|가비지 수집기 힙에서 손상된 곳이 있는지 확인하고 찾은 오류를 표시합니다.<br /><br /> 플랫폼 호출이 잘못 구성되면 힙이 손상될 수 있습니다.|
|**VerifyObj** \<*object address*>|기호 손상에 대한 인수로 전달되는 개체를 검사합니다.|
|**VMMap**|가상 주소 공간으로 이동하여 각 영역에 적용된 보호 형식을 표시합니다.|
|**VMStat**|가상 주소 공간의 요약 뷰를 제공합니다. 이 뷰에서는 해당 메모리에 적용된 각 보호 형식(사용 가능, 예약됨, 커밋됨, 전용, 매핑됨, 이미지)별로 정렬됩니다. TOTAL 열에는 AVERAGE 열에 BLK COUNT 열을 곱한 결과가 표시됩니다.|

## <a name="remarks"></a>설명

SOS 디버깅 확장을 사용하면 CLR 내에서 실행되는 코드에 대한 정보를 볼 수 있습니다. 예를 들어, SOS 디버깅 확장을 사용하여 관리되는 힙에 대한 정보를 표시하고, 힙 손상을 찾고, 런타임에 사용되는 내부 데이터 형식을 표시하고, 런타임 내에서 실행되는 관리되는 모든 코드에 대한 정보를 볼 수 있습니다.

Visual Studio에서 SOS 디버깅 확장을 사용하려면 [WDK(Windows 드라이버 키트)](/windows-hardware/drivers/download-the-wdk)를 설치합니다. Visual Studio의 통합 디버깅 환경에 대한 자세한 내용은 [디버깅 환경](/windows-hardware/drivers/debugger/debuggers-in-the-debugging-tools-for-windows-package)을 참조하세요.

[WinDbg.exe 디버거](/windows-hardware/drivers/debugger/debugger-download-tools)에 로드하고 WinDbg.exe 내에서 명령을 실행하여 SOS 디버깅 확장을 사용할 수도 있습니다.

SOS 디버깅 확장을 WinDbg.exe 디버거에 로드하려면 도구에서 다음 명령을 실행합니다.

```
.loadby sos clr
```

WinDbg.exe 및 Visual Studio에서는 현재 사용 중인 Mscorwks.dll 버전에 해당하는 버전의 SOS.dll을 사용합니다. 기본적으로 현재 Mscorwks.dll 버전과 일치하는 버전의 SOS.dll을 사용해야 합니다.

다른 컴퓨터에서 만든 덤프 파일을 사용하려면 해당 프로그램과 함께 설치된 Mscorwks.dll 파일이 기호 경로에 있는지 확인하고 해당하는 버전의 SOS.dll을 로드해야 합니다.

특정 버전의 SOS.dll을 로드하려면 Windows 디버거에 다음 명령을 입력합니다.

```
.load <full path to sos.dll>
```

## <a name="examples"></a>예제

다음 명령은 `00ad28d0` 주소에 있는 배열의 내용을 표시합니다.  두 번째 요소부터 시작하여 다섯 개의 요소까지 계속해서 표시합니다.

```
!dumparray -start 2 -length 5 -detail 00ad28d0
```

 다음 명령은 `1ca248` 주소에 있는 어셈블리의 내용을 표시합니다.

```
!dumpassembly 1ca248
```

 다음 명령은 가비지 수집기 힙에 대한 정보를 표시합니다.

```
!dumpheap
```

 다음 명령은 현재 디렉터리에 있는 StressLog.txt라는 (기본) 파일에 메모리 내 스트레스 로그의 내용을 씁니다.

```
!DumpLog
```

 다음 명령은 `MethodDesc` 주소의 `902f40` 구조체를 표시합니다.

```
!dumpmd 902f40
```

 다음 명령은 `1caa50` 주소의 모듈에 대한 정보를 표시합니다.

```
!dumpmodule 1caa50
```

 다음 명령은 `a79d40` 주소의 개체에 대한 정보를 표시합니다.

```
!DumpObj a79d40
```

 다음 명령은 `00a79d9c` 주소에서 메서드 테이블을 사용하여 `0090320c` 주소의 값 클래스 필드를 표시합니다.

```
!DumpVC 0090320c 00a79d9c
```

 다음 명령은 가비지 수집기에서 사용되는 프로세스 메모리를 표시합니다.

```
!eeheap -gc
```

 다음 명령은 종료하도록 예약된 모든 개체를 표시합니다.

```
!finalizequeue
```

 다음 명령은 `00a79d98` 주소에 있는 개체의 응용 프로그램 도메인을 확인합니다.

```
!findappdomain 00a79d98
```

 다음 명령은 현재 프로세스의 모든 가비지 수집기 핸들을 표시합니다.

```
!gcinfo 5b68dbb8
```

 다음 명령은 `MethodTable` 모듈에 있는 `EEClass` 클래스의 `Main` 메서드에 대한 `MainClass` 및 `unittest.exe` 구조체를 표시합니다.

```
!name2ee unittest.exe MainClass.Main
```

 다음 명령은 `02000003` 모듈에 있는 `unittest.exe` 주소의 메타데이터 토큰에 대한 정보를 표시합니다.

```
!token2ee unittest.exe 02000003
```

## <a name="see-also"></a>참고 항목

- [도구](../../../docs/framework/tools/index.md)
- [명령 프롬프트](../../../docs/framework/tools/developer-command-prompt-for-vs.md)