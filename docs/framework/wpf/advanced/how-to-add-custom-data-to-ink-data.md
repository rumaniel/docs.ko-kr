---
title: '방법: 잉크 데이터에 사용자 지정 데이터 추가'
ms.date: 03/30/2017
helpviewer_keywords:
- ink data [WPF], adding custom data
- InkCanvas [WPF], displaying
ms.assetid: f02aac6f-3436-4f7c-b6ea-0452cba5332c
ms.openlocfilehash: 7c59a205df5358daec101339cc6a308c8e38a9d6
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64640862"
---
# <a name="how-to-add-custom-data-to-ink-data"></a>방법: 잉크 데이터에 사용자 지정 데이터 추가
Serialize 된 잉크 형식 (ISF)으로 잉크를 저장할 때 저장 되는 잉크를 사용자 지정 데이터를 추가할 수 있습니다.  사용자 지정 데이터를 저장할 수 있습니다 합니다 <xref:System.Windows.Ink.DrawingAttributes>는 <xref:System.Windows.Ink.StrokeCollection>, 또는 <xref:System.Windows.Ink.Stroke>합니다.  객체에 사용자 지정 데이터를 저장할 수 있는 데이터를 저장할 최적의 위치를 선택할 수가 있습니다.  세 클래스 모두 저장 하 고 사용자 지정 데이터 액세스 이와 유사한 메서드를 사용 합니다.  
  
 다음 형식의 사용자 지정 데이터로 저장할 수 있습니다.  
  
- <xref:System.Boolean>  
  
- <xref:System.Boolean>[]  
  
- <xref:System.Byte>  
  
- <xref:System.Byte>[]  
  
- <xref:System.Char>  
  
- <xref:System.Char>[]  
  
- <xref:System.DateTime>  
  
- <xref:System.DateTime>[]  
  
- <xref:System.Decimal>  
  
- <xref:System.Decimal>[]  
  
- <xref:System.Double>  
  
- <xref:System.Double>[]  
  
- <xref:System.Int16>  
  
- <xref:System.Int16>[]  
  
- <xref:System.Int32>  
  
- <xref:System.Int32>[]  
  
- <xref:System.Int64>  
  
- <xref:System.Int64>[]  
  
- <xref:System.Single>  
  
- <xref:System.Single>[]  
  
- <xref:System.String>  
  
- <xref:System.UInt16>  
  
- <xref:System.UInt16>[]  
  
- <xref:System.UInt32>  
  
- <xref:System.UInt32>[]  
  
- <xref:System.UInt64>  
  
- <xref:System.UInt64>[]  
  
## <a name="example"></a>예제  
 다음 예제에서는 추가 하 고 사용자 지정 데이터를 검색 하는 방법을 보여 줍니다는 <xref:System.Windows.Ink.StrokeCollection>합니다.  
  
 [!code-csharp[HowToAddCustomDataToInk#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml.cs#1)]  
  
 다음 예제에서는 표시 하는 응용 프로그램을 만듭니다는 <xref:System.Windows.Controls.InkCanvas> 및 두 개의 단추입니다.  단추를 `switchAuthor`, 두 명의 작성자가 사용할 두 개의 펜을 사용 하도록 설정 합니다.  단추 `changePenColors` 에서 각 선의 색을 변경 합니다 <xref:System.Windows.Controls.InkCanvas> 작성자에 따라 합니다.  두 응용 프로그램 정의 <xref:System.Windows.Ink.DrawingAttributes> 저자 그린 나타내는 각각에 사용자 지정 속성을 추가 하 고 개체를 <xref:System.Windows.Ink.Stroke>입니다.  클릭할 때 `changePenColors`, 응용 프로그램에 사용자 지정 속성의 값에 따라 스트로크의 모양을 변경 합니다.  
  
 [!code-xaml[HowToAddCustomDataToInk#2](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml#2)]  
  
 [!code-csharp[HowToAddCustomDataToInk#3](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml.cs#3)]
