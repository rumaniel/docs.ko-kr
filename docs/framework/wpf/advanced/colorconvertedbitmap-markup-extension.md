---
title: ColorConvertedBitmap 태그 확장
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [WPF], ColorConvertedBitmap markup extension
- ColorConvertedBitmap markup extension [WPF]
ms.assetid: 18321c18-c898-4470-93fa-a702b47770c1
ms.openlocfilehash: e8a36a1b8592146eb2474805638cdc3697adb0c4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62010659"
---
# <a name="colorconvertedbitmap-markup-extension"></a>ColorConvertedBitmap 태그 확장
포함된 된 프로필이 없는 비트맵 소스를 지정 하는 방법을 제공 합니다. 색 컨텍스트 프로필에서 지정 된 / [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]이미지 소스는 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]합니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xml  
<object property="{ColorConvertedBitmap imageSource sourceIIC destinationIIC}" .../>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`imageSource`|[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 예측할 비트맵입니다.|  
|`sourceIIC`|[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 원본 프로필 구성 합니다.|  
|`destinationIIC`|[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 대상 프로필 구성|  
  
## <a name="remarks"></a>설명  
 이 태그 확장 사용 되기 위한 관련된 이미지 원본 속성이 값 집합을 같은 <xref:System.Windows.Media.Imaging.BitmapImage.UriSource%2A>합니다.  
  
 특성 구문은 이러한 태그 확장에 가장 많이 사용되는 구문입니다. `ColorConvertedBitmap` (또는 `ColorConvertedBitmapExtension`) 값만 값으로 문자열인 초기 생성자에서 설정할 수 있으므로 속성 요소 구문에서 사용할 수 없습니다 확장 식별자를 수행 합니다.  
  
 `ColorConvertedBitmap`은 태그 확장입니다. 태그 확장은 특성 값을 리터럴 값 또는 처리기 이름이 아닌 다른 값이 되도록 이스케이프해야 하는 요구 사항이 있는 경우 일반적으로 구현되며 이러한 요구 사항은 특정 형식 또는 속성에 형식 변환기를 배치하는 것보다 더 포괄적입니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]의 모든 태그 확장은 특성 구문에서 { 및 } 문자를 사용합니다. 이러한 문자는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 프로세서가 태그 확장이 특성을 처리해야 함을 인식하는 데 사용되는 규칙입니다. 자세한 내용은 [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Imaging.BitmapImage.UriSource%2A>
- [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)
- [이미징 개요](../graphics-multimedia/imaging-overview.md)
