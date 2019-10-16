---
title: '방법: 데이터 CollectionView에서 개체 탐색'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CollectionView [WPF], navigating through objects
- data binding [WPF], navigating through objects in data CollectionView
- navigating through objects in data CollectionView [WPF]
ms.assetid: fcd37590-bce1-4ac9-8b74-3b96c7458b8a
ms.openlocfilehash: 1507ab4db0c91b670d8bca754f6fd67d887c7041
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61931505"
---
# <a name="how-to-navigate-through-the-objects-in-a-data-collectionview"></a>방법: 데이터 CollectionView에서 개체 탐색
뷰는 동일한 데이터 수집을 정렬, 필터링 또는 그룹화에 따라 다른 방법으로 볼 수 있도록 합니다. 뷰는 또한 현재 레코드 포인터 개념을 제공 하 고 포인터를 이동 하는 사용 하도록 설정 합니다. 현재 개체를 가져올 수 있을 뿐만 아니라에서 제공 하는 기능을 사용 하 여 데이터 컬렉션의 개체를 통해 이동 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Data.CollectionView> 클래스입니다.  
  
## <a name="example"></a>예제  
 이 예에서 `myCollectionView` 는 <xref:System.Windows.Data.CollectionView> 개체 뷰를 바인딩 컬렉션입니다.  
  
 다음 예에서 `OnButton` 에 대 한 이벤트 처리기는 `Previous` 및 `Next` 응용 프로그램에서 데이터 컬렉션을 탐색 하는 데 사용할 수 있는 단추는 단추입니다. <xref:System.Windows.Data.CollectionView.IsCurrentBeforeFirst%2A> 하 고 <xref:System.Windows.Data.CollectionView.IsCurrentAfterLast%2A> 속성이 있는지 여부를 현재 레코드 포인터에 제공 시작과 목록의 끝에 각각 하므로 보고서 <xref:System.Windows.Data.CollectionView.MoveCurrentToFirst%2A> 및 <xref:System.Windows.Data.CollectionView.MoveCurrentToLast%2A> 으로 적절 하 게 호출할 수 있습니다.  
  
 <xref:System.Windows.Data.CollectionView.CurrentItem%2A> 보기의 속성으로 캐스팅 됩니다는 `Order` 컬렉션의 현재 주문 항목을 반환 합니다.  
  
 [!code-csharp[CollectionView#OnButton](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionView/CSharp/Page1.xaml.cs#onbutton)]
 [!code-vb[CollectionView#OnButton](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionView/VisualBasic/Page1.xaml.vb#onbutton)]  
  
## <a name="see-also"></a>참고자료

- [데이터 바인딩 개요](data-binding-overview.md)
- [뷰의 데이터 정렬](how-to-sort-data-in-a-view.md)
- [뷰에서 데이터 필터링](how-to-filter-data-in-a-view.md)
- [XAML 데이터 정렬 및 그룹화](how-to-sort-and-group-data-using-a-view-in-xaml.md)
- [방법 항목](data-binding-how-to-topics.md)
