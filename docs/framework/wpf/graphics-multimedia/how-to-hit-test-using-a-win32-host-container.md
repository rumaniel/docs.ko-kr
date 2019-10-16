---
title: '방법: Win32 호스트 컨테이너를 사용하여 적중 테스트'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hit tests [WPF], using Win32 host containers
- visual objects [WPF], hit tests on
- Win32 host containers [WPF], hit tests using
ms.assetid: 9491f7f3-d8ba-4573-a888-2f064d1349dc
ms.openlocfilehash: ac5cae5bcd94dc8bf80ff95b8971914e1fa5ba2c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62025108"
---
# <a name="how-to-hit-test-using-a-win32-host-container"></a>방법: Win32 호스트 컨테이너를 사용하여 적중 테스트
내에서 시각적 개체를 만들 수는 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 시각적 개체에 대 한 호스트 창 컨테이너를 제공 하 여 창입니다. 포함된 시각적 개체에 대한 이벤트 처리를 제공하려면 호스트 창 컨테이너의 메시지 필터 루프에 전달된 메시지를 처리합니다. 참조 [자습서: Win32 응용 프로그램에서 시각적 개체 호스팅](tutorial-hosting-visual-objects-in-a-win32-application.md) 에서 시각적 개체를 호스트 하는 방법에 대 한 자세한 내용은 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창입니다.  
  
## <a name="example"></a>예제  
 다음 코드에 대 한 마우스 이벤트 처리기를 설정 하는 방법을 보여 줍니다는 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 시각적 개체에 대 한 호스트 컨테이너로 사용 되는 창입니다.  
  
 [!code-csharp[VisualsHitTesting#103](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#103)]
 [!code-vb[VisualsHitTesting#103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#103)]  
  
 다음 예제에서는 특정 마우스 이벤트 트래핑에 대 한 응답에서 적중된 테스트를 설정 하는 방법을 보여 줍니다.  
  
 [!code-csharp[VisualsHitTesting#104](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyCircle.cs#104)]
 [!code-vb[VisualsHitTesting#104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyCircle.vb#104)]  
  
 합니다 <xref:System.Windows.Interop.HwndSource> 개체가 나타내는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 내에서 콘텐츠를 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 창. 값을 <xref:System.Windows.Interop.HwndSource.RootVisual%2A> 속성의는 <xref:System.Windows.Interop.HwndSource> 개체 시각적 트리 계층의 최상위 노드를 나타냅니다.  
  
 적중 테스트에서 전체 샘플 Win32 호스트 컨테이너를 사용 하 여 개체에 대 한 참조 [Win32 상호 운용 샘플을 사용 하 여 적중 테스트](https://go.microsoft.com/fwlink/?LinkID=159995)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Interop.HwndSource>
- [시각적 계층에서 적중 테스트](hit-testing-in-the-visual-layer.md)
- [자습서: Win32 응용 프로그램에서 시각적 개체 호스팅](tutorial-hosting-visual-objects-in-a-win32-application.md)
