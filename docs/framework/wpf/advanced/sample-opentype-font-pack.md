---
title: 샘플 OpenType 글꼴 팩
ms.date: 03/30/2017
helpviewer_keywords:
- OpenType font pack [WPF]
- fonts [WPF], OpenType font pack
- typography [WPF], OpenType font pack
ms.assetid: 56b46fa1-a44e-419b-8f14-25ad51c715c3
ms.openlocfilehash: 76438b85a12d75efa0fc106a645fb592b3205fad
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960979"
---
# <a name="sample-opentype-font-pack"></a>샘플 OpenType 글꼴 팩
이 항목에서는와 함께 [!INCLUDE[TLA2#tla_wcsdk](../../../../includes/tla2sharptla-wcsdk-md.md)]배포 되는 샘플 OpenType 글꼴의 개요를 제공 합니다. 샘플 글꼴은 응용 프로그램에서 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 사용할 수 있는 확장 된 OpenType 기능을 지원 합니다.  

<a name="overview"></a>   
## <a name="fonts-in-the-opentype-font-pack"></a>OpenType 글꼴 팩의 글꼴  
 에서는 [!INCLUDE[TLA2#tla_wcsdk](../../../../includes/tla2sharptla-wcsdk-md.md)] 응용 프로그램을 만드는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 데 사용할 수 있는 샘플 OpenType 글꼴 집합을 제공 합니다. 샘플 글꼴은 Ascender Corporation으로부터 사용 허가를 받아 제공됩니다. 이러한 글꼴은 OpenType 형식으로 정의 된 전체 기능의 하위 집합만 구현 합니다. 다음 표에서는 샘플 OpenType 글꼴의 이름을 나열 합니다.  
  
|**이름**|**파일**|  
|--------------|--------------|  
|Kootenay|Kooten.ttf|  
|Lindsey|Linds.ttf|  
|Miramonte|Miramo.ttf|  
|Miramonte Bold|Miramob.ttf|  
|Pericles|Peric.ttf|  
|Pericles Light|Pericl.ttf|  
|Pescadero|Pesca.ttf|  
|Pescadero Bold|Pescab.ttf|  
  
 다음 그림은 샘플 OpenType 글꼴의 모양을 보여 줍니다.  
  
 ![샘플 글꼴 팩의 글꼴 이름 목록](./media/sample-opentype-font-pack/font-names-sample-pack.gif)  
  
 샘플 글꼴은 Ascender Corporation으로부터 사용 허가를 받아 제공됩니다. Ascender는 고급 글꼴 제품의 공급자입니다. 샘플 글꼴의 확장 또는 사용자 지정 버전을 사용 허가하려면 [Ascender Corporation의 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=182627)를 참조하세요.  
  
> [!NOTE]
> 애플리케이션 내에 포함하거나 재배포할 글꼴에 대한 필요한 라이선스 권한이 있는지 확인하는 것은 개발자의 책임입니다.  
  
<a name="installing_the_fonts"></a>   
## <a name="installing-the-fonts"></a>글꼴 설치  
 샘플 OpenType 글꼴을 기본 Windows 글꼴 디렉터리인 **\WINDOWS\Fonts**에 설치 하는 옵션이 있습니다. [글꼴] 컨트롤 패널을 사용하여 글꼴을 설치합니다. 이러한 글꼴이 컴퓨터에 있으면 기본 Windows 글꼴을 참조 하는 모든 응용 프로그램에 액세스할 수 있습니다. 글꼴 파일을 두 번 클릭하여 대표 문자 집합을 여러 글꼴 크기로 표시할 수 있습니다. 다음 스크린샷은 Lindsey 글꼴 파일인 Linds.ttf를 보여 줍니다.  
  
 ![Lindsey 글꼴 &#40;OpenType&#41; ](./media/typographyinwpf-04.png "TypographyInWPF_04")  
Lindsey 글꼴 표시  
  
<a name="using_the_fonts"></a>   
## <a name="using-the-fonts"></a>글꼴 사용  
 애플리케이션에서 글꼴을 사용할 수 있는 두 가지 방법이 있습니다. 어셈블리 내에 리소스로 포함되지 않은 프로젝트 콘텐츠 항목으로 애플리케이션에 글꼴을 추가할 수 있습니다. 또는 애플리케이션의 어셈블리 파일에 포함된 프로젝트 리소스 항목으로 애플리케이션에 글꼴을 추가할 수 있습니다. 자세한 내용은 [애플리케이션과 함께 글꼴 패키징](packaging-fonts-with-applications.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Documents.Typography>
- [OpenType 글꼴 기능](opentype-font-features.md)
- [응용 프로그램과 함께 글꼴 패키징](packaging-fonts-with-applications.md)
