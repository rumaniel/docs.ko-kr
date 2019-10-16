---
title: 전역 및 지역 변환
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- matrices [Windows Forms], using transformations
- transformations [Windows Forms], global
- transformations [Windows Forms], local
ms.assetid: b601d66d-d572-4f11-9d2e-92f0dc8893f3
ms.openlocfilehash: f62efb31e95b0797272997fadbc28459579a0de0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69955187"
---
# <a name="global-and-local-transformations"></a>전역 및 지역 변환
전역 변환은 지정 <xref:System.Drawing.Graphics> 된 개체에 의해 그려지는 모든 항목에 적용 되는 변환입니다. 반면 로컬 변환은 그릴 특정 항목에 적용 되는 변환입니다.  
  
## <a name="global-transformations"></a>전역 변환  
 전역 변환을 만들려면 <xref:System.Drawing.Graphics> 개체를 생성 한 다음 해당 <xref:System.Drawing.Graphics.Transform%2A> 속성을 조작 합니다. <xref:System.Drawing.Graphics.Transform%2A> 속성<xref:System.Drawing.Drawing2D.Matrix> 은 개체 이므로 상관 변환의 모든 시퀀스를 포함할 수 있습니다. <xref:System.Drawing.Graphics.Transform%2A> 속성에 저장 된 변환을 전역 변환 이라고 합니다. 클래스 <xref:System.Drawing.Graphics> <xref:System.Drawing.Graphics.MultiplyTransform%2A>는,, 및 <xref:System.Drawing.Graphics.ScaleTransform%2A> <xref:System.Drawing.Graphics.RotateTransform%2A> 복합세계변환을빌드하기위한여러메서드<xref:System.Drawing.Graphics.TranslateTransform%2A>를 제공 합니다. 다음 예제에서는 타원을 두 번 그립니다. 전 세계 변환을 만들고 한 번은 한 번입니다. 변환은 먼저 y 방향으로 0.5의 비율로 크기를 조정 하 고 x 방향으로 50 단위를 변환한 다음 30도 회전 합니다.  
  
 [!code-csharp[System.Drawing.CoordinateSystems#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.CoordinateSystems#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#21)]  
  
 다음 그림에서는 변환과 관련 된 행렬을 보여 줍니다.  
  
 ![Transformations](./media/aboutgdip05-art14.gif "AboutGdip05_art14")  
  
> [!NOTE]
> 앞의 예제에서는 클라이언트 영역의 왼쪽 위 모퉁이에 있는 좌표계의 원점에 대해 타원이 회전 합니다. 그러면 타원을 자체 중심으로 회전 하는 것과 다른 결과가 생성 됩니다.  
  
## <a name="local-transformations"></a>로컬 변환  
 로컬 변환은 그릴 특정 항목에 적용 됩니다. 예를 들어 개체 <xref:System.Drawing.Drawing2D.GraphicsPath> <xref:System.Drawing.Drawing2D.GraphicsPath.Transform%2A> 에는 해당 경로의 데이터 요소를 변환 하는 데 사용할 수 있는 메서드가 있습니다. 다음 예제에서는 변환이 없고 회전 변환이 있는 경로를 사용 하 여 사각형을 그립니다. (전 세계 변환이 없는 것으로 가정)  
  
 [!code-csharp[System.Drawing.CoordinateSystems#22](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.CoordinateSystems#22](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#22)]  
  
 전역 변환을 로컬 변환과 결합 하 여 다양 한 결과를 달성할 수 있습니다. 예를 들어 세계 변형을 사용 하 여 좌표계를 수정 하 고 로컬 변형을 사용 하 여 새 좌표계에 그려진 개체를 회전 하 고 크기를 조정할 수 있습니다.  
  
 클라이언트 영역의 왼쪽 가장자리에서 200 픽셀의 원점 및 클라이언트 영역의 위쪽에서 150 픽셀을 가진 좌표계를 만들려고 한다고 가정 합니다. 또한 측정 단위가 픽셀 임을 가정 합니다. x 축이 오른쪽을 가리키고 y 축은 위쪽을 가리킵니다. 기본 좌표계에는 y 축이 있고 가로 축에서 반사를 수행 해야 합니다. 다음 그림에서는 이러한 리플렉션의 행렬을 보여 줍니다.  
  
 ![Transformations](./media/aboutgdip05-art15.gif "AboutGdip05_art15")  
  
 다음으로, 200 단위를 오른쪽으로 이동 하 고 150 단위를 종료 해야 한다고 가정 합니다.  
  
 다음 예에서는 <xref:System.Drawing.Graphics> 개체의 세계 변형을 설정 하 여 설명한 대로 좌표계를 설정 합니다.  
  
 [!code-csharp[System.Drawing.CoordinateSystems#23](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#23)]
 [!code-vb[System.Drawing.CoordinateSystems#23](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#23)]  
  
 이전 예제의 끝에 있는 다음 코드는 새 좌표계의 원점에서 왼쪽 아래 모퉁이가 있는 단일 사각형으로 구성 된 경로를 만듭니다. 사각형은 로컬 변환이 없고 로컬 변환을 사용 하 여 한 번 채워집니다. 로컬 변환은 요소 2의 가로 크기 조정 후 30도 회전으로 구성 됩니다.  
  
 [!code-csharp[System.Drawing.CoordinateSystems#24](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#24)]
 [!code-vb[System.Drawing.CoordinateSystems#24](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#24)]  
  
 다음 그림에서는 새 좌표계와 두 개의 사각형을 보여 줍니다.  
  
 ![Transformations](./media/aboutgdip05-art16.gif "AboutGdip05_art16")  
  
## <a name="see-also"></a>참고자료

- [좌표계 및 변형](coordinate-systems-and-transformations.md)
- [관리 GDI+에서 변형 사용](using-transformations-in-managed-gdi.md)
