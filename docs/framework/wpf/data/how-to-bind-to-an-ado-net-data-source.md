---
title: '방법: ADO.NET 데이터 소스 바인딩'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], binding to ADO.NET data sources
- ADO.NET data sources [WPF], binding to
- binding [WPF], to ADO.NET data sources
ms.assetid: a70c6d7b-7b38-4fdf-b655-4804db7c8315
ms.openlocfilehash: dbe34cba8f01320fbf37beea65ed95656e09395c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697135"
---
# <a name="how-to-bind-to-an-adonet-data-source"></a>방법: ADO.NET 데이터 소스 바인딩

이 예제에서는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.Controls.ListBox> 컨트롤을 ADO.NET `DataSet`에 바인딩하는 방법을 보여 줍니다.

## <a name="example"></a>예제

이 예에서는 `OleDbConnection` 개체를 사용하여 연결 문자열에 지정된 `Access MDB` 파일인 데이터 소스에 연결합니다. 연결이 설정되고 나면 `OleDbDataAdapter` 개체가 생성됩니다. @No__t-0 개체는 select 구조적 쿼리 언어 (SQL) 문을 실행 하 여 데이터베이스에서 레코드 집합을 검색 합니다. SQL 명령의 결과는-3 @no__t의 `Fill` 메서드를 호출 하 여 `DataSet`의 `DataTable`에 저장 됩니다. 이 예에서 `DataTable`은 `BookTable`로 이름이 지정됩니다. 그런 다음이 예에서는 <xref:System.Windows.Controls.ListBox>의 <xref:System.Windows.FrameworkElement.DataContext%2A> 속성을 `DataSet` 개체로 설정 합니다.

[!code-csharp[ADODataSet#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ADODataSet/CSharp/Window1.xaml.cs#1)]
[!code-vb[ADODataSet#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ADODataSet/VisualBasic/Window1.xaml.vb#1)]

그런 다음 <xref:System.Windows.Controls.ListBox>의 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 속성을 `DataSet`의 `BookTable`에 바인딩할 수 있습니다.

[!code-xaml[ADODataSet#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ADODataSet/CSharp/Window1.xaml#2)]

`BookItemTemplate`은 데이터가 표시 되는 방법을 정의 하는 @no__t 1입니다.

[!code-xaml[ADODataSet#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ADODataSet/CSharp/Window1.xaml#3)]

`IntColorConverter`는 `int`를 색상으로 변환합니다. 이 변환기를 사용 하면 `NumPages` 값이 350 보다 작은 경우 세 번째 <xref:System.Windows.Controls.TextBlock>의 @no__t 0 색이 녹색으로 표시 되 고 그렇지 않으면 빨간색으로 표시 됩니다. 변환기의 구현은 여기에 표시되지 않습니다.

## <a name="see-also"></a>참조

- <xref:System.Windows.Data.BindingListCollectionView>
- [데이터 바인딩 개요](data-binding-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
