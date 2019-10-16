---
title: '방법: 시스템 글꼴 열거'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- typography [WPF], enumerating system fonts
- fonts [WPF], enumerating
- system fonts [WPF], enumerating
- enumerating [WPF], system fonts
ms.assetid: 36e37791-55b9-4f01-a496-5cc10335e6a6
ms.openlocfilehash: c7e81b5d1b70ba911a0b505219f7977e019038cf
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001600"
---
# <a name="how-to-enumerate-system-fonts"></a>방법: 시스템 글꼴 열거
## <a name="example"></a>예제  
 다음 예제에서는 시스템 글꼴 컬렉션의에서 글꼴을 열거 하는 방법을 보여 줍니다. 각각의 글꼴 패밀리 이름 <xref:System.Windows.Media.FontFamily> 내에서 <xref:System.Windows.Media.Fonts.SystemFontFamilies%2A> 콤보 상자에 항목으로 추가 됩니다.  
  
 [!code-csharp[TextOverview#100](~/samples/snippets/csharp/VS_Snippets_Wpf/TextOverview/CSharp/Window1.xaml.cs#100)]
 [!code-vb[TextOverview#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextOverview/visualbasic/window1.xaml.vb#100)]  
  
 같은 디렉터리에 있는 여러 버전의 동일한 글꼴 패밀리를 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 글꼴 열거형 글꼴의 최신 버전을 반환 합니다. 버전 정보를 확인 하지 않습니다, 경우에 최신 타임 스탬프를 사용 하 여 글꼴 반환 됩니다. 타임 스탬프 정보를 해당 하는 경우에 알파벳 순서로 첫 번째는 글꼴 파일 반환 됩니다.
