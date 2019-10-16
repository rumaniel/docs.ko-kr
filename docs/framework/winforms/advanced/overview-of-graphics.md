---
title: 그래픽 개요
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [Windows Forms], using managed interface
- graphics [Windows Forms], about graphics
ms.assetid: a602aef8-a8c8-4c36-9816-74e7bad96a68
ms.openlocfilehash: f0e2fd9dcf31e5fdce16b5a3b6fd21eab6eab66a
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505327"
---
# <a name="overview-of-graphics"></a>그래픽 개요
GDI +는 API (응용 프로그래밍 인터페이스)는 Microsoft Windows 운영 체제의 하위 시스템을 구성 하는 경우 GDI +는 화면과 프린터에 정보를 표시 하는 일을 담당 합니다. 해당 이름에서 알 수 있듯이, GDI +는 GDI, 이전 버전의 Windows에 포함 된 그래픽 장치 인터페이스에 대 한 후속입니다.  
  
## <a name="managed-class-interface"></a>관리되는 클래스 인터페이스  
 GDI + API는 관리 코드로 배포 된 클래스 집합을 통해 노출 됩니다. 이 클래스 집합을 이라고 합니다 *관리 되는 클래스 인터페이스* GDI +입니다. 다음 네임스페이스는 관리되는 클래스 인터페이스를 구성합니다.  
  
- <xref:System.Drawing>  
  
- <xref:System.Drawing.Drawing2D>  
  
- <xref:System.Drawing.Imaging>  
  
- <xref:System.Drawing.Text>  
  
- <xref:System.Drawing.Printing>  
  
 GDI +에서 같은 그래픽 장치 인터페이스를 사용 하 여 특정 디스플레이 장치의 세부 정보를 염려 하지 않고 화면 또는 프린터에 정보를 표시할 수 있습니다. 프로그래머가 GDI + 클래스에서 제공 하는 메서드를 호출 합니다. 이러한 메서드가 다시 특정 디바이스 드라이버에 대한 적절한 호출을 수행합니다. GDI + 그래픽 하드웨어에서 응용 프로그램을 분리 합니다. 이 프로그래머가 장치 독립적인 응용 프로그램을 만들 수는 것입니다.  
  
## <a name="see-also"></a>참고자료

- [그래픽 개요](graphics-overview-windows-forms.md)
