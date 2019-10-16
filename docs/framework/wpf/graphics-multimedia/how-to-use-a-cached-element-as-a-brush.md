---
title: '방법: 캐시된 요소를 브러시로 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- BitmapCache [WPF], using
- cached element [WPF], use as a brush
- BitmapCacheBrush [WPF], using
- CacheMode [WPF], using
ms.assetid: d36e944a-866e-4baf-98c4-fd6a75f6fdd0
ms.openlocfilehash: 78df242c7f00b69e36ea4ab6751f51509d9e2220
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61769259"
---
# <a name="how-to-use-a-cached-element-as-a-brush"></a>방법: 캐시된 요소를 브러시로 사용
사용 하 여는 <xref:System.Windows.Media.BitmapCacheBrush> 클래스를 효율적으로 캐시 된 요소를 다시 사용 합니다. 새 인스턴스를 만들고 요소를 캐시 하려면 합니다 <xref:System.Windows.Media.BitmapCache> 클래스 및 요소에 할당할 <xref:System.Windows.UIElement.CacheMode%2A> 속성입니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 캐시 된 요소를 다시 사용 하는 방법을 보여 줍니다. 캐시 된 요소는 <xref:System.Windows.Controls.Image> 큰 이미지를 표시 하는 컨트롤입니다. <xref:System.Windows.Controls.Image> 컨트롤이 사용 하 여 비트맵으로 캐시 되는 <xref:System.Windows.Media.BitmapCache> 할당 하 여 클래스 및 캐시를 다시 사용을 <xref:System.Windows.Media.BitmapCacheBrush>입니다. 브러시는 효율적인 재사용을 표시할 25 단추의 배경을에 할당 됩니다.  
  
 [!code-xaml[System.Windows.Media.BitmapCacheBrush#_BitmapCacheBrushXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/system.windows.media.bitmapcachebrush/cs/window1.xaml#_bitmapcachebrushxaml)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.BitmapCache>
- <xref:System.Windows.Media.BitmapCacheBrush>
- <xref:System.Windows.UIElement.CacheMode%2A>
- [방법: 요소를 캐시 하 여 렌더링 성능 향상](how-to-improve-rendering-performance-by-caching-an-element.md)
