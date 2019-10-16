---
title: '방법: 그리는 데 필요한 그래픽 개체 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- graphics [Windows Forms], creating
- images [Windows Forms], creating
- GDI+, creating images
ms.assetid: 162861f9-f050-445e-8abb-b2c43a918b8b
ms.openlocfilehash: 3d3ab62896f6b799cd38a8180b90f33125a9929b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964335"
---
# <a name="how-to-create-graphics-objects-for-drawing"></a>방법: 그리는 데 필요한 그래픽 개체 만들기
선 및 도형을 그리거나, 텍스트를 렌더링 하거나, gdi +를 사용 하 여 이미지를 표시 하 고 조작 하려면 먼저 <xref:System.Drawing.Graphics> 개체를 만들어야 합니다. <xref:System.Drawing.Graphics> 개체는 gdi + 그리기 화면을 나타내며 그래픽 이미지를 만드는 데 사용 되는 개체입니다.  
  
 그래픽 작업에는 두 가지 단계가 있습니다.  
  
1. <xref:System.Drawing.Graphics> 개체 만들기  
  
2. <xref:System.Drawing.Graphics> 개체를 사용 하 여 선과 도형을 그리거나, 텍스트를 렌더링 하거나, 이미지를 표시 하 고 조작 합니다.  
  
## <a name="creating-a-graphics-object"></a>그래픽 개체 만들기  
 그래픽 개체는 다양 한 방법으로 만들 수 있습니다.  
  
#### <a name="to-create-a-graphics-object"></a>그래픽 개체를 만들려면  
  
- 폼 또는 컨트롤의 경우의 <xref:System.Windows.Forms.PaintEventArgs> <xref:System.Windows.Forms.Control.Paint> 일부로 그래픽 개체에 대 한 참조를 받습니다. 일반적으로 컨트롤의 그리기 코드를 만들 때 그래픽 개체에 대 한 참조를 가져오는 방법입니다. 마찬가지로,에 대 한 <xref:System.Drawing.Printing.PrintPageEventArgs> <xref:System.Drawing.Printing.PrintDocument.PrintPage> <xref:System.Drawing.Printing.PrintDocument>이벤트를 처리할 때 그래픽 개체를의 속성으로 가져올 수도 있습니다.  
  
     또는  
  
- 컨트롤이 나 <xref:System.Windows.Forms.Control.CreateGraphics%2A> 폼의 메서드를 호출 하 여 해당 컨트롤이 나 폼의 <xref:System.Drawing.Graphics> 그리기 화면을 나타내는 개체에 대 한 참조를 가져옵니다. 이미 존재 하는 폼 이나 컨트롤에 그리려는 경우이 메서드를 사용 합니다.  
  
     또는  
  
- <xref:System.Drawing.Graphics> 에서<xref:System.Drawing.Image>상속 되는 개체에서 개체를 만듭니다. 이 방법은 이미 존재 하는 이미지를 변경 하려는 경우에 유용 합니다.  
  
     다음 섹션에서는 이러한 각 프로세스에 대 한 세부 정보를 제공 합니다.  
  
## <a name="painteventargs-in-the-paint-event-handler"></a>Paint 이벤트 처리기의 PaintEventArgs  
 컨트롤 <xref:System.Windows.Forms.PaintEventHandler> <xref:System.Windows.Forms.PaintEventArgs> <xref:System.Drawing.Printing.PrintPageEventArgs>또는의에 대 한를 프로그래밍할 때 그래픽 개체는 또는의 속성 중 하나로 제공 됩니다. <xref:System.Drawing.Printing.PrintDocument.PrintPage> <xref:System.Drawing.Printing.PrintDocument>  
  
#### <a name="to-obtain-a-reference-to-a-graphics-object-from-the-painteventargs-in-the-paint-event"></a>Paint 이벤트의 PaintEventArgs에서 그래픽 개체에 대 한 참조를 가져오려면  
  
1. 개체를 <xref:System.Drawing.Graphics> 선언 합니다.  
  
2. 의 일부로 전달 된 <xref:System.Drawing.Graphics> 개체를 참조 하는 변수를 할당 합니다. <xref:System.Windows.Forms.PaintEventArgs>  
  
3. 폼 이나 컨트롤을 그리는 코드를 삽입 합니다.  
  
     다음 예제에서는 <xref:System.Drawing.Graphics> <xref:System.Windows.Forms.Control.Paint> 이벤트 <xref:System.Windows.Forms.PaintEventArgs> 의에서 개체를 참조 하는 방법을 보여 줍니다.  
  
    ```vb  
    Private Sub Form1_Paint(sender As Object, pe As PaintEventArgs) Handles _  
       MyBase.Paint  
       ' Declares the Graphics object and sets it to the Graphics object  
       ' supplied in the PaintEventArgs.  
       Dim g As Graphics = pe.Graphics  
       ' Insert code to paint the form here.  
    End Sub  
    ```  
  
    ```csharp  
    private void Form1_Paint(object sender,   
       System.Windows.Forms.PaintEventArgs pe)   
    {  
       // Declares the Graphics object and sets it to the Graphics object  
       // supplied in the PaintEventArgs.  
       Graphics g = pe.Graphics;  
       // Insert code to paint the form here.  
    }  
    ```  
  
    ```cpp  
    private:  
       void Form1_Paint(System::Object ^ sender,  
          System::Windows::Forms::PaintEventArgs ^ pe)  
       {  
          // Declares the Graphics object and sets it to the Graphics object  
          // supplied in the PaintEventArgs.  
          Graphics ^ g = pe->Graphics;  
          // Insert code to paint the form here.  
       }  
    ```  
  
