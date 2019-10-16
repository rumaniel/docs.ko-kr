---
title: 좌표계 형식
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- transformations [Windows Forms], page
- unit of measure
- world coordinate system
- page coordinate system
- page transformation
- device coordinate system
- world transformation
- coordinate systems
- transformations [Windows Forms], world
ms.assetid: c61ff50a-eb1d-4e6c-83cd-f7e9764cfa9f
ms.openlocfilehash: 23d9374f1f46c4480079eb4ad5269a197a13a5bf
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963886"
---
# <a name="types-of-coordinate-systems"></a>좌표계 형식
GDI +-세 가지 좌표 공간을 사용 하는 중: 전역, 페이지 및 디바이스입니다. 세계 좌표 좌표 특정 그래픽 월드를 모델링 하는 데 사용 되며.NET Framework의 메서드에 전달 합니다. 페이지 좌표는 폼 또는 컨트롤과 같은 그리기 화면에서 사용 하는 좌표계를 나타냅니다. 장치 좌표는 화면이 나 용지와 같이 그려지는 실제 장치에서 사용 하는 좌표입니다. 호출 `myGraphics.DrawLine(myPen, 0, 0, 160, 80)`을 수행 하는 경우 <xref:System.Drawing.Graphics.DrawLine%2A> 메서드에 전달 하는 요소 (`(0, 0)` 및 `(160, 80)`)는 세계 좌표 공간에 있습니다. GDI +에서 화면에 선을 그리려면 좌표는 일련의 변환으로 전달 됩니다. 세계 좌표 변환 이라고 하는 한 가지 변환은 세계 좌표를 페이지 좌표로 변환 하 고 페이지 변환 이라고 하는 다른 변환은 페이지 좌표를 장치 좌표로 변환 합니다.  
  
## <a name="transforms-and-coordinate-systems"></a>시스템 변환 및 조정  
 왼쪽 위 모퉁이가 아닌 클라이언트 영역의 본문에서 원점이 있는 좌표계를 사용 하 려 한다고 가정 합니다. 예를 들어, 클라이언트 영역의 왼쪽 가장자리에서 100 픽셀, 클라이언트 영역의 맨 위에 있는 50 픽셀을 기준으로 픽셀을 만들려고 한다고 가정 합니다. 다음 그림에서는 이러한 좌표 시스템을 보여 줍니다.  
  
 ![좌표계](./media/aboutgdip05-art01.gif "AboutGdip05_art01")  
  
 전화를 걸 `myGraphics.DrawLine(myPen, 0, 0, 160, 80)`때 다음 그림에 표시 된 줄을 얻을 수 있습니다.  
  
 ![좌표계](./media/aboutgdip05-art02.gif "AboutGdip05_art02")  
  
 세 좌표 공간의 선 끝점 좌표는 다음과 같습니다.  
  
