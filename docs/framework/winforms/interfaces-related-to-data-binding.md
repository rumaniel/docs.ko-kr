---
title: 데이터 바인딩과 관련된 인터페이스
ms.date: 03/30/2017
helpviewer_keywords:
- data [Windows Forms], data-binding interfaces
- INotifyPropertyChanged interface
- IBindingListView interface
- IList interface [Windows Forms], Windows Forms data binding
- IBindingList interface [Windows Forms], Windows Forms data binding
- interfaces [Windows Forms], Windows Forms data binding
- IEditableObject interface [Windows Forms], Windows Forms data binding
- data binding [Windows Forms], interfaces
- IDataErrorInfo interface [Windows Forms], Windows Forms data binding
ms.assetid: 14e49a2e-3e46-47ca-b491-70d546333277
ms.openlocfilehash: 4e40f7ec1922cdf43e6a0b8f5734acaaeefbc514
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834584"
---
# <a name="interfaces-related-to-data-binding"></a>데이터 바인딩과 관련된 인터페이스

ADO.NET를 사용 하면 응용 프로그램의 바인딩 요구 사항과 작업 중인 데이터에 맞게 다양 한 데이터 구조를 만들 수 있습니다. Windows Forms에서 데이터를 제공하거나 사용하는 고유 클래스를 만들고 싶을 수도 있습니다. 이러한 개체는 기본 데이터 바인딩부터 디자인 타임 지원, 오류 확인, 변경 사항 알림, 심지어 데이터 자체에 적용된 변경 내용의 구조화된 롤백 지원에 이르기까지 다양한 수준의 복합 기능을 제공할 수 있습니다.

## <a name="consumers-of-data-binding-interfaces"></a>데이터 바인딩 인터페이스의 소비자

다음 섹션에서는 인터페이스 개체의 두 그룹에 대해 설명 합니다. 첫 번째 그룹에서는 데이터 소스 작성자에 의해 데이터 소스에 구현된 인터페이스를 나열합니다. 이러한 인터페이스는 데이터 소스 소비자가 사용하며, 이러한 소비자의 대부분은 Windows Forms 컨트롤 또는 구성 요소입니다. 두 번째 그룹에서는 구성 요소 작성자를 위해 설계된 인터페이스를 나열합니다. 구성 요소 작성자는 Windows Forms 데이터 바인딩 엔진에서 사용할 데이터 바인딩을 지원하는 구성 요소를 만들 때 이러한 인터페이스를 사용합니다. 양식과 연결된 클래스 내에 이러한 인터페이스를 구현하여 데이터 바인딩을 사용할 수 있습니다. 각 경우에 데이터와의 상호 작용이 가능한 인터페이스를 구현하는 클래스가 제공됩니다. Visual Studio RAD (신속한 응용 프로그램 개발) 데이터 디자인 환경 도구는이 기능을 이미 활용 하 고 있습니다.

### <a name="interfaces-for-implementation-by-data-source-authors"></a>데이터 소스 작성자가 구현할 수 있는 인터페이스

다음 인터페이스는 Windows Forms 컨트롤에서 사용할 수 있도록 설계되었습니다.

- <xref:System.Collections.IList> 인터페이스

  @No__t-0 인터페이스를 구현 하는 클래스는 <xref:System.Array>, <xref:System.Collections.ArrayList> 또는 <xref:System.Collections.CollectionBase> 일 수 있습니다. @No__t-0 형식의 항목에 대 한 인덱싱된 목록입니다. 인덱스의 첫 번째 항목에 따라 형식이 결정되기 때문에 이러한 목록에는 같은 형식이 포함되어 있어야 합니다. <xref:System.Collections.IList>은 런타임에만 바인딩에 사용할 수 있습니다.

  > [!NOTE]
  > Windows Forms 바인딩할 비즈니스 개체 목록을 만들려는 경우에는-0 @no__t를 사용 하는 것이 좋습니다. @No__t-0은 양방향 Windows Forms 데이터 바인딩에 필요한 기본 인터페이스를 구현 하는 확장 가능한 클래스입니다.

