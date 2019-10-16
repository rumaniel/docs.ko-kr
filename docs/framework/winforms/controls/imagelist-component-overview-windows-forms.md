---
title: ImageList 구성 요소 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- ImageList
helpviewer_keywords:
- collection controls [Windows Forms], images
- icon list control
- ImageList component [Windows Forms], about ImageList component
ms.assetid: 7e25d89b-5633-40c1-afc3-82e0e301ffa2
ms.openlocfilehash: d4513439594c9bceac3463a5b878f9059a16046e
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645692"
---
# <a name="imagelist-component-overview-windows-forms"></a>ImageList 구성 요소 개요(Windows Forms)

Windows Forms <xref:System.Windows.Forms.ImageList> 구성 요소는 컨트롤에 의해 표시될 수 있는 이미지를 저장하는 데 사용됩니다. 이미지 목록을 통해 일관된 단일 이미지 카탈로그에 대한 코드를 작성할 수 있습니다. 예를 들어 단추의 <xref:System.Windows.Forms.ButtonBase.ImageIndex%2A> 또는 <xref:System.Windows.Forms.ButtonBase.ImageKey%2A> 속성을 변경하여 <xref:System.Windows.Forms.Button> 컨트롤에 의해 표시되는 이미지를 회전할 수 있습니다. 동일한 이미지 목록을 여러 컨트롤에 연결할 수도 있습니다. 예를 들어 <xref:System.Windows.Forms.ListView> 컨트롤과 <xref:System.Windows.Forms.TreeView> 컨트롤 둘 다를 사용하여 동일한 파일 목록을 표시하는 경우 이미지 목록에서 파일 아이콘을 변경하면 두 보기에 모두 새 아이콘이 나타납니다.

## <a name="using-imagelist-with-controls"></a>컨트롤과 함께 ImageList 사용

`ImageList` 속성 또는 <xref:System.Windows.Forms.ListView> 컨트롤의 경우 <xref:System.Windows.Forms.ListView.SmallImageList%2A> 및 <xref:System.Windows.Forms.ListView.LargeImageList%2A> 속성이 있는 모든 컨트롤과 함께 이미지 목록을 사용할 수 있습니다. 이미지 목록에 연결할 수 있는 컨트롤에는 <xref:System.Windows.Forms.ListView>, <xref:System.Windows.Forms.TreeView>, <xref:System.Windows.Forms.ToolBar>, <xref:System.Windows.Forms.TabControl>, <xref:System.Windows.Forms.Button>, <xref:System.Windows.Forms.CheckBox>, <xref:System.Windows.Forms.RadioButton> 및 <xref:System.Windows.Forms.Label> 컨트롤이 포함됩니다. 이미지 목록을 컨트롤에 연결하려면 컨트롤의 `ImageList` 속성을 <xref:System.Windows.Forms.ImageList> 구성 요소의 이름으로 설정합니다.

## <a name="key-properties"></a>키 속성

<xref:System.Windows.Forms.ImageList> 구성 요소의 키 속성은 연결된 컨트롤에서 사용할 그림을 포함하는 <xref:System.Windows.Forms.ImageList.Images%2A>입니다. 인덱스 값이나 해당 키를 통해 각 개별 이미지에 액세스할 수 있습니다. <xref:System.Windows.Forms.ImageList.ColorDepth%2A> 속성은 이미지 렌더링에 사용되는 색 수를 결정합니다. 이미지는 모두 <xref:System.Windows.Forms.ImageList.ImageSize%2A> 속성에 설정된 동일한 크기로 표시됩니다. 더 큰 이미지는 적절하게 크기가 조정됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ImageList>
- [방법: Windows Forms ImageList 구성 요소를 사용 하 여 이미지 추가 또는 제거](how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)
