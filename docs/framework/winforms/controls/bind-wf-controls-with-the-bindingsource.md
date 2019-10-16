---
title: '방법: 디자이너를 사용하여 Windows Forms 컨트롤에서 BindingSource 구성 요소 바인딩'
ms.date: 03/30/2017
helpviewer_keywords:
- controls [Windows Forms], binding
- BindingSource component [Windows Forms], binding controls
- data binding [Windows Forms], BindingSource component
ms.assetid: 391ae170-de5c-40f8-8233-91cb2ee4683a
ms.openlocfilehash: 180fafa9ace5927fd84ec5dc0a1b2a342f771efd
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040021"
---
# <a name="how-to-bind-windows-forms-controls-with-the-bindingsource-component-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms 컨트롤에서 BindingSource 구성 요소 바인딩
폼에 컨트롤을 추가 하 고 응용 프로그램에 대 한 사용자 인터페이스를 확인 한 후에는 런타임에 사용자가 응용 프로그램과 관련 된 데이터를 변경 하 고 저장할 수 있도록 컨트롤을 데이터 소스에 바인딩할 수 있습니다.

 컨트롤과 컨트롤 Windows Forms을 바인딩하는 것은 <xref:System.Windows.Forms.BindingSource> 컨트롤을 폼의 컨트롤과 데이터 소스 간의 브리지로 연결 하 여 가장 쉽게 수행할 수 있습니다.

 폼에 있는 하나 이상의 컨트롤을 데이터에 바인딩할 수 있습니다. 다음 절차 <xref:System.Windows.Forms.TextBox> 에서는 컨트롤이 데이터 소스에 바인딩되어 있습니다.

 이 절차를 완료 하려면 데이터베이스에서 파생 된 데이터 원본에 바인딩하는 것으로 가정 합니다. 다른 데이터 저장소에서 데이터 원본을 만드는 방법에 대 한 자세한 내용은 [새 데이터 소스 추가](/visualstudio/data-tools/add-new-data-sources)를 참조 하세요.

## <a name="to-bind-a-control-at-design-time"></a>디자인 타임에 컨트롤을 바인딩하려면

1. 컨트롤을 <xref:System.Windows.Forms.TextBox> 폼으로 끌어 옵니다.

2. **속성** 창에서 다음을 수행 합니다.

    1. **(데이터 바인딩)** 노드를 확장 합니다.

    2. <xref:System.Windows.Forms.TextBox.Text%2A> 속성 옆의 화살표를 클릭 합니다.

         **DataSource** UI 형식 편집기가 열립니다.

         프로젝트 또는 폼에 대해 데이터 소스를 이전에 구성한 경우 표시 됩니다.

3. **프로젝트 데이터 소스 추가**를 클릭하여 데이터에 연결한 다음 데이터 소스를 만듭니다.

4. **데이터 소스 구성 마법사** 시작 페이지에서 **다음**을 클릭합니다.

5. **데이터 소스 형식 선택** 페이지에서 **데이터베이스**를 선택 합니다.

6. **데이터 연결 선택** 페이지의 사용 가능한 연결 목록에서 데이터 연결을 선택 합니다. 원하는 데이터 연결을 사용할 수 없는 경우 새 **연결** 을 선택 하 여 새 데이터 연결을 만듭니다.

7. **예, 연결을 저장** 합니다 .를 선택 하 여 응용 프로그램 구성 파일에 연결 문자열을 저장 합니다.

8. 애플리케이션에 바인딩할 데이터베이스 개체를 선택합니다. 이 경우 테이블 <xref:System.Windows.Forms.TextBox> 에서 표시할 필드를 선택 합니다.

9. 원하는 경우 기본 데이터 세트 이름을 바꿉니다.

10. **마침**을 클릭합니다.

11. **속성** 창에서 <xref:System.Windows.Forms.TextBox.Text%2A> 속성 옆의 화살표를 다시 클릭 합니다. **DataSource** UI 형식 편집기에서에 바인딩할 <xref:System.Windows.Forms.TextBox> 필드의 이름을 선택 합니다.

     **DataSource** UI 유형 편집기가 닫히고 데이터 집합 <xref:System.Windows.Forms.BindingSource> 및 해당 데이터 연결과 관련 된 테이블 어댑터가 폼에 추가 됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.BindingSource>
- <xref:System.Windows.Forms.BindingNavigator>
- [새 데이터 소스 추가](/visualstudio/data-tools/add-new-data-sources)
- [데이터 소스 창](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/6ckyxa83(v=vs.120))
