---
title: CLR ETW 키워드 및 수준
ms.date: 03/30/2017
helpviewer_keywords:
- CLR ETW keywords
- CLR ETW levels
- ETW, CLR keywords
- ETW, CLR levels
ms.assetid: fdf5856d-516b-4042-849d-911c4518a6cb
author: mairaw
ms.author: mairaw
ms.openlocfilehash: dce8c58f94c66bcf2336d3708ebc64699148d556
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046712"
---
# <a name="clr-etw-keywords-and-levels"></a>CLR ETW 키워드 및 수준
<a name="top"></a> 범주 및 수준별로 ETW(Windows용 이벤트 추적) 이벤트를 필터링할 수 있습니다. 이벤트 [CLR ETW 키워드](#keywords)를 통해 범주별로 이벤트를 필터링할 수 있습니다. 런타임 및 런다운 공급자를 위해 여러 키워드를 조합하여 사용할 수 있습니다. [이벤트 수준](#levels) 은 플래그로 식별됩니다.  
  
<a name="keywords"></a>   
## <a name="clr-etw-keywords"></a>CLR ETW 키워드  
 키워드는 값을 생성하기 위해 조합할 수 있는 플래그입니다. 실제로는 명령줄 유틸리티를 호출할 때 키워드 이름 대신 키워드의 16진수 값을 사용합니다.  
  
 다음 표에서는 키워드에 대해 설명합니다.  
  
- [CLR ETW 런타임 키워드](#runtime)  
  
- [CLR ETW 런다운 키워드](#rundown)  
  
- [런타임 공급자를 위한 기호 확인용 키워드 조합](#runtime_combo)  
  
- [런다운 공급자를 위한 기호 확인용 키워드 조합](#rundown_combo)  
  
<a name="runtime"></a>   
### <a name="clr-etw-runtime-keywords"></a>CLR ETW 런타임 키워드  
 다음 표에는 CLR ETW 런타임 키워드, 해당 값 및 용도가 나와 있습니다.  
  
|런타임 키워드 이름|값|용도|  
|--------------------------|-----------|-------------|  
|`GCKeyword`|0x00000001|[가비지 수집 이벤트](garbage-collection-etw-events.md)를 수집할 수 있도록 합니다.|  
|`LoaderKeyword`|0x00000008|[로더 이벤트](loader-etw-events.md)를 수집할 수 있도록 합니다.|  
|`JITKeyword`|0x00000010|[JIT(Just-In-Time) 이벤트](jit-tracing-etw-events.md)를 수집할 수 있도록 합니다.|  
|`NGenKeyword`|0x00000020|네이티브 이미지 메서드(네이티브 이미지 생성기, Ngen.exe에서 처리하는 메서드)의 이벤트를 수집할 수 있도록 합니다. `StartEnumerationKeyword` 및 `EndEnumerationKeyword`와 함께 사용됩니다. 이 키워드는 오버헤드가 높습니다. 로드된 모든 NGen 모듈 내부에 모든 메서드에 대한 이벤트를 생성합니다. 가능한 경우 이 키워드를 사용하는 대신 프로파일링 도구에서 생성한 프로그램 데이터베이스(PDB)를 사용하여 NGen 모듈의 메서드에 대한 정보를 검색하는 것이 좋습니다. 또한 이 표의 뒷부분에 나오는 `OverrideAndSuppressNGenEventsKeyword` 도 참조하세요.|  
|`StartEnumerationKeyword`|0x00000040|런타임에서 모든 메서드를 열거할 수 있도록 합니다. `NGenKeyword`와 함께 사용됩니다.|  
|`EndEnumerationKeyword`|0x00000080|런타임에서 소멸된 모든 메서드를 열거할 수 있도록 합니다. `JITKeyword` 및 `NGenKeyword`와 함께 사용됩니다.|  
|`SecurityKeyword`|0x00000400|[보안 이벤트](security-etw-events.md)를 수집할 수 있도록 합니다.|  
|`AppDomainResourceManagementKeyword`|0x00000800|애플리케이션 도메인 수준에서 이벤트를 모니터링하는 리소스를 수집할 수 있도록 합니다.|  
|`JITTracingKeyword`|0x00001000|[JIT 추적 이벤트](jit-tracing-etw-events.md)를 수집할 수 있도록 합니다.|  
|`InteropKeyword`|0x00002000|[interop 이벤트](interop-etw-events.md)를 수집할 수 있도록 합니다.|  
|`ContentionKeyword`|0x00004000|[경합 이벤트](contention-etw-events.md)를 수집할 수 있도록 합니다.|  
|`ExceptionKeyword`|0x00008000|[예외 이벤트](exception-thrown-v1-etw-event.md)를 수집할 수 있도록 합니다.|  
|`ThreadingKeyword`|0x00010000|[스레드 풀 이벤트](thread-pool-etw-events.md)를 수집할 수 있도록 합니다.|  
|`OverrideAndSuppressNGenEventsKeyword`|0x00040000|.NET Framework 4.5 이상에서 사용할 수 있습니다. 높은 오버헤드의 `NGenKeyword` 키워드를 표시하지 않으며, NGen 모듈 내부에 있는 메서드에 대한 이벤트 생성을 방지합니다. .NET Framework 4.5부터 프로 파일링 도구에서 및 `OverrideAndSuppressNGenEventsKeyword` `NGenKeyword` 를 함께 사용 하 여 NGen 모듈의 메서드에 대 한 이벤트를 생성 하지 않아야 합니다. 이를 통해 프로파일링 도구에서 더욱 효율적인 NGen PDB를 사용하여 NGen 모듈의 메서드에 대한 정보를 가져올 수 있습니다. .NET Framework 4 및 이전 버전의 CLR은 NGen PDB의 생성을 지원하지 않습니다. 이러한 초기 버전에서는 CLR에서 `OverrideAndSuppressNGenEventsKeyword` 를 인식하지 못하며, `NGenKeyword` 를 처리하여 NGen 모듈의 메서드에 대한 이벤트를 생성합니다.|  
|`PerfTrackKeyWord`|0x2000000|`ModuleLoad` 및 `ModuleRange` 이벤트를 수집할 수 있도록 합니다.|  
|`StackKeyword`|0x40000000|CLR [스택 추적 이벤트](stack-etw-event.md)를 수집할 수 있도록 합니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="rundown"></a>   
### <a name="clr-etw-rundown-keywords"></a>CLR ETW 런다운 키워드  
 다음 표에는 CLR ETW 런다운 키워드, 해당 값 및 용도가 나와 있습니다.  
  
|런다운 키워드 이름|값|용도|  
|--------------------------|-----------|-------------|  
|`LoaderRundownKeyword`|0x00000008|`StartRundownKeyword` 및 `EndRundownKeyword`와 함께 사용될 때 로더 이벤트를 수집할 수 있도록 합니다.|  
|`JitRundownKeyword`|0x00000010|`DCStart` 및 `DCEnd` 와 함께 사용될 때 `StartRundownKeyword` 및 `EndRundownKeyword`메서드 이벤트를 수집할 수 있도록 합니다.|  
|`NGenRundownKeyword`|0x00000020|`DCStart` 및 `DCEnd` 와 함께 사용될 때 NGen 네이티브 이미지에 대한 `StartRundownKeyword` 및 `EndRundownKeyword`메서드 이벤트를 수집할 수 있도록 합니다. 이 키워드는 오버헤드가 높습니다. 로드된 모든 NGen 모듈 내부에 모든 메서드에 대한 이벤트를 생성합니다. 가능한 경우 이 키워드를 사용하는 대신 프로파일링 도구에서 생성한 프로그램 데이터베이스(PDB)를 사용하여 NGen 모듈의 메서드에 대한 정보를 검색하는 것이 좋습니다. 또한 이 표의 뒷부분에 나오는 `OverrideAndSuppressNGenEventsRundownKeyword` 도 참조하세요.|  
|`StartRundownKeyword`|0x00000040|시작 런다운 동안 시스템 상태를 열거할 수 있도록 합니다.|  
|`EndRundownKeyword`|0x00000100|종료 런다운 동안 시스템 상태를 열거할 수 있도록 합니다.|  
|`AppDomainResourceManagementRundownKeyword`|0x00000800|<xref:System.AppDomain> 또는 `StartRundownKeyword` 와 함께 사용될 때 `EndRundownKeyword`수준에서 리소스 모니터링에 대한 이벤트를 수집할 수 있도록 합니다.|  
|`ThreadingKeyword`|0x00010000|스레드 풀 이벤트를 수집할 수 있도록 합니다.|  
|`OverrideAndSuppressNGenEventsRundownKeyword`|0x00040000|.NET Framework 4.5 이상에서 사용할 수 있습니다. 높은 오버헤드의 `NGenRundownKeyword` 키워드를 표시하지 않으며, NGen 모듈 내부에 있는 메서드에 대한 이벤트 생성을 방지합니다. .NET Framework 4.5부터 프로 파일링 도구에서 및 `OverrideAndSuppressNGenEventsRundownKeyword` `NGenRundownKeyword` 를 함께 사용 하 여 NGen 모듈의 메서드에 대 한 이벤트를 생성 하지 않아야 합니다. 이를 통해 프로파일링 도구에서 더욱 효율적인 NGen PDB를 사용하여 NGen 모듈의 메서드에 대한 정보를 가져올 수 있습니다. .NET Framework 4 및 이전 버전의 CLR은 NGen PDB의 생성을 지원하지 않습니다. 이러한 초기 버전에서는 CLR에서 `OverrideAndSuppressNGenEventsRundownKeyword` 를 인식하지 못하며, `NGenRundownKeyword` 를 처리하여 NGen 모듈의 메서드에 대한 이벤트를 생성합니다.|  
|`PerfTrackKeyWord`|0x2000000|`ModuleDCStart`, `ModuleDCEnd`, `ModuleRangeDCStart`및 `ModuleRangeDCEnd` 이벤트를 수집할 수 있도록 합니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="runtime_combo"></a>   
### <a name="keyword-combinations-for-symbol-resolution-for-the-runtime-provider"></a>런타임 공급자를 위한 기호 확인용 키워드 조합  
  
|키워드 및 플래그|애플리케이션 도메인, 어셈블리, 모듈 로드/언로드 이벤트|메서드 로드/언로드 이벤트(동적 이벤트 제외)|동적 메서드 로드/소멸 이벤트|  
|------------------------|--------------------------------------------------------------|----------------------------------------------------------|-----------------------------------------|  
|`LoaderKeyword`|이벤트를 로드 및 언로드합니다.|없음|없음|  
|`JITKeyword`<br /><br /> (+ `StartEnumerationKeyword` 는 아무것도 추가하지 않음)|없음.|이벤트를 로드합니다.|이벤트를 로드 및 언로드합니다.|  
|`JITKeyword` +<br /><br /> `EndEnumerationKeyword`|없음|이벤트를 로드 및 언로드합니다.|이벤트를 로드 및 언로드합니다.|  
|`NGenKeyword`|없음|없음.|해당 사항 없음.|  
|`NGenKeyword` +<br /><br /> `StartEnumerationKeyword`|없음|이벤트를 로드합니다.|해당 사항 없음.|  
|`NGenKeyword` +<br /><br /> `EndEnumerationKeyword`|없음|이벤트를 언로드합니다.|해당 사항 없음.|  
  
 [맨 위로 이동](#top)  
  
<a name="rundown_combo"></a>   
### <a name="keyword-combinations-for-symbol-resolution-for-the-rundown-provider"></a>런다운 공급자를 위한 기호 확인용 키워드 조합  
  
|키워드 및 플래그|애플리케이션 도메인, 어셈블리, 모듈 DCStart/DCEnd 이벤트|메서드 DCStart/DCEnd 이벤트(동적 메서드 이벤트 포함)|  
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------|  
|`LoaderRundownKeyword` +<br /><br /> `StartRundownKeyword`|`DCStart` 이벤트|없음|  
|`LoaderRundownKeyword` +<br /><br /> `EndRundownKeyword`|`DCEnd` 이벤트|없음|  
|`JITKeyword` +<br /><br /> `StartRundownKeyword`|없음|`DCStart` 이벤트|  
|`JITKeyword` +<br /><br /> `EndRundownKeyword`|없음|`DCEnd` 이벤트|  
|`NGenKeyword` +<br /><br /> `StartRundownKeyword`|없음|`DCStart` 이벤트|  
|`NGenKeyword` +<br /><br /> `EndRundownKeyword`|없음|`DCEnd` 이벤트|  
  
 [맨 위로 이동](#top)  
  
<a name="levels"></a>   
## <a name="etw-event-levels"></a>ETW 이벤트 수준  
 ETW 이벤트는 수준별로도 필터링될 수 있습니다. 수준이 0x5로 설정된 경우 0x5 이하를 포함하여 모든 수준의 이벤트(키워드를 통해 활성화된 범주에 속하는 이벤트)가 발생합니다. 수준이 0x2로 설정된 경우 수준 0x2 이하에 속한 이벤트만 발생합니다.  
  
 수준의 의미는 다음과 같습니다.  
  
 0x5 - 자세한 정보 표시  
  
 0x4 - 정보  
  
 0x3 - 경고  
  
 0x2 - 오류  
  
 0x1 - 위험  
  
 0x0 - LogAlways  
  
## <a name="see-also"></a>참고자료

- [CLR ETW 공급자](clr-etw-providers.md)
- [CLR ETW 이벤트](clr-etw-events.md)
- [공용 언어 런타임의 ETW 이벤트](etw-events-in-the-common-language-runtime.md)
