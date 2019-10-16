---
title: 데이터 바인딩 및 Windows Forms
ms.date: 03/30/2017
helpviewer_keywords:
- master-details lists
- data [Windows Forms], data binding
- reports [Windows Forms], Windows Forms
- lookup tables [Windows Forms], data binding
- data [Windows Forms], complex data binding
- data binding [Windows Forms], Windows Forms
- data [Windows Forms], simple data binding
- Windows Forms controls, data binding
- data-bound controls [Windows Forms], Windows Forms
ms.assetid: 419aac5e-819b-4aad-88b0-73a2f8c0bd27
ms.openlocfilehash: 240b68f901f819313fcae7aab0474abd5535c30d
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592313"
---
# <a name="data-binding-and-windows-forms"></a>데이터 바인딩 및 Windows Forms
Windows Forms에서는 기존의 데이터 소스뿐 아니라 데이터를 포함하는 거의 모든 구조에 바인딩할 수 있습니다. 런타임에 계산하거나 파일에서 읽거나 다른 컨트롤의 값에서 파생하는 값 배열에 바인딩할 수 있습니다.  
  
 또한 컨트롤의 속성을 데이터 소스에 바인딩할 수도 있습니다. 일반적인 데이터 바인딩에서는 대개 표시 속성(예: <xref:System.Windows.Forms.Control.Text%2A> 컨트롤의 <xref:System.Windows.Forms.TextBox> 속성)을 데이터 소스에 바인딩합니다. .NET Framework를 사용 하 여 바인딩을 통해 다른 속성을 설정 하는 옵션을 있어야 합니다. 바인딩을 사용하여 수행할 수 있는 작업은 다음과 같습니다.  
  
- 이미지 컨트롤의 그래픽 설정  
  
- 컨트롤 하나 이상의 배경색 설정  
  
- 컨트롤의 크기 설정  
  
 기본적으로 데이터 바인딩은 폼에 있는 컨트롤의 런타임 액세스 가능 속성을 자동으로 설정하는 방법입니다.  
  
## <a name="types-of-data-binding"></a>데이터 바인딩의 형식  
 Windows Forms는 단순 바인딩과 복합 바인딩의 두 가지 데이터 바인딩 형식을 사용할 수 있습니다. 각 바인딩 형식은 서로 다른 이점을 제공합니다.  
  
|데이터 바인딩 형식|설명|  
|--------------------------|-----------------|  
|단순 데이터 바인딩|컨트롤이 데이터 세트 테이블의 열 값과 같은 단일 데이터 요소에 바인딩하는 기능입니다. 이러한 형식의 바인딩은 일반적으로 <xref:System.Windows.Forms.TextBox> 컨트롤 또는 <xref:System.Windows.Forms.Label> 컨트롤과 같이 보통 단일 값만 표시하는 컨트롤에 사용됩니다. 실제로 컨트롤의 모든 속성은 데이터베이스의 필드에 바인딩할 수 있습니다. Visual Studio에서이 기능에 대해 폭넓게 지원이 됩니다.<br /><br /> 자세한 내용은 다음을 참조하세요.<br /><br /> -   [데이터 바인딩과 관련 된 인터페이스](interfaces-related-to-data-binding.md)<br />-   [방법: Windows Forms에서 데이터 탐색](how-to-navigate-data-in-windows-forms.md)<br />-   [방법: Windows Form에 단순 바인딩된 컨트롤 만들기](how-to-create-a-simple-bound-control-on-a-windows-form.md)|  
|복합 데이터 바인딩|둘 이상의 데이터 요소(일반적으로 데이터베이스 내 둘 이상의 레코드)에 바인딩하는 컨트롤의 기능입니다. 복합 바인딩은 목록 기반 바인딩이라고도 합니다. 복합 바인딩을 지원하는 컨트롤의 예로는 <xref:System.Windows.Forms.DataGridView>, <xref:System.Windows.Forms.ListBox> 및 <xref:System.Windows.Forms.ComboBox> 컨트롤이 있습니다. 복합 데이터 바인딩의 예제를 참조 하세요. [방법: Windows Forms ComboBox 또는 ListBox 컨트롤을 데이터에 바인딩할](./controls/how-to-bind-a-windows-forms-combobox-or-listbox-control-to-data.md)합니다.|  
  
