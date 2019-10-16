---
title: '방법: Windows Forms BindingSource 구성 요소를 사용하여 조회 테이블 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- lookup tables
- tables [Windows Forms], creating lookup tables
- BindingSource component [Windows Forms], creating a lookup table
- BindingSource component [Windows Forms], examples
ms.assetid: 622fce80-879d-44be-abbf-8350ec22ca2b
ms.openlocfilehash: 33b9e4e98a8a3f8c0d5dd6433ebbf15c049b608e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64643069"
---
# <a name="how-to-create-a-lookup-table-with-the-windows-forms-bindingsource-component"></a>방법: Windows Forms BindingSource 구성 요소를 사용하여 조회 테이블 만들기
조회 테이블은 관련 테이블의 레코드에서 데이터를 표시하는 열이 포함된 데이터 테이블입니다. 다음 절차에서는 <xref:System.Windows.Forms.ComboBox> 컨트롤을 사용하여 부모에서 자식 테이블로의 외래 키 관계로 필드를 표시합니다.  
  
 이러한 두 테이블과 해당 관계를 쉽게 표시하기 위해 아래의 부모 및 자식 테이블 예제를 사용합니다.  
  
 CustomersTable(부모 테이블)  
  
|CustomerID|CustomerName|  
|----------------|------------------|  
|712|Paul Koch|  
|713|Tamara Johnston|  
  
 OrdersTable(자식 테이블)  
  
|OrderID|OrderDate|CustomerID|  
|-------------|---------------|----------------|  
|903|2004년 2월 12일|712|  
|904|2004년 2월 13일|713|  
  
 이 시나리오의 테이블 중 하나인 CustomersTable에는 표시 및 저장할 실제 정보가 저장됩니다. 그러나 여기서는 공간 절약을 위해 명확성에 도움이 되는 일부 데이터를 제외했습니다. 또 하나의 테이블인 OrdersTables에는 주문 날짜 및 주문 ID에 해당하는 고객 ID 번호에 대한 표시 관련 정보만 포함됩니다. 고객 이름은 언급되지 않습니다.  
  
 조회 테이블을 만들기 위해 [ComboBox 컨트롤](combobox-control-windows-forms.md) 컨트롤에는 4가지 주요 속성이 설정됩니다.  
  
- <xref:System.Windows.Forms.ComboBox.DataSource%2A> 속성은 테이블 이름을 포함합니다.  
  
- <xref:System.Windows.Forms.ListControl.DisplayMember%2A> 속성은 컨트롤 텍스트(고객 이름)에 대해 표시할 해당 테이블의 데이터 열을 포함합니다.  
  
- <xref:System.Windows.Forms.ListControl.ValueMember%2A> 속성은 저장된 정보(부모 테이블의 ID 번호)가 포함된 해당 테이블의 데이터 열을 포함합니다.  
  
- <xref:System.Windows.Forms.ListControl.SelectedValue%2A> 속성은 <xref:System.Windows.Forms.ListControl.ValueMember%2A>를 기준으로 자식 테이블에 대한 조회 값을 제공합니다.  
  
 아래 절차에서는 폼을 조회 테이블로 배치하고 해당 폼의 컨트롤에 데이터를 바인딩하는 방법을 보여줍니다. 이 절차를 올바르게 완료하려면 위에서 설명한 것처럼 외래 키 관계가 적용된 부모 및 자식 테이블을 포함하는 데이터 소스가 있어야 합니다.  
  
### <a name="to-create-the-user-interface"></a>사용자 인터페이스를 만들려면  
  
1. **도구 상자**를 끌어를 <xref:System.Windows.Forms.ComboBox> 컨트롤을 폼으로 합니다.  
  
     이 컨트롤에는 부모 테이블의 열이 표시됩니다.  
  
2. 다른 컨트롤을 끌어 자식 테이블의 세부 정보를 표시합니다. 테이블의 데이터 형식에 맞는 컨트롤을 선택해야 합니다. 자세한 내용은 [기능별 Windows Forms 컨트롤](windows-forms-controls-by-function.md)을 참조하세요.  
  
