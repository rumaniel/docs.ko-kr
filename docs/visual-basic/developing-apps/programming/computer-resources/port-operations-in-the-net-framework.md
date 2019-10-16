---
title: Visual Basic을 사용한 .NET Framework의 포트 작업
ms.date: 07/20/2015
helpviewer_keywords:
- ports, Visual Basic
ms.assetid: 1eba223b-7bd3-401a-b097-982bce96df1b
ms.openlocfilehash: 936ff4c861444d3a971b38fd7b2a0af38b19494b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916598"
---
# <a name="port-operations-in-the-net-framework-with-visual-basic"></a>Visual Basic을 사용한 .NET Framework의 포트 작업
<xref:System.IO.Ports?displayProperty=nameWithType> 네임스페이스의 .NET Framework 클래스를 통해 컴퓨터의 직렬 포트에 액세스할 수 있습니다. 가장 중요한 클래스인 <xref:System.IO.Ports.SerialPort>는 동기 및 이벤트 구동 I/O, 핀 및 중단 상태 액세스, 그리고 직렬 드라이버 속성 액세스를 위한 프레임워크를 제공합니다. 이 클래스는 <xref:System.IO.Ports.SerialPort.BaseStream> 속성을 통해 액세스 가능한 <xref:System.IO.Stream> 개체에 래핑할 수 있습니다. <xref:System.IO.Stream> 개체에 <xref:System.IO.Ports.SerialPort>를 래핑하면 스트림을 사용하는 클래스가 직렬 포트에 액세스할 수 있습니다. 네임스페이스에는 직렬 포트의 제어를 간소화하는 열거형이 포함됩니다.  
  
 <xref:System.IO.Ports.SerialPort> 개체를 만드는 가장 간단한 방법은 <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A> 메서드를 사용하는 것입니다.  
  
> [!NOTE]
> .NET Framework 클래스를 사용하여 병렬 포트, USB 포트 등 다른 유형의 포트에 직접 액세스할 수 없습니다.  
  
## <a name="enumerations"></a>열거형  
 이 표에서는 직렬 포트 액세스에 사용되는 주요 열거형에 대해 설명합니다.  
  
|열거형|설명|  
|---|---|   
|<xref:System.IO.Ports.Handshake>|<xref:System.IO.Ports.SerialPort> 개체에 대한 직렬 포트 통신을 설정할 때 사용되는 제어 프로토콜을 지정합니다.|  
|<xref:System.IO.Ports.Parity>|<xref:System.IO.Ports.SerialPort> 개체에 대한 패리티 비트를 지정합니다.|  
|<xref:System.IO.Ports.SerialData>|<xref:System.IO.Ports.SerialPort> 개체의 직렬 포트에서 수신된 문자 형식을 지정합니다.|  
|<xref:System.IO.Ports.SerialError>|<xref:System.IO.Ports.SerialPort> 개체에서 발생하는 오류를 지정합니다.|  
|<xref:System.IO.Ports.SerialPinChange>|<xref:System.IO.Ports.SerialPort> 개체에서 수행된 변경의 유형을 지정합니다.|  
|<xref:System.IO.Ports.StopBits>|<xref:System.IO.Ports.SerialPort> 개체에 사용되는 정지 비트의 수를 지정합니다.|  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.Devices.Ports>
- [컴퓨터 포트에 액세스](../../../../visual-basic/developing-apps/programming/computer-resources/accessing-the-computer-s-ports.md)
