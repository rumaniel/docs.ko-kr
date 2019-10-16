---
title: Direct3D9 및 WPF 상호 운용성을 위한 성능 고려 사항
ms.date: 03/30/2017
helpviewer_keywords:
- WPF [WPF], Direct3D9 interop performance
- Direct3D9 [WPF interoperability], performance
ms.assetid: ea8baf91-12fe-4b44-ac4d-477110ab14dd
ms.openlocfilehash: 02a91c1824c5d6374f37b0af66a3308d33210c4a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69932489"
---
# <a name="performance-considerations-for-direct3d9-and-wpf-interoperability"></a>Direct3D9 및 WPF 상호 운용성을 위한 성능 고려 사항
클래스를 <xref:System.Windows.Interop.D3DImage> 사용 하 여 Direct3D9 콘텐츠를 호스트할 수 있습니다. Direct3D9 콘텐츠를 호스팅하면 응용 프로그램의 성능에 영향을 줄 수 있습니다. 이 항목에서는 Windows Presentation Foundation (WPF) 응용 프로그램에서 Direct3D9 콘텐츠를 호스팅할 때 성능을 최적화 하는 모범 사례에 대해 설명 합니다. 이러한 모범 사례에는 windows Vista <xref:System.Windows.Interop.D3DImage> , windows XP 및 다중 모니터 디스플레이를 사용 하는 경우 및 모범 사례를 사용 하는 방법이 포함 됩니다.  
  
> [!NOTE]
> 이러한 모범 사례를 보여 주는 코드 예제는 [WPF 및 Direct3D9 상호 운용성](wpf-and-direct3d9-interoperation.md)을 참조 하세요.  
  
## <a name="use-d3dimage-sparingly"></a>D3DImage만 사용  
 <xref:System.Windows.Interop.D3DImage> 인스턴스에서 호스트 되는 Direct3D9 콘텐츠는 순수 Direct3D 응용 프로그램에서와 같이 렌더링 되지 않습니다. 화면을 복사 하 고 명령 버퍼를 플러시하는 작업은 비용이 많이 들 수 있습니다. <xref:System.Windows.Interop.D3DImage> 인스턴스 수가 늘어나면 더 많은 플러시가 발생 하 고 성능이 저하 됩니다. 따라서를 사용 하는 <xref:System.Windows.Interop.D3DImage> 경우에만 사용 해야 합니다.  
  
## <a name="best-practices-on-windows-vista"></a>Windows Vista에 대 한 모범 사례  
 Windows Vista에서 WDDM (windows display Driver Model)을 사용 하도록 구성 된 디스플레이를 사용 하는 최상의 성능을 위해 `IDirect3DDevice9Ex` 장치에서 Direct3D9 화면을 만듭니다. 이렇게 하면 화면 공유를 사용할 수 있습니다. 비디오 카드는 Windows Vista의 `D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES` 및 `D3DCAPS2_CANSHARERESOURCE` 드라이버 기능을 지원 해야 합니다. 다른 모든 설정은 화면을 소프트웨어를 통해 복사 하 여 성능을 현저 하 게 줄입니다.  
  
> [!NOTE]
> Windows Vista에서 XDDM (Windows XP Display Driver Model)을 사용 하도록 구성 된 디스플레이를 사용 하는 경우 화면은 설정에 관계 없이 항상 소프트웨어를 통해 복사 됩니다. 적절 한 설정 및 비디오 카드를 사용 하면 화면 복사본이 하드웨어에서 수행 되기 때문에 WDDM을 사용 하면 Windows Vista에서 더 나은 성능을 볼 수 있습니다.  
  
## <a name="best-practices-on-windows-xp"></a>Windows XP에 대 한 모범 사례  
 Xddm (windows xp 디스플레이 드라이버 모델)을 사용 하는 windows xp의 성능을 최적화 하려면 `IDirect3DSurface9::GetDC` 메서드가 호출 될 때 올바르게 동작 하는 잠글 수 있는 화면을 만듭니다. 내부적으로이 `BitBlt` 메서드는 하드웨어의 장치에서 화면을 전송 합니다. 메서드 `GetDC` 는 항상 xrgb 표면에서 작동 합니다. 그러나 클라이언트 컴퓨터에서 Windows XP SP3 또는 s p 2를 실행 하 고 있고 계층 창 기능에 대 한 핫픽스도 클라이언트에 있는 경우이 메서드는 ARGB 표면 에서만 작동 합니다. 비디오 카드에서 드라이버 기능을 `D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES` 지원 해야 합니다.  
  
 16 비트 데스크톱 디스플레이 깊이가 성능을 크게 낮출 수 있습니다. 32 비트 데스크톱을 권장 합니다.  
  
 Windows Vista 및 Windows XP 용으로 개발 하는 경우 Windows XP에서 성능을 테스트 합니다. Windows XP에서 비디오 메모리가 부족 하 게 되는 것이 중요 합니다. 또한 <xref:System.Windows.Interop.D3DImage> windows XP에서는 필요한 추가 비디오 메모리 복사로 인해 windows Vista WDDM 보다 더 많은 비디오 메모리와 대역폭을 사용 합니다. 따라서 동일한 비디오 하드웨어에 대해 windows Vista 보다 Windows XP에서 성능이 저하 될 수 있습니다.  
  