|||  
|-|-|  
|World|(0, 0) ~ (160, 80)|  
|페이지|(100, 50) to (260, 130)|  
|디바이스|(100, 50) to (260, 130)|  
  
 페이지 좌표 공간의 원점은 클라이언트 영역의 왼쪽 위 모퉁이에 있습니다. 이는 항상입니다. 또한 측정 단위가 픽셀 이므로 장치 좌표는 페이지 좌표와 동일 합니다. 측정 단위를 픽셀 (예: 인치) 이외의 다른 항목으로 설정 하는 경우에는 장치 좌표가 페이지 좌표와 다릅니다.  
  
 세계 좌표를 페이지 좌표로 매핑하는 세계 변환은 <xref:System.Drawing.Graphics.Transform%2A> <xref:System.Drawing.Graphics> 클래스의 속성에 저장 됩니다. 앞의 예제에서 전 세계 변환은 x 방향으로 변환 100 단위이 고 y 방향으로 50 단위입니다. 다음 예제에서는 <xref:System.Drawing.Graphics> 개체의 전 세계 변환을 설정 하 고 해당 <xref:System.Drawing.Graphics> 개체를 사용 하 여 앞의 그림에 표시 된 줄을 그립니다.  
  
 [!code-csharp[System.Drawing.CoordinateSystems#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.CoordinateSystems#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#31)]  
  
 페이지 변환은 페이지 좌표를 장치 좌표로 매핑합니다. 클래스 <xref:System.Drawing.Graphics> 는 페이지 변환을 <xref:System.Drawing.Graphics.PageUnit%2A> 조작 <xref:System.Drawing.Graphics.PageScale%2A> 하기 위한 및 속성을 제공 합니다. 또한 <xref:System.Drawing.Graphics> 클래스는 두 개의 읽기 전용 <xref:System.Drawing.Graphics.DpiX%2A> 속성인 및 <xref:System.Drawing.Graphics.DpiY%2A>를 제공 하 여 디스플레이 장치의 가로 및 세로 dpi를 검사 합니다.  
  
 클래스의 속성<xref:System.Drawing.Graphics.PageUnit%2A> 을 사용 하 여 픽셀 이외의 측정 단위를 지정할 수 있습니다. <xref:System.Drawing.Graphics>  
  
> [!NOTE]
> 이는 물리적 단위가 <xref:System.Drawing.Graphics.PageUnit%2A> 아니고 예외 <xref:System.Drawing.GraphicsUnit.World>를 발생 시킬 수 있으므로 속성을로 설정할 수 없습니다.  
  
 다음 예에서는 (0, 0)에서 (2, 1) 사이의 줄을 그립니다. 여기서 point (2, 1)는 오른쪽의 2 인치이 고 점 (0, 0)에서 1 인치가 됩니다.  
  
 [!code-csharp[System.Drawing.CoordinateSystems#32](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.CoordinateSystems#32](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#32)]  
  
> [!NOTE]
> 펜을 생성할 때 펜 너비를 지정 하지 않으면 앞의 예제에서는 1 인치 너비의 줄을 그립니다. <xref:System.Drawing.Pen> 생성자에 대 한 두 번째 인수에서 펜 너비를 지정할 수 있습니다.  
  
 [!code-csharp[System.Drawing.CoordinateSystems#33](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#33)]
 [!code-vb[System.Drawing.CoordinateSystems#33](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#33)]  
  
 디스플레이 장치에 가로 방향으로 96 dpi가 있고 세로 방향으로 96 점이 있는 경우 위의 예제에서 선의 끝점에는 세 좌표 공간에 다음 좌표가 있습니다.  
  
|||  
|-|-|  
|World|(0, 0)-(2, 1)|  
|페이지|(0, 0)-(2, 1)|  
|디바이스|(0, 0, ~ (192, 96)|  
  
 세계 좌표 공간의 원점이 클라이언트 영역의 왼쪽 위 모퉁이에 있기 때문에 페이지 좌표는 세계 좌표와 동일 합니다.  
  
 전 세계와 페이지 변형을 결합 하 여 다양 한 효과를 달성할 수 있습니다. 예를 들어 인치를 측정 단위로 사용 하 고 좌표계의 원점을 클라이언트 영역의 왼쪽 가장자리에서 2 인치로, 클라이언트 영역의 위쪽에서 1/2 인치로 만들려고 한다고 가정 합니다. 다음 예제에서는 <xref:System.Drawing.Graphics> 개체의 전 세계 및 페이지 변환을 설정 하 고 (0, 0)에서 (2, 1)로 줄을 그립니다.  
  
 [!code-csharp[System.Drawing.CoordinateSystems#34](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#34)]
 [!code-vb[System.Drawing.CoordinateSystems#34](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#34)]  
  
 다음 그림에서는 선 및 좌표계를 보여 줍니다.  
  
 ![좌표계](./media/aboutgdip05-art03.gif "AboutGdip05_art03")  
  
 디스플레이 장치에 가로 방향으로 96 dpi가 있고 세로 방향으로 96 점이 있는 경우 위의 예제에서 선의 끝점에는 세 좌표 공간에 다음 좌표가 있습니다.  
  
|||  
|-|-|  
|World|(0, 0)-(2, 1)|  
|페이지|(2, 0.5) ~ (4, 1.5)|  
|디바이스|(192, 48) to (384, 144)|  
  
## <a name="see-also"></a>참고자료

- [좌표계 및 변형](coordinate-systems-and-transformations.md)
- [매트릭스에 의한 변형 표시](matrix-representation-of-transformations.md)
