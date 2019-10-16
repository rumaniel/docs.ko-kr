---
title: Windows Forms 및 관리되지 않는 애플리케이션
ms.date: 03/30/2017
helpviewer_keywords:
- ActiveX controls [Windows Forms]
- COM interop [Windows Forms], Windows Forms
- COM [Windows Forms]
- Windows Forms, unmanaged
- Windows Forms, interop
ms.assetid: 81bc100c-fa49-4614-85a6-0f7ab59eac8a
ms.openlocfilehash: 65465f22b1806d385523c894cce2103afe33c2f0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61746730"
---
# <a name="windows-forms-and-unmanaged-applications"></a>Windows Forms 및 관리되지 않는 애플리케이션
Windows Forms 애플리케이션과 컨트롤은 관리되지 않는 애플리케이션과 상호 운용될 수 있지만 몇 가지 주의할 사항이 있습니다. 다음 섹션에서는 Windows Forms 애플리케이션과 컨트롤이 지원하는 시나리오 및 구성과 지원하지 않는 시나리오 및 구성을 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [Windows Forms 및 관리되지 않는 응용 프로그램 개요](windows-forms-and-unmanaged-applications-overview.md)  
 관리되지 않는 애플리케이션에서 작동하는 Windows Forms 컨트롤을 사용 및 구현하는 방법에 대한 일반적인 정보를 제공합니다.  
  
 [방법: ShowDialog 메서드로 Windows Form을 표시 하 여 COM Interop 지원](com-interop-by-displaying-a-windows-form-shadow.md)  
 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> 메서드를 사용하여 관리되지 않는 애플리케이션에서 Windows Form을 실행하는 방법을 보여 주는 코드 예제를 제공합니다.  
  
 [방법: 각 Windows Form을 별개의 스레드에서 표시 하 여 COM Interop 지원](how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)  
 고유한 스레드에서 Windows Form을 실행하는 방법을 보여 주는 코드 예제를 제공합니다.  
  
 또한 참조 [연습: 각 Windows Form을 별개의 스레드에서 표시 하 여 COM Interop 지원](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233639(v=vs.100))합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType>  
 Windows Form에 대한 별도 스레드를 만드는 데 사용됩니다.  
  
 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType>  
 스레드에 대한 메시지 루프를 시작합니다.  
  
 <xref:System.Windows.Forms.Control.Invoke%2A>  
 관리되지 않는 애플리케이션에서의 폼 호출을 마샬링합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [.NET Framework 구성 요소를 COM에 노출](../../interop/exposing-dotnet-components-to-com.md)  
 관리되지 않는 애플리케이션에서 .NET Framework 형식을 사용하는 방법에 대한 일반적인 정보를 제공합니다.
