---
title: '방법: Windows Form에 단순 바인딩된 컨트롤 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [Windows Forms], simple data binding
- Windows Forms controls, data binding
ms.assetid: 3bcaded8-0f1a-4cc0-8830-f59be253bf4e
ms.openlocfilehash: df87f00e6e03de67c3fb1adc28472c96f4a47ef4
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015628"
---
# <a name="how-to-create-a-simple-bound-control-on-a-windows-form"></a>방법: Windows Form에 단순 바인딩된 컨트롤 만들기

*단순 바인딩을*사용 하면 데이터 집합 테이블의 열 값과 같은 단일 데이터 요소를 컨트롤에 표시할 수 있습니다. 컨트롤의 모든 속성을 데이터 값에 단순 하 게 바인딩할 수 있습니다.

## <a name="to-simple-bind-a-control"></a>컨트롤을 간단 하 게 바인딩하려면

1. 데이터 소스에 연결합니다. 자세한 내용은 [데이터 원본에 연결](../data/adonet/connecting-to-a-data-source.md)을 참조 하세요.

2. Visual Studio의 폼에서 컨트롤을 선택 하 고 **속성** 창을 표시 합니다.

3. **(데이터 바인딩)** 속성을 확장 합니다.

     가장 자주 바인딩되는 속성은 **(데이터 바인딩)** 속성 아래에 표시 됩니다. 예를 들어 대부분의 컨트롤에서 **Text** 속성은 가장 자주 바인딩됩니다.

4. 바인딩하려는 속성이 일반적으로 바인딩되는 속성 중 하나가 아닌 경우 (고급) 상자의 **줄임표** ![단추 (...)를 클릭 하 여 **(고급)** 상자의 줄임표 단추 (... 속성 창)를](./media/how-to-create-a-simple-bound-control-on-a-windows-form/visual-studio-ellipsis-button.png)클릭 하 여 다음을 표시 **합니다. 서식 지정 및 고급 바인딩** 대화 상자를 사용 하 여 해당 컨트롤의 전체 속성 목록을 표시 합니다.

5. 바인딩할 속성을 선택 하 고 **바인딩**아래의 드롭다운 화살표를 클릭 합니다.

     사용 가능한 데이터 소스 목록이 표시됩니다.

6. 원하는 단일 데이터 요소를 찾을 때까지 바인딩할 데이터 소스를 확장합니다. 예를 들어 데이터 세트의 테이블에서 열 값에 바인딩할 경우 데이터 세트 이름을 확장하고 나서 테이블을 이름을 확장하여 열 이름을 표시합니다.

7. 바인딩할 요소 이름을 클릭합니다.

8. **서식 지정 및 고급 바인딩** 대화 상자에서 작업 하는 경우 **확인** 을 클릭 하 여 **속성** 창으로 돌아갑니다.

9. 컨트롤의 추가 속성을 바인딩하려면 3 ~ 7 단계를 반복 합니다.

    > [!NOTE]
    > 단순 바인딩된 컨트롤은 단일 데이터 요소만 표시 하기 때문에 단순 바인딩된 컨트롤을 사용 하 여 Windows Form에 탐색 논리를 포함 하는 것이 매우 일반적입니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Binding>
- [Windows Forms 데이터 바인딩](windows-forms-data-binding.md)
- [데이터 바인딩 및 Windows Forms](data-binding-and-windows-forms.md)
