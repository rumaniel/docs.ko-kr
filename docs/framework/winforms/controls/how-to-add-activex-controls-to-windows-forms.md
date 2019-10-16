---
title: '방법: Windows Forms에 ActiveX 컨트롤 추가'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms controls, ActiveX controls
- forms [Windows Forms], adding ActiveX controls
- ActiveX controls [Windows Forms], adding
ms.assetid: 54a61e5b-555e-4887-b41e-6244fed271eb
ms.openlocfilehash: 8c4c6c3f96c49401b032e360314794cc800c0551
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987083"
---
# <a name="how-to-add-activex-controls-to-windows-forms"></a>방법: Windows Forms에 ActiveX 컨트롤 추가

Visual Studio의 Windows Forms 디자이너은 Windows Forms 컨트롤을 호스팅하도록 최적화 되어 있지만 ActiveX 컨트롤을 Windows Forms에 배치할 수도 있습니다.

> [!CAUTION]
> ActiveX 컨트롤이 추가 될 때 Windows Forms에 대 한 성능 제한이 있습니다.

ActiveX 컨트롤을 폼에 추가 하기 전에 도구 상자에 추가 해야 합니다. 자세한 내용은 [COM 구성 요소, 도구 상자 사용자 지정 대화 상자](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/cby6tzh5(v=vs.100))를 참조 하세요.

## <a name="add-an-activex-control-to-your-windows-form"></a>Windows Form에 ActiveX 컨트롤 추가

Windows Form에 ActiveX 컨트롤을 추가 하려면 도구 상자에서 컨트롤을 두 번 클릭 합니다.

Visual Studio는 프로젝트의 컨트롤에 대 한 모든 참조를 추가 합니다. Windows Forms에서 ActiveX 컨트롤을 사용할 때 고려해 야 할 사항에 대 한 자세한 내용은 [Windows Form에서 Activex 컨트롤을 호스팅할 때의 고려 사항](considerations-when-hosting-an-activex-control-on-a-windows-form.md)을 참조 하세요.

> [!NOTE]
> Activex 컨트롤 가져오기 (Aximp.exe) Windows Forms activex 동적 연결 라이브러리를 가져올 때 예상과 다른 형식의 이벤트 인수를 만듭니다. Aximp.exe에서 생성 되는 인수는가 필요한 경우 `Invoke(object sender, DWebBrowserEvents2_ProgressChangeEvent e)` `Invoke(object sender, DWebBrowserEvents2_ProgressChangeEventArgs e)` 와 유사 합니다. 이 irregularity는 코드가 정상적으로 작동 하는 것을 방지 하지 않습니다. 자세한 내용은 [Windows Forms ActiveX 컨트롤 가져오기 (aximp.exe)](../../tools/aximp-exe-windows-forms-activex-control-importer.md)를 참조 하세요.

## <a name="see-also"></a>참고자료

- [Windows Forms 컨트롤](index.md)
- [여러 언어 및 라이브러리에서 사용되는 컨트롤 및 프로그래밍 가능한 개체 비교](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/0061wezk(v=vs.100))
- [방법: Windows Forms에 컨트롤 추가](how-to-add-controls-to-windows-forms.md)
- [개별 Windows Forms 컨트롤 레이블 지정 및 바로 가기 제공](labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
- [기능별 Windows Forms 컨트롤](windows-forms-controls-by-function.md)
