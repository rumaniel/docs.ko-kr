---
title: '방법: DBNull 데이터베이스 값에 Windows Forms 컨트롤 바인딩'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- BindingSource component [Windows Forms], binding to DBNull values
- examples [Windows Forms], BindingSource component
- controls [Windows Forms], binding to DBNull values
ms.assetid: 96494e6f-5f40-4f83-af97-bbd7192c2af8
ms.openlocfilehash: 8abce5d69a7cece6528e0c9d8728de0e0acd9305
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591419"
---
# <a name="how-to-bind-windows-forms-controls-to-dbnull-database-values"></a>방법: DBNull 데이터베이스 값에 Windows Forms 컨트롤 바인딩
Windows Forms 컨트롤을 데이터 소스에 바인딩하고 데이터 소스가 <xref:System.DBNull> 값을 반환하는 경우 이벤트를 처리, 형식 지정 또는 구문 분석하지 않고 적절한 값을 대체할 수 있습니다. <xref:System.Windows.Forms.Binding.NullValue%2A> 속성은 데이터 소스 값을 형식 지정 또는 구문 분석할 때 <xref:System.DBNull>을 지정된 개체로 변환합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 가지 다른 상황에서 <xref:System.DBNull> 값을 바인딩하는 방법을 보여 줍니다. 첫 번째 예제에서는 문자열 속성에 대해 <xref:System.Windows.Forms.Binding.NullValue%2A>를 설정하는 방법을 보여 주고, 두 번째 예제에서는 이미지 속성에 대해 <xref:System.Windows.Forms.Binding.NullValue%2A>를 설정하는 방법을 보여 줍니다.  
  
 [!code-csharp[System.Windows.Forms.BindingDBNull#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingDBNull/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.BindingDBNull#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingDBNull/VB/form1.vb#1)]  
  
 바인딩된 속성의 형식 및 <xref:System.Windows.Forms.Binding.NullValue%2A> 속성은 같아야 합니다. 그러지 않으면 오류가 발생하고 더 이상 <xref:System.Windows.Forms.Binding.NullValue%2A> 값이 처리되지 않습니다. 이 경우 예외가 발생하지 않습니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System, System.Data, System.Drawing 및 System.Windows.Forms 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- [BindingSource 구성 요소](bindingsource-component.md)
- [방법: 오류 및 데이터 바인딩에서 발생 하는 예외 처리](how-to-handle-errors-and-exceptions-that-occur-with-databinding.md)
- [방법: 형식에는 Windows Forms 컨트롤 바인딩](how-to-bind-a-windows-forms-control-to-a-type.md)
