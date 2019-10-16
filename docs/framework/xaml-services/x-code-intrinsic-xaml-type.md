---
title: x:Code 내장 XAML 형식
ms.date: 03/30/2017
f1_keywords:
- Code
- x:Code
- xCode
helpviewer_keywords:
- Code directive in XAML [XAML Services]
- x:Code XAML directive element [XAML Services]
- XAML [XAML Services], x:Code directive element
ms.assetid: 87986b13-1a2e-4830-ae36-15f9dc5629e8
ms.openlocfilehash: 2b7713548b6269f079ef32b5bf1fe4fa630edcc8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053787"
---
# <a name="xcode-intrinsic-xaml-type"></a>x:Code 내장 XAML 형식
XAML 프로덕션 내에서 코드를 배치할 수 있습니다. 이러한 코드는 xaml을 컴파일하는 XAML 프로세서 구현에 의해 컴파일하거나 나중에 런타임에의 한 해석을 위해 XAML 프로덕션에 남아 있을 수 있습니다.  
  
## <a name="xaml-object-element-usage"></a>XAML 개체 요소 사용  
  
```xaml  
<x:Code>  
   // code instructions, usually enclosed by CDATA...  
</x:Code>  
```  
  
## <a name="remarks"></a>설명  
 `x:Code` Xaml 지시문 요소 내의 코드는 여전히 일반 XML 네임 스페이스 및 제공 된 xaml 네임 스페이스 내에서 해석 됩니다. 따라서 일반적으로 `x:Code` `CDATA` 세그먼트 내부에 사용 되는 코드를 묶어야 합니다.  
  
 `x:Code`는 XAML 프로덕션의 모든 가능한 배포 메커니즘에 대해 허용 되지 않습니다. 특정 프레임 워크 (예: WPF)에서 코드를 컴파일해야 합니다. 다른 프레임 워크에서는 `x:Code` 일반적으로 사용이 허용 되지 않을 수 있습니다.  
  
 관리 `x:Code` 되는 콘텐츠를 허용 하는 프레임 워크의 경우 `x:Code` 콘텐츠에 사용할 올바른 언어 컴파일러는 응용 프로그램을 컴파일하는 데 사용 되는 포함 하는 프로젝트의 설정 및 대상에 따라 결정 됩니다.  
  
## <a name="wpf-usage-notes"></a>WPF 사용 정보  
 WPF 용 내 `x:Code` 에 선언 된 코드에는 몇 가지 주목할 만한 제한 사항이 있습니다.  
  
- 지시문 `x:Code` 요소는 XAML 프로덕션의 루트 요소에 대 한 직계 자식 요소 여야 합니다.  
  
- [X:Class 지시문](x-class-directive.md) 은 부모 루트 요소에 제공 해야 합니다.  
  
- 내 `x:Code` 에 배치 된 코드는 해당 XAML 페이지에 대해 이미 만들어진 partial 클래스의 범위 내에 있도록 컴파일에서 처리 됩니다. 따라서 사용자가 정의 하는 모든 코드는 해당 partial 클래스의 멤버 또는 변수 여야 합니다.  
  
- Partial 클래스 내에 클래스를 중첩 하는 것 외에는 추가 클래스를 정의할 수 없습니다. 중첩은 허용 되지만 XAML에서 중첩 된 클래스를 참조할 수 없기 때문에 일반적이 지 않습니다. 기존 partial 클래스에 사용 되는 네임 스페이스가 아닌 CLR 네임 스페이스는 정의 하거나에 추가할 수 없습니다.  
  
- Partial class CLR 네임 스페이스 외부에 있는 코드 엔터티에 대 한 참조는 모두 정규화 되어야 합니다. 선언 되는 멤버가 partial 클래스 재정의 가능한 멤버에 대 한 재정의 인 경우 언어별 override 키워드를 사용 하 여이를 지정 해야 합니다. 범위에 `x:Code` 선언 된 멤버가 XAML에서 생성 된 partial 클래스의 멤버와 충돌 하는 경우, 컴파일러에서 충돌을 보고 하는 경우 xaml 파일을 컴파일하거나 로드할 수 없습니다.  
  
## <a name="see-also"></a>참고자료

- [x:Class 지시문](x-class-directive.md)
- [WPF의 코드 숨김 및 XAML](../wpf/advanced/code-behind-and-xaml-in-wpf.md)
- [XAML 개요(WPF)](../wpf/advanced/xaml-overview-wpf.md)
