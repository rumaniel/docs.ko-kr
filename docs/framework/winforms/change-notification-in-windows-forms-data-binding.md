---
title: Windows Forms 데이터 바인딩의 변경 알림
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, data binding
- Windows Forms, adding change notification for data binding
ms.assetid: b5b10f90-0585-41d9-a377-409835262a92
ms.openlocfilehash: b4a70f96ad256b22ce0d933a633475161160e5a4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665854"
---
# <a name="change-notification-in-windows-forms-data-binding"></a>Windows Forms 데이터 바인딩의 변경 알림
Windows Forms 데이터 바인딩의 가장 중요 한 개념 중 하나인 *변경 알림*합니다. 데이터 소스와 바인딩되는 컨트롤에 항상 최신 데이터를 갖도록 변경 알림 데이터 바인딩에 대 한 추가 해야 합니다. 구체적으로 바인딩된 컨트롤에 대 한 알림을 해당 데이터 원본에 대 한 변경 내용을 확인 하려는 하 고 데이터 소스 컨트롤의 바인딩된 속성에 대 한 변경 내용을 알립니다.  
  
 데이터 바인딩의 종류에 따라 변경 알림의 다양 한 종류가 있습니다.  
  
- 단순 바인딩 개체의 단일 인스턴스에서 단일 컨트롤 속성 바인딩되어 있습니다.  
  
- 목록 기반 바인딩을 목록에 있는 항목의 속성 또는 컨트롤 속성에 바인딩된 컨트롤 속성을 포함할 수 있는 개체의 목록에 바인딩됩니다.  
  
 또한 데이터 바인딩에 사용 하려는 Windows Forms 컨트롤을 만드는 경우 적용 해야 합니다는 *PropertyName*패턴 컨트롤을 컨트롤의 바인딩된 속성에 변경 내용이 전파 되도록 변경 합니다 데이터 원본입니다.  
  
## <a name="change-notification-for-simple-binding"></a>단순 바인딩에 대 한 변경 알림  
 단순 바인딩 이와 비슷하게 바인딩된 속성의 값이 변경 될 때 비즈니스 개체 변경 알림을 제공 해야 합니다. 노출 하 여이 수행할 수는 *PropertyName*비즈니스 개체를 사용 하 여 컨트롤 바인딩할 비즈니스 개체의 각 속성에 대 한 Changed 이벤트를 <xref:System.Windows.Forms.BindingSource> 또는 선호 되는 비즈니스 개체를 구현 하는 방법 합니다 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스 및 발생을 <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> 속성의 값 변경 시 이벤트입니다. 자세한 내용은 [방법: INotifyPropertyChanged 인터페이스를 구현](how-to-implement-the-inotifypropertychanged-interface.md)합니다. 구현 하는 개체를 사용 하는 경우는 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스를 필요가 없습니다 사용 하는 <xref:System.Windows.Forms.BindingSource> 개체를 컨트롤을 바인딩할 하지만 사용 하 여는 <xref:System.Windows.Forms.BindingSource> 것이 좋습니다.  
  
## <a name="change-notification-for-list-based-binding"></a>목록 기반 바인딩에 대 한 변경 알림  
 Windows Forms 속성 변경 (목록 항목 속성 값 변경)를 제공 하는 바인딩된 목록 및 목록 변경에 따라 달라 집니다 (항목을 삭제 하거나 목록에 추가)를 바인딩된 컨트롤에 대 한 정보입니다. 따라서 데이터 바인딩에 사용 되는 목록을 구현 해야 합니다는 <xref:System.ComponentModel.IBindingList>, 두 가지 유형의 변경 알림 제공 하는 합니다. 합니다 <xref:System.ComponentModel.BindingList%601> 의 제네릭 구현 <xref:System.ComponentModel.IBindingList> 및 Windows Forms 데이터 바인딩과 함께 사용 하도록 설계 되었습니다. 만들 수 있습니다는 <xref:System.ComponentModel.BindingList%601> 구현 하는 비즈니스 개체 형식을 포함 하는 <xref:System.ComponentModel.INotifyPropertyChanged> 목록에서 자동으로 변환 하 고는 <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> 이벤트를 <xref:System.ComponentModel.IBindingList.ListChanged> 이벤트입니다. 바인딩된 목록의 없는 경우는 <xref:System.ComponentModel.IBindingList>, 개체 목록을 사용 하 여 Windows Forms 컨트롤에 바인딩해야 합니다는 <xref:System.Windows.Forms.BindingSource> 구성 요소입니다. 합니다 <xref:System.Windows.Forms.BindingSource> 구성 요소와 비슷한 속성 목록 변환 하면는 <xref:System.ComponentModel.BindingList%601>합니다. 자세한 내용은 [방법: BindingSource와 INotifyPropertyChanged 인터페이스를 사용 하 여 변경 알림 발생](./controls/raise-change-notifications--bindingsource.md)합니다.  
  
## <a name="change-notification-for-custom-controls"></a>사용자 지정 컨트롤에 대 한 변경 알림  
 마지막으로, 컨트롤에서 노출 해야 합니다는 *PropertyName*Changed 이벤트 데이터에 바인딩되도록 디자인 된 각 속성에 대 한 합니다. 컨트롤 속성에 변경 내용은 바인딩된 데이터 원본에 전파 됩니다. 자세한 내용은 [방법: PropertyNameChanged 패턴 적용](how-to-apply-the-propertynamechanged-pattern.md)  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.BindingSource>
- <xref:System.ComponentModel.INotifyPropertyChanged>
- <xref:System.ComponentModel.BindingList%601>
- [Windows Forms 데이터 바인딩](windows-forms-data-binding.md)
- [Windows Forms에서 지원하는 데이터 소스](data-sources-supported-by-windows-forms.md)
- [데이터 바인딩 및 Windows Forms](data-binding-and-windows-forms.md)