## <a name="bindingsource-component"></a>BindingSource 구성 요소  
 Windows Forms에서는 데이터 바인딩을 간소화하기 위해 데이터 소스를 <xref:System.Windows.Forms.BindingSource> 구성 요소에 바인딩한 다음 컨트롤을 <xref:System.Windows.Forms.BindingSource>에 바인딩할 수 있습니다. 단순 또는 복합 바인딩 시나리오에서 <xref:System.Windows.Forms.BindingSource>를 사용할 수 있습니다. 두 경우 모두 <xref:System.Windows.Forms.BindingSource>는 데이터 소스와 바인딩되는 컨트롤 간의 매개 역할을 하며 변경 알림, 현재 항목 관리 및 기타 서비스를 제공합니다.  
  
## <a name="common-scenarios-that-employ-data-binding"></a>데이터 바인딩을 사용하는 일반적인 시나리오  
 거의 모든 상업용 애플리케이션에서는 대개 데이터 바인딩을 통해 특정 형식의 데이터 소스에서 읽은 정보를 사용합니다. 다음 목록에는 데이터 표시 및 조작 방법으로 데이터 바인딩을 사용하는 가장 일반적인 몇 가지 시나리오가 나와 있습니다.  
  
|시나리오|설명|  
|--------------|-----------------|  
|보고|보고서를 사용하면 데이터를 인쇄된 문서에 유동적으로 표시 및 요약할 수 있습니다. 일반적으로는 데이터 소스의 선택한 콘텐츠를 화면이나 프린터에 인쇄하는 보고서를 만듭니다. 일반적인 보고서에는 목록, 송장, 요약 등이 포함됩니다. 항목은 보통 목록의 열로 서식이 지정되며 각 목록 항목 아래에는 하위 항목이 구성되지만 데이터에 가장 적합한 레이아웃을 선택해야 합니다.|  
|데이터 입력|일반적으로는 데이터 입력 양식을 통해 많은 양의 관련 데이터를 입력하거나 사용자에게 정보를 표시합니다. 사용자는 텍스트 상자, 옵션 단추, 드롭다운 목록 및 확인란을 사용하여 정보를 입력하거나 항목을 선택할 수 있습니다. 그러면 정보가 전송되어 데이터베이스에 저장됩니다. 이 데이터베이스의 구조는 입력된 정보를 기반으로 합니다.|  
|마스터/세부 관계|마스터/세부 애플리케이션은 관련된 데이터를 확인하기 위한 하나의 형식입니다. 이 응용 프로그램에는 두 데이터 테이블이 관계로 연결됩니다. 기존의 비즈니스 예제에서는 "Customers" 테이블과 "Orders" 테이블 간의 관계가 고객과 해당 주문을 연결합니다. 두 개의 Windows Forms를 사용 하 여 마스터/세부 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 <xref:System.Windows.Forms.DataGridView> 컨트롤을 참조 하세요. [방법: 두 개의 Windows Forms DataGridView 컨트롤을 사용 하 여 마스터/세부 폼 만들기](./controls/create-a-master-detail-form-using-two-datagridviews.md)|  
|조회 테이블|또 다른 일반적인 데이터 표시/조작 시나리오는 테이블 조회입니다. <xref:System.Windows.Forms.ComboBox> 컨트롤은 대규모 데이터 표시의 일부분으로 데이터를 표시하고 조작하는 경우가 많습니다. 여기서 중요한 점은, <xref:System.Windows.Forms.ComboBox> 컨트롤에 표시되는 데이터와 데이터베이스에 기록되는 데이터가 다르다는 점입니다. 예를 들어 식료품점에서 구입할 수 있는 품목을 표시하는 <xref:System.Windows.Forms.ComboBox> 컨트롤을 사용하는 경우에는 빵, 우유, 계란 등의 제품 이름을 표시하는 경우가 많습니다. 그러나 데이터베이스 내의 정보를 쉽게 검색하고 데이터베이스를 표준화하기 위해 지정된 주문의 특정 품목 정보를 #501, #603 등의 품목 번호로 저장할 수 있습니다. 이처럼 폼에 있는 <xref:System.Windows.Forms.ComboBox> 컨트롤의 식료품 "이름"과 주문에 포함된 관련 항목 번호 간에는 암시적 연결이 설정됩니다. 그리고 이러한 연결이 테이블 조회의 핵심 요소입니다. 자세한 내용은 [방법: Windows Forms BindingSource 구성 요소를 사용 하 여 조회 테이블 만들기](./controls/how-to-create-a-lookup-table-with-the-windows-forms-bindingsource-component.md)합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Binding>
- [Windows Forms 데이터 바인딩](windows-forms-data-binding.md)
- [방법: 데이터 소스에 Windows Forms DataGrid 컨트롤 바인딩](./controls/how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)
- [BindingSource 구성 요소](./controls/bindingsource-component.md)
