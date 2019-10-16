---
title: '방법: Windows Forms ImageList 구성 요소를 사용하여 이미지 추가 또는 제거'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- images [Windows Forms], removing from ImageList component
- images [Windows Forms], storing for controls
- ImageList component [Windows Forms], adding images
- ImageList component [Windows Forms], removing images
- images [Windows Forms], adding to ImageList component
- images [Windows Forms], displaying with controls
ms.assetid: c5eacc56-f769-4e2e-bfb7-f756620913db
ms.openlocfilehash: 430b7f573b115c21b9e2fa87f0ace74205717285
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925114"
---
# <a name="how-to-add-or-remove-images-with-the-windows-forms-imagelist-component"></a>방법: Windows Forms ImageList 구성 요소를 사용하여 이미지 추가 또는 제거
일반적으로 <xref:System.Windows.Forms.ImageList> Windows Forms 구성 요소는 컨트롤과 연결 되기 전에 이미지로 채워집니다. 그러나 이미지 목록을 컨트롤과 연결한 후에 이미지를 추가 하 고 제거할 수 있습니다.  
  
> [!NOTE]
> 이미지를 제거할 때 연결 된 컨트롤의 <xref:System.Windows.Forms.ButtonBase.ImageIndex%2A> 속성이 여전히 유효한 지 확인 합니다.  
  
### <a name="to-add-images-programmatically"></a>프로그래밍 방식으로 이미지를 추가 하려면  
  
- <xref:System.Windows.Forms.ImageList.ImageCollection.Add%2A> 이미지<xref:System.Windows.Forms.ImageList.Images%2A> 목록의 속성 메서드를 사용 합니다.  
  
     다음 코드 예제에서 이미지의 위치에 대해 설정 된 경로는 **내 문서** 폴더입니다. 이 위치는 Windows 운영 체제를 실행 하는 대부분의 컴퓨터에이 폴더가 포함 될 수 있다고 가정할 수 있으므로 사용 됩니다. 이 위치를 선택 하면 최소한의 시스템 액세스 수준이 있는 사용자도 응용 프로그램을 안전 하 게 실행할 수 있습니다. 다음 코드 예제를 사용 하려면 <xref:System.Windows.Forms.ImageList> 컨트롤이 이미 추가 된 폼이 있어야 합니다.  
  
    ```vb  
    Public Sub LoadImage()  
       Dim myImage As System.Drawing.Image = _  
         Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
       ImageList1.Images.Add(myImage)  
    End Sub  
    ```  
  
    ```csharp  
    public void addImage()  
    {  
    // Be sure that you use an appropriate escape sequence (such as the   
    // @) when specifying the location of the file.  
       System.Drawing.Image myImage =   
         Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Image.gif");  
       imageList1.Images.Add(myImage);  
    }  
    ```  
  
    ```cpp  
    public:  
       void addImage()  
       {  
       // Replace the bold image in the following sample   
       // with your own icon.  
       // Be sure that you use an appropriate escape sequence (such as   
       // \\) when specifying the location of the file.  
          System::Drawing::Image ^ myImage =   
             Image::FromFile(String::Concat(  
             System::Environment::GetFolderPath(  
             System::Environment::SpecialFolder::Personal),  
             "\\Image.gif"));  
          imageList1->Images->Add(myImage);  
       }  
    ```  
  
### <a name="to-add-images-with-a-key-value"></a>키 값이 포함 된 이미지를 추가 하려면입니다.  
  
- 키 값을 사용 <xref:System.Windows.Forms.ImageList.ImageCollection.Add%2A> 하는 이미지 <xref:System.Windows.Forms.ImageList.Images%2A> 목록 속성의 메서드 중 하나를 사용 합니다.  
  
     다음 코드 예제에서 이미지의 위치에 대해 설정 된 경로는 **내 문서** 폴더입니다. 이 위치는 Windows 운영 체제를 실행 하는 대부분의 컴퓨터에이 폴더가 포함 될 수 있다고 가정할 수 있으므로 사용 됩니다. 이 위치를 선택 하면 최소한의 시스템 액세스 수준이 있는 사용자도 응용 프로그램을 안전 하 게 실행할 수 있습니다. 다음 코드 예제를 사용 하려면 <xref:System.Windows.Forms.ImageList> 컨트롤이 이미 추가 된 폼이 있어야 합니다.  
  
    ```vb  
    Public Sub LoadImage()  
       Dim myImage As System.Drawing.Image = _  
         Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
       ImageList1.Images.Add("myPhoto", myImage)  
    End Sub  
    ```  
  
```csharp  
public void addImage()  
{  
// Be sure that you use an appropriate escape sequence (such as the   
// @) when specifying the location of the file.  
   System.Drawing.Image myImage =   
     Image.FromFile  
   (System.Environment.GetFolderPath  
   (System.Environment.SpecialFolder.Personal)  
   + @"\Image.gif");  
   imageList1.Images.Add("myPhoto", myImage);  
}  
```  
  
### <a name="to-remove-all-images-programmatically"></a>모든 이미지를 프로그래밍 방식으로 제거 하려면  
  
- 단일 이미지 <xref:System.Windows.Forms.ImageList.ImageCollection.Remove%2A> 를 제거 하려면 메서드를 사용 합니다.  
  
     ,-또는-  
  
     메서드를 <xref:System.Windows.Forms.ImageList.ImageCollection.Clear%2A> 사용 하 여 이미지 목록의 모든 이미지를 지웁니다.  
  
    ```vb  
    ' Removes the first image in the image list  
    ImageList1.Images.Remove(myImage)  
    ' Clears all images in the image list  
    ImageList1.Images.Clear()  
    ```  
  
```csharp  
// Removes the first image in the image list.  
imageList1.Images.Remove(myImage);  
// Clears all images in the image list.  
imageList1.Images.Clear();  
```  
  
### <a name="to-remove-images-by-key"></a>키로 이미지를 제거 하려면  
  
- 키를 <xref:System.Windows.Forms.ImageList.ImageCollection.RemoveByKey%2A> 사용 하 여 단일 이미지를 제거 하려면 메서드를 사용 합니다.  
  
    ```vb  
    ' Removes the image named "myPhoto" from the list.  
    ImageList1.Images.RemoveByKey("myPhoto")  
    ```  
  
```csharp  
// Removes the image named "myPhoto" from the list.  
imageList1.Images.RemoveByKey("myPhoto");  
```  
  
## <a name="see-also"></a>참고자료

- [ImageList 구성 요소](imagelist-component-windows-forms.md)
- [ImageList 구성 요소 개요](imagelist-component-overview-windows-forms.md)
- [이미지, 비트맵 및 메타파일](../advanced/images-bitmaps-and-metafiles.md)
