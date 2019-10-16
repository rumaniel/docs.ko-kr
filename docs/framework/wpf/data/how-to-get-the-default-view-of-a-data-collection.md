---
title: '방법: 데이터 컬렉션의 기본 보기 가져오기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data collections [WPF], creating views of
- data binding [WPF], creating views of data collections
ms.assetid: b641e96c-c2f6-42ea-9c5d-bac81176ad65
ms.openlocfilehash: 746331e69ee1e5eee795a0e35202f4889b72c53f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61931523"
---
# <a name="how-to-get-the-default-view-of-a-data-collection"></a>방법: 데이터 컬렉션의 기본 보기 가져오기
뷰는 동일한 데이터 수집을 정렬, 필터링 또는 그룹화 기준에 따라 다른 방법으로 볼 수 있도록 합니다. 모든 컬렉션에 바인딩 소스로 컬렉션을 지정 하는 경우 실제 바인딩 소스로 사용 되는 하나의 공유 기본 보기를 있습니다. 이 예제에는 컬렉션의 기본 보기를 가져오는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 보기를 만들려면 컬렉션에 개체 참조가 필요 합니다. 데이터 원본의 속성 가져오기 또는 바인딩 속성을 가져오거나 데이터 컨텍스트를 가져와서 사용자 고유의 코드 숨김 개체를 참조 하 여이 데이터 개체를 가져올 수 있습니다. 이 예제에서는 가져오는 방법을 보여 줍니다는 <xref:System.Windows.FrameworkElement.DataContext%2A> 데이터 개체 및 사용 하 여가이 컬렉션에 대 한 보기를 직접 기본 컬렉션을 가져옵니다.  
  
 [!code-csharp[CollectionView#2](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionView/CSharp/Page1.xaml.cs#2)]
 [!code-vb[CollectionView#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionView/VisualBasic/Page1.xaml.vb#2)]  
  
 이 예제에서는 루트 요소는는 <xref:System.Windows.Controls.StackPanel>합니다. <xref:System.Windows.FrameworkElement.DataContext%2A> 로 설정 되어 *myDataSource*에 데이터 공급자를 참조 하는 <xref:System.Collections.ObjectModel.ObservableCollection%601> 의 *순서* 개체입니다.  
  
 [!code-xaml[CollectionView#CollectionViewDataContext](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionView/CSharp/Page1.xaml#collectionviewdatacontext)]  
  
 또는 인스턴스화할 수를 고유한 컬렉션 뷰를 사용 하 여 바인딩할는 <xref:System.Windows.Data.CollectionViewSource> 클래스입니다. 이 컬렉션 뷰에서 직접 바인딩되는 컨트롤에만 공유 됩니다. 예를 들어 뷰 섹션 만들기 방법을 참조 합니다 [데이터 바인딩 개요](data-binding-overview.md)합니다.  
  
 컬렉션 뷰에서 제공 하는 기능의 예제를 참조 하세요. [뷰에서 데이터 정렬](how-to-sort-data-in-a-view.md)를 [뷰에서 데이터 필터링](how-to-filter-data-in-a-view.md), 및 [개체 탐색 데이터 수집 뷰의](how-to-navigate-through-the-objects-in-a-data-collectionview.md).  
  
## <a name="see-also"></a>참고자료

- [XAML 데이터 정렬 및 그룹화](how-to-sort-and-group-data-using-a-view-in-xaml.md)
- [방법 항목](data-binding-how-to-topics.md)