> [!NOTE]
> XDDM은 Windows XP 및 Windows Vista에서 모두 사용할 수 있습니다. 그러나 WDDM은 Windows Vista 에서만 사용할 수 있습니다.  
  
## <a name="general-best-practices"></a>일반적인 모범 사례  
 장치를 만들 때 `D3DCREATE_MULTITHREADED` 만들기 플래그를 사용 합니다. 이렇게 하면 성능이 저하 되지만 WPF 렌더링 시스템은 다른 스레드에서이 장치에 대 한 메서드를 호출 합니다. 두 스레드가 동시에 장치에 액세스 하지 않도록 잠금 프로토콜을 올바르게 준수 해야 합니다.  
  
 WPF 관리 스레드에서 렌더링을 수행 하는 경우 `D3DCREATE_FPU_PRESERVE` 생성 플래그를 사용 하 여 장치를 만드는 것이 좋습니다. 이 설정이 없으면 D3D 렌더링은 WPF 배정밀도 작업의 정확도를 줄이고 렌더링 문제를 발생 시킬 수 있습니다.  
  
 하드웨어 지원 <xref:System.Windows.Interop.D3DImage> 없이 pow2 표면을 바둑판식으로 배열 하거나를 포함 하는 <xref:System.Windows.Media.DrawingBrush> 또는 <xref:System.Windows.Media.VisualBrush> 를 포함 <xref:System.Windows.Interop.D3DImage>하는 경우를 제외 하 고는 빠르게 바둑판식으로 배열 됩니다.  
  
## <a name="best-practices-for-multi-monitor-displays"></a>다중 모니터 표시에 대 한 모범 사례  
 여러 모니터가 있는 컴퓨터를 사용 하는 경우 앞에서 설명한 모범 사례를 따라야 합니다. 다중 모니터 구성의 경우 몇 가지 추가 성능 고려 사항도 있습니다.  
  
 백 버퍼를 만들 때 특정 장치 및 어댑터에서 만들어지므로 WPF는 모든 어댑터에 프런트 버퍼를 표시할 수 있습니다. 프런트 버퍼를 업데이트 하기 위해 어댑터 간에 복사 하는 데는 매우 많은 비용이 소요 될 수 있습니다. 여러 비디오 카드와 `IDirect3DDevice9Ex` 장치를 사용 하 여 WDDM을 사용 하도록 구성 된 Windows Vista에서는 프런트 버퍼가 다른 어댑터에 있지만 동일한 비디오 카드를 사용 하는 경우 성능 저하가 발생 하지 않습니다. 그러나 Windows XP 및 여러 비디오 카드를 사용 하는 XDDM에서는 프런트 버퍼가 백 버퍼가 아닌 다른 어댑터에 표시 되는 경우 상당한 성능 저하가 발생 합니다. 자세한 내용은 [WPF 및 Direct3D9 상호 운용성](wpf-and-direct3d9-interoperation.md)을 참조 하세요.  
  
## <a name="performance-summary"></a>성능 요약  
 다음 표에서는 운영 체제, 픽셀 형식 및 표면 잠금 기능의 기능으로 서의 프런트 버퍼 업데이트 성능을 보여 줍니다. 프런트 버퍼와 백 버퍼는 동일한 어댑터에 있는 것으로 간주 됩니다. 어댑터 구성에 따라 하드웨어 업데이트는 일반적으로 소프트웨어 업데이트 보다 훨씬 빠릅니다.  
  
|표면 픽셀 형식|Windows Vista, WDDM 및 9Ex|기타 Windows Vista 구성|Windows XP SP3 또는 SP2 w/핫픽스|Windows XP SP2|  
|--------------------------|---------------------------------|----------------------------------------|--------------------------------------|--------------------|  
|D3DFMT_X8R8G8B8 (잠글 수 없음)|**하드웨어 업데이트**|소프트웨어 업데이트|소프트웨어 업데이트|소프트웨어 업데이트|  
|D3DFMT_X8R8G8B8 (잠금 가능)|**하드웨어 업데이트**|소프트웨어 업데이트|**하드웨어 업데이트**|**하드웨어 업데이트**|  
|D3DFMT_A8R8G8B8 (잠글 수 없음)|**하드웨어 업데이트**|소프트웨어 업데이트|소프트웨어 업데이트|소프트웨어 업데이트|  
|D3DFMT_A8R8G8B8 (잠금 가능)|**하드웨어 업데이트**|소프트웨어 업데이트|**하드웨어 업데이트**|소프트웨어 업데이트|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Interop.D3DImage>
- [WPF 및 Direct3D9 상호 운용성](wpf-and-direct3d9-interoperation.md)
- [연습: WPF에서 호스팅할 Direct3D9 콘텐츠 만들기](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)
- [연습: WPF에서 Direct3D9 콘텐츠 호스팅](walkthrough-hosting-direct3d9-content-in-wpf.md)
