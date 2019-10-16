---
title: '방법: XAML에서 보기를 사용하여 데이터 정렬 및 그룹화'
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [WPF], grouping data in views in XAML
- XAML [WPF], sorting data in views
- grouping data in views in XAML [WPF]
- data binding [WPF], sorting data in views in XAML
- sorting data in views in XAML [WPF]
- XAML [WPF], grouping data in views
- views [WPF], sorting data
- views [WPF], grouping data
ms.assetid: 145c8c3f-dbdd-4d0d-816f-90b35eba7eda
ms.openlocfilehash: ca4439b574264ebebfda745f0765f750099bc95f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62020740"
---
# <a name="how-to-sort-and-group-data-using-a-view-in-xaml"></a>방법: XAML에서 보기를 사용하여 데이터 정렬 및 그룹화
이 예제에서 데이터 컬렉션의 뷰를 만드는 방법을 보여 줍니다 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]합니다. 뷰 그룹화, 정렬, 필터링의 기능 및 현재 항목의 개념을 허용 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 정적 리소스 이름이 *배치* 컬렉션으로 정의 됩니다 *장소* 개체를 각 *위치* 도시 이름으로 구성 된 개체 및 상태입니다. 접두사 *src* 네임 스페이스에 매핑되는 데이터 원본 *자릿수* 정의 됩니다. 접두사 *scm* 매핑됩니다 `"clr-namespace:System.ComponentModel;assembly=WindowsBase"` 하 고 *dat* 매핑됩니다 `"clr-namespace:System.Windows.Data;assembly=PresentationFramework"`합니다.  
  
 다음 예제에서는 도시 이름별으로 정렬 되 고 상태별으로 그룹화 된 데이터 컬렉션의 뷰를 만듭니다.  
  
 [!code-xaml[CollectionViewSource#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#1)]  
  
 뷰에는 바인딩 소스는 다음 예제와 같이 될 수 있습니다.  
  
 [!code-xaml[CollectionViewSource#2](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#2)]  
  
 에 정의 된 XML 데이터에 대 한 바인딩의 <xref:System.Windows.Data.XmlDataProvider> 리소스를 사용 하 여 XML 이름 앞에 @ 기호.  
  
 [!code-xaml[CollectionViewSource#XDPChunk](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#xdpchunk)]  
  
 [!code-xaml[CollectionViewSource#Attribute](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#attribute)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Data.CollectionViewSource>
- [데이터 수집의 기본 뷰 가져오기](how-to-get-the-default-view-of-a-data-collection.md)
- [데이터 바인딩 개요](data-binding-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
