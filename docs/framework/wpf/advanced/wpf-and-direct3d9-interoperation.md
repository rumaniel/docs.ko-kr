---
title: WPF 및 Direct3D9 상호 운용성
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- WPF [WPF], creating Direct3D9 content
- Direct3D9 [WPF interoperability], creating Direct3D9 content
ms.assetid: 1b14b823-69c4-4e8d-99e4-f6dade58f89a
ms.openlocfilehash: 5fccd49b4f6fa64e5902197423d732ba0b31790e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917433"
---
# <a name="wpf-and-direct3d9-interoperation"></a>WPF 및 Direct3D9 상호 운용성
Windows Presentation Foundation (WPF) 응용 프로그램에 Direct3D9 콘텐츠를 포함할 수 있습니다. 이 항목에서는 WPF와 효율적으로 상호 운용 되도록 Direct3D9 콘텐츠를 만드는 방법에 대해 설명 합니다.  
  
> [!NOTE]
> WPF에서 Direct3D9 콘텐츠를 사용 하는 경우 성능에 대해서도 고려해 야 합니다. 성능을 최적화 하는 방법에 대 한 자세한 내용은 [Direct3D9 및 WPF 상호 운용성에 대 한 성능 고려 사항](performance-considerations-for-direct3d9-and-wpf-interoperability.md)을 참조 하세요.  
  
## <a name="display-buffers"></a>버퍼 표시  
 <xref:System.Windows.Interop.D3DImage> 클래스 라고 하는 두 디스플레이 버퍼를 관리 합니다 *백 버퍼* 하며 *프런트 버퍼가*. 백 버퍼는 Direct3D9 화면입니다. 백 버퍼에 대 한 변경 내용은 메서드를 <xref:System.Windows.Interop.D3DImage.Unlock%2A> 호출할 때 front 버퍼에 복사 됩니다.  
  
 다음 그림에서는 백 버퍼와 프런트 버퍼 간의 관계를 보여 줍니다.  
  
 ![D3DImage 표시 버퍼](./media/d3dimage-buffers.png "D3DImage_buffers")  
  
## <a name="direct3d9-device-creation"></a>Direct3D9 장치 만들기  
 Direct3D9 콘텐츠를 렌더링 하려면 Direct3D9 장치를 만들어야 합니다. 장치를 `IDirect3D9` 만드는 데 사용할 수 있는 두 가지 Direct3D9 개체와 `IDirect3D9Ex`가 있습니다. 이러한 개체를 사용 하 `IDirect3DDevice9` 여 `IDirect3DDevice9Ex` 및 장치를 각각 만들 수 있습니다.  
  
 다음 방법 중 하나를 호출 하 여 장치를 만듭니다.  
  
- `IDirect3D9 * Direct3DCreate9(UINT SDKVersion);`  
  
- `HRESULT Direct3DCreate9Ex(UINT SDKVersion, IDirect3D9Ex **ppD3D);`  
  
 Windows Vista 이상 운영 체제에서 WDDM (windows display `Direct3DCreate9Ex` Driver Model)을 사용 하도록 구성 된 디스플레이와 함께 메서드를 사용 합니다. 다른 플랫폼 `Direct3DCreate9` 에서 메서드를 사용 합니다.  
  
### <a name="availability-of-the-direct3dcreate9ex-method"></a>Direct3DCreate9Ex 메서드의 가용성  
 D3d9에는 Windows Vista 이상 `Direct3DCreate9Ex` 운영 체제에만 해당 하는 메서드가 있습니다. Windows XP에서 함수를 직접 연결 하는 경우 응용 프로그램을 로드 하지 못합니다. `Direct3DCreate9Ex` 메서드가 지원 되는지 여부를 확인 하려면 DLL을 로드 하 고 프로시저 주소를 찾습니다. 다음 코드에서는 `Direct3DCreate9Ex` 메서드를 테스트 하는 방법을 보여 줍니다. 전체 코드 예제를 보려면 [연습: WPF](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)에서 호스팅할 Direct3D9 콘텐츠 만들기  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_EnsureD3DObjects](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_ensured3dobjects)]  
  
### <a name="hwnd-creation"></a>HWND 만들기  
 장치를 만들려면 HWND가 필요 합니다. 일반적으로 사용할 Direct3D9에 대 한 더미 HWND를 만듭니다. 다음 코드 예제에서는 더미 HWND를 만드는 방법을 보여 줍니다.  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_EnsureHWND](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_ensurehwnd)]  
  
