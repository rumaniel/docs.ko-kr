---
title: '방법: 속성 변경 알림 구현'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- notifications of change [WPF]
- data binding [WPF], property change notifications
- change notifications [WPF]
- properties [WPF], change notifications
ms.assetid: 30b59d9e-8c3a-4349-aa82-4be837e841cf
ms.openlocfilehash: d37d468acc94470be8c2afdc495b40168932ec83
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61931445"
---
# <a name="how-to-implement-property-change-notification"></a>방법: 속성 변경 알림 구현
지원 하기 위해 <xref:System.Windows.Data.BindingMode.OneWay> 또는 <xref:System.Windows.Data.BindingMode.TwoWay> 바인딩 소스 (예를 들어 사용자가 폼을 편집할 때 자동으로 업데이트 미리 보기 창이), 동적 변경 사항을 자동으로 반영 하도록 바인딩 대상 속성을 사용 하도록 설정 하려면 바인딩 클래스 적절 한 속성 변경 알림을 제공 해야 합니다. 이 예제에는 구현 하는 클래스를 만드는 방법을 보여 줍니다 <xref:System.ComponentModel.INotifyPropertyChanged>합니다.  
  
## <a name="example"></a>예제  
 구현 <xref:System.ComponentModel.INotifyPropertyChanged> 선언 해야 합니다 <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> 이벤트 만들고를 `OnPropertyChanged` 메서드. 그런 다음 변경 알림이 필요한 각 속성이 업데이트될 때마다 `OnPropertyChanged`를 호출합니다.  
  
 [!code-csharp[SimpleBinding#PersonClass](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Person.cs#personclass)]
 [!code-vb[SimpleBinding#PersonClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Person.vb#personclass)]  
  
 예제를 보려면 `Person` 클래스를 사용 하 여를 지원할 수 있습니다 <xref:System.Windows.Data.BindingMode.TwoWay> 바인딩 참조 [TextBox 텍스트의 소스를 업데이트 하는 경우 제어](how-to-control-when-the-textbox-text-updates-the-source.md)입니다.  
  
## <a name="see-also"></a>참고자료

- [바인딩 소스 개요](binding-sources-overview.md)
- [데이터 바인딩 개요](data-binding-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