- <xref:System.ComponentModel.IBindingList> 인터페이스

  @No__t-0 인터페이스를 구현 하는 클래스는 훨씬 높은 수준의 데이터 바인딩 기능을 제공 합니다. 이 구현은 목록 자체가 변경된 경우(예: 목록 항목 개수의 증가/감소)뿐 아니라 목록 항목이 변경된 경우(예: 고객 목록의 세 번째 항목에서 주소 필드가 변경됨)에도 기본적인 정렬 기능과 변경 알림을 제공합니다. 변경 알림은 여러 컨트롤을 같은 데이터에 바인딩할 때 한 컨트롤의 데이터 변경을 다른 바인딩된 컨트롤에 전파하려는 경우에 중요합니다.

  > [!NOTE]
  > @No__t-1 속성을 통해 <xref:System.ComponentModel.IBindingList> 인터페이스에 대해 변경 알림을 사용 하도록 설정 합니다 .이 속성은 `true` 인 경우 목록이 변경 되었거나 목록의 항목이 변경 되었음을 나타내는 <xref:System.ComponentModel.IBindingList.ListChanged> 이벤트를 발생 시킵니다.

  변경 형식은 <xref:System.ComponentModel.ListChangedEventArgs> 매개 변수의 <xref:System.ComponentModel.ListChangedType> 속성으로 설명 됩니다. 그러므로 데이터 모델이 업데이트될 때마다 같은 데이터 소스에 바인딩된 다른 컨트롤과 같은 모든 종속 뷰도 업데이트됩니다. 그러나 목록에 포함 된 개체는 목록에서 <xref:System.ComponentModel.IBindingList.ListChanged> 이벤트를 발생 시킬 수 있도록 변경 될 때이를 알려야 합니다.

  > [!NOTE]
  > @No__t-0은 <xref:System.ComponentModel.IBindingList> 인터페이스의 제네릭 구현을 제공 합니다.

- <xref:System.ComponentModel.IBindingListView> 인터페이스

  @No__t-0 인터페이스를 구현 하는 클래스는 <xref:System.ComponentModel.IBindingList>의 구현에 대 한 모든 기능 뿐만 아니라 필터링 및 고급 정렬 기능을 제공 합니다. 이 구현은 문자열 기반 필터링 기능과 속성 설명자 방향 쌍을 사용한 여러 열 정렬 기능을 제공합니다.

- <xref:System.ComponentModel.IEditableObject> 인터페이스

  @No__t-0 인터페이스를 구현 하는 클래스를 사용 하면 개체에서 해당 개체에 대 한 변경 내용이 영구적으로 적용 되는 시기를 제어할 수 있습니다. 이 구현은 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>, <xref:System.ComponentModel.IEditableObject.EndEdit%2A> 및 <xref:System.ComponentModel.IEditableObject.CancelEdit%2A> 메서드를 사용 하 여 개체에 대 한 변경 내용을 롤백할 수 있습니다. 다음은 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>, <xref:System.ComponentModel.IEditableObject.EndEdit%2A> 및 @no__t 방법의 작동 방식에 대 한 간략 한 설명과 데이터 변경 내용에 대 한 변경 내용을 롤백할 수 있도록 서로 함께 작동 하는 방법입니다.

  - @No__t-0 메서드는 개체에 대 한 편집을 시작 함을 신호로 보냅니다. 이 인터페이스를 구현 하는 개체는 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> 메서드 호출 이후의 업데이트를 저장 해야 합니다 .이 경우 <xref:System.ComponentModel.IEditableObject.CancelEdit%2A> 메서드가 호출 되 면 업데이트를 삭제할 수 있습니다. 데이터 바인딩 Windows Forms에서 단일 편집 트랜잭션 범위 내에서 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>을 여러 번 호출할 수 있습니다 (예: <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>, <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>, <xref:System.ComponentModel.IEditableObject.EndEdit%2A>). @No__t-0의 구현은 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>이 이미 호출 되었는지 여부를 추적 하 고 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>에 대 한 후속 호출을 무시 해야 합니다. 이 메서드를 여러 번 호출할 수 있기 때문에 후속 호출에서 비파괴를 호출 하는 것이 중요 합니다. 즉, 이후의 @no__t 0 호출은 생성 된 업데이트를 제거 하거나 첫 번째 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> 호출에서 저장 된 데이터를 변경할 수 없습니다.

  - 개체가 현재 편집 모드에 있는 경우 <xref:System.ComponentModel.IEditableObject.EndEdit%2A> 메서드는 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>이 내부 개체에 호출 된 이후 변경 내용을 푸시합니다.

  - @No__t-0 메서드는 개체에 대 한 변경 내용을 모두 삭제 합니다.

  @No__t-0, <xref:System.ComponentModel.IEditableObject.EndEdit%2A> 및 @no__t 방법의 작동 방식에 대 한 자세한 내용은 [데이터를 데이터베이스에 다시 저장](/visualstudio/data-tools/save-data-back-to-the-database)을 참조 하세요.

  데이터 기능의이 트랜잭션 개념은 <xref:System.Windows.Forms.DataGridView> 컨트롤에서 사용 됩니다.

