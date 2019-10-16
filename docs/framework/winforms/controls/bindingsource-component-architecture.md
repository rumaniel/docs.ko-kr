---
title: BindingSource 구성 요소 아키텍처
ms.date: 03/30/2017
helpviewer_keywords:
- BindingSource component [Windows Forms], architecture
- Windows Forms, data binding
- BindingSource component [Windows Forms], about BindingSource component
- data binding [Windows Forms], BindingSource component
ms.assetid: 7bc69c90-8a11-48b1-9336-3adab5b41591
ms.openlocfilehash: 54a23ba899ceb05701fe3580aefbb723c6b3f0fd
ms.sourcegitcommit: 30a83efb57c468da74e9e218de26cf88d3254597
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2019
ms.locfileid: "68364411"
---
# <a name="bindingsource-component-architecture"></a>BindingSource 구성 요소 아키텍처
<xref:System.Windows.Forms.BindingSource> 구성 요소를 사용 하 여 모든 Windows Forms 컨트롤을 데이터 원본에 전체적으로 바인딩할 수 있습니다.  
  
 구성 <xref:System.Windows.Forms.BindingSource> 요소는 데이터 소스에 컨트롤을 바인딩하는 프로세스를 간소화 하 고 기존 데이터 바인딩에 비해 다음과 같은 이점을 제공 합니다.  
  
- 비즈니스 개체에 대 한 디자인 타임 바인딩을 활성화 합니다.  
  
- 디자인 <xref:System.Windows.Forms.CurrencyManager> 타임에 기능 <xref:System.Windows.Forms.CurrencyManager> 을 캡슐화 하 고 이벤트를 노출 합니다.  
  
- 기본적으로 목록 변경 알림을 지원 하지 <xref:System.ComponentModel.IBindingList> 않는 데이터 원본에 대 한 목록 변경 알림을 제공 하 여 인터페이스를 지 원하는 목록 만들기를 간소화 합니다.  
  
- <xref:System.ComponentModel.IBindingList.AddNew%2A?displayProperty=nameWithType> 메서드에 대 한 확장성 지점을 제공 합니다.  
  
- 데이터 소스와 컨트롤 간의 간접 참조 수준을 제공 합니다. 이 간접 참조는 런타임에 데이터 소스가 변경 될 때 중요 합니다.  
  
- 다른 데이터 관련 Windows Forms 컨트롤, 특히 <xref:System.Windows.Forms.BindingNavigator> <xref:System.Windows.Forms.DataGridView> 및 컨트롤과 상호 운용 합니다.  
  
 이러한 이유로 <xref:System.Windows.Forms.BindingSource> 구성 요소는 Windows Forms 컨트롤을 데이터 원본에 바인딩하는 데 선호 되는 방법입니다.  
  
## <a name="bindingsource-features"></a>BindingSource 기능  
 구성 <xref:System.Windows.Forms.BindingSource> 요소는 컨트롤을 데이터에 바인딩하기 위한 여러 기능을 제공 합니다. 이러한 기능을 사용 하면 코드를 거의 사용 하지 않고 대부분의 데이터 바인딩 시나리오를 구현할 수 있습니다.  
  
 구성 <xref:System.Windows.Forms.BindingSource> 요소는 다양 한 종류의 데이터 원본에 액세스 하기 위한 일관 된 인터페이스를 제공 하 여이를 수행 합니다. 즉, 모든 형식에 바인딩하는 것과 동일한 절차를 사용 합니다. 예를 들어 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 속성 <xref:System.Data.DataSet> 을 또는 비즈니스 개체에 연결할 수 있으며, 두 경우 모두 동일한 속성, 메서드 및 이벤트 집합을 사용 하 여 데이터 소스를 조작할 수 있습니다.  
  
 <xref:System.Windows.Forms.BindingSource> 구성 요소에서 제공 하는 일관 된 인터페이스를 통해 데이터를 컨트롤에 바인딩하는 프로세스를 크게 간소화할 수 있습니다. 변경 알림을 제공 하는 데이터 원본 형식의 경우 구성 요소 <xref:System.Windows.Forms.BindingSource> 는 컨트롤과 데이터 소스 간의 변경 내용을 자동으로 전달 합니다. 변경 알림을 제공 하지 않는 데이터 원본 유형의 경우 변경 알림을 발생 시킬 수 있는 이벤트가 제공 됩니다. 다음 목록에서는 <xref:System.Windows.Forms.BindingSource> 구성 요소에서 지 원하는 기능을 보여 줍니다.  
  
