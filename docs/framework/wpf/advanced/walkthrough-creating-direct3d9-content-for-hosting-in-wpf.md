---
title: '연습: WPF에서 호스팅할 Direct3D9 콘텐츠 만들기'
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- WPF [WPF], creating Direct3D9 content
- Direct3D9 [WPF interoperability], creating Direct3D9 content
ms.assetid: 286e98bc-1eaa-4b5e-923d-3490a9cca5fc
ms.openlocfilehash: 462220b526db90d3acfa90a28f9bfd56dbe813e2
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991405"
---
# <a name="walkthrough-creating-direct3d9-content-for-hosting-in-wpf"></a>연습: WPF에서 호스팅할 Direct3D9 콘텐츠 만들기
이 연습에서는 Windows Presentation Foundation (WPF) 응용 프로그램에서 호스트 하는 데 적합 한 Direct3D9 콘텐츠를 만드는 방법을 보여 줍니다. WPF 응용 프로그램에서 Direct3D9 콘텐츠를 호스트 하는 방법에 대 한 자세한 내용은 [wpf 및 Direct3d9 상호 운용성](wpf-and-direct3d9-interoperation.md)을 참조 하세요.

 이 연습에서는 다음 작업을 수행합니다.

- Direct3D9 프로젝트를 만듭니다.

- WPF 응용 프로그램에서 호스팅을 위한 Direct3D9 프로젝트를 구성 합니다.

 작업이 완료 되 면 WPF 응용 프로그램에서 사용할 수 있도록 Direct3D9 콘텐츠를 포함 하는 DLL이 만들어집니다.

## <a name="prerequisites"></a>필수 구성 요소
 이 연습을 완료하려면 다음 구성 요소가 필요합니다.

- Visual Studio 2010

- DirectX SDK 9 이상

## <a name="creating-the-direct3d9-project"></a>Direct3D9 프로젝트 만들기
 첫 번째 단계는 Direct3D9 프로젝트를 만들고 구성 하는 것입니다.

#### <a name="to-create-the-direct3d9-project"></a>Direct3D9 프로젝트를 만들려면

1. C++ 이라는`D3DContent`새 Win32 프로젝트를 만듭니다.

     Win32 응용 프로그램 마법사가 열리고 시작 화면이 표시 됩니다.

2. **다음**을 클릭합니다.

     응용 프로그램 설정 화면이 나타납니다.

3. **응용 프로그램 종류:** 섹션에서 **DLL** 옵션을 선택 합니다.

4. **마침**을 클릭합니다.

     D3DContent 프로젝트가 생성 됩니다.

5. 솔루션 탐색기에서 D3DContent 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.

     **D3DContent 속성 페이지** 대화 상자가 열립니다.

6. **C/C++**  노드를 선택 합니다.

7. **추가 포함 디렉터리** 필드에서 DirectX Include 폴더의 위치를 지정 합니다. 이 폴더의 기본 위치는%ProgramFiles%\Microsoft DirectX SDK (*version*) \Include.입니다.

8. **링커** 노드를 두 번 클릭 하 여 확장 합니다.

9. **추가 라이브러리 디렉터리** 필드에서 DirectX 라이브러리 폴더의 위치를 지정 합니다. 이 폴더의 기본 위치는%ProgramFiles%\Microsoft DirectX SDK (*version*) \Lib\x86.입니다.

10. **입력** 노드를 선택 합니다.

11. **추가 종속성** 필드에 `d3d9.lib` 및 `d3dx9.lib` 파일을 추가 합니다.

12. 솔루션 탐색기에서 라는 `D3DContent.def` 새 모듈 정의 파일 (.def)을 프로젝트에 추가 합니다.

## <a name="creating-the-direct3d9-content"></a>Direct3D9 콘텐츠 만들기
 최상의 성능을 얻으려면 Direct3D9 콘텐츠에서 특정 설정을 사용 해야 합니다. 다음 코드에서는 최상의 성능 특성이 있는 Direct3D9 화면을 만드는 방법을 보여 줍니다. 자세한 내용은 [Direct3D9 및 WPF 상호 운용성을 위한 성능 고려 사항](performance-considerations-for-direct3d9-and-wpf-interoperability.md)합니다.

#### <a name="to-create-the-direct3d9-content"></a>Direct3D9 콘텐츠를 만들려면

1. 솔루션 탐색기를 사용 하 여 C++ 프로젝트에 다음의 세 가지 클래스를 추가 합니다.

     `CRenderer`(가상 소멸자 포함)

     `CRendererManager`

     `CTriangleRenderer`

2. 코드 편집기에서 렌더러를 열고 자동으로 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#RendererH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.h#rendererh)]

3. 코드 편집기에서 렌더러를 열고 자동으로 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#RendererCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderercpp)]

4. 코드 편집기에서 RendererManager .h를 열고 자동으로 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.h#renderermanagerh)]

5. 코드 편집기에서 RendererManager .cpp를 열고 자동으로 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanagercpp)]

6. 코드 편집기에서 TriangleRenderer을 열고 자동으로 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.h#trianglerendererh)]

7. 코드 편집기에서 TriangleRenderer을 열고 자동으로 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.cpp#trianglerenderercpp)]

8. 코드 편집기에서 stdafx.h를 열고 자동으로 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#StdafxH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/stdafx.h#stdafxh)]

9. 코드 편집기에서 dllmain을 열고 자동으로 생성 된 코드를 다음 코드로 바꿉니다.

     [!code-cpp[System.Windows.Interop.D3DImage#DllMain](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/dllmain.cpp#dllmain)]

10. 코드 편집기에서 D3DContent를 엽니다.

11. 자동으로 생성 된 코드를 다음 코드로 바꿉니다.

    ```cpp
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

- WPF 응용 프로그램에서 Direct3D9 콘텐츠를 호스팅합니다. 자세한 내용은 [연습: WPF](walkthrough-hosting-direct3d9-content-in-wpf.md)에서 Direct3D9 콘텐츠 호스팅

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Interop.D3DImage>
- [Direct3D9 및 WPF 상호 운용성을 위한 성능 고려 사항](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
- [연습: WPF에서 Direct3D9 콘텐츠 호스팅](walkthrough-hosting-direct3d9-content-in-wpf.md)