- <xref:System.ComponentModel.ICancelAddNew> 인터페이스

  @No__t-0 인터페이스를 구현 하는 클래스는 일반적으로 @no__t 1 인터페이스를 구현 하 고 <xref:System.ComponentModel.IBindingList.AddNew%2A> 메서드를 사용 하 여 추가 된 데이터 소스에 대 한 추가 작업을 롤백할 수 있습니다. 데이터 원본에서 <xref:System.ComponentModel.IBindingList> 인터페이스를 구현 하는 경우에는 <xref:System.ComponentModel.ICancelAddNew> 인터페이스도 구현 해야 합니다.

- <xref:System.ComponentModel.IDataErrorInfo> 인터페이스

  @No__t-0 인터페이스를 구현 하는 클래스를 통해 개체가 바인딩된 컨트롤에 사용자 지정 오류 정보를 제공할 수 있습니다.

  - @No__t-0 속성은 일반 오류 메시지 텍스트 (예: "오류가 발생 했습니다.")를 반환 합니다.

  - @No__t-0 속성은 열에서 특정 오류 메시지를 포함 하는 문자열을 반환 합니다 (예: "`State` 열의 값이 잘못 되었습니다.").

- <xref:System.Collections.IEnumerable> 인터페이스

  @No__t-0 인터페이스를 구현 하는 클래스는 일반적으로 ASP.NET에서 사용 됩니다. 이 인터페이스에 대 한 Windows Forms 지원은 <xref:System.Windows.Forms.BindingSource> 구성 요소를 통해서만 사용할 수 있습니다.

  > [!NOTE]
  > @No__t-0 구성 요소는 바인딩을 목적으로 모든 <xref:System.Collections.IEnumerable> 항목을 별도의 목록에 복사 합니다.

- <xref:System.ComponentModel.ITypedList> 인터페이스

  @No__t-0 인터페이스를 구현 하는 collections 클래스는 바인딩된 컨트롤에 노출 되는 속성 집합 및 순서를 제어 하는 기능을 제공 합니다.

  > [!NOTE]
  > @No__t-0 메서드를 구현 하 고 <xref:System.ComponentModel.PropertyDescriptor> 배열이 null이 아닌 경우 배열의 마지막 항목은 다른 항목 목록에 해당 하는 목록 속성을 설명 하는 속성 설명자가 됩니다.

- <xref:System.ComponentModel.ICustomTypeDescriptor> 인터페이스

  @No__t-0 인터페이스를 구현 하는 클래스는 자체에 대 한 동적 정보를 제공 합니다. 이 인터페이스는 <xref:System.ComponentModel.ITypedList>과 유사 하지만 목록 대신 개체에 사용 됩니다. 이 인터페이스는 <xref:System.Data.DataRowView>에서 기본 행의 스키마를 프로젝션 하는 데 사용 됩니다. @No__t-0의 간단한 구현은 <xref:System.ComponentModel.CustomTypeDescriptor> 클래스에서 제공 합니다.

  > [!NOTE]
  > @No__t-0을 구현 하는 형식에 대 한 디자인 타임 바인딩을 지원 하려면 형식이-1 @no__t 구현 하 고 폼의 인스턴스로 존재 해야 합니다.

- <xref:System.ComponentModel.IListSource> 인터페이스

  @No__t-0 인터페이스를 구현 하는 클래스는 목록에 없는 개체에 대 한 목록 기반 바인딩을 활성화 합니다. @No__t-1의 <xref:System.ComponentModel.IListSource.GetList%2A> 메서드는 <xref:System.Collections.IList>에서 상속 되지 않는 개체에서 바인딩할 수 있는 목록을 반환 하는 데 사용 됩니다. <xref:System.ComponentModel.IListSource> 사용 되는 <xref:System.Data.DataSet> 클래스입니다.

- <xref:System.ComponentModel.IRaiseItemChangedEvents> 인터페이스

  @No__t-0 인터페이스를 구현 하는 클래스는 <xref:System.ComponentModel.IBindingList> 인터페이스도 구현 하는 바인딩 가능한 목록입니다. 이 인터페이스는 형식이 <xref:System.ComponentModel.IRaiseItemChangedEvents.RaisesItemChangedEvents%2A> 속성을 통해 <xref:System.ComponentModel.ListChangedType.ItemChanged> 형식의 <xref:System.ComponentModel.IBindingList.ListChanged> 이벤트를 발생 시키는 지 여부를 나타내는 데 사용 됩니다.

  > [!NOTE]
  > 데이터 원본에서 이전에 설명한 이벤트 변환을 나열 하기 위해 속성을 제공 하 고 <xref:System.Windows.Forms.BindingSource> 구성 요소와 상호 작용 하는 경우 <xref:System.ComponentModel.IRaiseItemChangedEvents>을 구현 해야 합니다. 그렇지 않으면 <xref:System.Windows.Forms.BindingSource>은 이벤트 변환을 나열 하는 속성을 수행 하 여 성능이 저하 됩니다.

