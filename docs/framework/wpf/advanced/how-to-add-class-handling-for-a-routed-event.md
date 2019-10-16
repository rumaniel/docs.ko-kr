---
title: '방법: 라우트된 이벤트에 대한 클래스 처리 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- routed events [WPF], class handlers
- task_core_add_class_handling_routed_properties [WPF]
- class handlers [WPF], routed events
ms.assetid: 15b7b06c-9112-4ee5-b30a-65d10c5c5df6
ms.openlocfilehash: 7b897954cbdab461dc0305c6290e67c1af5282c3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61777041"
---
# <a name="how-to-add-class-handling-for-a-routed-event"></a>방법: 라우트된 이벤트에 대한 클래스 처리 추가
클래스 처리기 또는 경로의 지정 된 모든 노드에서 인스턴스 처리기 라우트된 이벤트를 처리할 수 있습니다. 클래스 처리기는 먼저 호출 및 인스턴스 처리에서 이벤트를 억제 하는 기본 클래스를 소유 하는 이벤트에 다른 이벤트가 특정 동작을 소개 클래스 구현에서 사용할 수 있습니다. 이 예제에는 클래스 처리기를 구현 하는 것에 대 한 밀접 한 관련이 있는 두 가지 기술을 보여 줍니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 사용자 지정을 기반으로 클래스는 <xref:System.Windows.Controls.Canvas> 패널입니다. 응용 프로그램의 기본 전제는 사용자 지정 클래스 모든 마우스 왼쪽된 단추 클릭을 가로채 고 처리 된 것으로, 자식 요소 클래스 또는 인스턴스 처리기에서 호출 될 전에 표시를 포함 하 여 해당 자식 요소에 대 한 동작을는 것입니다.  
  
 <xref:System.Windows.UIElement> 클래스에서 처리를 사용 하도록 설정 하는 가상 메서드를 노출 하는 클래스는 <xref:System.Windows.UIElement.PreviewMouseLeftButtonDown> 단순히 이벤트를 재정의 하 여 이벤트입니다. 이것이 이러한 가상 메서드는 클래스의 계층 구조 내의 사용 가능한 경우 클래스 처리를 구현 하는 가장 간단한 방법입니다. 다음 코드에서는 합니다 <xref:System.Windows.UIElement.OnPreviewMouseLeftButtonDown%2A> 에 "MyEditContainer"에서 파생 된 구현 <xref:System.Windows.Controls.Canvas>합니다. 구현 인수를 처리 하는 대로 이벤트를 표시 하 고 기본 화면상의 변화 소스 요소를 제공 하도록 몇 가지 코드를 추가 합니다.  
  
 [!code-csharp[ClassHandling#OnStarClassHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/ClassHandling/CSharp/SDKSampleLibrary/class1.cs#onstarclasshandler)]
 [!code-vb[ClassHandling#OnStarClassHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ClassHandling/visualbasic/sdksamplelibrary/class1.vb#onstarclasshandler)]  
  
 유틸리티 메서드를 사용 하 여 직접 클래스 처리를 추가할 수 없습니다 가상 인 경우 또는 특정 메서드에 대 한 기본 클래스에서 사용할 수는 <xref:System.Windows.EventManager> 클래스인 <xref:System.Windows.EventManager.RegisterClassHandler%2A>합니다. 이 메서드는 클래스 처리를 추가 하는 클래스의 정적 초기화 내 에서만 호출 해야 합니다. 에 대 한 다른 처리기를 추가 하는이 예제 <xref:System.Windows.UIElement.PreviewMouseLeftButtonDown> ,이 경우에 등록 된 클래스는 사용자 지정 클래스 및 합니다. 반면, 가상 메서드를 사용 하면 등록 된 클래스는 실제로 <xref:System.Windows.UIElement> 기본 클래스입니다. 기본 클래스 및 하위 클래스는 각 등록할 클래스 처리에 있는 경우에는 서브 클래스 처리기는 먼저 호출 됩니다. 응용 프로그램의 동작이 우선이 처리기는 해당 messagebox를 표시 하 고 다음 가상 메서드를 처리기의 시각적 변경 내용이 표시 되는 것입니다.  
  
 [!code-csharp[ClassHandling#StaticAndRegisterClassHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/ClassHandling/CSharp/SDKSampleLibrary/class1.cs#staticandregisterclasshandler)]
 [!code-vb[ClassHandling#StaticAndRegisterClassHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ClassHandling/visualbasic/sdksamplelibrary/class1.vb#staticandregisterclasshandler)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.EventManager>
- [라우트된 이벤트를 처리된 것으로 표시 및 클래스 처리](marking-routed-events-as-handled-and-class-handling.md)
- [라우트된 이벤트 처리](how-to-handle-a-routed-event.md)
- [라우트된 이벤트 개요](routed-events-overview.md)
