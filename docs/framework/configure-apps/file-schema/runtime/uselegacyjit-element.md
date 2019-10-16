---
title: <useLegacyJit> 요소
ms.date: 04/26/2017
ms.assetid: c2cf97f0-9262-4f1f-a754-5568b51110ad
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3b783a82b1ef964de308532ef544bbfab2397400
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252220"
---
# <a name="uselegacyjit-element"></a>\<useLegacyJit> 요소

공용 언어 런타임이 Just-In-Time 컴파일에 레거시 64비트 JIT 컴파일러를 사용할지를 결정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<useLegacyJit>**  
  
## <a name="syntax"></a>구문  
  
```xml
<useLegacyJit enabled=0|1 />
```

요소 이름은 `useLegacyJit` 대/소문자를 구분 합니다.
  
## <a name="attributes-and-elements"></a>특성 및 요소

다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
| 특성 | 설명                                                                                   |  
| --------- | --------------------------------------------------------------------------------------------- |  
| `enabled` | 필수 특성입니다.<br><br>런타임이 레거시 64 비트 JIT 컴파일러를 사용 하는지 여부를 지정 합니다. |  
  
### <a name="enabled-attribute"></a>enabled 특성  
  
| 값 | 설명                                                                                                         |  
| ----- | ------------------------------------------------------------------------------------------------------------------- |  
| 0     | 공용 언어 런타임은 .NET Framework 4.6 이상 버전에 포함 된 새로운 64 비트 JIT 컴파일러를 사용 합니다. |  
| 1     | 공용 언어 런타임에서는 이전 64 비트 JIT 컴파일러를 사용 합니다.                                                     |  
  
### <a name="child-elements"></a>자식 요소

없음
  
### <a name="parent-elements"></a>부모 요소  
  
| 요소         | 설명                                                                                                       |  
| --------------- | ----------------------------------------------------------------------------------------------------------------- |  
| `configuration` | 공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다. |  
| `runtime`       | 런타임 초기화 옵션에 대한 정보를 포함합니다.                                                        |  
  
## <a name="remarks"></a>설명  

4\.6 .NET Framework부터 공용 언어 런타임은 기본적으로 JIT (Just-in-time) 컴파일에 새로운 64 비트 컴파일러를 사용 합니다. 일부 경우에는 이전 버전의 64 비트 JIT 컴파일러에 의해 JIT 컴파일된 응용 프로그램 코드의 동작이 달라질 수 있습니다. `enabled` 요소의 특성을 로`1`설정 하 여 새 64 비트 jit 컴파일러를 사용 하지 않도록 설정 하 고 대신 레거시 64 비트 jit 컴파일러를 사용 하 여 앱을 컴파일할 수 있습니다. `<useLegacyJit>`  
  
> [!NOTE]
> 요소 `<useLegacyJit>` 는 64 비트 JIT 컴파일에만 영향을 줍니다. 32 비트 JIT 컴파일러를 사용 하는 컴파일은 영향을 받지 않습니다.  
  
구성 파일 설정을 사용 하는 대신 두 가지 다른 방법으로 레거시 64 비트 JIT 컴파일러를 사용 하도록 설정할 수 있습니다.  
  
- 환경 변수 설정

  환경 변수 `COMPLUS_useLegacyJit` 를 `0` (새로운 64 비트 jit 컴파일러 사용) 또는 `1` (이전 64 비트 jit 컴파일러 사용)로 설정 합니다.
  
  ```  
  COMPLUS_useLegacyJit=0|1  
  ```  
  
  환경 변수에는 *전역 범위가*있습니다. 즉, 컴퓨터에서 실행 되는 모든 응용 프로그램에 영향을 줍니다. 설정 하는 경우 응용 프로그램 구성 파일 설정으로 재정의할 수 있습니다. 환경 변수 이름은 대/소문자를 구분 하지 않습니다.
  
- 레지스트리 키 추가

  레지스트리의 `REG_DWORD` `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework` 또는 키`HKEY_CURRENT_USER\SOFTWARE\Microsoft\.NETFramework` 중 하나에 값을 추가 하 여 레거시 64 비트 JIT 컴파일러를 사용 하도록 설정할 수 있습니다. 값의 이름은 `useLegacyJit`입니다. 값이 0 이면 새 컴파일러가 사용 됩니다. 값이 1 이면 레거시 64 비트 JIT 컴파일러를 사용할 수 있습니다. 레지스트리 값 이름에 대/소문자를 구분 하지 않습니다.
  
  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework` 키에 값을 추가 하면 컴퓨터에서 실행 되는 모든 앱에 영향을 줍니다. `HKEY_CURRENT_USER\SOFTWARE\Microsoft\.NETFramework` 키에 값을 추가 하면 현재 사용자가 실행 하는 모든 앱에 영향을 줍니다. 여러 사용자 계정을 사용 하 여 컴퓨터를 구성 하는 경우 다른 사용자에 대 한 레지스트리 키에 값을 추가 하지 않으면 현재 사용자가 실행 하는 앱만 영향을 받습니다. 구성 파일에 요소를 추가 하면 레지스트리 설정 (있는 경우)이 재정의 됩니다. `<useLegacyJit>`  
  
## <a name="example"></a>예제  

다음 구성 파일은 새 64 비트 JIT 컴파일러를 사용 하 여 컴파일을 사용 하지 않도록 설정 하 고 대신 레거시 64 비트 JIT 컴파일러를 사용 합니다.  
  
```xml  
<?xml version ="1.0"?>  
<configuration>  
  <runtime>  
    <useLegacyJit enabled="1" />  
  </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목

- [\<런타임 > 요소](runtime-element.md)
- [\<configuration> 요소](../configuration-element.md)
- [조치 새 64 비트 JIT 컴파일러](../../../migration-guide/mitigation-new-64-bit-jit-compiler.md)
