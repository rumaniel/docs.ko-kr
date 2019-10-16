---
title: '방법: 파일 대화 상자에 사용자 지정 위치 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Custom Place to dialog box
- adding Custom Place to dialog box
- CustomPlaces collection
ms.assetid: 63f6469b-59cd-40f6-9e61-8b5831856780
ms.openlocfilehash: 824c948fafd0a0995ad261389414d2d79918c8a1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916346"
---
# <a name="how-to-add-a-custom-place-to-a-file-dialog-box"></a>방법: 파일 대화 상자에 사용자 지정 위치 추가
[!INCLUDE[wiprlhext](../../../../includes/wiprlhext-md.md)]의 기본 열기 및 저장 대화 상자 왼쪽에는 **즐겨찾기 링크**라는 영역이 있습니다. 이 영역을 사용자 지정 위치라고 합니다. 및 클래스를 사용 하 여 <xref:System.Windows.Forms.FileDialog.CustomPlaces%2A> 컬렉션에 폴더를 추가할 수 있습니다. <xref:System.Windows.Forms.SaveFileDialog> <xref:System.Windows.Forms.OpenFileDialog>  
  
> [!NOTE]
> <xref:System.Windows.Forms.OpenFileDialog> 사용자 지정 위치가 `true` 또는 <xref:System.Windows.Forms.SaveFileDialog>에 표시 되려면 속성을 (기본값)로 설정 해야 합니다. <xref:System.Windows.Forms.FileDialog.AutoUpgradeEnabled%2A>  
  
### <a name="to-add-a-custom-place-to-a-file-dialog-box"></a>파일 대화 상자에 사용자 지정 위치를 추가하려면  
  
- 대화 상자의 <xref:System.Windows.Forms.FileDialogCustomPlace> <xref:System.Windows.Forms.FileDialog.CustomPlaces%2A> 컬렉션에 경로, 알려진 폴더 GUID 또는 개체를 추가 합니다.  
  
     다음 코드 예제에서는 경로를 추가하는 방법을 보여 줍니다.  
  
    ```vb  
    OpenFileDialog1.CustomPlaces.Add("C:\MyCustomPlace")  
    ```  
  
    ```csharp  
    openFileDialog1.CustomPlaces.Add("C:\\MyCustomPlace");  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.FileDialog>
- <xref:System.Windows.Forms.FileDialogCustomPlacesCollection.Add%2A?displayProperty=nameWithType>
- [파일 대화 상자의 사용자 지정 위치에 대한 알려진 폴더 GUID](known-folder-guids-for-file-dialog-custom-places.md)
