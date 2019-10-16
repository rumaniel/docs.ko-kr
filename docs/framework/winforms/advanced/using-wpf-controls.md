---
title: WPF 컨트롤 사용
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms Designer [Windows Forms], interoperability with WPF
- interoperability [WPF]
ms.assetid: 03c85dce-26ad-44cd-bc1d-8e0cb56de096
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 5ea92b24a2ca30c0ad137d83c8f521a952ad0c6b
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69658496"
---
# <a name="use-wpf-controls-in-windows-forms-apps"></a>Windows Forms apps에서 WPF 컨트롤 사용

Windows Forms 기반 응용 프로그램에서 Windows Presentation Foundation (WPF) 컨트롤을 사용할 수 있습니다. 두 가지 서로 다른 뷰 기술 이지만 원활 하 게 상호 운용 됩니다.

Visual Studio의 Windows Forms 디자이너은 Windows Presentation Foundation 컨트롤을 호스팅하기 위한 시각적 디자인 환경을 제공 합니다. WPF 컨트롤은 라는 <xref:System.Windows.Forms.Integration.ElementHost>특수 한 Windows Forms 컨트롤에서 호스팅됩니다. 이 컨트롤을 통해 WPF 컨트롤은 폼의 레이아웃에 참여 하 고 키보드 및 마우스 메시지를 받을 수 있습니다. 디자인 타임에 컨트롤 Windows Forms 제어 하는 <xref:System.Windows.Forms.Integration.ElementHost> 것과 동일한 방식으로 컨트롤을 정렬할 수 있습니다.

WPF 기반 응용 프로그램에서 Windows Forms 컨트롤을 사용할 수도 있습니다. 자세한 내용은 [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)을 참조 하세요.

## <a name="see-also"></a>참고자료

- [WPF 및 Windows Forms 상호 운용성](/dotnet/framework/wpf/advanced/wpf-and-windows-forms-interoperation)
