---
title: BindingSource 구성 요소
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [Windows Forms], Windows Forms
- Windows Forms, data binding control
- BindingSource component [Windows Forms]
ms.assetid: 3e2faf4c-f5b8-4fa6-9fbc-f59c37ec2fb9
ms.openlocfilehash: 54639edb512a8bc6c5909282d5e4c210439e2a6e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61683420"
---
# <a name="bindingsource-component"></a>BindingSource 구성 요소
컨트롤에 바인딩하기 위해 데이터 소스를 캡슐화합니다.  
  
 <xref:System.Windows.Forms.BindingSource> 구성 요소는 두가지 용도로 사용됩니다. 첫째, 폼의 컨트롤을 데이터에 바인딩할 때 간접 참조 계층을 제공합니다. 이 작업은 <xref:System.Windows.Forms.BindingSource> 구성 요소를 데이터 소스에 바인딩한 다음 폼의 컨트롤을 <xref:System.Windows.Forms.BindingSource> 구성 요소에 바인딩하여 수행됩니다. 탐색, 정렬, 필터링, 업데이트 등 데이터와의 모든 상호 작용은 <xref:System.Windows.Forms.BindingSource> 구성 요소를 호출하여 수행됩니다.  
  
 둘째, <xref:System.Windows.Forms.BindingSource> 구성 요소는 강력한 형식의 데이터 소스로 사용될 수 있습니다. <xref:System.Windows.Forms.BindingSource.Add%2A> 메서드를 통해 <xref:System.Windows.Forms.BindingSource> 구성 요소에 형식을 추가하면 해당 형식의 목록이 만들어집니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [BindingSource 구성 요소 개요](bindingsource-component-overview.md)  
 데이터 소스를 컨트롤에 바인딩할 수 있게 해주는 <xref:System.Windows.Forms.BindingSource> 구성 요소의 일반적인 개념을 소개합니다.  
  
 [방법: DBNull 데이터베이스 값에 Windows Forms 컨트롤 바인딩](how-to-bind-windows-forms-controls-to-dbnull-database-values.md)  
 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용하여 데이터 소스의 <xref:System.DBNull> 값을 처리하는 방법을 보여 줍니다.  
  
 [방법: Forms BindingSource 구성 요소는 Windows 사용 하 여 ADO.NET 데이터 정렬 및 필터링](sort-and-filter-ado-net-data-with-wf-bindingsource-component.md)  
 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용하여 표시된 데이터에 정렬 및 필터를 적용하는 방법을 보여 줍니다.  
  
 [방법: Windows Forms BindingSource를 사용 하 여 웹 서비스에 바인딩](how-to-bind-to-a-web-service-using-the-windows-forms-bindingsource.md)  
 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용하여 웹 서비스에 바인딩하는 방법을 보여 줍니다.  
  
 [방법: 오류 및 데이터 바인딩에서 발생 하는 예외 처리](how-to-handle-errors-and-exceptions-that-occur-with-databinding.md)  
 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용하여 데이터 바인딩 작업에서 발생하는 오류를 정상적으로 처리하는 방법을 보여 줍니다.  
  
 [방법: 형식에는 Windows Forms 컨트롤 바인딩](how-to-bind-a-windows-forms-control-to-a-type.md)  
 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용하여 형식에 바인딩하는 방법을 보여 줍니다.  
  
 [방법: 팩터리 개체에 Windows Forms 컨트롤 바인딩](how-to-bind-a-windows-forms-control-to-a-factory-object.md)  
 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용하여 팩터리 개체나 메서드에 바인딩하는 방법을 보여 줍니다.  
  
 [방법: Windows Forms BindingSource 사용 하 여 항목 추가 사용자 지정](how-to-customize-item-addition-with-the-windows-forms-bindingsource.md)  
 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용하여 새 항목을 만들고 데이터 소스에 추가하는 방법을 보여 줍니다.  
  
 [방법: BindingSource ResetItem 메서드를 사용 하 여 변경 알림 발생](how-to-raise-change-notifications-using-the-bindingsource-resetitem-method.md)  
 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용하여 변경 알림을 지원하지 않는 데이터 소스에 대한 변경 알림 이벤트를 발생시키는 방법을 보여 줍니다.  
  
 [방법: BindingSource와 INotifyPropertyChanged 인터페이스를 사용 하 여 변경 알림 발생](raise-change-notifications--bindingsource.md)  
 <xref:System.Windows.Forms.BindingSource> 컨트롤을 통해 <xref:System.ComponentModel.INotifyPropertyChanged>에서 상속되는 형식을 사용하는 방법을 보여 줍니다.  
  
 [방법: BindingSource 사용 하 여 Windows Forms 컨트롤에 데이터 소스 업데이트 내용 반영](reflect-data-source-updates-in-a-wf-control-with-the-bindingsource.md)  
 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용하여 데이터 소스의 변경 내용에 응답하는 방법을 보여 줍니다.  
  
 [방법: BindingSource 구성 요소를 사용 하 여 양식 간에 바인딩된 데이터 공유](how-to-share-bound-data-across-forms-using-the-bindingsource-component.md)  
 <xref:System.Windows.Forms.BindingSource>를 사용하여 여러 개의 폼을 동일한 데이터 소스에 바인딩하는 방법을 보여 줍니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Windows.Forms.BindingSource>  
 <xref:System.Windows.Forms.BindingSource> 구성 요소에 대한 참조 설명서를 제공합니다.  
  
 <xref:System.Windows.Forms.BindingNavigator>  
 <xref:System.Windows.Forms.BindingNavigator> 컨트롤에 대한 참조 설명서를 제공합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [Windows Forms 데이터 바인딩](../windows-forms-data-binding.md)  
 Windows Forms 데이터 바인딩 아키텍처를 설명하는 항목의 링크를 포함합니다.  
  
 [Visual Studio에서 데이터에 컨트롤 바인딩](/visualstudio/data-tools/bind-controls-to-data-in-visual-studio)도 참조하세요.
