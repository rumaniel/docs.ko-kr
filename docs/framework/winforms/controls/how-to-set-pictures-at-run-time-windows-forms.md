---
title: '방법: 런타임에 그림 설정 (Windows Forms)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- pictures [Windows Forms], setting display
- examples [Windows Forms], PictureBox control
- bitmaps [Windows Forms], displaying in PictureBox control [Windows Forms]
- PictureBox control [Windows Forms], adding images
- images [Windows Forms], adding with PictureBox control [Windows Forms]
- PictureBox control [Windows Forms], adding pictures
ms.assetid: 18ca41d0-68a5-4660-985e-a6c1fbc01d76
ms.openlocfilehash: 99d78a275c8ad8f55d9b0832a794545b65da7e20
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917524"
---
# <a name="how-to-set-pictures-at-run-time-windows-forms"></a>방법: 런타임에 그림 설정 (Windows Forms)
Windows Forms <xref:System.Windows.Forms.PictureBox> 컨트롤에 의해 표시 되는 이미지를 프로그래밍 방식으로 설정할 수 있습니다.  
  
### <a name="to-set-a-picture-programmatically"></a>프로그래밍 방식으로 그림을 설정 하려면  
  
- 클래스의 <xref:System.Drawing.Image.FromFile%2A> <xref:System.Windows.Forms.PictureBox.Image%2A> 메서드를사용하여속성을설정합니다<xref:System.Drawing.Image> .  
  
     아래 예제에서 이미지 위치에 대해 설정 된 경로는 내 문서 폴더입니다. Windows 운영 체제를 실행 하는 대부분의 컴퓨터에이 디렉터리가 포함 되어 있다고 가정할 수 있으므로이 작업을 수행 합니다. 또한 최소한의 시스템 액세스 수준을 가진 사용자가 안전하게 애플리케이션을 실행할 수 있습니다. 아래 예제에서는 <xref:System.Windows.Forms.PictureBox> 컨트롤이 이미 추가 된 폼을 가정 합니다.  
  
    ```vb  
    Private Sub LoadNewPict()  
       ' You should replace the bold image   
       ' in the sample below with an icon of your own choosing.  
       PictureBox1.Image = Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
    End Sub  
    ```  
  
    ```csharp  
    private void LoadNewPict(){  
       // You should replace the bold image   
       // in the sample below with an icon of your own choosing.  
       // Note the escape character used (@) when specifying the path.  
       pictureBox1.Image = Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Image.gif");  
    }  
    ```  
  
    ```cpp  
    private:  
       void LoadNewPict()  
       {  
          // You should replace the bold image   
          // in the sample below with an icon of your own choosing.  
          pictureBox1->Image = Image::FromFile(String::Concat(  
             System::Environment::GetFolderPath(  
             System::Environment::SpecialFolder::Personal),  
             "\\Image.gif"));  
       }  
    ```  
  
### <a name="to-clear-a-graphic"></a>그래픽을 지우려면  
  
- 먼저 이미지에 사용 되는 메모리를 해제 한 다음 그래픽의 선택을 취소 합니다. 메모리 관리가 문제가 되 면 가비지 수집에서 나중에 메모리를 해제 합니다.  
  
    ```vb  
    If Not (PictureBox1.Image Is Nothing) Then  
       PictureBox1.Image.Dispose()  
       PictureBox1.Image = Nothing  
    End If  
    ```  
  
    ```csharp  
    if (pictureBox1.Image != null)   
    {  
       pictureBox1.Image.Dispose();  
       pictureBox1.Image = null;  
    }  
    ```  
  
    ```cpp  
    if (pictureBox1->Image != nullptr)  
    {  
       pictureBox1->Image->Dispose();  
       pictureBox1->Image = nullptr;  
    }  
    ```  
  
    > [!NOTE]
    > 이러한 방법으로 메서드를 <xref:System.Drawing.Image.Dispose%2A> 사용 해야 하는 이유에 대 한 자세한 내용은 [관리 되지 않는 리소스 정리](../../../standard/garbage-collection/unmanaged.md)를 참조 하세요.  
  
     디자인 타임에 그래픽이 컨트롤에 로드 된 경우에도이 코드는 이미지를 지웁니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.PictureBox>
- <xref:System.Drawing.Image.FromFile%2A?displayProperty=nameWithType>
- [PictureBox 컨트롤 개요](picturebox-control-overview-windows-forms.md)
- [방법: 디자이너를 사용 하 여 그림 로드](how-to-load-a-picture-using-the-designer-windows-forms.md)
- [방법: 런타임에 그림의 크기 또는 위치 수정](how-to-modify-the-size-or-placement-of-a-picture-at-run-time-windows-forms.md)
- [PictureBox 컨트롤](picturebox-control-windows-forms.md)