3. <xref:System.Windows.Forms.BindingNavigator> 컨트롤을 폼으로 끌어 옵니다. 그러면 자식 테이블의 데이터를 탐색할 수 있습니다.  
  
### <a name="to-connect-to-the-data-and-bind-it-to-controls"></a>데이터에 연결하여 컨트롤에 데이터를 바인딩하려면  
  
1. <xref:System.Windows.Forms.ComboBox>를 선택하고 스마트 작업 문자 모양을 클릭하여 스마트 작업 대화 상자를 표시합니다.  
  
2. **데이터 바인딩된 항목 사용**을 선택합니다.  
  
3. **데이터 소스** 드롭다운 상자 옆의 화살표를 클릭합니다. 프로젝트 또는 폼에 대해 데이터 소스를 이전에 구성한 경우 해당 데이터 소스가 표시됩니다. 표시되지 않으면 다음 단계를 완료합니다. 이 예에서는 Northwind 샘플 데이터베이스의 Customers 및 Orders 테이블을 사용하며 괄호로 묶은 부분에서 이러한 테이블을 참조합니다.  
  
    1. **프로젝트 데이터 소스 추가**를 클릭하여 데이터에 연결한 다음 데이터 소스를 만듭니다.  
  
    2. **데이터 소스 구성 마법사** 시작 페이지에서 **다음**을 클릭합니다.  
  
    3. **데이터 소스 형식 선택** 페이지에서 **데이터베이스**를 선택합니다.  
  
    4. **데이터 연결 선택** 페이지의 사용 가능한 연결 목록에서 데이터 연결을 선택합니다. 원하는 데이터 연결을 사용할 수 없으면 **새 연결**을 선택하여 새 데이터 연결을 만듭니다.  
  
    5. **예, 연결을 저장합니다.** 를 클릭하여 응용 프로그램 구성 파일에 연결 문자열을 저장합니다.  
  
    6. 애플리케이션에 바인딩할 데이터베이스 개체를 선택합니다. 여기서는 외래 키 관계가 적용된 부모 테이블과 자식 테이블(예: Customers 및 Orders)을 선택합니다.  
  
    7. 원하는 경우 기본 데이터 세트 이름을 바꿉니다.  
  
    8. **마침**을 클릭합니다.  
  
4. **구성원 표시** 드롭다운 상자에서 콤보 상자에 표시할 ContactName 등의 열 이름을 선택합니다.  
  
5. **값 구성원** 드롭다운 상자에서 자식 테이블에서 조회 작업을 수행할 CustomerID 등의 열을 선택합니다.  
  
6. **선택한 값** 드롭다운 상자에서 **프로젝트 데이터 소스**로 이동한 다음 부모 및 자식 테이블이 포함된 방금 만든 데이터 집합으로 이동합니다. 부모 테이블의 값 멤버인 자식 테이블의 동일 속성(예: Orders.CustomerID)을 선택합니다. 해당하는 <xref:System.Windows.Forms.BindingSource>, 데이터 집합 및 테이블 어댑터 구성 요소가 작성되어 폼에 추가됩니다.  
  
7. <xref:System.Windows.Forms.BindingNavigator> 컨트롤을 자식 테이블의 <xref:System.Windows.Forms.BindingSource>(예: `OrdersBindingSource`)에 바인딩합니다.  
  
8. <xref:System.Windows.Forms.ComboBox> 및 <xref:System.Windows.Forms.BindingNavigator> 컨트롤 이외의 컨트롤은 표시하려는 자식 테이블의 <xref:System.Windows.Forms.BindingSource>(예: `OrdersBindingSource`)의 세부 정보 필드에 바인딩합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.BindingSource>
- [BindingSource 구성 요소](bindingsource-component.md)
- [ComboBox 컨트롤](combobox-control-windows-forms.md)
- [Visual Studio에서 데이터에 컨트롤 바인딩](/visualstudio/data-tools/bind-controls-to-data-in-visual-studio)
