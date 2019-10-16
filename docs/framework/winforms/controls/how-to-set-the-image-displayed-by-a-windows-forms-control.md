---
title: '방법: Windows Forms 컨트롤에서 표시하는 이미지 설정'
ms.date: 08/20/2019
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Button control [Windows Forms], images
- Windows Forms controls, images
- controls [Windows Forms], images
- images [Windows Forms], Windows Forms controls
- examples [Windows Forms], controls
ms.assetid: 9445af8f-4f62-48b0-a3f6-068058964b9f
ms.openlocfilehash: b1b1dbbb50c3b19cf8d8a7d7030d0bc168afb6a7
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666197"
---
# <a name="how-to-set-the-image-displayed-by-a-windows-forms-control"></a>방법: Windows Forms 컨트롤에 의해 표시 되는 이미지 설정

여러 가지 Windows Forms 컨트롤에서 이미지를 표시할 수 있습니다. 이러한 이미지는 저장 명령을 나타내는 단추의 디스켓 아이콘 처럼 컨트롤의 용도를 명확히 나타내는 아이콘 일 수 있습니다. 또는 원하는 모양과 동작을 컨트롤에 제공 하기 위해 아이콘을 배경 이미지로 사용할 수 있습니다.

## <a name="programmatic"></a>기능의

컨트롤의 `Image` 또는 `BackgroundImage` 속성을 형식의 <xref:System.Drawing.Image>개체로 설정 합니다. 일반적으로 메서드를 <xref:System.Drawing.Image.FromFile%2A> 사용 하 여 파일에서 이미지를 로드 합니다.

다음 코드 예제에서 이미지의 위치에 대해 설정 된 경로는 **내 그림** 폴더입니다. Windows 운영 체제를 실행 하는 대부분의 컴퓨터는이 디렉터리를 포함 합니다. 이를 통해 최소한의 시스템 액세스 수준을 가진 사용자도 응용 프로그램을 안전 하 게 실행할 수 있습니다. 다음 코드 예제를 사용 하려면 <xref:System.Windows.Forms.PictureBox> 컨트롤이 추가 된 폼이 이미 있어야 합니다.

```vb
' Replace the image named below with your own icon.
PictureBox1.Image = Image.FromFile _
   (System.Environment.GetFolderPath _
   (System.Environment.SpecialFolder.MyPictures) _
   & "\Image.gif")
```

```csharp
// Replace the image named below with your own icon.
// Note the escape character used (@) when specifying the path.
pictureBox1.Image = Image.FromFile
   (System.Environment.GetFolderPath
   (System.Environment.SpecialFolder.MyPictures)
   + @"\Image.gif");
```

```cpp
// Replace the image named below with your own icon.
pictureBox1->Image = Image::FromFile(String::Concat
   (System::Environment::GetFolderPath
   (System::Environment::SpecialFolder::MyPictures),
   "\\Image.gif"));
```

## <a name="designer"></a>Designer

1. Visual studio의 **속성** 창에서 컨트롤의 **Image** 또는 **BackgroundImage** 속성을 선택 하 고 줄임표 (![Visual Studio](./media/visual-studio-ellipsis-button.png)의 줄임표 단추)를 선택 하 여 select를 표시 합니다.  **리소스** 대화 상자.

2. 표시 하려는 이미지를 선택 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Image.FromFile%2A>
- <xref:System.Drawing.Image>
- <xref:System.Windows.Forms.Control.BackgroundImage%2A>
