---
title: '방법: 애플리케이션 제스처 인식'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application gestures [WPF], recognizing
- gestures [WPF], recognizing
ms.assetid: d58b740f-5192-4a3e-af59-7aa162e6ca15
ms.openlocfilehash: 647e7c9c1d785cebfdc362dc48511d865f3945dc
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61768435"
---
# <a name="how-to-recognize-application-gestures"></a>방법: 애플리케이션 제스처 인식
다음 예제에서는 사용자 하면 잉크를 지우는 방법을 <xref:System.Windows.Ink.ApplicationGesture.ScratchOut> 제스처는 <xref:System.Windows.Controls.InkCanvas>합니다. 이 예에서는 가정를 <xref:System.Windows.Controls.InkCanvas>라는 `inkCanvas1`, XAML 파일에서 선언 됩니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[HowToRecognizeGestures#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToRecognizeGestures/CSharp/Window1.xaml.cs#1)]
 [!code-vb[HowToRecognizeGestures#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToRecognizeGestures/VisualBasic/Window1.xaml.vb#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Ink.ApplicationGesture>
- <xref:System.Windows.Controls.InkCanvas>
- <xref:System.Windows.Controls.InkCanvas.Gesture>