- 간접 참조.  
  
- 통화 관리.  
  
- 데이터 원본을 목록으로 표시 합니다.  
  
- <xref:System.Windows.Forms.BindingSource><xref:System.ComponentModel.IBindingList>로 서  
  
- 사용자 지정 항목을 만듭니다.  
  
- 트랜잭션 항목을 만듭니다.  
  
- <xref:System.Collections.IEnumerable>지원은.  
  
- 디자인 타임 지원.  
  
- 정적 <xref:System.Windows.Forms.ListBindingHelper> 메서드.  
  
- <xref:System.ComponentModel.IBindingListView> 인터페이스를 사용 하 여 정렬 및 필터링  
  
- 와의 <xref:System.Windows.Forms.BindingNavigator>통합  
  
### <a name="indirection"></a>간접 참조  
 구성 <xref:System.Windows.Forms.BindingSource> 요소는 컨트롤과 데이터 소스 간의 간접 참조 수준을 제공 합니다. 컨트롤을 데이터 소스에 직접 바인딩하는 대신 컨트롤 <xref:System.Windows.Forms.BindingSource>을에 바인딩한 다음 <xref:System.Windows.Forms.BindingSource> 구성 요소의 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 속성에 데이터 소스를 연결 합니다.  
  
 이 수준의 간접 참조를 사용 하 여 컨트롤 바인딩을 다시 설정 하지 않고 데이터 소스를 변경할 수 있습니다. 이렇게 하면 다음과 같은 기능을 제공 합니다.  
  
- 현재 컨트롤 바인딩을 유지 <xref:System.Windows.Forms.BindingSource> 하면서를 다른 데이터 소스에 연결할 수 있습니다.  
  
- 데이터 소스의 항목을 변경 하 고 바인딩된 컨트롤을 알릴 수 있습니다. 자세한 내용은 [방법: BindingSource](reflect-data-source-updates-in-a-wf-control-with-the-bindingsource.md)를 사용 하 여 Windows Forms 컨트롤의 데이터 소스 업데이트를 반영 합니다.  
  
- 메모리의 개체 <xref:System.Type> 대신에 바인딩할 수 있습니다. 자세한 내용은 [방법: Windows Forms 컨트롤을 형식](how-to-bind-a-windows-forms-control-to-a-type.md)에 바인딩합니다. 그런 다음 런타임에 개체에 바인딩할 수 있습니다.  
  
### <a name="currency-management"></a>통화 관리  
 구성 <xref:System.Windows.Forms.BindingSource> 요소는 인터페이스 <xref:System.Windows.Forms.ICurrencyManagerProvider> 를 구현 하 여 사용자의 통화 관리를 처리 합니다. 인터페이스를 사용 하면 동일한 <xref:System.Windows.Forms.BindingSource> <xref:System.Windows.Forms.BindingSource> 에바인딩된다른의통화관리자와함께의통화관리자에도액세스할수있습니다.<xref:System.Windows.Forms.BindingSource.DataMember%2A> <xref:System.Windows.Forms.ICurrencyManagerProvider>  
  
 구성 <xref:System.Windows.Forms.BindingSource> 요소는 <xref:System.Windows.Forms.CurrencyManager> 기능을 캡슐화 하 고 가장 <xref:System.Windows.Forms.CurrencyManager> 일반적인 속성 및 이벤트를 노출 합니다. 다음 표에서는 통화 관리와 관련 된 일부 구성원에 대해 설명 합니다.  
  
 <xref:System.Windows.Forms.ICurrencyManagerProvider.CurrencyManager%2A> 속성  
 와 연결 된 현재 위치 관리자를 <xref:System.Windows.Forms.BindingSource>가져옵니다.  
  
 <xref:System.Windows.Forms.ICurrencyManagerProvider.GetRelatedCurrencyManager%2A> 메서드  
 지정 된 데이터 멤버 <xref:System.Windows.Forms.BindingSource> 에 바인딩된 다른가 있으면 해당 통화 관리자를 가져옵니다.  
  
 <xref:System.Windows.Forms.BindingSource.Current%2A> 속성  
 데이터 소스의 현재 항목을 가져옵니다.  
  
 <xref:System.Windows.Forms.BindingSource.Position%2A> 속성  
 내부 목록에서 현재 위치를 가져오거나 설정합니다.  
  
 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 메서드  
 내부 데이터 소스에 보류 중인 변경 내용을 적용합니다.  
  
 <xref:System.Windows.Forms.BindingSource.CancelEdit%2A> 메서드  
 현재 편집 작업을 취소합니다.  
  
