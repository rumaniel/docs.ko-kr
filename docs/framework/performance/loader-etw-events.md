---
title: 로더 ETW 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- loader events [.NET Framework]
- ETW, loader events (CLR)
ms.assetid: cb403cc6-56f8-4609-b467-cdfa09f07909
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6177bdff873feb75eb15dba53bcdb5197260fa9d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046399"
---
# <a name="loader-etw-events"></a>로더 ETW 이벤트
<a name="top"></a> 이들 이벤트는 응용 프로그램 도메인, 어셈블리 및 모듈 로드 및 언로드와 관련된 정보를 수집합니다.  
  
 모든 로더 이벤트는 `LoaderKeyword` (0x8) 키워드에서 발생합니다. `DCStart` 및 `DCEnd` 이벤트는 `StartRundown`/`EndRundown`이 사용되는 `LoaderRundownKeyword`(0x8)에서 발생합니다. 자세한 내용은 [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md)을 참조하세요.  
  
 로더 이벤트는 다음으로 다시 구분됩니다.  
  
- [응용 프로그램 도메인 이벤트](#application_domain_events)  
  
- [CLR 로더 어셈블리 이벤트](#clr_loader_assembly_events)  
  
- [모듈 이벤트](#module_events)  
  
- [CLR 도메인 모듈 이벤트](#clr_domain_module_events)  
  
- [모듈 범위 이벤트](#module_range_events)  
  
<a name="application_domain_events"></a>   
## <a name="application-domain-events"></a>애플리케이션 도메인 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|이벤트(event)|수준|  
|-----------------------------------|-----------|-----------|  
|`LoaderKeyword` (0x8)|`AppDomainLoad_V1` 및 `AppDomainUnLoad_V1`|정보(4)|  
|`LoaderRundownKeyword` (0x8) +<br /><br /> `StartRundownKeyword`|`AppDomainDCStart_V1`|정보(4)|  
|`LoaderRundownKeyword` (0x8) +<br /><br /> `EndRundownKeyword`|`AppDomainDCEnd_V1`|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|설명|  
|-----------|--------------|-----------------|  
|`AppDomainLoad_V1` (모든 응용 프로그램 도메인에 대해 기록됨)|156|프로세스 수명 중에 애플리케이션 도메인이 만들어질 때마다 발생합니다.|  
|`AppDomainUnLoad_V1`|157|프로세스 수명 중에 애플리케이션 도메인이 삭제될 때마다 발생합니다.|  
|`AppDomainDCStart_V1`|157|시작 런다운 중에 애플리케이션 도메인을 열거합니다.|  
|`AppDomainDCEnd_V1`|158|끝 런다운 중에 애플리케이션 도메인을 열거합니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|AppDomainID|win:UInt64|애플리케이션 도메인의 고유 식별자입니다.|  
|AppDomainFlags|win:UInt32|0x1: 기본 도메인입니다.<br /><br /> 0x2: Executable.<br /><br /> 0x4: 응용 프로그램 도메인, 비트 28-31: 이 도메인의 정책 공유.<br /><br /> 0: 공유 도메인.|  
|AppDomainName|win:UnicodeString|친숙한 애플리케이션 도메인 이름입니다. 프로세스 수명 중에 변경될 수 있습니다.|  
|AppDomainIndex|win:UInt32|이 애플리케이션 도메인의 인덱스입니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="clr_loader_assembly_events"></a>   
## <a name="clr-loader-assembly-events"></a>CLR 로더 어셈블리 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|이벤트(event)|수준|  
|-----------------------------------|-----------|-----------|  
|`LoaderKeyword` (0x8)|`AssemblyLoad` 및 `AssemblyUnload`|정보(4)|  
|`LoaderRundownKeyword` (0x8) +<br /><br /> `StartRundownKeyword`|`AssemblyDCStart`|정보(4)|  
|`LoaderRundownKeyword` (0x8) +<br /><br /> `EndRundownKeyword`|`AssemblyDCEnd`|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|설명|  
|-----------|--------------|-----------------|  
|`AssemblyLoad_V1`|154|어셈블리가 로드될 때 발생합니다.|  
|`AssemblyUnload_V1`|155|어셈블리가 언로드될 때 발생합니다.|  
|`AssemblyDCStart_V1`|155|시작 런다운 중에 어셈블리를 열거합니다.|  
|`AssemblyDCEnd_V1`|156|끝 런다운 중에 어셈블리를 열거합니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|AssemblyID|win:UInt64|어셈블리의 고유 ID입니다.|  
|AppDomainID|win:UInt64|이 어셈블리의 도메인 ID입니다.|  
|BindingID|win:UInt64|어셈블리 바인딩을 고유하게 식별하는 ID입니다.|  
|AssemblyFlags|win:UInt32|0x1: 도메인 중립 어셈블리.<br /><br /> 0x2: 동적 어셈블리입니다.<br /><br /> 0x4: 어셈블리에 네이티브 이미지가 있습니다.<br /><br /> 0x8: 수집 가능한 어셈블리입니다.|  
|AssemblyName|win:UnicodeString|정규화된 어셈블리 이름입니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="module_events"></a>   
## <a name="module-events"></a>모듈 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|이벤트(event)|수준|  
|-----------------------------------|-----------|-----------|  
|`LoaderKeyword` (0x8)|`ModuleLoad_V2` 및 `ModuleUnload_V2`|정보(4)|  
|`LoaderRundownKeyword` (0x8) +<br /><br /> `StartRundownKeyword`|`ModuleDCStart_V2`|정보(4)|  
|`LoaderRundownKeyword` (0x8) +<br /><br /> `EndRundownKeyword`|`ModuleDCEnd_V2`|정보(4)|  
||||  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|설명|  
|-----------|--------------|-----------------|  
|`ModuleLoad_V2`|152|프로세스 수명 중에 모듈이 로드될 때 발생합니다.|  
|`ModuleUnload_V2`|153|프로세스 수명 중에 모듈이 언로드될 때 발생합니다.|  
|`ModuleDCStart_V2`|153|시작 런다운 중에 모듈을 열거합니다.|  
|`ModuleDCEnd_V2`|154|끝 런다운 중에 모듈을 열거합니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|ModuleID|win:UInt64|모듈의 고유 ID입니다.|  
|AssemblyID|win:UInt64|이 모듈이 있는 어셈블리의 ID입니다.|  
|ModuleFlags|win:UInt32|0x1: 도메인 중립 모듈.<br /><br /> 0x2: 모듈에 네이티브 이미지가 있습니다.<br /><br /> 0x4: 동적 모듈입니다.<br /><br /> 0x8: 매니페스트 모듈.|  
|Reserved1|win:UInt32|예약된 필드입니다.|  
|ModuleILPath|win:UnicodeString|모듈에 대한 MSIL(Microsoft intermediate language) 이미지의 경로 또는 동적 어셈블리인 경우 동적 모듈 이름(null로 종료됨)입니다.|  
|ModuleNativePath|win:UnicodeString|있는 경우 모듈 네이티브 이미지의 경로입니다(null로 종료됨).|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
|ManagedPdbSignature|win:GUID|이 모듈과 일치하는 관리되는 PDB(프로그램 데이터베이스)의 GUID 서명입니다. 설명 부분을 참조하세요.|  
|ManagedPdbAge|win:UInt32|이 모듈과 일치하는 관리되는 PDB에 작성된 기간 수입니다. 설명 부분을 참조하세요.|  
|ManagedPdbBuildPath|win:UnicodeString|이 모듈과 일치하는 관리되는 PDB가 빌드된 위치의 경로입니다. 경우에 따라 파일 이름일 수도 있습니다. 설명 부분을 참조하세요.|  
|NativePdbSignature|win:GUID|이 모듈과 일치하는 네이티브 이미지 생성기(NGen) PDB의 GUID 서명입니다(적용 가능한 경우). 설명 부분을 참조하세요.|  
|NativePdbAge|win:UInt32|이 모듈과 일치하는 NGen PDB에 작성된 기간 수입니다(적용 가능한 경우). 설명 부분을 참조하세요.|  
|NativePdbBuildPath|win:UnicodeString|이 모듈과 일치하는 NGen PDB가 빌드된 위치의 경로입니다(적용 가능한 경우). 경우에 따라 파일 이름일 수도 있습니다. 설명 부분을 참조하세요.|  
  
### <a name="remarks"></a>설명  
  
- 이름에 "Pdb"가 포함된 필드는 도구를 프로파일링하여 프로파일링 세션 중에 로드된 모듈과 일치하는 PDB를 찾는 방식으로 사용할 수 있습니다. 이들 필드 값은 일반적으로 로드된 모듈과 일치하는 PDB를 찾도록 도와주는 디버거에서 사용되는 모듈의 IMAGE_DIRECTORY_ENTRY_DEBUG 섹션에 작성된 데이터에 해당합니다.  
  
- "ManagedPdb"로 시작하는 필드 이름은 관리되는 컴파일러(예: C# 또는 Visual Basic 컴파일러)에서 생성된 MSIL 모듈에 해당하는 관리되는 PDB를 나타냅니다. 이 PDB는 관리되는 PDB 형식을 사용하고 원래 관리되는 소스 코드의 요소(예: 파일, 줄 번호 및 기호 이름)를 MSIL 모듈로 컴파일된 MSIL 요소에 매핑하는 방법을 설명합니다.  
  
- "NativePdb"로 시작하는 필드 이름은 `NGEN createPDB`를 호출하여 생성된 NGen PDB를 나타냅니다. 이 PDB는 네이티브 PDB 형식을 사용하고 원래 관리되는 소스 코드의 요소(예: 파일, 줄 번호 및 기호 이름)를 NGen 모듈로 컴파일된 네이티브 요소에 매핑하는 방법을 설명합니다.  
  
 [맨 위로 이동](#top)  
  
<a name="clr_domain_module_events"></a>   
## <a name="clr-domain-module-events"></a>CLR 도메인 모듈 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|이벤트(event)|수준|  
|-----------------------------------|-----------|-----------|  
|`LoaderKeyword` (0x8)|`DomainModuleLoad_V1`|정보(4)|  
|`LoaderRundownKeyword` (0x8) +<br /><br /> `StartRundownKeyword`|`DomainModuleDCStart_V1`|정보(4)|  
|`LoaderRundownKeyword` (0x8) +<br /><br /> `EndRundownKeyword`|`DomainModuleDCEnd_V1`|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|설명|  
|-----------|--------------|-----------------|  
|`DomainModuleLoad_V1`|151|애플리케이션 도메인에 대한 모듈이 로드될 때 발생합니다.|  
|`DomainModuleDCStart_V1`|151|시작 런다운 중에 애플리케이션 도메인에 대해 로드된 모듈을 열거하고 모든 애플리케이션 도메인에 대해 기록됩니다.|  
|`DomainModuleDCEnd_V1`|152|끝 런다운 중에 애플리케이션 도메인에 대해 로드된 모듈을 열거하고 모든 애플리케이션 도메인에 대해 기록됩니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|ModuleID|win:UInt64|이 모듈이 속한 어셈블리를 식별합니다.|  
|AssemblyID|win:UInt64|이 모듈이 있는 어셈블리의 ID입니다.|  
|AppDomainID|win:UInt64|이 모듈이 사용되는 애플리케이션 도메인의 ID입니다.|  
|ModuleFlags|win:UInt32|0x1: 도메인 중립 모듈.<br /><br /> 0x2: 모듈에 네이티브 이미지가 있습니다.<br /><br /> 0x4: 동적 모듈입니다.<br /><br /> 0x8: 매니페스트 모듈.|  
|Reserved1|win:UInt32|예약된 필드입니다.|  
|ModuleILPath|win:UnicodeString|모듈에 대한 MSIL 이미지의 경로 또는 동적 어셈블리인 경우 동적 모듈 이름(null로 종료됨)입니다.|  
|ModuleNativePath|win:UnicodeString|있는 경우 모듈 네이티브 이미지의 경로입니다(null로 종료됨).|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="module_range_events"></a>   
## <a name="module-range-events"></a>모듈 범위 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|이벤트(event)|수준|  
|-----------------------------------|-----------|-----------|  
|`PerfTrackKeyWord`)|`ModuleRange`|정보(4)|  
|`PerfTrackKeyWord`|`ModuleRangeDCStart`|정보(4)|  
|`PerfTrackKeyWord`|`ModuleRangeDCEnd`|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|설명|  
|-----------|--------------|-----------------|  
|`ModuleRange`|158|이 이벤트는 로드된 네이티브 이미지 생성기(NGen) 이미지가 IBC로 최적화된 경우 존재하고 NGen 이미지의 핫 섹션에 대한 정보를 포함합니다.|  
|`ModuleRangeDCStart`|160|런다운 시작 시 발생한 `ModuleRange` 이벤트입니다.|  
|`ModuleRangeDCEnd`|161|런다운 종료 시 발생한 `ModuleRange` 이벤트입니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|ClrInstanceID|win:UInt16|CLR의 여러 인스턴스가 로드된 경우 프로세스 CLR의 특정 인스턴스를 고유하게 식별합니다.|  
|ModuleID|win:UInt64|이 모듈이 속한 어셈블리를 식별합니다.|  
|RangeBegin|win:UInt32|지정된 범위 형식에 대한 범위 시작을 나타내는 모듈의 오프셋입니다.|  
|RangeSize|win:UInt32|지정된 범위의 크기(바이트)입니다.|  
|RangeType|win:UInt32|콜드 IBC 범위를 나타내는 단일 값, 0x4입니다. 이 필드는 나중에 더 많은 값을 나타낼 수 있습니다.|  
|RangeSize1|win:UInt32|0은 잘못된 데이터를 나타냅니다.|  
|RangeBegin2|win:UnicodeString||  
  
### <a name="remarks"></a>설명  
 .NET Framework 프로세스에서 로드된 NGen 이미지가 IBC로 최적화된 경우 NGen 이미지의 핫 범위를 포함하는 `ModuleRange` 이벤트가 `moduleID` 및 `ClrInstanceID`와 함께 기록됩니다.  NGen 이미지가 IBC로 최적화되지 않으면 이 이벤트가 기록되지 않습니다. 모듈 이름을 확인하려면 이 이벤트를 모듈 로드 ETW 이벤트와 대조해야 합니다.  
  
 이 이벤트의 페이로드 크기는 변수이고, `Count` 필드는 이벤트에 포함된 범위 오프셋 수를 나타냅니다.  실제 범위를 확인하려면 이 이벤트를 Windows `IStart` 이벤트와 대조해야 합니다. Windows 이미지 로드 이벤트는 이미지가 로드될 때마다 기록되고 로드된 이미지의 가상 주소를 포함합니다.  
  
 모듈 범위 이벤트는 ETW 수준이 4보다 크거나 같으면 발생하고 정보 제공 이벤트로 분류됩니다.  
  
## <a name="see-also"></a>참고자료

- [CLR ETW 이벤트](clr-etw-events.md)
