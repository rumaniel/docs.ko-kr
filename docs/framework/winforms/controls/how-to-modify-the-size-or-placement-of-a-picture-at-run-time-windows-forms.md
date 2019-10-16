---
title: '방법: 런타임에 (Windows Forms) 크기 또는 그림의 위치 수정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- images [Windows Forms], controlling placement in PictureBox control [Windows Forms]
- examples [Windows Forms], PictureBox control
- PictureBox control [Windows Forms], picture size and alignment
- pictures [Windows Forms], controlling placement in PictureBox control [Windows Forms]
ms.assetid: d0b332a3-fae2-4891-957c-dc3e17743326
ms.openlocfilehash: 695abf51870ef9164e4543a91b3183e801eee55f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64649247"
---
# <a name="how-to-modify-the-size-or-placement-of-a-picture-at-run-time-windows-forms"></a>방법: 런타임에 (Windows Forms) 크기 또는 그림의 위치 수정
Windows Forms를 사용 하는 경우 <xref:System.Windows.Forms.PictureBox> 컨트롤을 폼에 설정할 수 있습니다는 <xref:System.Windows.Forms.PictureBox.SizeMode%2A> 되도록 속성:  
  
- 그림의 왼쪽된 위 모퉁이 컨트롤의 왼쪽된 위 모퉁이 사용 하 여 정렬  
  
- 컨트롤 내에서 가운데  
  
- 표시 되는 그림에 맞게 컨트롤의 크기를 조정 합니다.  
  
- 컨트롤에 맞게 표시 사진을 스트레치합니다  
  
 (특히 비트맵 형식으로 하나) 그림 늘이기 이미지 품질에서 손실을 생성할 수 있습니다. 메타 파일은 런타임 시 이미지를 그리기 위한 그래픽 명령 목록에는 더 비트맵 보다 스트레치에 적합 합니다.  
  
### <a name="to-set-the-sizemode-property-at-run-time"></a>런타임 시 SizeMode 속성을 설정 하려면  
  
1. 설정 <xref:System.Windows.Forms.PictureBox.SizeMode%2A> 하 <xref:System.Windows.Forms.PictureBoxSizeMode.Normal> (기본값), <xref:System.Windows.Forms.PictureBoxSizeMode.AutoSize>를 <xref:System.Windows.Forms.PictureBoxSizeMode.CenterImage>, 또는 <xref:System.Windows.Forms.PictureBoxSizeMode.StretchImage>합니다. <xref:System.Windows.Forms.PictureBoxSizeMode.Normal> 이미지가 컨트롤의 왼쪽 위 모퉁이;에 배치 되는 방법 이미지 컨트롤 보다 큰 경우 아래쪽 및 오른쪽 가장자리가 클리핑됩니다. <xref:System.Windows.Forms.PictureBoxSizeMode.CenterImage> 이미지 컨트롤 내에서 가운데 정렬 되어 있음을 의미 합니다. 이미지 컨트롤 보다 큰 경우 그림의 외부 가장자리가 클리핑됩니다. <xref:System.Windows.Forms.PictureBoxSizeMode.AutoSize> 컨트롤의 크기는 이미지의 크기 조정 됩니다 것을 의미 합니다. <xref:System.Windows.Forms.PictureBoxSizeMode.StretchImage> 반대로, 이며 의미는 이미지의 크기는 컨트롤의 크기를 조정 됩니다.  
  
     아래 예제에서는 내 문서 폴더는 이미지의 위치에 대 한 설정 되었습니다. 이렇게 하면 수 없으므로 Windows 운영 체제를 실행 하는 대부분의 컴퓨터는이 디렉터리를 포함 합니다. 또한 최소한의 시스템 액세스 수준을 가진 사용자가 안전하게 애플리케이션을 실행할 수 있습니다. 아래 예제에서는 가정 된 폼을 <xref:System.Windows.Forms.PictureBox> 이미 추가 된 컨트롤입니다.  
  
    ```vb  
    Private Sub StretchPic()  
       ' Stretch the picture to fit the control.  
       PictureBox1.SizeMode = PictureBoxSizeMode.StretchImage  
       ' Load the picture into the control.  
       ' You should replace the bold image   
       ' in the sample below with an icon of your own choosing.  
       PictureBox1.Image = Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
    End Sub  
    ```  
  
    ```csharp  
    private void StretchPic(){  
       // Stretch the picture to fit the control.  
       PictureBox1.SizeMode = PictureBoxSizeMode.StretchImage;  
       // Load the picture into the control.  
       // You should replace the bold image   
       // in the sample below with an icon of your own choosing.  
       // Note the escape character used (@) when specifying the path.  
       PictureBox1.Image = Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       + @"\Image.gif")  
    }  
    ```  
  
    ```cpp  
    private:  
       void StretchPic()  
       {  
          // Stretch the picture to fit the control.  
          pictureBox1->SizeMode = PictureBoxSizeMode::StretchImage;  
          // Load the picture into the control.  
          // You should replace the bold image   
          // in the sample below with an icon of your own choosing.  
          pictureBox1->Image = Image::FromFile(String::Concat(  
             System::Environment::GetFolderPath(  
             System::Environment::SpecialFolder::Personal),  
             "\\Image.gif"));  
       }  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.PictureBox>
- [방법: 디자이너를 사용 하 여 그림 로드](how-to-load-a-picture-using-the-designer-windows-forms.md)
- [PictureBox 컨트롤 개요](picturebox-control-overview-windows-forms.md)
- [방법: 런타임에 그림 설정](how-to-set-pictures-at-run-time-windows-forms.md)
- [PictureBox 컨트롤](picturebox-control-windows-forms.md)
