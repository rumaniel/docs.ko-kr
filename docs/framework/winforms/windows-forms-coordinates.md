---
title: Windows Forms 좌표
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms coordinates
- screen coordinates
- client coordinates
- coordinates [Windows Forms], Windows Forms
ms.assetid: cc06e61f-43b6-4408-a676-2542dcfcd96e
ms.openlocfilehash: 6feabadff17538f4a7368c348f7b72226e2d678e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61800154"
---
# <a name="windows-forms-coordinates"></a>Windows Forms 좌표
Windows 폼을 위한 좌표계 장치 좌표를 기준으로 하며 Windows Forms에서 그릴 때의 기본 단위는 장치 단위 (일반적으로 픽셀)입니다. 지점은 화면에서 오른쪽, 위쪽에서 아래쪽 증가 y 좌표를 증가 하는 x 좌표를 사용 하 여 x 및 y 좌표 쌍에 의해 설명 되어 있습니다. 화면을 기준으로 원본 위치의 클라이언트 또는 화면 좌표를 지정 하는 여부에 따라 달라 집니다.  
  
## <a name="screen-coordinates"></a>화면 좌표  
 Windows Forms 응용 프로그램을 화면 좌표에서 화면에서 창의 위치를 지정 합니다. 화면 좌표에 대 한 원점은 화면의 왼쪽 위 모퉁이입니다. 창의 전체 위치에서 설명한 종종는 <xref:System.Drawing.Rectangle> 창의 왼쪽 및 오른쪽 아래 모퉁이 정의 하는 두 지점의 화면 좌표를 포함 하는 구조체입니다.  
  
## <a name="client-coordinates"></a>클라이언트 좌표  
 Windows Forms 응용 프로그램을 폼 이나 클라이언트 좌표를 사용 하 여 컨트롤에서 점의 위치를 지정 합니다. 클라이언트 좌표에 대 한 원본은 컨트롤이 나 폼의 클라이언트 영역의 왼쪽 위 모퉁이. 클라이언트 좌표로 응용 프로그램 폼 또는 폼 또는 화면에서 컨트롤의 위치에 관계 없이 컨트롤에서 그리기 하는 동안 일관 된 좌표 값을 사용할 수 있는지 확인 합니다.  
  
 클라이언트 영역의 크기에 대해서도 설명 하 여는 <xref:System.Drawing.Rectangle> 영역에 대 한 클라이언트 좌표를 포함 하는 구조입니다. 모든 경우에 사각형의 왼쪽 위 좌표는 오른쪽 아래 좌표는 제외 하는 동안 클라이언트 영역에 포함 됩니다. 그래픽 작업을 클라이언트 영역 오른쪽 및 아래쪽 가장자리를 포함 하지 않습니다. 예를 들어를 <xref:System.Drawing.Graphics.FillRectangle%2A> 메서드는 지정 된 사각형의 오른쪽 및 아래쪽 가장자리에 꽉 차게 됩니다 있지만 이러한 가장자리를 포함 하지 것입니다.  
  
## <a name="mapping-from-one-type-of-coordinate-to-another"></a>다른 한 가지 유형의 좌표에서 매핑  
 경우에 따라 클라이언트 좌표를 화면 좌표에서 지도를 해야 합니다. 사용 하 여 쉽게 수행할 수 있습니다 합니다 <xref:System.Windows.Forms.Control.PointToClient%2A> 및 <xref:System.Windows.Forms.Control.PointToScreen%2A> 에서 사용할 수 있는 메서드는 <xref:System.Windows.Forms.Control> 클래스입니다. 예를 들어를 <xref:System.Windows.Forms.Control.MousePosition%2A> 의 속성 <xref:System.Windows.Forms.Control> 화면 좌표에서 보고 되는 클라이언트 좌표로 변환할 필요할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Control.PointToClient%2A>
- <xref:System.Windows.Forms.Control.PointToScreen%2A>
