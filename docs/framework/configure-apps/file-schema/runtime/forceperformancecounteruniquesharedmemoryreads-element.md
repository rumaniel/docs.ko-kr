---
title: <forcePerformanceCounterUniqueSharedMemoryReads> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- forcePerformanceCounterUniqueSharedMemoryReads element
- <forcePerformanceCounterUniqueSharedMemoryReads> element
ms.assetid: 91149858-4810-4f65-9b48-468488172c9b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 54bccd134a2f77925e80bfc681770b28c05f77a1
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252599"
---
# <a name="forceperformancecounteruniquesharedmemoryreads-element"></a>\<forcePerformanceCounterUniqueSharedMemoryReads> Element
PerfCounter.dll이 .NET Framework 버전 1.1 애플리케이션에서 CategoryOptions 레지스트리 설정을 사용하여 성능 카운터 데이터를 범주별 공유 메모리에서 로드할지 또는 전역 메모리에서 로드할지를 결정하도록 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<forcePerformanceCounterUniqueSharedMemoryReads>**  
  
## <a name="syntax"></a>구문  
  
```xml  
<forcePerformanceCounterUniqueSharedMemoryReads   
enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`enabled`|필수 특성입니다.<br /><br /> PerfCounter가 CategoryOptions 레지스트리 설정을 사용 하 여 범주 특정 공유 메모리 또는 전역 메모리에서 성능 카운터 데이터를 로드할지 여부를 나타냅니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|`false`|PerfCounter는 CategoryOptions 레지스트리 설정을 사용 하지 않습니다.|  
|`true`|PerfCounter는 CategoryOptions 레지스트리 설정을 사용 합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 .NET Framework 4 이전의 .NET Framework 버전에서는 로드 된 PerfCounter의 버전이 프로세스에 로드 된 런타임으로 속하는지를. 컴퓨터에 .NET Framework 버전 1.1 및 .NET Framework 2.0이 모두 설치 되어 있는 경우 .NET Framework 1.1 응용 프로그램은 .NET Framework 1.1 버전의 PerfCounter를 로드 합니다. .NET Framework 4부터 설치 된 PerfCounter의 최신 버전이 로드 됩니다. 즉, 컴퓨터에 .NET Framework 4가 설치 된 경우 .NET Framework 1.1 응용 프로그램에서 PerfCounter의 .NET Framework 4 버전이 로드 됩니다.  
  
 .NET Framework 4부터 성능 카운터를 사용할 때 PerfCounter는 각 공급자에 대 한 CategoryOptions 레지스트리 항목을 확인 하 여 범주 특정 공유 메모리 또는 전역 공유 메모리에서 읽어야 하는지 여부를 확인 합니다. .NET Framework 1.1 PerfCounter는 범주 관련 공유 메모리를 인식 하지 못하기 때문에 해당 레지스트리 항목을 읽지 않습니다. 전역 공유 메모리에서 항상 읽습니다.  
  
 이전 버전과의 호환성을 위해 .NET Framework 4 PerfCounter는 .NET Framework 1.1 응용 프로그램에서 실행 될 때 CategoryOptions 레지스트리 항목을 확인 하지 않습니다. .NET Framework 1.1 PerfCounter와 마찬가지로 전역 공유 메모리를 사용 하기만 하면 됩니다. 그러나 `<forcePerformanceCounterUniqueSharedMemoryReads>` 요소를 사용 하도록 설정 하 여 레지스트리 설정을 확인 하도록 .NET Framework 4 PerfCounter에 지시할 수 있습니다.  
  
> [!NOTE]
> 요소를 `<forcePerformanceCounterUniqueSharedMemoryReads>` 사용 하도록 설정 해도 범주 관련 공유 메모리가 사용 되는 것은 아닙니다. Enabled를로 `true` 설정 하면 PerfCounter가 categoryoptions 레지스트리 설정을 참조 하 게 됩니다. CategoryOptions의 기본 설정은 범주 관련 공유 메모리를 사용 하는 것입니다. 그러나 CategoryOptions를 변경 하 여 전역 공유 메모리를 사용 해야 함을 나타낼 수 있습니다.  
  
 Categoryoptions 설정이 포함 된 레지스트리 키는 HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\\< 범주 \Performance.\> 기본적으로 CategoryOptions는 3으로 설정 되며,이는 PerfCounter에 범주 관련 공유 메모리를 사용 하도록 지시 합니다. CategoryOptions가 0으로 설정 된 경우 PerfCounter는 전역 공유 메모리를 사용 합니다. 인스턴스 데이터는 생성 중인 인스턴스의 이름이 다시 사용 중인 인스턴스와 동일한 경우에만 다시 사용 됩니다. 모든 버전은 범주에 쓸 수 있습니다. CategoryOptions를 1로 설정 하면 전역 공유 메모리가 사용 되지만 범주 이름이 다시 사용 하는 범주와 동일한 경우 인스턴스 데이터를 다시 사용할 수 있습니다.  
  
 설정 0 및 1은 메모리 누수를 야기 하 고 성능 카운터 메모리를 채울 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 PerfCounter에서 CategoryOptions 레지스트리 항목을 참조 하 여 범주 관련 공유 메모리를 사용 해야 하는지 여부를 확인 하도록 지정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
  <runtime>  
    <forcePerformanceCounterUniqueSharedMemoryReads enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
