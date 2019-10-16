---
title: 런타임 정보 ETW 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- runtime information events [.NET Framework]
- ETW, runtime information events
ms.assetid: 68b4edbc-7f3b-45f6-ab75-4fd066d6af9a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6ab3844b293d09cec02236fb9befd836aa4113ea
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046221"
---
# <a name="runtime-information-etw-events"></a>런타임 정보 ETW 이벤트
이러한 ETW 이벤트에서는 SKU, 버전 번호, 런타임이 활성화된 방법, 시작하는 데 사용된 명령줄 매개 변수, GUID(해당되는 경우) 및 다른 관련 정보를 비롯한 런타임 관련 정보를 로깅합니다. 프로세스에서 여러 런타임이 실행되는 경우 해당 이벤트(ClrInstanceID)에서 제공한 정보를 통해 런타임이 명확해질 수 있습니다.  
  
 다음 표에서는 두 개의 런타임 정보 이벤트를 보여 줍니다. 이벤트는 임의 키워드 또는 마스크를 통해 발생할 수 있습니다. 자세한 내용은 [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md)을 참조하세요.  
  
|이벤트|이벤트 ID|공급자|Description|  
|-----------|--------------|--------------|-----------------|  
|`RuntimeInformationEvent`|187|CLRRuntime|런타임이 로드될 때 발생합니다.|  
|`RuntimeInformationDCStart`|187|CLRRundown|로드된 런타임을 열거합니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
|Sku|win:UInt16|1 – 데스크톱 CLR.<br /><br /> 2 – CoreCLR.|  
|BclVersion – 주 버전입니다.|win:UInt16|mscorlib.dll의 주 버전입니다.|  
|BclVersion – 부 버전입니다.|win:UInt16|mscorlib.dll의 부 버전 번호입니다.|  
|BclVersion-빌드 번호|win:UInt16|mscorlib.dll의 빌드 번호입니다.|  
|BclVersion – QFE|win:UInt16|mscorlib.dll의 핫픽스 버전 번호입니다.|  
|VMVersion – 주 버전|win:UInt16|SKU에 따라 다른 clr.dll 또는 coreclr.dll의 버전입니다.|  
|VMVersion - 부 버전|win:UInt16|SKU에 따라 다른 clr.dll 또는 coreclr.dll의 부 버전입니다.|  
|VMVersion - 빌드 번호|win:UInt16|clr.dll 또는 coreclr.dll의 빌드 번호입니다.|  
|VMVersion – QFE|win:UInt16|clr.dll 또는 coreclr.dll의 핫픽스 버전 번호입니다.|  
|StartupFlags|win:UInt32|mscoree.h에 정의된 시작 플래그입니다.|  
|StartupMode|win:UInt8|0x01 - 관리되는 실행 파일입니다.<br /><br /> 0x02 - 호스팅된 CLR입니다.<br /><br /> 0x04 - C++ 관리되는 interop입니다.<br /><br /> 0x08 - COM이 활성화되었습니다.<br /><br /> 0x10 - 기타.|  
|명령줄|win:UnicodeString|Non- StartupMode=0x01인 경우에만 Null입니다.|  
|ComObjectGUID|win:GUID|Non- StartupMode=0x08인 경우에만 Null입니다.|  
|RuntimeDLLPath|win:UnicodeString|프로세스에 로드된 CLR.dll 파일의 경로입니다.|  
  
## <a name="see-also"></a>참고자료

- [CLR ETW 이벤트](clr-etw-events.md)
