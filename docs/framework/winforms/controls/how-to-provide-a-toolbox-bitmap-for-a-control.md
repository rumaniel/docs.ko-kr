---
title: '방법: 컨트롤에 대한 도구 상자 비트맵 제공'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Toolbox [Windows Forms], adding bitmaps for custom controls
- custom controls [Windows Forms], Toolbox bitmaps
- bitmaps [Windows Forms], custom controls
ms.assetid: 0ed0840a-616d-41ba-a27d-3573241932ad
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e6da7318ba481af721a9220c8f71af2a18e764a3
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015783"
---
# <a name="how-to-provide-a-toolbox-bitmap-for-a-control"></a>방법: 컨트롤에 대한 도구 상자 비트맵 제공

Visual Studio의 **도구 상자** 에 컨트롤에 대 한 특별 한 아이콘을 표시 하려면를 사용 하 <xref:System.Drawing.ToolboxBitmapAttribute>여 특정 이미지를 지정 하면 됩니다. 이 클래스는 *특성*이라는 다른 클래스에 연결할 수 있는 특수한 유형의 클래스입니다. 특성에 대 한 자세한 내용은 Visual Basic 또는 [특성C#](../../../csharp/programming-guide/concepts/attributes/index.md) 에 대 한 [특성 개요 (Visual Basic)](../../../visual-basic/programming-guide/concepts/attributes/index.md) 를 참조 C#하세요.

<xref:System.Drawing.ToolboxBitmapAttribute>을 사용 하 여 16 x 16 픽셀 비트맵의 경로 및 파일 이름을 나타내는 문자열을 지정할 수 있습니다. 그런 다음 이 비트맵은 **도구 상자**에 추가될 때 컨트롤 옆에 표시됩니다. 를 지정할 <xref:System.Type>수도 있습니다 .이 경우 해당 형식과 연결 된 비트맵이 로드 됩니다. <xref:System.Type> 및 문자열을 모두 지정 하는 경우 컨트롤은 <xref:System.Type> 매개 변수로 지정 된 형식을 포함 하는 어셈블리의 문자열 매개 변수로 지정 된 이름을 사용 하 여 이미지 리소스를 검색 합니다.

## <a name="to-specify-a-toolbox-bitmap-for-your-control"></a>컨트롤의 도구 상자 비트맵을 지정하려면

1. Visual Basic <xref:System.Drawing.ToolboxBitmapAttribute> 의 `Class` 키워드 앞 및 시각적 개체 C#선언 위에 있는 컨트롤의 클래스 선언에를 추가 합니다.

    ```vb
    ' Specifies the bitmap associated with the Button type.
    <ToolboxBitmap(GetType(Button))> Class MyControl1
    ' Specifies a bitmap file.
    End Class
    <ToolboxBitmap("C:\Documents and Settings\Joe\MyPics\myImage.bmp")> _
       Class MyControl2
    End Class
    ' Specifies a type that indicates the assembly to search, and the name
    ' of an image resource to look for.
    <ToolboxBitmap(GetType(MyControl), "MyControlBitmap")> Class MyControl
    End Class
    ```

    ```csharp
    // Specifies the bitmap associated with the Button type.
    [ToolboxBitmap(typeof(Button))]
    class MyControl1 : UserControl
    {
    }
    // Specifies a bitmap file.
    [ToolboxBitmap(@"C:\Documents and Settings\Joe\MyPics\myImage.bmp")]
    class MyControl2 : UserControl
    {
    }
    // Specifies a type that indicates the assembly to search, and the name
    // of an image resource to look for.
    [ToolboxBitmap(typeof(MyControl), "MyControlBitmap")]
    class MyControl : UserControl
    {
    }
    ```

2. 프로젝트를 다시 빌드합니다.

    > [!NOTE]
    > 비트맵은 자동으로 생성된 컨트롤 및 구성 요소의 도구 상자에 나타나지 않습니다. 비트맵을 보려면 **도구 상자 항목 선택** 대화 상자를 사용하여 컨트롤을 다시 로드합니다. 자세한 내용은 [연습: 도구 상자에 사용자 지정 구성 요소](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)를 자동으로 채웁니다.

## <a name="see-also"></a>참고자료

- <xref:System.Drawing.ToolboxBitmapAttribute>
- [연습: 사용자 지정 구성 요소를 사용 하 여 도구 상자 자동 채우기](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)
- [디자인 타임에 Windows Forms 컨트롤 개발](developing-windows-forms-controls-at-design-time.md)
- [특성 개요(Visual Basic)](../../../visual-basic/programming-guide/concepts/attributes/index.md)
- [특성(C#)](../../../csharp/programming-guide/concepts/attributes/index.md)
