---
title: '방법: 사용자 지정 개체에 대한 유효성 검사 논리 구현'
ms.date: 08/02/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- checking for validation errors [WPF]
- validation errors [WPF], checking for
- implementing validation logic on custom objects [WPF]
- custom objects [WPF], implementing validation logic on
ms.assetid: 751fda9b-44f9-4d63-b4f2-1df07ac41e0f
ms.openlocfilehash: 8520504757e9e9ec9557b84ca2608b4cb99daf62
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61931402"
---
# <a name="how-to-implement-validation-logic-on-custom-objects"></a>방법: 사용자 지정 개체에 대한 유효성 검사 논리 구현
이 예제에서는 사용자 지정 개체에서 유효성 검사 논리를 구현 하 고 다음에 바인딩하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 소스 개체가 구현 하는 경우 비즈니스 계층에 유효성 검사 논리를 제공할 수 있습니다 <xref:System.ComponentModel.IDataErrorInfo>정의 하는 다음 예제 에서처럼를 `Person` 구현 하는 개체 <xref:System.ComponentModel.IDataErrorInfo>:  
  
 [!code-csharp[BusinessLayerValidation#IDataErrorInfo](~/samples/snippets/csharp/VS_Snippets_Wpf/BusinessLayerValidation/CSharp/Data.cs#idataerrorinfo)]
 [!code-vb[BusinessLayerValidation#IDataErrorInfo](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BusinessLayerValidation/VisualBasic/Data.vb#idataerrorinfo)]  
  
 다음 예제에서는 텍스트 상자의 text 속성에 바인딩합니다 합니다 `Person.Age` 바인딩에 지정 된 리소스 선언을 통해 사용할 수 있는 속성을 `x:Key` `data`. 합니다 <xref:System.Windows.Controls.DataErrorValidationRule> 에서 발생 한 유효성 검사 오류에 대 한 검사를 <xref:System.ComponentModel.IDataErrorInfo> 구현 합니다.  
  
 [!code-xaml[BusinessLayerValidation#BoundTextBox](~/samples/snippets/csharp/VS_Snippets_Wpf/BusinessLayerValidation/CSharp/Window1.xaml?highlight=8,11-19,25-42)]  
  
 사용 하는 대신 또는 합니다 <xref:System.Windows.Controls.DataErrorValidationRule>를 설정할 수 있습니다 합니다 <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A> 속성을 `true`.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ExceptionValidationRule>
- [바인딩 유효성 검사 구현](how-to-implement-binding-validation.md)
- [방법 항목](data-binding-how-to-topics.md)
