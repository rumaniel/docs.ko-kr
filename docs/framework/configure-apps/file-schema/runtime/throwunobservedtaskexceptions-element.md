---
title: <ThrowUnobservedTaskExceptions> 요소
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ThrowUnobservedTaskExceptions element
- <ThrowUnobservedTaskExceptions> element
ms.assetid: cea7e588-8b8d-48d2-9ad5-8feaf3642c18
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3ed1e66c4aadab656455686a7a1e5028b035676a
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252261"
---
# <a name="throwunobservedtaskexceptions-element"></a>\<ThrowUnobservedTaskExceptions > 요소
작업 예외가 처리되지 않으면 실행 중인 프로세스를 종료할지를 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<ThrowUnobservedTaskExceptions>**  
  
## <a name="syntax"></a>구문  
  
```xml  
<ThrowUnobservedTaskExceptions  
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`enabled`|필수 특성입니다.<br /><br /> 처리 되지 않은 태스크 예외가 실행 중인 프로세스를 종료할지 여부를 지정 합니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|`false`|처리 되지 않은 작업 예외에 대 한 실행 중인 프로세스를 종료 하지 않습니다. 이 값이 기본값입니다.|  
|`true`|처리 되지 않은 작업 예외에 대 한 실행 중인 프로세스를 종료 합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|런타임 초기화 옵션에 대한 정보를 포함합니다.|  
|||  
  
## <a name="remarks"></a>설명  
 와 <xref:System.Threading.Tasks.Task> 연결 된 예외가 관찰 되지 않은 경우에는 작업이 없으며 <xref:System.Threading.Tasks.Task.Wait%2A> , 부모가 연결 <xref:System.Threading.Tasks.Task.Exception%2A?displayProperty=nameWithType> 되지 않으며, 속성을 읽지 않은 경우 태스크 예외가 관찰 되지 않은으로 간주 됩니다.  
  
 .NET Framework 4에서는 기본적으로 관찰 되지 않은 예외가 있는이 가비지 <xref:System.Threading.Tasks.Task> 수집 되는 경우 종료자는 예외를 throw 하 고 프로세스를 종료 합니다. 프로세스 종료는 가비지 수집 및 종료 시간에 따라 결정 됩니다.  
  
 개발자가 작업을 기반으로 비동기 코드를 보다 쉽게 작성할 수 있도록 .NET Framework 4.5은 관찰 되지 않은 예외에 대 한이 기본 동작을 변경 합니다. 관찰 되지 않은 예외는 <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException> 여전히 이벤트를 발생 시킵니다. 하지만 기본적으로이 프로세스는 종료 되지 않습니다. 대신, 이벤트 처리기가 예외를 준수 하는지 여부에 관계 없이 이벤트가 발생 한 후 예외가 무시 됩니다.  
  
 .NET Framework 4.5에서는 응용 프로그램 구성 파일에서 [ \<ThrowUnobservedTaskExceptions > 요소](throwunobservedtaskexceptions-element.md) 를 사용 하 여 예외를 throw 하는 .NET Framework 4 동작을 사용 하도록 설정할 수 있습니다.  
  
 다음 방법 중 하나로 예외 동작을 지정할 수도 있습니다.  
  
- 환경 변수 `COMPlus_ThrowUnobservedTaskExceptions` (`set COMPlus_ThrowUnobservedTaskExceptions=1`)를 설정 합니다.  
  
- HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\에서 레지스트리 DWORD 값 ThrowUnobservedTaskExceptions = 1을 설정 합니다. NETFramework 키입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 응용 프로그램 구성 파일을 사용 하 여 작업에서 예외를 throw 하도록 설정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>   
    <runtime>   
        <ThrowUnobservedTaskExceptions enabled="true"/>   
    </runtime>   
</configuration>  
```  
  
## <a name="example"></a>예제  
 다음 예제에서는 작업에서 관찰 되지 않은 예외가 throw 되는 방법을 보여 줍니다. 제대로 작동 하려면 코드가 릴리스 된 프로그램으로 실행 되어야 합니다.  
  
 [!code-csharp[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/throwunobservedtaskexceptions/cs/program.cs#1)]
 [!code-vb[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/throwunobservedtaskexceptions/vb/program.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
