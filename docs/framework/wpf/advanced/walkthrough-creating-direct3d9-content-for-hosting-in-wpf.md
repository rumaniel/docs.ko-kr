---
title: '연습: WPF에서 호스팅할 Direct3D9 콘텐츠 만들기'
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- WPF [WPF], creating Direct3D9 content
- Direct3D9 [WPF interoperability], creating Direct3D9 content
ms.assetid: 286e98bc-1eaa-4b5e-923d-3490a9cca5fc
ms.openlocfilehash: 321c4ba8659bd2226fff96e74e81ef24f0077c3d
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200916"
---
# <a name="walkthrough-creating-direct3d9-content-for-hosting-in-wpf"></a>연습: WPF에서 호스팅할 Direct3D9 콘텐츠 만들기
이 연습에는 Windows Presentation Foundation (WPF) 응용 프로그램에서 호스팅에 적합 한 Direct3D9 콘텐츠를 만드는 방법을 보여 줍니다. WPF 응용 프로그램에서 호스팅할 Direct3D9 콘텐츠 호스팅에 대 한 자세한 내용은 참조 하세요. [WPF 및 Direct3D9 상호 운용성](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md)합니다.

 이 연습에서는 다음 작업을 수행합니다.

-   Direct3D9 프로젝트를 만듭니다.

-   WPF 응용 프로그램에서 호스팅용 Direct3D9 프로젝트를 구성 합니다.

 작업을 완료 하는 경우에 WPF 응용 프로그램에서 호스팅할 Direct3D9 콘텐츠를 포함 하는 DLL 해야 합니다.

## <a name="prerequisites"></a>전제 조건
 이 연습을 완료하려면 다음 구성 요소가 필요합니다.

-   Visual Studio 2010

-   DirectX SDK 9or에 나중에 해당 합니다.

## <a name="creating-the-direct3d9-project"></a>Direct3D9 프로젝트 만들기
 첫 번째 단계는 Direct3D9 프로젝트 만들기 및 구성 하는 것입니다.

#### <a name="to-create-the-direct3d9-project"></a>Direct3D9 프로젝트를 만들려면

1.  명명 된 c + +에서 새 Win32 프로젝트를 만들 `D3DContent`합니다.

     Win32 응용 프로그램 마법사가 열리고 시작 화면을 표시 합니다.

2.  **다음**을 클릭합니다.

     응용 프로그램 설정 화면이 나타납니다.

3.  에 **응용 프로그램 유형:** 섹션에서 합니다 **DLL** 옵션입니다.

4.  **마침**을 클릭합니다.

     D3DContent 프로젝트가 생성 됩니다.

5.  솔루션 탐색기에서 D3DContent 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.

     합니다 **D3DContent 속성 페이지** 대화 상자가 열립니다.

6.  선택 된 **C/c + +** 노드.

7.  에 **Additional Include Directories** 필드에 폴더를 포함 하는 DirectX의 위치를 지정 합니다. 이 폴더에 대 한 기본 위치는 %ProgramFiles%\Microsoft DirectX SDK (*버전*) \Include 합니다.

8.  두 번 클릭 합니다 **링커** 노드를 확장 합니다.

9. 에 **추가 라이브러리 디렉터리** 필드, DirectX 라이브러리 폴더의 위치를 지정 합니다. 이 폴더에 대 한 기본 위치는 %ProgramFiles%\Microsoft DirectX SDK (*버전*) \Lib\x86 합니다.

10. 선택 된 **입력** 노드.

11. 에 **추가 종속성** 필드를 추가 합니다 `d3d9.lib` 및 `d3dx9.lib` 파일입니다.

12. 솔루션 탐색기에서 새 모듈 정의 파일 (.def) 라는 추가 `D3DContent.def` 프로젝트에 있습니다.

## <a name="creating-the-direct3d9-content"></a>Direct3D9 콘텐츠 만들기
 최상의 성능을 얻으려면, Direct3D9 콘텐츠 특정 설정을 사용 해야 합니다. 다음 코드에는 최상의 성능 특징이 있는 Direct3D9 화면을 만드는 방법을 보여 줍니다. 자세한 내용은 [Direct3D9 및 WPF 상호 운용성을 위한 성능 고려 사항](../../../../docs/framework/wpf/advanced/performance-considerations-for-direct3d9-and-wpf-interoperability.md)합니다.

#### <a name="to-create-the-direct3d9-content"></a>에 Direct3D9 콘텐츠 만들기

1.  솔루션 탐색기를 사용 하면 다음 프로젝트에 세 개의 c + + 클래스를 추가 합니다.

     `CRenderer` (사용 하 여 가상 소멸자)

     `CRendererManager`

     `CTriangleRenderer`

2.  Renderer.h 코드 편집기에서 열고 자동 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#RendererH](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.h#rendererh)]

3.  Renderer.cpp 코드 편집기에서 열고 자동 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#RendererCPP](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderercpp)]

4.  RendererManager.h 코드 편집기에서 열고 자동 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerH](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.h#renderermanagerh)]

5.  RendererManager.cpp 코드 편집기에서 열고 자동 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerCPP](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanagercpp)]

6.  TriangleRenderer.h 코드 편집기에서 열고 자동 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererH](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.h#trianglerendererh)]

7.  TriangleRenderer.cpp 코드 편집기에서 열고 자동 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererCPP](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.cpp#trianglerenderercpp)]

8.  Stdafx.h 코드 편집기에서 열고 자동 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#StdafxH](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/stdafx.h#stdafxh)]

9. Dllmain.cpp 코드 편집기에서 열고 자동 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#DllMain](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/dllmain.cpp#dllmain)]

10. D3DContent.def 코드 편집기에서 엽니다.

11. 자동으로 생성 된 코드를 다음 코드로 바꿉니다.

    ```
    LIBRARY "D3DContent"

    EXPORTS

    SetSize
    SetAlpha
    SetNumDesiredSamples
    SetAdapter

    GetBackBufferNoRef
    Render
    Destroy
    ```

12. 프로젝트를 빌드합니다.

## <a name="next-steps"></a>다음 단계

-   WPF 응용 프로그램에서 호스팅할 Direct3D9 콘텐츠를 호스트 합니다. 자세한 내용은 [연습: WPF에서 Direct3D9 콘텐츠 호스팅](../../../../docs/framework/wpf/advanced/walkthrough-hosting-direct3d9-content-in-wpf.md)합니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Windows.Interop.D3DImage>
- [Direct3D9 및 WPF 상호 운용성을 위한 성능 고려 사항](../../../../docs/framework/wpf/advanced/performance-considerations-for-direct3d9-and-wpf-interoperability.md)
- [연습: WPF에서 Direct3D9 콘텐츠 호스팅](../../../../docs/framework/wpf/advanced/walkthrough-hosting-direct3d9-content-in-wpf.md)