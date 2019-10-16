---
title: '방법: 요소 및 컨트롤의 여백 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- setting [WPF], Margin property
- properties [WPF], Margin property
- Margin property [WPF], setting
ms.assetid: 70ebee01-6f87-4352-8dd4-402c65eaaed6
ms.openlocfilehash: 3263810806b6b4bbec15eadfd1f1da3a57d12698
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62052367"
---
# <a name="how-to-set-margins-of-elements-and-controls"></a>방법: 요소 및 컨트롤의 여백 설정
이 예제에서는 설정 하는 방법을 설명 합니다 <xref:System.Windows.FrameworkElement.Margin%2A> 여백 코드 숨김에 대 한 기존 속성 값을 변경 하 여 속성입니다. 합니다 <xref:System.Windows.FrameworkElement.Margin%2A> 속성은 속성의는 <xref:System.Windows.FrameworkElement> 기본 요소 및 다양 한 컨트롤 및 기타 요소에 의해 상속 되므로 됩니다.  
  
 이 예제로 작성 된 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], 하는 코드 숨김 파일을 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 가리킵니다. 코드 숨김 둘 다에 표시 됩니다는 C# 및 Microsoft Visual Basic 버전입니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[FEMarginProgrammatic#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FEMarginProgrammatic/CSharp/default.xaml#xaml)]  
  
 [!code-csharp[FEMarginProgrammatic#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/FEMarginProgrammatic/CSharp/default.xaml.cs#handler)]
 [!code-vb[FEMarginProgrammatic#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FEMarginProgrammatic/VisualBasic/default.xaml.vb#handler)]
