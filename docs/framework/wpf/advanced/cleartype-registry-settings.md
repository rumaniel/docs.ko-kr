---
title: ClearType 레지스트리 설정
ms.date: 03/30/2017
helpviewer_keywords:
- ClearType [WPF], registry settings
- typography [WPF], ClearType registry settings
ms.assetid: 56f314bb-b30b-4f67-8492-8b8a9fa432ae
ms.openlocfilehash: ab6ff2ba6e0f3f1ea9e34de80b67276a990bc83b
ms.sourcegitcommit: 3ac05b2c386c8cc5e73f4c7665f6c0a7ed3da1bd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2019
ms.locfileid: "71151840"
---
# <a name="cleartype-registry-settings"></a>ClearType 레지스트리 설정
이 항목에서는 WPF 응용 프로그램에서 사용 되는 Microsoft ClearType 레지스트리 설정에 대 한 개요를 제공 합니다.  

<a name="overview"></a>   
## <a name="technology-overview"></a>기술 개요  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]디스플레이 장치에 텍스트를 렌더링 하는 응용 프로그램은 ClearType 기능을 사용 하 여 향상 된 읽기 환경을 제공 합니다. ClearType은 랩톱 화면, Pocket PC 화면, 평면 패널 모니터 등 기존 Lcd (액체 크리스탈 디스플레이)의 텍스트 가독성을 향상 시키는 Microsoft에서 개발한 소프트웨어 기술입니다. ClearType은 LCD 화면의 모든 픽셀에서 개별 세로 색 줄무늬 요소에 액세스 하는 방식으로 작동 합니다. ClearType에 대 한 자세한 내용은 [Cleartype 개요](cleartype-overview.md)를 참조 하세요.  
  
 ClearType으로 렌더링 되는 텍스트는 다양 한 디스플레이 장치에서 볼 때 현저 하 게 다를 수 있습니다. 예를 들어 적은 수의 모니터가 색 스트라이프 요소를 보다 일반적인 빨강, 녹색, 파랑 (RGB) 순서 대신 파란색, 녹색, 빨간색 순서로 구현 합니다.  
  
 ClearType으로 렌더링 되는 텍스트는 다양 한 수준의 색 민감도를 사용 하 여 개인이 볼 때 크게 다르게 보일 수도 있습니다. 어떤 사람은 다른 사람보다 미묘한 색의 차이를 더 잘 감지할 수 있습니다.  
  
 이러한 각 경우에는 각 개인에 게 최상의 읽기 환경을 제공 하기 위해 ClearType 기능을 수정 해야 합니다.  
  
<a name="registry_settings"></a>   
## <a name="registry-settings"></a>레지스트리 설정  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]ClearType 기능을 제어 하기 위한 네 가지 레지스트리 설정을 지정 합니다.  
  
|설정|설명|  
|-------------|-----------------|  
|ClearType 수준|ClearType 색의 명확성 수준을 설명 합니다.|  
|감마 수준|디스플레이 디바이스의 픽셀 색 구성 요소 수준을 설명합니다.|  
|픽셀 구조체|디스플레이 디바이스의 픽셀 배치를 설명합니다.|  
|텍스트 대비 수준|표시되는 텍스트의 대비 수준을 설명합니다.|  
  
 이러한 설정은 식별 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]된 ClearType 레지스트리 설정을 참조 하는 방법을 알고 있는 외부 구성 유틸리티에서 액세스할 수 있습니다. 이러한 설정은 Windows 레지스트리 편집기를 사용 하 여 값에 직접 액세스 하 여 만들거나 수정할 수도 있습니다.  
  
 ClearType 레지스트리 설정 (기본 상태)이 설정 되어 있지 않으면 응용 프로그램은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] Windows 시스템 매개 변수 정보에서 글꼴 다듬기 설정을 쿼리 합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]  
  
