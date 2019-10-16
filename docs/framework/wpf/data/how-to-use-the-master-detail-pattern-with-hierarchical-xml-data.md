---
title: '방법: 계층적 XML 데이터에서 마스터-세부 정보 패턴 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [WPF], Master-Detail data paradigm
- Master-Detail data paradigm
ms.assetid: eb8dbdd8-5871-42bb-a16b-04e655fea677
ms.openlocfilehash: ba6c932f519ffa5c3c70ecb21eb9b5d08c40fb28
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61931757"
---
# <a name="how-to-use-the-master-detail-pattern-with-hierarchical-xml-data"></a>방법: 계층적 XML 데이터에서 마스터-세부 정보 패턴 사용
이 예제에 사용 하 여 마스터-세부 시나리오를 구현 하는 방법을 보여 줍니다 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 데이터입니다.  
  
## <a name="example"></a>예제  
 이 예제는 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 에서 설명 하는 예제 데이터 버전이 [계층적 데이터에 마스터-세부 패턴 사용](how-to-use-the-master-detail-pattern-with-hierarchical-data.md)합니다. 이 예제에서는 데이터가 파일에서 `League.xml`합니다. 참고 하는 방법 세 번째 <xref:System.Windows.Controls.ListBox> 컨트롤의 두 번째에서 선택 변경을 추적 <xref:System.Windows.Controls.ListBox> 바인딩하여 해당 <xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A> 속성입니다.  
  
 [!code-xaml[MasterDetailXml#HowTo1](~/samples/snippets/csharp/VS_Snippets_Wpf/MasterDetailXml/CS/Window1.xaml#howto1)]  
[!code-xaml[MasterDetailXml#HowTo2](~/samples/snippets/csharp/VS_Snippets_Wpf/MasterDetailXml/CS/Window1.xaml#howto2)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.HierarchicalDataTemplate>
- [방법 항목](data-binding-how-to-topics.md)