### <a name="data-source-as-a-list"></a>데이터 원본을 목록으로  
 구성 <xref:System.Windows.Forms.BindingSource> 요소는 <xref:System.ComponentModel.IBindingListView> 및<xref:System.ComponentModel.ITypedList> 인터페이스를 구현 합니다. 이 구현에서는 외부 저장소 없이 <xref:System.Windows.Forms.BindingSource> 구성 요소 자체를 데이터 원본으로 사용할 수 있습니다.  
  
 <xref:System.Windows.Forms.BindingSource> 구성 요소가 데이터 원본에 연결 된 경우 데이터 소스를 목록으로 노출 합니다.  
  
 속성 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 은 여러 데이터 원본으로 설정할 수 있습니다. 여기에는 형식, 개체 및 형식 목록이 포함 됩니다. 결과 데이터 소스 목록으로 노출 됩니다. 다음 표에서 일부 일반적인 데이터 원본 및 목록 계산 결과 보여 줍니다.  
  
|데이터 원본 속성|목록 결과|  
|-------------------------|------------------|  
|null 참조(Visual Basic의 경우 `Nothing`)|빈 <xref:System.ComponentModel.IBindingList> 개체입니다. 추가 된 항목의 형식으로 목록을 설정 항목을 추가 합니다.|  
|집합을 사용 하`Nothing` <xref:System.Windows.Forms.BindingSource.DataMember%2A> 는 null 참조 (Visual Basic)|지원 되지 않음 가 <xref:System.ArgumentException>발생 합니다.|  
|목록이 아닌 형식 또는 "T" 형식의 개체|"T <xref:System.ComponentModel.IBindingList> " 형식의 빈입니다.|  
|배열 인스턴스|배열 요소를 포함 하는입니다. <xref:System.ComponentModel.IBindingList>|  
|<xref:System.Collections.IEnumerable> 인스턴스|항목 <xref:System.ComponentModel.IBindingList> 을<xref:System.Collections.IEnumerable> 포함 하는입니다.|  
|"T" 형식을 포함 하는 인스턴스 목록|"T" 형식이 포함 된 인스턴스입니다.<xref:System.ComponentModel.IBindingList>|  
  
 또한, <xref:System.Windows.Forms.BindingSource.DataSource%2A> <xref:System.ComponentModel.IListSource> <xref:System.Windows.Forms.BindingSource> 및 와같은다른목록형식으로를설정할수있으며,에서적절하게처리합니다.<xref:System.ComponentModel.ITypedList> 이 경우 목록에 포함 된 형식에는 매개 변수가 없는 생성자가 있어야 합니다.  
  
### <a name="bindingsource-as-an-ibindinglist"></a>IBindingList로 BindingSource  
 구성 <xref:System.Windows.Forms.BindingSource> 요소는 내부 데이터를 <xref:System.ComponentModel.IBindingList>로 액세스 하 고 조작 하기 위한 멤버를 제공 합니다. 다음 표에서는 이러한 멤버 중 일부에 대해 설명 합니다.  
  
|멤버|Description|  
|------------|-----------------|  
|<xref:System.Windows.Forms.BindingSource.List%2A> 속성|<xref:System.Windows.Forms.BindingSource.DataSource%2A> 또는<xref:System.Windows.Forms.BindingSource.DataMember%2A> 속성을 평가한 결과로 생성 되는 목록을 가져옵니다.|  
|<xref:System.Windows.Forms.BindingSource.AddNew%2A> 메서드|내부 목록에 새 항목을 추가합니다. 인터페이스를 <xref:System.ComponentModel.IBindingList> 구현 하 고 항목 추가 (즉 <xref:System.Windows.Forms.BindingSource.AllowNew%2A> , 속성이로 `true`설정 됨)를 허용 하는 데이터 원본에 적용 됩니다.|  
  