- <xref:System.ComponentModel.ISupportInitialize> 인터페이스

  @No__t-0 인터페이스를 구현 하는 구성 요소는 속성을 설정 하 고 공동 종속 속성을 초기화 하기 위해 일괄 처리 최적화의 장점을 활용 합니다. @No__t-0에는 두 가지 방법이 있습니다.

  - <xref:System.ComponentModel.ISupportInitialize.BeginInit%2A>은 개체 초기화가 시작 됨을 나타냅니다.

  - <xref:System.ComponentModel.ISupportInitialize.EndInit%2A>은 개체 초기화가 완료 됨을 나타냅니다.

- <xref:System.ComponentModel.ISupportInitializeNotification> 인터페이스

  @No__t-0 인터페이스를 구현 하는 구성 요소는 <xref:System.ComponentModel.ISupportInitialize> 인터페이스도 구현 합니다. 이 인터페이스를 사용 하면 초기화가 완료 되었음을 다른 <xref:System.ComponentModel.ISupportInitialize> 구성 요소에 알릴 수 있습니다. @No__t-0 인터페이스에는 두 개의 멤버가 포함 되어 있습니다.

  - <xref:System.ComponentModel.ISupportInitializeNotification.IsInitialized%2A>은 구성 요소가 초기화 되었는지 여부를 나타내는 `boolean` 값을 반환 합니다.

  - <xref:System.ComponentModel.ISupportInitialize.EndInit%2A>이 호출 @no__t 될 때 0이 발생 합니다.

- <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스

  이 인터페이스를 구현하는 클래스는 해당 속성 값이 변경될 때 이벤트를 발생시키는 형식입니다. 이 인터페이스는 각 컨트롤 속성에서 변경 이벤트를 갖는 패턴을 바꾸는 데 사용됩니다. @No__t-0에서 사용 하는 경우 비즈니스 개체는 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스를 구현 해야 하 고, BindingList @ no__t-21은 <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> 이벤트를 <xref:System.ComponentModel.ListChangedType.ItemChanged> 형식의 <xref:System.ComponentModel.BindingList%601.ListChanged> 이벤트로 변환 합니다.

  > [!NOTE]
  > 바인딩된 클라이언트와 데이터 소스 간의 바인딩에서 변경 알림이 발생 하도록 하려면 바인딩된 데이터 소스 형식이 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스 (기본 설정)를 구현 하거나 바인딩 형식에 대해 *propertyName*`Changed` 이벤트를 제공할 수 있어야 합니다. 둘 다 수행 해서는 안 됩니다.

### <a name="interfaces-for-implementation-by-component-authors"></a>구성 요소 작성자가 구현할 수 있는 인터페이스

다음 인터페이스는 Windows Forms 데이터 바인딩 엔진에서 사용됩니다.

- <xref:System.Windows.Forms.IBindableComponent> 인터페이스

  이 인터페이스를 구현하는 클래스는 컨트롤이 아닌 구성 요소이며 데이터 바인딩을 지원합니다. 이 클래스는이 인터페이스의 <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> 및 <xref:System.Windows.Forms.IBindableComponent.BindingContext%2A> 속성을 통해 구성 요소의 데이터 바인딩 및 바인딩 컨텍스트를 반환 합니다.

  > [!NOTE]
  > 구성 요소가 <xref:System.Windows.Forms.Control>에서 상속 하는 경우 <xref:System.Windows.Forms.IBindableComponent> 인터페이스를 구현할 필요가 없습니다.

- <xref:System.Windows.Forms.ICurrencyManagerProvider> 인터페이스

  @No__t-0 인터페이스를 구현 하는 클래스는 고유한 <xref:System.Windows.Forms.CurrencyManager>을 제공 하 여이 특정 구성 요소와 관련 된 바인딩을 관리 하는 구성 요소입니다. 사용자 지정 <xref:System.Windows.Forms.CurrencyManager>에 대 한 액세스는 <xref:System.Windows.Forms.ICurrencyManagerProvider.CurrencyManager%2A> 속성에 의해 제공 됩니다.

  > [!NOTE]
  > @No__t-0에서 상속 하는 클래스는 <xref:System.Windows.Forms.Control.BindingContext%2A> 속성을 통해 바인딩을 자동으로 관리 하므로 <xref:System.Windows.Forms.ICurrencyManagerProvider>를 구현 해야 하는 경우가 매우 드뭅니다.

## <a name="see-also"></a>참조

- [데이터 바인딩 및 Windows Forms](data-binding-and-windows-forms.md)
- [방법: Windows Form에 단순 바인딩된 컨트롤 만들기 @ no__t-0
- [Windows Forms 데이터 바인딩](windows-forms-data-binding.md)
