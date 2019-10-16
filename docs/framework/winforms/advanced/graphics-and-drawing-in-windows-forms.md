---
title: Windows Forms의 그래픽 및 그리기
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [Windows Forms]
- graphics [Windows Forms], using in Windows Forms
- GDI+, using in managed code
- drawing [Windows Forms]
ms.assetid: 362532c5-1a06-4257-bdc8-723461009ede
ms.openlocfilehash: e110203605c31f90f71c949f81c18ebf464d52eb
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505549"
---
# <a name="graphics-and-drawing-in-windows-forms"></a>Windows Forms의 그래픽 및 그리기
공용 언어 런타임에서 고급 구현에는 Windows 인터페이스 GDI (그래픽 장치) GDI +를 사용 합니다. GDI +를 사용 하 여 만들고 그래픽, 텍스트를 그릴 하 그래픽 이미지를 개체로 조작 합니다. GDI + 성능 및 사용 편의성을 제공 하도록 설계 되었습니다. GDI + 하 여 Windows Forms 및 컨트롤에 그래픽 이미지를 렌더링 합니다. 사용할 수는 없지만 GDI + Web Forms에서 직접, 이미지 웹 서버 컨트롤을 통해 그래픽 이미지를 표시할 수 있습니다.  
  
 이 섹션에서는 GDI + 프로그래밍의 기초를 소개 하는 항목을 찾을 수 있습니다. 포괄적인 참조는 아니지만 이 섹션은 <xref:System.Drawing.Graphics>, <xref:System.Drawing.Pen>, <xref:System.Drawing.Brush> 및 <xref:System.Drawing.Color> 개체에 대한 정보를 포함하며 도형 그리기, 텍스트 그리기 또는 이미지 표시와 같은 작업을 수행하는 방법을 설명합니다. 자세한 내용은 [GDI + 참조](/windows/desktop/gdiplus/-gdiplus-class-gdi-reference)합니다.  
  
 바로 시작하려면 [그래픽 프로그래밍 시작](getting-started-with-graphics-programming.md)을 참조하세요. Windows Forms에서 코드를 사용하여 선, 도형, 텍스트 등을 그리는 방법에 대한 항목이 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [그래픽 개요](graphics-overview-windows-forms.md)  
 그래픽 관련 관리되는 클래스를 소개합니다.  
  
 [GDI + 관리 코드 정보](about-gdi-managed-code.md)  
 관리 되는 GDI + 클래스에 대 한 정보를 제공합니다.  
  
 [관리되는 그래픽 클래스 사용](using-managed-graphics-classes.md)  
 어떻게 완료 GDI +를 사용 하 여 작업의 다양 한 관리 되는 클래스를 보여 줍니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Drawing>  
 GDI + 기본 그래픽 기능에 대 한 액세스를 제공합니다.  
  
 <xref:System.Drawing.Drawing2D>  
 고급 2D 및 벡터 그래픽 기능을 제공합니다.  
  
 <xref:System.Drawing.Imaging>  
 고급 GDI + 이미징 기능을 제공 합니다.  
  
 <xref:System.Drawing.Text>  
 고급 GDI + 입력 체계 기능을 제공 합니다. 이 네임스페이스의 클래스를 통해 글꼴 컬렉션을 만들고 사용할 수 있습니다.  
  
 <xref:System.Drawing.Printing>  
 인쇄 기능을 제공합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [사용자 지정 컨트롤 그리기 및 렌더링](../controls/custom-control-painting-and-rendering.md)  
 컨트롤을 그리기 위한 코드를 제공하는 방법을 자세히 설명합니다.