### <a name="present-parameters"></a>현재 매개 변수  
 장치를 만들려면 `D3DPRESENT_PARAMETERS` 구조체도 필요 하지만 몇 개의 매개 변수만 중요 합니다. 이러한 매개 변수는 메모리 사용 공간을 최소화 하기 위해 선택 됩니다.  
  
 `BackBufferHeight` 및`BackBufferWidth` 필드를 1로 설정 합니다. 이를 0으로 설정 하면 해당 항목을 HWND의 차원으로 설정 합니다.  
  
 항상 `D3DCREATE_MULTITHREADED` 및`D3DCREATE_FPU_PRESERVE` 플래그를 설정 하 여 direct3d9에서 사용 되는 메모리 손상을 방지 하 고 direct3d9에서 FPU 설정을 변경 하지 않도록 합니다.  
  
 다음 코드에서는 `D3DPRESENT_PARAMETERS` 구조체를 초기화 하는 방법을 보여 줍니다.  
  
 [!code-cpp[System.Windows.Interop.D3DImage#Renderer_Init](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderer_init)]  
  
## <a name="creating-the-back-buffer-render-target"></a>백 버퍼 렌더링 대상 만들기  
 에서 <xref:System.Windows.Interop.D3DImage>direct3d9 콘텐츠를 표시 하려면 direct3d9 화면을 만들고 메서드를 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 호출 하 여 할당 합니다.  
  
### <a name="verifying-adapter-support"></a>어댑터 지원 확인  
 화면을 만들기 전에 모든 어댑터가 필요한 표면 속성을 지원 하는지 확인 합니다. 하나의 어댑터에만 렌더링 하더라도 WPF 창은 시스템의 모든 어댑터에 표시 될 수 있습니다. 항상 다중 어댑터 구성을 처리 하는 Direct3D9 코드를 작성 해야 합니다. WPF는 사용 가능한 어댑터 사이에서 화면을 이동할 수 있으므로 모든 어댑터를 지원 하는지 확인 해야 합니다.  
  
 다음 코드 예제에서는 시스템의 모든 어댑터에서 Direct3D9 지원을 확인 하는 방법을 보여 줍니다.  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_TestSurfaceSettings](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_testsurfacesettings)]  
  