> [!NOTE]
> 표시 장치 이름을 열거 하는 `SystemParametersInfo` [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 방법에 대 한 자세한 내용은 함수를 참조 하세요.  
  
<a name="ClearType_level"></a>   
## <a name="cleartype-level"></a>ClearType 수준  
 ClearType 수준을 사용 하면 개인의 색 민감도 및 인식에 따라 텍스트 렌더링을 조정할 수 있습니다. 일부 개인의 경우 가장 높은 수준에서 ClearType을 사용 하는 텍스트를 렌더링 하는 것은 최상의 읽기 환경을 생성 하지 않습니다.  
  
 ClearType 수준은 0에서 100 사이의 정수 값입니다. 기본 수준은 100입니다. 즉, ClearType은 표시 장치에서 색 stripe 요소의 최대 기능을 사용 합니다. 그러나 ClearType 수준 0은 텍스트를 회색 눈금으로 렌더링 합니다. ClearType 수준을 0에서 100 사이로 설정 하면 개인의 색 민감도에 적합 한 중간 수준을 만들 수 있습니다.  
  
### <a name="registry-setting"></a>레지스트리 설정  
 ClearType 수준에 대 한 레지스트리 설정 위치는 특정 디스플레이 장치 이름에 해당 하는 개별 사용자 설정입니다.  
  
 `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 사용자의 각 표시 장치 이름에 대해 `ClearTypeLevel` DWORD 값이 정의 됩니다. 다음 스크린샷은 ClearType 수준에 대 한 레지스트리 편집기 설정을 보여 줍니다.  
  
 ![레지스트리 편집기의 ClearType 설정](./media/cleartype-registry-settings/cleartype-settings-registry-editor.png)  
  
> [!NOTE]
> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]응용 프로그램은 ClearType을 사용 하거나 사용 하지 않고 두 가지 모드 중 하나로 텍스트를 렌더링 합니다. ClearType 없이 텍스트를 렌더링 하는 경우 회색조 렌더링 이라고 합니다.  
  
<a name="gamma_level"></a>   
## <a name="gamma-level"></a>감마 수준  
 감마 수준은 픽셀 값과 광도 사이의 비선형 관계를 가리킵니다. 감마 수준 설정은 디스플레이 디바이스의 물리적 특성과 일치해야 합니다. 그렇지 않으면 렌더링된 출력에서 왜곡이 발생할 수 있습니다. 예를 들어 텍스트가 너무 크거나 너무 좁게 표시 되거나 문자 모양에 대 한 세로 fringes의 가장자리에 색이 나타날 수 있습니다.  
  
 감마 수준은 1,000에서 2,200까지의 정수 값입니다. 기본 수준은 1,900입니다.  
  
### <a name="registry-setting"></a>레지스트리 설정  
 감마 수준에 대한 레지스트리 설정 위치는 특정 디스플레이 디바이스 이름에 해당하는 로컬 컴퓨터 설정입니다.  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 사용자의 각 표시 장치 이름에 대해 `GammaLevel` DWORD 값이 정의 됩니다. 다음 스크린샷에서는 감마 수준에 대한 레지스트리 편집기 설정을 보여 줍니다.  
  
 ![레지스트리 편집기의 ClearType 감마 수준 설정](./media/cleartype-registry-settings/cleartype-gamma-level-settings-registry-editor.png)  
  
<a name="pixel_structure"></a>   
## <a name="pixel-structure"></a>픽셀 구조체  
 픽셀 구조체는 디스플레이 디바이스를 구성하는 픽셀 형식을 설명합니다. 픽셀 구조체는 다음 세 가지 형식 중 하나로 정의됩니다.  
  
|형식|값|설명|  
|----------|-----------|-----------------|  
|플랫|0|디스플레이 디바이스에는 픽셀 구조체가 없습니다. 즉 각 색의 광원이 픽셀 영역에서 고르게 분산되며, 이를 회색조 렌더링이라고 합니다. 이 형식은 표준 디스플레이 디바이스에서 작동하는 방법입니다. ClearType은 렌더링 된 텍스트에 적용 되지 않습니다.|  
|RGB|1|디스플레이 디바이스에는 빨강, 녹색 및 파랑 순서의 3개 스트라이프로 구성되는 픽셀이 있습니다. ClearType은 렌더링 된 텍스트에 적용 됩니다.|  
|BGR|2|디스플레이 디바이스에는 파랑, 녹색 및 빨강 순서의 3개 스트라이프로 구성되는 픽셀이 있습니다. ClearType은 렌더링 된 텍스트에 적용 됩니다. 색의 순서가 RGB 형식과는 반대입니다.|  
  
 픽셀 구조체는 0에서 2까지의 정수 값에 해당합니다. 기본 수준은 플랫 픽셀 구조체를 나타내는 0입니다.  
  
> [!NOTE]
> 표시 장치 이름을 열거 하는 `EnumDisplayDevices` [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 방법에 대 한 자세한 내용은 함수를 참조 하세요.  
  
### <a name="registry-setting"></a>레지스트리 설정  
 픽셀 구조체에 대한 레지스트리 설정 위치는 특정 디스플레이 디바이스 이름에 해당하는 로컬 컴퓨터 설정입니다.  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 사용자의 각 표시 장치 이름에 대해 `PixelStructure` DWORD 값이 정의 됩니다. 다음 스크린샷에서는 픽셀 구조체에 대한 레지스트리 편집기 설정을 보여 줍니다.  
  
 ![레지스트리 편집기의 ClearType 감마 수준 설정](./media/cleartype-registry-settings/cleartype-gamma-level-settings-registry-editor.png)  
  
<a name="text_contrast_level"></a>   
## <a name="text-contrast-level"></a>텍스트 대비 수준  
 텍스트 대비 수준을 사용하면 문자 모양의 획 너비를 기준으로 텍스트 렌더링을 조정할 수 있습니다. 텍스트 대비 수준은 0에서 6까지의 정수 값이며, 정수 값이 클수록 획이 넓어집니다. 기본 수준은 1입니다.  
  
### <a name="registry-setting"></a>레지스트리 설정  
 텍스트 대비 수준에 대한 레지스트리 설정 위치는 특정 디스플레이 디바이스 이름에 해당하는 개별 사용자 설정입니다.  
  
 `HKEY_CURRENT_USER\Software\Microsoft\Avalon.Graphics\<displayName>`  
  
 사용자의 각 표시 장치 이름에 대해 `TextContrastLevel` DWORD 값이 정의 됩니다. 다음 스크린샷에서는 텍스트 대조 수준에 대한 레지스트리 편집기 설정을 보여 줍니다.  
  
 ![레지스트리 편집기의 ClearType 설정](./media/cleartype-registry-settings/cleartype-settings-registry-editor.png)  
  
## <a name="see-also"></a>참고 항목

- [ClearType 개요](cleartype-overview.md)
- [ClearType 앤티 앨리어싱](/windows/desktop/gdi/cleartype-antialiasing)
