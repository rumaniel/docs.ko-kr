---
title: 네트워크 추적 해석
ms.date: 03/30/2017
helpviewer_keywords:
- TraceMode attribute
- hexidecimal data, network tracing output
- network tracing, analyzing
- protocolonly
- text, network tracing output
- includehex
ms.assetid: ad22b4b8-00af-4778-9cca-cb609ce1f8ff
ms.openlocfilehash: fd617e152b1e86cc71dd8e3cc8a01f1d2f52c30a
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71047898"
---
# <a name="interpreting-network-tracing"></a>네트워크 추적 해석
네트워크 추적이 사용하도록 설정되면 추적 기능을 사용하여 애플리케이션이 다양한 <xref:System.Net> 클래스 멤버에 대해 실행하는 호출을 캡처할 수 있습니다. 이러한 호출의 출력은 다음 예제와 비슷할 수 있습니다.  
  
```output
[588]   (4357)   Entering Socket#33574638::Send()  
[588]   (4387)   Exiting Socket#33574638::Send()-> 61#61
```  
  
 이전 예제에서 [588]은 현재 스레드의 고유 식별자입니다. (4357) 및 (4387)은 애플리케이션이 시작된 이후 경과한 시간(밀리초)을 나타내는 타임스탬프입니다. 타임스탬프 뒤의 데이터는 애플리케이션이 **Socket.Send** 메서드를 시작 및 종료하는 것을 보여 줍니다. **Send** 메서드를 실행하는 개체의 고유 식별자는 33574638입니다. 메서드 종료 추적에는 반환 값이 포함됩니다(이전 예제의 경우 61).  
  
 네트워크 추적은 HTTP(Hypertext Transfer Protocol)와 같은 애플리케이션 수준 프로토콜을 사용하여 애플리케이션이 보내고 받은 네트워크 트래픽을 캡처할 수 있습니다. 이 데이터는 텍스트로 캡처할 수 있고 필요한 경우 16진수 데이터로 캡처할 수 있습니다. 16진수 데이터는 **includehex**를 **tracemode** 특성 값으로 지정할 때 사용할 수 있습니다. (이 특성에 대한 자세한 내용은 [방법: 네트워크 추적 구성](how-to-configure-network-tracing.md)을 참조하세요.) 다음 예제 추적은 **includehex**를 사용하여 생성되었습니다.  
  
 `[1692]   (1142)   00000000 : 47 45 54 20 2F 77 70 61-64 2E 64 61 74 20 48 54 : GET /wpad.dat HT`  
  
 `[1692]   (1142)   00000010 : 54 50 2F 31 2E 31 0D 0A-48 6F 73 74 3A 20 69 74 : TP/1.1..Host: it`  
  
 `[1692]   (1142)   00000020 : 67 70 72 6F 78 79 0D 0A-43 6F 6E 6E 65 63 74 69 : gproxy..Connecti`  
  
 `[1692]   (1142)   00000030 : 6F 6E 3A 20 43 6C 6F 73-65 0D 0A 0D 0A     : on: Close....`  
  
 16진수 데이터를 제외하려면 **protocolonly**를 **tracemode** 특성 값으로 지정합니다. 다음 예제에서는 **protocolonly**가 지정될 경우의 추적을 보여 줍니다.  
  
 `[2444]   (594)   Data from ConnectStream#33574638::WriteHeaders<<GET /wpad.dat HTTP/1.1`  
  
 `Host: itgproxy`  
  
 `Connection: Close`  
  
## <a name="see-also"></a>참고 항목

- [네트워크 추적 사용](enabling-network-tracing.md)
- [방법: 네트워크 추적 구성](how-to-configure-network-tracing.md)
- [.NET Framework의 네트워크 추적](network-tracing.md)