### <a name="creating-the-surface"></a>화면 만들기  
 화면을 만들기 전에 장치 기능이 대상 운영 체제에서 적절 한 성능을 지원 하는지 확인 합니다. 자세한 내용은 [Direct3D9 및 WPF 상호 운용성을 위한 성능 고려 사항](performance-considerations-for-direct3d9-and-wpf-interoperability.md)합니다.  
  
 장치 기능을 확인 한 경우 화면을 만들 수 있습니다. 다음 코드 예제에서는 렌더링 대상을 만드는 방법을 보여 줍니다.  
  
 [!code-cpp[System.Windows.Interop.D3DImage#Renderer_CreateSurface](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderer_createsurface)]  
  
### <a name="wddm"></a>WDDM  
 WDDM을 사용 하도록 구성 된 Windows Vista 이상 운영 체제에서 렌더링 대상 질감을 만들고 수준 0 화면 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 을 메서드에 전달할 수 있습니다. 이 방법은 Windows XP에서 사용 하지 않는 것이 좋습니다 .이는 잠글 수 있는 렌더링 대상 질감을 만들 수 없으며 성능이 저하 되기 때문입니다.  
  
## <a name="handling-device-state"></a>장치 상태 처리  
 <xref:System.Windows.Interop.D3DImage> 클래스 라고 하는 두 디스플레이 버퍼를 관리 합니다 *백 버퍼* 하며 *프런트 버퍼가*. 백 버퍼는 프로그램 Direct3D 화면입니다.  백 버퍼에 대 한 변경 내용에 복사 됩니다 프런트 버퍼가 호출할 때를 <xref:System.Windows.Interop.D3DImage.Unlock%2A> 메서드를 하드웨어에 표시 됩니다. 경우에 따라 프런트 버퍼가 수 없게 됩니다. 화면 잠금, Direct3D 애플리케이션을 제외 하는 전체 화면, 사용자 전환 또는 기타 시스템 활동과이 부족 한 가용성을 발생할 수 있습니다. WPF 애플리케이션을 처리 하 여 알려집니다 이런 경우는 <xref:System.Windows.Interop.D3DImage.IsFrontBufferAvailableChanged> 이벤트입니다.  애플리케이션이 사용할 수 없게 되는 프런트 버퍼가에 반응 하는 방법을 소프트웨어 렌더링으로 대체 WPF 사용 여부에 따라 달라 집니다. <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 메서드 소프트웨어 렌더링으로 WPF 다시 속하는지 여부를 지정 하는 매개 변수를 받아들이는 오버 로드가 있습니다.  
  
 호출 하는 경우는 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%28System.Windows.Interop.D3DResourceType%2CSystem.IntPtr%29> 오버 로드 하거나 호출 합니다 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%28System.Windows.Interop.D3DResourceType%2CSystem.IntPtr%2CSystem.Boolean%29> 오버 로드는 `enableSoftwareFallback` 매개 변수 설정 `false`, 프런트 버퍼를 사용할 수 없게 하 고 아무 것도 렌더링 시스템 백 버퍼에 대 한 참조를 해제 표시 됩니다. 프런트 버퍼가 다시 제공 되 면 렌더링 발생을 <xref:System.Windows.Interop.D3DImage.IsFrontBufferAvailableChanged> WPF 애플리케이션에 알리는 이벤트입니다.  에 대 한 이벤트 처리기를 만들 수는 <xref:System.Windows.Interop.D3DImage.IsFrontBufferAvailableChanged> 유효한 Direct3D 화면을 사용 하 여 다시 렌더링을 다시 시작 하는 이벤트입니다. 렌더링을 다시 시작 하려면 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A>합니다.  
  
 호출 하는 경우는 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%28System.Windows.Interop.D3DResourceType%2CSystem.IntPtr%2CSystem.Boolean%29> 오버 로드는 `enableSoftwareFallback` 매개 변수 설정 `true`를 호출 하지 않아도 되므로 프런트 버퍼를 사용할 수 없을 때 렌더링 시스템은 백 버퍼에 대 한 참조를 유지 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 때 앞 버퍼를 다시 사용할 수 있습니다.  
  
 소프트웨어 렌더링이 사용 하도록 설정 된 경우 사용자의 장치를 사용할 수 없게 되는 경우가 있습니다. 하지만 렌더링 시스템은 Direct3D 화면에 대 한 참조를 유지 합니다. Direct3D9 장치를 사용할 수 없는지 여부를 확인 하려면 `TestCooperativeLevel` 메서드를 호출 합니다. Direct3D9Ex 장치를 확인 하려면 메서드가 사용 `CheckDeviceState` 되지 않으며 항상 success `TestCooperativeLevel` 를 반환 하기 때문에 메서드를 호출 합니다. 사용자 장치를 사용할 수 없게 되 면를 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 호출 하 여 WPF의 백 버퍼 참조를 해제 합니다.  디바이스를 재설정 해야 할 경우 호출 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 사용 하 여는 `backBuffer` 매개 변수 설정 `null`, 다음 호출 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> 사용 하 여 다시 `backBuffer` 유효한 Direct3D 화면을로 설정 합니다.  
  
 다중 어댑터 `Reset` 지원을 구현 하는 경우에만 잘못 된 장치에서 복구 하려면 메서드를 호출 합니다. 그렇지 않으면 모든 Direct3D9 인터페이스를 해제 하 고 완전히 다시 만듭니다. 어댑터 레이아웃이 변경 된 경우 변경 하기 전에 생성 된 Direct3D9 개체는 업데이트 되지 않습니다.  
  
## <a name="handling-resizing"></a>크기 조정 처리  
 이 기본 크기와 다른 해상도로 표시 <xref:System.Windows.Media.RenderOptions.BitmapScalingMode%2A> <xref:System.Windows.Media.Effects.SamplingMode.Bilinear> <xref:System.Windows.Media.BitmapScalingMode.Fant> <xref:System.Windows.Interop.D3DImage> 되는 경우이로 대체 되는 경우를 제외 하 고는 현재에 따라 크기가 조정 됩니다.  
  
 더 높은 충실도가 필요한 경우의 컨테이너가 <xref:System.Windows.Interop.D3DImage> 크기를 변경할 때 새 표면을 만들어야 합니다.  
  
 크기 조정을 처리할 수 있는 세 가지 방법이 있습니다.  
  
- 레이아웃 시스템에 참여 하 고 크기가 변경 될 때 새 화면을 만듭니다. 비디오 메모리를 고갈 하거나 조각화 할 수 있으므로 너무 많은 표면을 만들지 마세요.  
  
- 고정 된 기간 동안 새 화면을 만드는 데 크기 조정 이벤트가 발생 하지 않을 때까지 기다립니다.  
  
- 컨테이너 차원을 <xref:System.Windows.Threading.DispatcherTimer> 초당 여러 번 확인 하는을 만듭니다.  
  
## <a name="multi-monitor-optimization"></a>다중 모니터 최적화  
 렌더링 시스템에서을 <xref:System.Windows.Interop.D3DImage> 다른 모니터로 이동 하면 성능이 크게 저하 될 수 있습니다.  
  
 WDDM에서 모니터가 동일한 비디오 카드에 있고를 사용 `Direct3DCreate9Ex`하는 경우 성능이 저하 되지 않습니다. 모니터가 별도의 비디오 카드에 있는 경우 성능이 저하 됩니다. Windows XP에서는 성능이 항상 저하 됩니다.  
  
 가 <xref:System.Windows.Interop.D3DImage> 다른 모니터로 이동 하면 적절 한 성능을 복원 하기 위해 해당 어댑터에서 새 화면을 만들 수 있습니다.  
  
 성능 저하를 방지 하려면 다중 모니터 사례에 대해 특별히 코드를 작성 합니다. 다음 목록에서는 다중 모니터 코드를 작성 하는 한 가지 방법을 보여 줍니다.  
  
1. 메서드`Visual.ProjectToScreen` 를 사용 하 여 <xref:System.Windows.Interop.D3DImage> 화면 공간에서의 지점을 찾습니다.  
  
2. 해당 지점을 표시 하는 모니터를 찾으려면 GDI메서드를사용합니다.`MonitorFromPoint`  
  
3. 모니터를 `IDirect3D9::GetAdapterMonitor` 사용 하는 Direct3D9 어댑터를 찾으려면 메서드를 사용 합니다.  
  
4. 어댑터가 백 버퍼를 사용 하는 어댑터와 같지 않은 경우 새 모니터에 새 백 버퍼를 만들고 <xref:System.Windows.Interop.D3DImage> 백 버퍼에 할당 합니다.  
  
> [!NOTE]
> Cmio 모니터링 <xref:System.Windows.Interop.D3DImage> 하는 경우 WDDM 및 `IDirect3D9Ex` 동일한 어댑터의 경우를 제외 하 고 성능이 저하 됩니다. 이 경우 성능을 향상 시킬 수 있는 방법은 없습니다.  
  
 다음 코드 예제에서는 현재 모니터를 찾는 방법을 보여 줍니다.  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_SetAdapter](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_setadapter)]  
  
 <xref:System.Windows.Interop.D3DImage> 컨테이너의 크기나 위치가 변경 될 때 모니터를 업데이트 하거나, 초당 몇 번 업데이트 되는을 `DispatcherTimer` 사용 하 여 모니터를 업데이트 합니다.  
  
