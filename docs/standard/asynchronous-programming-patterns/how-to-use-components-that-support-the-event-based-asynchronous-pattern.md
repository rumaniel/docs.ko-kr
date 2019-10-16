---
title: '방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 사용'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- components [.NET Framework], asynchronous
- AsyncOperation class
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 35e9549c-1568-4768-ad07-17cc6dff11e1
ms.openlocfilehash: 9ac98b5c576c065f8944714c72b492539e0d2f05
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59330885"
---
# <a name="how-to-use-components-that-support-the-event-based-asynchronous-pattern"></a>방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 사용
많은 구성 요소가 비동기적으로 작업을 수행하는 옵션을 제공합니다. 예를 들어 <xref:System.Media.SoundPlayer> 및 <xref:System.Windows.Forms.PictureBox> 구성 요소를 사용하면 기본 스레드가 중단 없이 계속 실행되는 동안 사운드 및 이미지를 “배경”으로 로드할 수 있습니다.  
  
 [이벤트 기반 비동기 패턴 개요](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)를 지원하는 클래스에 비동기 메서드를 사용하는 작업은 다른 이벤트의 경우와 같이 구성 요소의 _MethodName_**Completed** 이벤트에 이벤트 처리기를 연결하는 것처럼 간단할 수 있습니다. _MethodName_**Async** 메서드를 호출하면 애플리케이션은 _MethodName_**Completed** 이벤트가 발생할 때까지 중단 없이 계속 실행됩니다. 이벤트 처리기에서 <xref:System.ComponentModel.AsyncCompletedEventArgs> 매개 변수를 검사하여 비동기 작업이 성공적으로 완료되었는지 또는 취소되었는지 확인할 수 있습니다.  
  
 이벤트 처리기 사용에 대한 자세한 내용은 [이벤트 처리기 개요](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md)를 참조하세요.  
  
 다음 절차는 <xref:System.Windows.Forms.PictureBox> 컨트롤의 비동기 이미지 로드 기능을 사용하는 방법을 보여줍니다.  
  
### <a name="to-enable-a-picturebox-control-to-asynchronously-load-an-image"></a>PictureBox 컨트롤을 사용하여 이미지를 비동기적으로 로드하게 하려면  
  
1. 폼에서 <xref:System.Windows.Forms.PictureBox> 구성 요소의 인스턴스를 만듭니다.  
  
2. 이벤트 처리기를 <xref:System.Windows.Forms.PictureBox.LoadCompleted> 이벤트에 할당합니다.  
  
     여기에서 비동기 다운로드 중에 발생했을 수 있는 오류를 확인합니다. 여기에서 취소를 확인할 수도 있습니다.  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#2)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#5)]  
  
3. `loadButton` 및 `cancelLoadButton`이라는 두 개의 단추를 폼에 추가합니다. <xref:System.Windows.Forms.Control.Click> 이벤트 처리기를 추가하여 다운로드를 시작 및 취소합니다.  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#3)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#4)]  
  
4. 애플리케이션을 실행합니다.  
  
     이미지 다운로드가 진행되면 폼을 자유롭게 이동하고, 최소화하고, 최대화할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [방법: 백그라운드에서 작업 실행](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)
- [이벤트 기반 비동기 패턴 개요](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)
