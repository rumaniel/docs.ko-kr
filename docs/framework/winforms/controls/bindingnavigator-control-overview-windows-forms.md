---
title: BindingNavigator 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- DataNavigator
helpviewer_keywords:
- BindingNavigator control [Windows Forms], about BindingNavigator control
- records [Windows Forms], navigating on a form
- data [Windows Forms], navigating
- data navigation
ms.assetid: 4423eede-f8d1-4d02-822f-5bf8432680d0
ms.openlocfilehash: ad63f622aae55cb4175eddc93ab5e086965a8fe8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62011788"
---
# <a name="bindingnavigator-control-overview-windows-forms"></a>BindingNavigator 컨트롤 개요(Windows Forms)
<xref:System.Windows.Forms.BindingNavigator> 컨트롤을 사용하여 사용자가 Windows Form에서 데이터를 검색 및 변경할 수 있게 해주는 표준화된 방법을 만들 수 있습니다. 사용자가 폼의 데이터 레코드를 탐색하고 레코드와 상호 작용할 수 있도록 <xref:System.Windows.Forms.BindingSource> 구성 요소와 함께 <xref:System.Windows.Forms.BindingNavigator>를 사용하는 경우가 많습니다.  
  
## <a name="how-the-bindingnavigator-works"></a>BindingNavigator 작동 방식  

 <xref:System.Windows.Forms.BindingNavigator> 컨트롤은 데이터 추가, 데이터 삭제 및 데이터 탐색과 같은 대부분의 일반적인 데이터 관련 작업을 위한 일련의 <xref:System.Windows.Forms.ToolStripItem> 개체를 포함하는 <xref:System.Windows.Forms.ToolStrip>으로 구성됩니다. 기본적으로 <xref:System.Windows.Forms.BindingNavigator> 컨트롤은 이러한 표준 단추를 포함합니다. 다음 스크린 샷에 표시 된 <xref:System.Windows.Forms.BindingNavigator> 양식에 컨트롤:
  
 ![BindingNavigator 컨트롤을 보여주는 스크린샷.](./media/bindingnavigator-control-overview-windows-forms/bindingnavigator-control-form.gif)  
  
 다음 표에서는 컨트롤을 나열하고 해당 기능을 설명합니다.  
  
|컨트롤|함수|  
|-------------|--------------|  
|<xref:System.Windows.Forms.BindingNavigator.AddNewItem%2A> 단추|내부 데이터 소스에 새 행을 삽입합니다.|  
|<xref:System.Windows.Forms.BindingNavigator.DeleteItem%2A> 단추|내부 데이터 소스에서 현재 행을 삭제합니다.|  
|<xref:System.Windows.Forms.BindingNavigator.MoveFirstItem%2A> 단추|내부 데이터 소스의 첫 번째 행으로 이동합니다.|  
|<xref:System.Windows.Forms.BindingNavigator.MoveLastItem%2A> 단추|내부 데이터 소스의 마지막 행으로 이동합니다.|  
|<xref:System.Windows.Forms.BindingNavigator.MoveNextItem%2A> 단추|내부 데이터 소스의 다음 행으로 이동합니다.|  
|<xref:System.Windows.Forms.BindingNavigator.MovePreviousItem%2A> 단추|내부 데이터 소스의 이전 행으로 이동합니다.|  
|<xref:System.Windows.Forms.BindingNavigator.PositionItem%2A> 텍스트 상자|내부 데이터 소스 내의 현재 위치를 반환합니다.|  
|<xref:System.Windows.Forms.BindingNavigator.CountItem%2A> 텍스트 상자|내부 데이터 소스의 총 항목 수를 반환합니다.|  
  
 이 컬렉션의 각 컨트롤에 대해 프로그래밍 방식으로 동일한 기능을 제공하는 <xref:System.Windows.Forms.BindingSource> 구성 요소의 해당 멤버가 있습니다. 예를 들어 <xref:System.Windows.Forms.BindingNavigator.MoveFirstItem%2A> 단추는 <xref:System.Windows.Forms.BindingSource> 구성 요소의 <xref:System.Windows.Forms.BindingSource.MoveFirst%2A> 메서드에 해당하고 <xref:System.Windows.Forms.BindingNavigator.DeleteItem%2A> 단추는 <xref:System.Windows.Forms.BindingSource.RemoveCurrent%2A> 메서드에 해당합니다.  
  
 기본 단추가 애플리케이션에 적합하지 않은 경우 또는 다른 유형의 기능을 지원하기 위해 추가 단추가 필요한 경우 고유한 <xref:System.Windows.Forms.ToolStrip> 단추를 제공할 수 있습니다. 또한 참조 [방법: 저장, 로드를 추가 하 고 취소 단추는 Windows Forms BindingNavigator 컨트롤](load-save-and-cancel-bindingnavigator.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.BindingNavigator>
- <xref:System.Windows.Forms.BindingSource>
- [BindingNavigator 컨트롤](bindingnavigator-control-windows-forms.md)