## <a name="wpf-software-rendering"></a>WPF 소프트웨어 렌더링  
 WPF는 다음과 같은 상황에서 소프트웨어의 UI 스레드에서 동기적으로 렌더링 합니다.  
  
- 인쇄  
  
- <xref:System.Windows.Media.Effects.BitmapEffect>  
  
- <xref:System.Windows.Media.Imaging.RenderTargetBitmap>  
  
 이러한 상황 중 하나가 발생 하면 렌더링 시스템은 메서드를 <xref:System.Windows.Interop.D3DImage.CopyBackBuffer%2A> 호출 하 여 하드웨어 버퍼를 소프트웨어에 복사 합니다. 기본 구현에서는 화면을 `GetRenderTargetData` 사용 하 여 메서드를 호출 합니다. 이 호출은 잠금/잠금 해제 패턴 외부에서 발생 하므로 실패할 수 있습니다. 이 경우 메서드는 `CopyBackBuffer` 을 반환 `null` 하 고 이미지는 표시 되지 않습니다.  
  
 <xref:System.Windows.Interop.D3DImage.CopyBackBuffer%2A> 메서드를 재정의 하 고, 기본 구현을 호출 하 고, 반환 `null`되는 경우 자리 표시자 <xref:System.Windows.Media.Imaging.BitmapSource>를 반환할 수 있습니다.  
  
 기본 구현을 호출 하는 대신 자체 소프트웨어 렌더링을 구현할 수도 있습니다.  
  
> [!NOTE]
> Wpf가 소프트웨어 <xref:System.Windows.Interop.D3DImage> 에서 완전히 렌더링 되는 경우에는 wpf에 프런트 버퍼가 없으므로가 표시 되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Interop.D3DImage>
- [Direct3D9 및 WPF 상호 운용성을 위한 성능 고려 사항](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
- [연습: WPF에서 호스팅할 Direct3D9 콘텐츠 만들기](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)
- [연습: WPF에서 Direct3D9 콘텐츠 호스팅](walkthrough-hosting-direct3d9-content-in-wpf.md)
