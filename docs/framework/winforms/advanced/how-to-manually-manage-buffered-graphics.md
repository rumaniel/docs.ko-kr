---
title: '방법: 버퍼링된 그래픽 수동 관리'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- flicker [Windows Forms], reducing by manually managing graphics
- graphics [Windows Forms], managing buffered
ms.assetid: 4c2a90ee-bbbe-4ff6-9170-1b06c195c918
ms.openlocfilehash: 6010d52750b20c07db51917621f8643e9d9b47d7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968595"
---
# <a name="how-to-manually-manage-buffered-graphics"></a>방법: 버퍼링된 그래픽 수동 관리
고급 이중 버퍼링 시나리오의 경우 .NET Framework 클래스를 사용 하 여 사용자 고유의 더블 버퍼링 논리를 구현할 수 있습니다. 개별 그래픽 버퍼 <xref:System.Drawing.BufferedGraphicsContext> 를 할당 하 고 관리 하는 클래스는 클래스입니다. 모든 응용 프로그램에는 해당 <xref:System.Drawing.BufferedGraphicsContext> 응용 프로그램에 대 한 모든 기본 이중 버퍼링을 관리 하는 고유한 기본값이 있습니다. 을 호출 <xref:System.Drawing.BufferedGraphicsManager.Current%2A>하 여이 인스턴스에 대 한 참조를 검색할 수 있습니다.  
  
### <a name="to-obtain-a-reference-to-the-default-bufferedgraphicscontext"></a>기본 System.drawing.bufferedgraphicscontext>에 대 한 참조를 가져오려면  
  
- 다음 코드 예제와 같이 속성을설정합니다.<xref:System.Drawing.BufferedGraphicsManager.Current%2A>  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#11)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#11)]  
  
    > [!NOTE]
    > 클래스에서 <xref:System.Drawing.BufferedGraphicsContext> `Dispose` 받는참조에대해메서드를호출할필요가없습니다<xref:System.Drawing.BufferedGraphicsManager> . 는 <xref:System.Drawing.BufferedGraphicsManager> 기본<xref:System.Drawing.BufferedGraphicsContext> 인스턴스에 대 한 모든 메모리 할당과 배포를 처리 합니다.  
  
     애니메이션 등 <xref:System.Drawing.BufferedGraphicsContext> <xref:System.Drawing.BufferedGraphicsManager>의 그래픽을 많이 사용 하는 응용 프로그램의 경우에서 제공하는대신전용를사용하여성능을향상시킬수있습니다.<xref:System.Drawing.BufferedGraphicsContext> 이를 통해 응용 프로그램에서 사용 하는 메모리는 증가 하지만 응용 프로그램에 연결 된 다른 버퍼링 된 모든 그래픽을 관리 하는 성능 오버 헤드를 발생 시 키 지 않고 그래픽 버퍼를 개별적으로 만들고 관리할 수 있습니다.  
  
### <a name="to-create-a-dedicated-bufferedgraphicscontext"></a>전용 System.drawing.bufferedgraphicscontext>를 만들려면  
  
- 다음 코드 예제와 같이 <xref:System.Drawing.BufferedGraphicsContext> 클래스의 새 인스턴스를 선언 하 고 만듭니다.  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#12](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#12)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#12](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#12)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.BufferedGraphicsContext>
- [이중 버퍼링 그래픽](double-buffered-graphics.md)
- [방법: 버퍼링 된 그래픽 수동 렌더링](how-to-manually-render-buffered-graphics.md)
