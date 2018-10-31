---
title: 네트워크 추적 사용
ms.date: 03/30/2017
helpviewer_keywords:
- trace destinations
- sending traces to log file
- trace listeners, network tracing
- network tracing, enabling
- CLR Debugger
- default listeners
- logs, trace
- destination for tracing output
ms.assetid: 5fff458c-51a6-4134-ba47-8a6137ddc41e
ms.openlocfilehash: b289aa2a60deb10ebda0ca8efc3e172caf2df8a6
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50202070"
---
# <a name="enabling-network-tracing"></a>네트워크 추적 사용
네트워크 추적은 메서드 호출에 대한 정보와 관리되는 응용 프로그램에서 생성된 네트워크 트래픽 정보에 대한 액세스를 제공합니다. 응용 프로그램에서 네트워크 추적을 사용하도록 설정하려면 다음 작업을 완료해야 합니다.  
  
-   추적을 사용하도록 설정하고 코드를 컴파일합니다. 추적을 사용하도록 설정하는 데 필요한 컴파일러 스위치에 대한 자세한 내용은 [방법: 추적 및 디버그를 사용한 조건부 컴파일](../../../docs/framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)을 참조하세요.  
  
-   추적 출력 대상을 지정합니다.  
  
-   네트워크 추적 동작을 구성합니다. 자세한 내용은 [방법: 네트워크 추적 구성](../../../docs/framework/network-programming/how-to-configure-network-tracing.md)을 참조하세요.  
  
 추적 수신기라고도 하는 가장 일반적인 추적 대상은 기본 수신기 및 로그 파일입니다.  
  
 추적 수신기를 지정하지 않으면 기본 수신기가 추적에 사용됩니다. .NET Framework SDK와 함께 제공된 CLR 디버거 또는 Windows SDK와 함께 제공된 DBwin32.exe 같이 관리 코드를 사용할 수 있는 디버거에서 코드를 실행하여 기본 수신기에 전송된 메시지를 볼 수 있습니다. CLR 디버거를 사용하면 추적 메시지가 **출력** 창에 나타납니다.  
  
 파일을 사용하여 추적을 받으려면 다음 예제와 같이 구성 설정을 사용하여 로그 파일을 지정할 수 있습니다. 구성 파일에 대한 일반적인 설명은 [구성 파일](../../../docs/framework/configure-apps/index.md)을 참조하세요.  
  
 추적을 로그 파일에 보내려면 해당하는 구성 파일의 `<system.diagnostics>` 노드(응용 프로그램 또는 컴퓨터)에 다음 노드를 추가합니다. 필요에 맞도록 파일(trace.log)의 이름을 변경할 수 있습니다.  
  
```xml  
<system.diagnostics>  
  <trace autoflush="true" indentsize="4">  
    <listeners>  
      <add name="file" type="System.Diagnostics.TextWriterTraceListener" initializeData="trace.log"/>  
    </listeners>   
  </trace>  
</system.diagnostics>  
```  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 추적 해석](../../../docs/framework/network-programming/interpreting-network-tracing.md)  
 [.NET Framework의 네트워크 추적](../../../docs/framework/network-programming/network-tracing.md)  
 [응용 프로그램 추적 및 조율](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)
