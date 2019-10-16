---
title: '방법: INotifyPropertyChanged 인터페이스 구현'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- INotifyPropertyChanged interface [Windows Forms], implementing
ms.assetid: eac428af-b43b-46ac-80d9-1a5f88658725
ms.openlocfilehash: cfdfb22fd854a8f630243e0f612761c71cb778d8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61802039"
---
# <a name="how-to-implement-the-inotifypropertychanged-interface"></a>방법: INotifyPropertyChanged 인터페이스 구현
다음 코드 예제를 구현 하는 방법에 설명 합니다 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스입니다. Windows Forms 데이터 바인딩에 사용 되는 비즈니스 개체에서이 인터페이스를 구현 합니다. 구현 된 인터페이스 비즈니스 개체의 속성 변경 내용이 바인딩된 컨트롤에 통신 합니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[System.ComponentModel.IPropertyChangeExample#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.IPropertyChangeExample/CS/Form1.cs#1)]
 [!code-vb[System.ComponentModel.IPropertyChangeExample#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.IPropertyChangeExample/VB/Form1.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [방법: PropertyNameChanged 패턴 적용](how-to-apply-the-propertynamechanged-pattern.md)
- [Windows Forms 데이터 바인딩](windows-forms-data-binding.md)
- [방법: BindingSource와 INotifyPropertyChanged 인터페이스를 사용 하 여 변경 알림 발생](./controls/raise-change-notifications--bindingsource.md)
- [Windows Forms 데이터 바인딩의 변경 알림](change-notification-in-windows-forms-data-binding.md)