### <a name="custom-item-creation"></a>사용자 지정 항목 만들기  
 <xref:System.Windows.Forms.BindingSource.AddingNew> 이벤트를 처리 하 여 고유한 항목 생성 논리를 제공할 수 있습니다. 이 <xref:System.Windows.Forms.BindingSource.AddingNew> 이벤트는에 새 개체가 추가 <xref:System.Windows.Forms.BindingSource>되기 전에 발생 합니다. 이 이벤트는 <xref:System.Windows.Forms.BindingSource.AddNew%2A> 메서드를 호출한 후 새 항목이 기본 목록에 추가 되기 전에 발생 합니다. 이 이벤트를 처리 하 여 <xref:System.Windows.Forms.BindingSource> 클래스에서 파생 하지 않고 사용자 지정 항목 만들기 동작을 제공할 수 있습니다. 자세한 내용은 [방법: Windows Forms BindingSource](how-to-customize-item-addition-with-the-windows-forms-bindingsource.md)를 사용 하 여 항목 추가를 사용자 지정 합니다.  
  
### <a name="transactional-item-creation"></a>트랜잭션 항목 만들기  
 구성 요소는 트랜잭션 <xref:System.ComponentModel.ICancelAddNew> 항목을 만들 수 있도록 하는 인터페이스를 구현 합니다. <xref:System.Windows.Forms.BindingSource> 에 대 <xref:System.Windows.Forms.BindingSource.AddNew%2A>한 호출을 사용 하 여 새 항목을 만든 후에는 다음과 같은 방법으로 되었으면를 커밋하거나 롤백할 수 있습니다.  
  
- <xref:System.ComponentModel.ICancelAddNew.EndNew%2A> 메서드를 명시적으로 보류 중인 추가 커밋합니다.  
  
- 삽입, 제거 또는 이동과 같은 다른 수집 작업을 수행 하면 보류 중인 추가 작업을 암시적으로 커밋합니다.  
  
- 메서드가 <xref:System.ComponentModel.ICancelAddNew.CancelNew%2A> 아직 커밋되지 않은 경우 메서드는 보류 중인 추가를 롤백합니다.  
  
### <a name="ienumerable-support"></a>IEnumerable 지원  
 구성 <xref:System.Windows.Forms.BindingSource> 요소는 데이터 소스에 <xref:System.Collections.IEnumerable> 컨트롤을 바인딩할 수 있도록 합니다. 이 구성 요소를 사용 하 여와 <xref:System.Data.SqlClient.SqlDataReader?displayProperty=nameWithType>같은 데이터 소스에 바인딩할 수 있습니다.  
  
 <xref:System.Windows.Forms.BindingSource> <xref:System.Windows.Forms.BindingSource> 데이터소스가<xref:System.ComponentModel.IBindingList> 구성 요소에 할당 되 면는를 <xref:System.Collections.IEnumerable> 만들고 데이터 원본의 내용을 목록에 추가 합니다. <xref:System.Collections.IEnumerable>  
  
### <a name="design-time-support"></a>디자인 타임 지원  
 팩터리 클래스에서 만든 개체 또는 웹 서비스에서 반환 된 개체와 같이 디자인 타임에 일부 개체 유형을 만들 수 없습니다. 컨트롤을 바인딩할 수 있는 메모리에 개체가 없더라도 디자인 타임에 컨트롤을 이러한 형식에 바인딩해야 하는 경우도 있습니다. 예를 들어 사용자 지정 형식의 공용 속성의 이름으로 <xref:System.Windows.Forms.DataGridView> 컨트롤의 열 머리글에 레이블을 지정 해야 할 수 있습니다.  
  
 이 시나리오를 지원 하기 위해 <xref:System.Windows.Forms.BindingSource> 구성 요소는에 대 <xref:System.Type>한 바인딩을 지원 합니다. 를 <xref:System.Type> 속성<xref:System.Windows.Forms.BindingSource.DataSource%2A> <xref:System.ComponentModel.BindingList%601> 에 할당 하면 구성요소가<xref:System.Type> 빈 항목을 만듭니다. <xref:System.Windows.Forms.BindingSource> 이후에 <xref:System.Windows.Forms.BindingSource> 구성 요소에 바인딩하는 모든 컨트롤은 디자인 타임 또는 런타임에 형식의 속성이 나 스키마가 있는지에 대 한 경고를 받습니다. 자세한 내용은 [방법: Windows Forms 컨트롤을 형식](how-to-bind-a-windows-forms-control-to-a-type.md)에 바인딩합니다.  
  
### <a name="static-listbindinghelper-methods"></a>정적 ListBindingHelper 메서드  
 <xref:System.Windows.Forms.BindingContext?displayProperty=nameWithType>, 및형식은<xref:System.Windows.Forms.BindingSource> 모두 공통논리`DataSource` 를 공유 하 여 쌍에서`DataMember` 목록을생성합니다./ <xref:System.Windows.Forms.CurrencyManager?displayProperty=nameWithType> 또한이 일반적인 논리는 다음과 같은 `static` 방법으로 컨트롤 작성자 및 기타 타사에서 사용 하기 위해 공개적으로 노출 됩니다.  
  
