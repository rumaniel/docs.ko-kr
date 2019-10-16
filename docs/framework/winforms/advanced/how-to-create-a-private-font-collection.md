---
title: '방법: 개인 글꼴 컬렉션 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- private font collections [Windows Forms], creating
- fonts [Windows Forms], creating private collections
ms.assetid: 6533d5e5-a8dc-4b76-9fc4-3bf75c8b9212
ms.openlocfilehash: 0bb7293a5423004a13cf98b79bba0a6c411a7c97
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505520"
---
# <a name="how-to-create-a-private-font-collection"></a>방법: 개인 글꼴 컬렉션 만들기
합니다 <xref:System.Drawing.Text.PrivateFontCollection> 클래스에서 상속 된 <xref:System.Drawing.Text.FontCollection> 추상 기본 클래스입니다. 사용할 수는 <xref:System.Drawing.Text.PrivateFontCollection> 응용 프로그램에 맞게 글꼴 집합도 유지 관리 하는 개체입니다. 개인 글꼴 컬렉션 컴퓨터에 설치 되지 않은 글꼴 뿐만 아니라 설치 된 시스템 글꼴을 포함할 수 있습니다. 글꼴 파일을 개인 글꼴 컬렉션에 추가할 호출을 <xref:System.Drawing.Text.PrivateFontCollection.AddFontFile%2A> 메서드를 <xref:System.Drawing.Text.PrivateFontCollection> 개체입니다.  
  
 합니다 <xref:System.Drawing.Text.FontCollection.Families%2A> 의 속성을 <xref:System.Drawing.Text.PrivateFontCollection> 개체의 배열을 포함 <xref:System.Drawing.FontFamily> 개체입니다.  
  
 개인 글꼴 컬렉션에서 글꼴 패밀리 수가 아닐 컬렉션에 추가 된 글꼴 파일의 수와 동일 합니다. 예를 들어, 컬렉션에 ArialBd.tff, Times.tff, 및 TimesBd.tff 파일을 추가 합니다. 됩니다 파일 세 개 있지만 컬렉션에 있는 두 패밀리 Times.tff 및 TimesBd.tff 동일한 제품군에 속해 있으므로.  
  
## <a name="example"></a>예제  
 다음 예제에서는 다음 세 개의 글꼴 파일을 <xref:System.Drawing.Text.PrivateFontCollection> 개체:  
  
- C:\\*systemroot*\Fonts\Arial.tff (Arial, 일반)  
  
- C:\\*systemroot*\Fonts\CourBI.tff (Courier New 굵게 기울임꼴)  
  
- C:\\*systemroot*\Fonts\TimesBd.tff (Times New Roman 굵게 표시)  
  
 코드의 배열을 검색 <xref:System.Drawing.FontFamily> 에서 개체를 <xref:System.Drawing.Text.FontCollection.Families%2A> 의 속성을 <xref:System.Drawing.Text.PrivateFontCollection> 개체입니다.  
  
 각 <xref:System.Drawing.FontFamily> 코드를 호출 하 여 컬렉션에서 개체를 <xref:System.Drawing.FontFamily.IsStyleAvailable%2A> (일반, 굵게, 기울임꼴, 굵게 기울임꼴, 밑줄 및 취소선) 다양 한 스타일을 사용할 수 있는지 여부를 결정 하는 방법입니다. 인수에 전달 합니다 <xref:System.Drawing.FontFamily.IsStyleAvailable%2A> 의 멤버인 메서드는 <xref:System.Drawing.FontStyle> 열거형입니다.  
  
 지정 된 제품군/스타일 조합을 사용할 수 있으면를 <xref:System.Drawing.Font> 개체는 패밀리 및 스타일을 사용 하 여 생성 됩니다. 전달 된 첫 번째 인수는 <xref:System.Drawing.Font.%23ctor%2A> 생성자는 글꼴 패밀리 이름을 (하지는 <xref:System.Drawing.FontFamily> 의 다른 변형에 대 한 경우 개체는 <xref:System.Drawing.Font.%23ctor%2A> 생성자). 후는 <xref:System.Drawing.Font> 개체가 생성 되 면 전달 되는 <xref:System.Drawing.Graphics.DrawString%2A> 메서드의 <xref:System.Drawing.Graphics> 클래스 스타일의 이름과 함께 제품군 이름을 표시 합니다.  
  
 다음 코드의 출력은 다음 그림에 표시 된 출력과 비슷합니다.  
  
 ![다양 한 글꼴의 텍스트를 보여 주는 스크린샷.](./media/how-to-create-a-private-font-collection/various-fonts-text-output.png)  
  
 (다음 코드 예제에서 개인 글꼴 컬렉션에 추가 된)는 Arial.tff에 Arial 보통 스타일에 대 한 글꼴 파일입니다. 그러나는 프로그램 출력 Arial 글꼴 패밀리에 대 한 일반 이외의 여러 사용 가능한 스타일을 보여 줍니다. 이것은 GDI + 일반 스타일에서 굵게, 기울임꼴 및 굵은 기울임꼴 스타일을 시뮬레이션할 수 있습니다. GDI + 일반 스타일에서 밑줄과 만들 수 있습니다.  
  
 마찬가지로, GDI + 시뮬레이트하는 굵게 또는 기울임꼴 스타일에서 굵게 기울임꼴 스타일입니다. 굵은 기울임꼴 스타일 되 번 제품군에 사용할 수 있는 유일한 TimesBd.tff (Times New Roman 굵게 표시 된) 경우에 프로그램 출력에 표시 컬렉션에 있는 파일입니다.  
  
 [!code-csharp[System.Drawing.FontsAndText#51](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#51)]
 [!code-vb[System.Drawing.FontsAndText#51](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#51)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows Forms에서 사용 하도록 설계 되었으며 필요 <xref:System.Windows.Forms.PaintEventArgs> `e`의 매개 변수인 <xref:System.Windows.Forms.PaintEventHandler>합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Text.PrivateFontCollection>
- [글꼴 및 텍스트 사용](using-fonts-and-text.md)