## <a name="creategraphics-method"></a>CreateGraphics 메서드  
 컨트롤이 나 폼의 메서드 <xref:System.Windows.Forms.Control.CreateGraphics%2A> 를 사용 하 여 해당 컨트롤이 나 폼의 그리기 화면을 <xref:System.Drawing.Graphics> 나타내는 개체에 대 한 참조를 가져올 수도 있습니다.  
  
#### <a name="to-create-a-graphics-object-with-the-creategraphics-method"></a>CreateGraphics 메서드를 사용 하 여 그래픽 개체를 만들려면  
  
- 그래픽을 <xref:System.Windows.Forms.Control.CreateGraphics%2A> 렌더링 하려는 폼 이나 컨트롤의 메서드를 호출 합니다.  
  
    ```vb  
    Dim g as Graphics  
    ' Sets g to a Graphics object representing the drawing surface of the  
    ' control or form g is a member of.  
    g = Me.CreateGraphics  
    ```  
  
    ```csharp  
    Graphics g;  
    // Sets g to a graphics object representing the drawing surface of the  
    // control or form g is a member of.  
    g = this.CreateGraphics();  
    ```  
  
    ```cpp  
    Graphics ^ g;  
    // Sets g to a graphics object representing the drawing surface of the  
    // control or form g is a member of.  
    g = this->CreateGraphics();  
    ```  
  
## <a name="create-from-an-image-object"></a>이미지 개체에서 만들기  
 또한 <xref:System.Drawing.Image> 클래스에서 파생 되는 모든 개체에서 그래픽 개체를 만들 수 있습니다.  
  
#### <a name="to-create-a-graphics-object-from-an-image"></a>이미지에서 그래픽 개체를 만들려면  
  
- 개체를 만들려는 이미지 변수의 이름을 제공 하 여 메서드를호출합니다.<xref:System.Drawing.Graphics.FromImage%2A?displayProperty=nameWithType> <xref:System.Drawing.Graphics>  
  
     다음 예제에서는 개체를 <xref:System.Drawing.Bitmap> 사용 하는 방법을 보여 줍니다.  
  
    ```vb  
    Dim myBitmap as New Bitmap("C:\Documents and Settings\Joe\Pics\myPic.bmp")  
    Dim g as Graphics = Graphics.FromImage(myBitmap)  
    ```  
  
    ```csharp  
    Bitmap myBitmap = new Bitmap(@"C:\Documents and   
       Settings\Joe\Pics\myPic.bmp");  
    Graphics g = Graphics.FromImage(myBitmap);  
    ```  
  
    ```cpp  
    Bitmap ^ myBitmap = gcnew  
       Bitmap("D:\\Documents and Settings\\Joe\\Pics\\myPic.bmp");  
    Graphics ^ g = Graphics::FromImage(myBitmap);  
    ```  
  
> [!NOTE]
> 16 비트, 24 <xref:System.Drawing.Graphics> 비트 및 32 비트 .bmp 파일과 같은 인덱싱되지 않은 .bmp 파일의 개체만 만들 수 있습니다. 비인덱스 .bmp 파일의 각 픽셀은 색 테이블에 대 한 인덱스를 포함 하는 인덱싱된 .bmp 파일의 픽셀과 달리 색을 포함 합니다.  
  
## <a name="drawing-and-manipulating-shapes-and-images"></a>모양 및 이미지 그리기 및 조작  
 개체를 <xref:System.Drawing.Graphics> 만든 후에는 개체를 사용 하 여 선과 셰이프를 그리거나, 텍스트를 렌더링 하거나, 이미지를 표시 하 고 조작할 수 있습니다. <xref:System.Drawing.Graphics> 개체와 함께 사용 되는 보안 주체 개체는 다음과 같습니다.  
  
- <xref:System.Drawing.Pen> 클래스-선 그리기, 모양 개요 또는 다른 기하학적 표현 렌더링에 사용 됩니다.  
  
- <xref:System.Drawing.Brush> 클래스-채워진 도형, 이미지 또는 텍스트와 같은 그래픽 영역을 채우는 데 사용 됩니다.  
  
- <xref:System.Drawing.Font> 클래스-텍스트를 렌더링할 때 사용할 도형에 대 한 설명을 제공 합니다.  
  
- 구조 <xref:System.Drawing.Color> 는 표시할 여러 색을 나타냅니다.  
  
#### <a name="to-use-the-graphics-object-you-have-created"></a>만든 그래픽 개체를 사용 하려면  
  
- 위에 나열 된 적절 한 개체를 사용 하 여 필요한 항목을 그립니다.  
  
     자세한 내용은 다음 항목을 참조하십시오.  
  
    |렌더링 하려면|참조|  
    |---------------|---------|  
    |선|[방법: Windows Form에 선 그리기](how-to-draw-a-line-on-a-windows-form.md)|  
    |셰이프|[방법: 윤곽선이 있는 도형 그리기](how-to-draw-an-outlined-shape.md)|  
    |텍스트|[방법: Windows Form에 텍스트 그리기](how-to-draw-text-on-a-windows-form.md)|  
    |이미지|[방법: GDI +를 사용 하 여 이미지 렌더링](how-to-render-images-with-gdi.md)|  
  
## <a name="see-also"></a>참고자료

- [그래픽 프로그래밍 시작](getting-started-with-graphics-programming.md)
- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
- [선, 곡선 및 도형](lines-curves-and-shapes.md)
- [방법: GDI +를 사용 하 여 이미지 렌더링](how-to-render-images-with-gdi.md)
