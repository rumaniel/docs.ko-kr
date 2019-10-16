---
title: 필기 인식
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- handwriting recognition [WPF]
- recognition of handwriting [WPF]
ms.assetid: f4e8576d-e731-4bac-9818-22e2ae636636
ms.openlocfilehash: d6c09f063b6bd0eef2cb9f6bb444eac980ad4832
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956525"
---
# <a name="handwriting-recognition"></a>필기 인식
이 섹션에서는 WPF 플랫폼의 디지털 링크에 관련되므로 인식의 기본 개념을 설명합니다.  
  
## <a name="recognition-solutions"></a>인식 솔루션  
 다음 예에서는 [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)) 클래스를 사용하여 잉크를 인식하는 방법을 보여줍니다.  
  
> [!NOTE]
> 이 샘플에서는 필기 인식기를 시스템에 설치해야 합니다.  
  
 **InkRecognition**라는 새 WPF 응용 프로그램 프로젝트를 Visual Studio에 만듭니다. Window1.xaml 파일의 콘텐츠를 다음 XAML 코드로 바꿉니다. 이 코드는 애플리케이션의 사용자 인터페이스를 렌더링합니다.  
  
 [!code-xaml[InkRecognition#1](~/samples/snippets/csharp/VS_Snippets_Wpf/InkRecognition/CSharp/Window1.xaml#1)]  
  
 \Program Files\Common Files\Microsoft Shared\Ink에 있는 Microsoft Ink 어셈블리, Microsoft.Ink.dll에 참조를 추가합니다. 파일의 기반이 되는 코드의 콘텐츠를 다음 코드로 바꿉니다.  
  
 [!code-csharp[InkRecognition#2](~/samples/snippets/csharp/VS_Snippets_Wpf/InkRecognition/CSharp/Window1.xaml.cs#2)]
 [!code-vb[InkRecognition#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/InkRecognition/VisualBasic/Window1.xaml.vb#2)]  
  
## <a name="see-also"></a>참고자료

- [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90))
