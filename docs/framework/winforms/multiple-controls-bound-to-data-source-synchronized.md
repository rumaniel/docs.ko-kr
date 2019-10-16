---
title: '방법: 동일한 데이터 소스에 바인딩된 여러 컨트롤의 동기화 상태가 유지되도록 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [Windows Forms], binding multiple
- controls [Windows Forms], synchronizing with data source
ms.assetid: c2f0ecc6-11e6-4c2c-a1ca-0759630c451e
ms.openlocfilehash: 8a39c50bfc452c807a18a9bf0a65e56cb75d20aa
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64655625"
---
# <a name="how-to-ensure-multiple-controls-bound-to-the-same-data-source-remain-synchronized"></a>방법: 동일한 데이터 소스에 바인딩된 여러 컨트롤의 동기화 상태가 유지되도록 설정
Windows Forms에서 데이터 바인딩을 사용 하 여 작업을 하는 경우에 종종 여러 컨트롤은 동일한 데이터 소스에 바인딩됩니다. 일부 경우에는 컨트롤의 바인딩된 속성이 서로 데이터 소스를 사용 하 여 동기화 된 상태로 유지 되도록 추가 단계를 수행 해야 할 수도 있습니다. 이러한 단계는 두 가지 상황에서 필요 합니다.  
  
- 데이터 소스를 구현 하지 않는 경우 <xref:System.ComponentModel.IBindingList>를 생성 하므로 <xref:System.ComponentModel.IBindingList.ListChanged> 유형의 이벤트 <xref:System.ComponentModel.ListChangedType.ItemChanged>합니다.  
  
- 데이터 원본 구현 <xref:System.ComponentModel.IEditableObject>합니다.  
  
 전자의 경우에 사용할 수는 <xref:System.Windows.Forms.BindingSource> 데이터 소스 컨트롤에 바인딩할 합니다. 후자의 경우 사용 하 여는 <xref:System.Windows.Forms.BindingSource> 하 고 처리 합니다 <xref:System.Windows.Forms.BindingSource.BindingComplete> 이벤트 및 호출 <xref:System.Windows.Forms.BindingManagerBase.EndCurrentEdit%2A> 연결 된 <xref:System.Windows.Forms.BindingManagerBase>합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 세 가지 컨트롤을 바인딩하는 방법을 보여 줍니다-두 개의 텍스트 상자 컨트롤 및 <xref:System.Windows.Forms.DataGridView> 컨트롤-동일한 열에 <xref:System.Data.DataSet> 사용 하 여를 <xref:System.Windows.Forms.BindingSource> 구성 요소입니다. 이 예제에서는 처리 하는 방법에 설명 합니다 <xref:System.Windows.Forms.BindingSource.BindingComplete> 이벤트 하나의 입력란의 텍스트 값 변경 되 면 추가 텍스트 상자를 확인 및 <xref:System.Windows.Forms.DataGridView> 컨트롤은 올바른 값으로 업데이트 됩니다.  
  
 이 예제에서는 사용을 <xref:System.Windows.Forms.BindingSource> 데이터 원본과 컨트롤을 바인딩할 합니다. 또는 데이터 원본에 직접 컨트롤을 바인딩할 수를 검색 합니다 <xref:System.Windows.Forms.BindingManagerBase> 폼의 바인딩에 대 한 <xref:System.Windows.Forms.Control.BindingContext%2A> 처리 및를 <xref:System.Windows.Forms.BindingManagerBase.BindingComplete> 에 대 한 이벤트는 <xref:System.Windows.Forms.BindingManagerBase>합니다. 이 작업을 수행 하는 방법의 예에 대 한 도움말 페이지를 참조 합니다 <xref:System.Windows.Forms.BindingManagerBase.BindingComplete> 이벤트를 <xref:System.Windows.Forms.BindingManagerBase>입니다.  
  
 [!code-csharp[System.Windows.Forms.BindingSourceMultipleControls#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleControls/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.BindingSourceMultipleControls#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleControls/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- 이 코드 예제에서는  
  
- <xref:System>, <xref:System.Windows.Forms> 및 <xref:System.Drawing> 어셈블리에 대한 참조  
  
- 사용 하 여 폼을 <xref:System.Windows.Forms.Form.Load> 이벤트를 처리 하 고 호출 하는 `InitializeControlsAndDataSource` 폼의 예제에서 메서드 <xref:System.Windows.Forms.Form.Load> 이벤트 처리기입니다.  
  
## <a name="see-also"></a>참고자료

- [방법: BindingSource 구성 요소를 사용 하 여 양식 간에 바인딩된 데이터 공유](./controls/how-to-share-bound-data-across-forms-using-the-bindingsource-component.md)
- [Windows Forms 데이터 바인딩의 변경 알림](change-notification-in-windows-forms-data-binding.md)
- [데이터 바인딩과 관련된 인터페이스](interfaces-related-to-data-binding.md)
- [Windows Forms 데이터 바인딩](windows-forms-data-binding.md)