- <xref:System.Windows.Forms.ListBindingHelper.GetListItemProperties%2A>  
  
- <xref:System.Windows.Forms.ListBindingHelper.GetList%2A>.  
  
- <xref:System.Windows.Forms.ListBindingHelper.GetListName%2A>  
  
- <xref:System.Windows.Forms.ListBindingHelper.GetListItemType%2A>  
  
### <a name="sorting-and-filtering-with-the-ibindinglistview-interface"></a>IBindingListView 인터페이스를 사용 하 여 정렬 및 필터링  
 구성 요소는 인터페이스 <xref:System.ComponentModel.IBindingListView> 를 구현 합니다 .이 <xref:System.ComponentModel.IBindingList> 인터페이스는 인터페이스를 확장 합니다. <xref:System.Windows.Forms.BindingSource> 는 <xref:System.ComponentModel.IBindingList> 단일 열 정렬을 제공 하 고 <xref:System.ComponentModel.IBindingListView> 는 고급 정렬 및 필터링 기능을 제공 합니다. 데이터 <xref:System.ComponentModel.IBindingListView>소스가 이러한 인터페이스 중 하나를 구현 하는 경우를 사용 하 여 데이터 소스의 항목을 정렬 하 고 필터링 할 수 있습니다. 구성 <xref:System.Windows.Forms.BindingSource> 요소는 이러한 멤버의 참조 구현을 제공 하지 않습니다. 대신 호출은 기본 목록으로 전달 됩니다.  
  
 다음 표에서는 정렬 및 필터링에 사용 하는 속성에 대해 설명 합니다.  
  
|멤버|Description|  
|------------|-----------------|  
|<xref:System.Windows.Forms.BindingSource.Filter%2A> 속성|데이터 소스가 <xref:System.ComponentModel.IBindingListView>인 경우 표시할 행을 필터링하는 데 사용하는 식을 가져오거나 설정합니다.|  
|<xref:System.Windows.Forms.BindingSource.Sort%2A> 속성|데이터 소스가 <xref:System.ComponentModel.IBindingList>인 경우 정렬에 사용되는 열 이름과 정렬 순서 정보를 가져오거나 설정합니다.<br /><br /> 또는<br /><br /> 데이터 소스가이 <xref:System.ComponentModel.IBindingListView> 고 고급 정렬을 지 원하는 경우 정렬 및 정렬 순서에 사용 되는 여러 열 이름을 가져옵니다.|  
  
### <a name="integration-with-bindingnavigator"></a>BindingNavigator와 통합  
 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용 하 여 Windows Forms 컨트롤을 데이터 소스에 바인딩할 수 있지만 컨트롤은 <xref:System.Windows.Forms.BindingNavigator> <xref:System.Windows.Forms.BindingSource> 구성 요소와 함께 작동 하도록 설계 되었습니다. 컨트롤 <xref:System.Windows.Forms.BindingNavigator> 은 구성 요소의 현재 항목을 <xref:System.Windows.Forms.BindingSource> 제어 하기 위한 사용자 인터페이스를 제공 합니다. 기본적으로 컨트롤은 <xref:System.Windows.Forms.BindingNavigator> <xref:System.Windows.Forms.BindingSource> 구성 요소의 탐색 메서드에 해당 하는 단추를 제공 합니다. 자세한 내용은 [방법: Windows Forms BindingNavigator 컨트롤](how-to-navigate-data-with-the-windows-forms-bindingnavigator-control.md)을 사용 하 여 데이터를 탐색 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.BindingSource>
- <xref:System.Windows.Forms.BindingNavigator>
- [BindingSource 구성 요소 개요](bindingsource-component-overview.md)
- [BindingNavigator 컨트롤](bindingnavigator-control-windows-forms.md)
- [Windows Forms 데이터 바인딩](../windows-forms-data-binding.md)
- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
- [방법: Windows Forms 컨트롤을 형식에 바인딩](how-to-bind-a-windows-forms-control-to-a-type.md)
- [방법: BindingSource를 사용 하 여 Windows Forms 컨트롤의 데이터 소스 업데이트 반영](reflect-data-source-updates-in-a-wf-control-with-the-bindingsource.md)
