---
title: '방법: 요소에서 표시기(Adorner) 제거'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adorners [WPF], removing
ms.assetid: 97cf4d9f-0596-429e-8526-32a30aa4ae99
ms.openlocfilehash: 256dd6fa0117f88aec2ef6b60c6dcd4c33b57855
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770762"
---
# <a name="how-to-remove-an-adorner-from-an-element"></a>방법: 요소에서 표시기(Adorner) 제거
이 예제에서는 프로그래밍 방식으로 지정 된 특정 표시기를 제거 하는 방법을 보여 줍니다 <xref:System.Windows.UIElement>합니다.  
  
## <a name="example"></a>예제  
 반환 하는 표시기 (adorner)의 배열에서 첫 번째 표시기를 제거 하는 자세한 코드 예제 <xref:System.Windows.Documents.AdornerLayer.GetAdorners%2A>합니다.  이 예제에서는 발생에 표시기를 검색 하는 <xref:System.Windows.UIElement> 라는 *myTextBox*합니다.  요소에 대 한 호출에 지정 된 경우 <xref:System.Windows.Documents.AdornerLayer.GetAdorners%2A> 에 표시기가 없는, `null` 반환 됩니다.  이 코드는 명시적으로 null 배열에 대 한 확인 하 고는 null 배열 비교적 많이 필요한 응용 프로그램에 가장 적합 합니다.  
  
 [!code-csharp[AdornersMiscCode#_RemoveSpecificAdornerLong](~/samples/snippets/csharp/VS_Snippets_Wpf/AdornersMiscCode/CSharp/Window1.xaml.cs#_removespecificadornerlong)]
 [!code-vb[AdornersMiscCode#_RemoveSpecificAdornerLong](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdornersMiscCode/visualbasic/window1.xaml.vb#_removespecificadornerlong)]  
  
## <a name="example"></a>예제  
 이 압축 된 코드 예제는 위에 나와 있는 자세한 예와 기능적으로 동일 합니다. 이 코드 검사 하지는 명시적으로 null 배열에 있으므로는 <xref:System.NullReferenceException> 예외가 발생할 수 있습니다.  이 코드는 많지 않은 null 배열이 필요한 응용 프로그램에 가장 적합 합니다.  
  
 [!code-csharp[AdornersMiscCode#_RemoveSpecificAdornerShort](~/samples/snippets/csharp/VS_Snippets_Wpf/AdornersMiscCode/CSharp/Window1.xaml.cs#_removespecificadornershort)]
 [!code-vb[AdornersMiscCode#_RemoveSpecificAdornerShort](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdornersMiscCode/visualbasic/window1.xaml.vb#_removespecificadornershort)]  
  
## <a name="see-also"></a>참고자료

- [표시기 개요](adorners-overview.md)
