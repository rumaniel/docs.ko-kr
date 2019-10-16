---
title: '연습: WPF에서 Direct3D9 콘텐츠 호스팅'
ms.date: 03/30/2017
helpviewer_keywords:
- Direct3D9 [WPF interoperability], hosting Direct3D9 content
- WPF [WPF], hosting Direct3D9 content
ms.assetid: 60983736-0ab5-42cc-8b16-e9fbde261a43
ms.openlocfilehash: 2c31c044aa50a74255a61da1675037ab3d09f615
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053458"
---
# <a name="walkthrough-hosting-direct3d9-content-in-wpf"></a>연습: WPF에서 Direct3D9 콘텐츠 호스팅

이 연습에서는 Windows Presentation Foundation (WPF) 응용 프로그램에서 Direct3D9 콘텐츠를 호스트 하는 방법을 보여 줍니다.

이 연습에서는 다음 작업을 수행합니다.

- Direct3D9 콘텐츠를 호스팅할 WPF 프로젝트를 만듭니다.

- Direct3D9 콘텐츠를 가져옵니다.

- 클래스를 <xref:System.Windows.Interop.D3DImage> 사용 하 여 Direct3D9 콘텐츠를 표시 합니다.

 작업이 완료 되 면 WPF 응용 프로그램에서 Direct3D9 콘텐츠를 호스트 하는 방법을 알게 됩니다.

## <a name="prerequisites"></a>전제 조건

이 연습을 완료하려면 다음 구성 요소가 필요합니다.

- Visual Studio.

- DirectX SDK 9 이상

- WPF 호환 형식으로 Direct3D9 콘텐츠를 포함 하는 DLL입니다. 자세한 내용은 [WPF 및 Direct3D9 상호 운용성](wpf-and-direct3d9-interoperation.md) 및 [연습을 참조 하세요. WPF](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)에서 호스팅할 Direct3D9 콘텐츠 만들기

## <a name="creating-the-wpf-project"></a>WPF 프로젝트 만들기

첫 번째 단계는 WPF 응용 프로그램에 대 한 프로젝트를 만드는 것입니다.

### <a name="to-create-the-wpf-project"></a>WPF 프로젝트를 만들려면

C# 라는`D3DHost`시각적 개체에서 새 WPF 응용 프로그램 프로젝트를 만듭니다. 자세한 내용은 [연습: 내 첫 번째 WPF 데스크톱](../getting-started/walkthrough-my-first-wpf-desktop-application.md)응용 프로그램입니다.

Mainwindow.xaml가에서 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]열립니다.

## <a name="importing-the-direct3d9-content"></a>Direct3D9 콘텐츠 가져오기

특성을 `DllImport` 사용 하 여 관리 되지 않는 DLL에서 Direct3D9 콘텐츠를 가져옵니다.

### <a name="to-import-direct3d9-content"></a>Direct3D9 콘텐츠를 가져오려면

1. 코드 편집기에서 MainWindow.xaml.cs를 엽니다.

2. 자동으로 생성 된 코드를 다음 코드로 바꿉니다.

    [!code-csharp[System.Windows.Interop.D3DImage#1](~/samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml.cs#1)]

## <a name="hosting-the-direct3d9-content"></a>Direct3D9 콘텐츠 호스팅

마지막으로 <xref:System.Windows.Interop.D3DImage> 클래스를 사용 하 여 Direct3D9 콘텐츠를 호스팅합니다.

### <a name="to-host-the-direct3d9-content"></a>Direct3D9 콘텐츠를 호스팅하려면

1. Mainwindow.xaml에서 자동으로 생성 된 XAML을 다음 XAML로 바꿉니다.

    [!code-xaml[System.Windows.Interop.D3DImage#10](~/samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml#10)]

2. 프로젝트를 빌드합니다.

3. Direct3D9 콘텐츠를 포함 하는 DLL을 bin/Debug 폴더에 복사 합니다.

4. F5 키를 눌러 프로젝트를 실행합니다.

    Direct3D9 콘텐츠는 WPF 응용 프로그램 내에 표시 됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Interop.D3DImage>
- [Direct3D9 및 WPF 상호 운용성을 위한 성능 고려 사항](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
