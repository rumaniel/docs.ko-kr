---
title: x:Class 지시문
ms.date: 03/30/2017
f1_keywords:
- x:Class
- xClass
- Class
helpviewer_keywords:
- Class attribute in XAML [XAML Services]
- XAML [XAML Services], x:Class attribute
- x:Class attribute [XAML Services]
ms.assetid: bc4a3d8e-76e2-423e-a5d1-159a023e82ec
ms.openlocfilehash: 6e04085db0fa5a4c4170846dc4ac10d0131032a7
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053811"
---
# <a name="xclass-directive"></a>x:Class 지시문
태그와 코드 숨김으로 partial 클래스를 조인 하도록 XAML 태그 컴파일을 구성 합니다. 코드 partial 클래스는 CLS (공용 언어 사양) 언어로 된 별도의 코드 파일에 정의 되어 있지만 일반적으로 태그 partial 클래스는 XAML 컴파일 중에 코드 생성에 의해 생성 됩니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object x:Class="namespace.classname"...>  
  ...  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`namespace`|선택 사항입니다. 로 `classname`식별 되는 partial 클래스를 포함 하는 CLR 네임 스페이스를 지정 합니다. 을 `namespace` 지정 하면 점 (.)은 및 `classname`를 `namespace` 구분 합니다. 설명 부분을 참조하세요.|  
|`classname`|필수 요소. 해당 XAML에 대해 로드 된 XAML 및 코드 숨김이 연결 되는 partial 클래스의 CLR 이름을 지정 합니다.|  
  
## <a name="dependencies"></a>종속성  
 `x:Class`는 XAML 프로덕션의 루트 요소에만 지정할 수 있습니다. `x:Class`가 XAML 프로덕션에서 부모를 포함 하는 개체에서 유효 하지 않습니다. 자세한 내용은 [ \[4.3.1.6\] 섹션](https://go.microsoft.com/fwlink/?LinkId=114525)을 참조 하세요.  
  
## <a name="remarks"></a>설명  
 이 `namespace` 값에는 관련 된 네임 스페이스를 .NET Framework 프로그래밍의 일반적인 방법인 이름 계층으로 구성 하기 위한 추가 점이 포함 될 수 있습니다. 값의 `x:Class` 문자열에 있는 마지막 점은 개별 `namespace` 로 해석 되 고 `classname.` 로 `x:Class` 사용 되는 클래스는 중첩 된 클래스가 될 수 없습니다. 중첩 된 클래스를 사용할 수 있는 경우 문자열에 대 한 `x:Class` 점의 의미를 결정 하는 것은 허용 되지 않습니다.  
  
 `x:Class` 를`x:Class` 사용 하는 기존 프로그래밍 모델에서는 코드 숨김이 없는 XAML 페이지를 완전히 사용할 수 있다는 점에서 선택적 요소입니다. 그러나이 기능은 XAML을 사용 하는 프레임 워크에 의해 구현 되는 빌드 작업과 상호 작용 합니다. `x:Class`기능은 XAML로 지정 된 콘텐츠의 여러 분류가 응용 프로그램 모델 및 해당 빌드 작업에 포함 되는 역할의 영향을 받습니다. XAML이 이벤트 처리 특성 값을 선언 하거나 정의 클래스가 코드를 포함 하는 클래스에 있는 사용자 지정 요소를 인스턴스화하는 경우에는 `x:Class` 지시문 참조 (또는 [x:Subclass](x-subclass-directive.md))를 적절 한 클래스에 제공 해야 합니다. 코드 숨김이 있습니다.  
  
 `x:Class` 지시문의 값은 어셈블리 정보 없이 클래스의 정규화 된 이름을 지정 하는 문자열 이어야 합니다 (에 해당 <xref:System.Type.FullName%2A?displayProperty=nameWithType>). 간단한 응용 프로그램의 경우 코드 숨김이 해당 방식으로 구조화 된 경우 CLR 네임 스페이스 정보를 생략할 수 있습니다 (코드 정의는 클래스 수준에서 시작 됨).  
  
 페이지 또는 응용 프로그램 정의에 대 한 코드 숨겨진 파일은 컴파일된 응용 프로그램을 생성 하 고 태그 컴파일을 포함 하는 프로젝트의 일부로 포함 되는 코드 파일 내에 있어야 합니다. CLR 클래스에 대 한 이름 규칙을 따라야 합니다. 자세한 내용은 [프레임 워크 디자인 지침](../../standard/design-guidelines/index.md)을 참조 하세요. 기본적으로 코드 숨김이 클래스 `public`여야 합니다. 그러나 [x:classmodifier 지시어](x-classmodifier-directive.md)를 사용 하 여 다른 액세스 수준에서 정의할 수 있습니다.  
  
 이 `x:Class` 특성의 해석은 특히 xaml 서비스를 .NET Framework 하기 위해 CLR 기반 xaml 구현에만 적용 됩니다. CLR을 기반으로 하지 않고 .NET Framework XAML 서비스를 사용 하지 않는 다른 XAML 구현은 XAML 태그를 연결 하 고 런타임 코드를 지 원하는 데 다른 해결 수식을 사용할 수 있습니다. 의 `x:Class`일반적인 해석에 대 한 자세한 내용은 [ \[MS XAML\]](https://go.microsoft.com/fwlink/?LinkId=114525)을 참조 하십시오.  
  
 특정 수준의 아키텍처에서의 `x:Class` 의미는 .NET Framework XAML 서비스에서 정의 되지 않습니다. 이는 .NET Framework XAML 서비스에서 XAML 태그 및 백업 코드가 연결 되는 프로그래밍 모델을 지정 하지 않기 때문입니다. `x:Class` 지시문의 추가 사용은 프로그래밍 모델 또는 응용 프로그램 모델을 사용 하 여 XAML 태그 및 CLR 기반 코드 숨김으로 연결 하는 방법을 정의 하는 특정 프레임 워크에서 구현 될 수 있습니다. 각 프레임 워크에는 빌드 환경에 포함 되어야 하는 일부 동작이 나 특정 구성 요소를 사용할 수 있도록 하는 고유한 빌드 작업이 있을 수 있습니다. 프레임 워크 내에서 빌드 작업은 코드 숨김으로 사용 되는 특정 CLR 언어에 따라 달라질 수도 있습니다.  
  
## <a name="xclass-in-the-wpf-programming-model"></a>WPF 프로그래밍 모델의 x:Class  
 Wpf 응용 프로그램 및 wpf 응용 프로그램 모델 `x:Class` 에서는 xaml 파일의 루트이 고 컴파일되는 (xaml이 빌드 작업을 사용 하 `Page` 는 WPF 응용 프로그램 프로젝트에 포함 되는 경우) 또는에 대 한 특성으로 선언 될 수 있습니다. c4 > <xref:System.Windows.Application>  root는 컴파일된 WPF 응용 프로그램의 응용 프로그램 정의에 있습니다. 페이지 `x:Class` 루트나 응용 프로그램 루트 이외의 요소나 컴파일되지 않은 wpf xaml 파일에서 선언 하면 .NET Framework 3.0 및 .NET Framework 3.5 wpf xaml 컴파일러에서 컴파일 시간 오류가 발생 합니다. Wpf에서 처리의 `x:Class` 다른 측면에 대 한 자세한 내용은 [wpf의 코드 숨김과 XAML](../wpf/advanced/code-behind-and-xaml-in-wpf.md)을 참조 하세요.  
  
## <a name="xclass-for-windows-workflow-foundation"></a>Windows Workflow Foundation에 대 한 x:Class  
 Windows Workflow Foundation의 경우 `x:Class` 는 완전히 xaml로 구성 된 사용자 지정 작업의 클래스 이름을 지정 하거나 코드 숨김으로 활동 디자이너에 대 한 xaml 페이지의 partial 클래스의 이름을 지정 합니다.  
  
## <a name="silverlight-usage-notes"></a>Silverlight 사용 메모  
 `x:Class`Silverlight의는 별도로 설명 됩니다. 자세한 내용은 XAML 네임 스페이스 [(x:)를 참조 하세요. 언어 기능 (Silverlight)](https://go.microsoft.com/fwlink/?LinkId=199081).  
  
## <a name="see-also"></a>참고자료

- [x:Subclass 지시문](x-subclass-directive.md)
- [WPF에 대한 XAML 및 사용자 지정 클래스](../wpf/advanced/xaml-and-custom-classes-for-wpf.md)
- [x:ClassModifier 지시문](x-classmodifier-directive.md)
- [WPF에서 System.Xaml로 마이그레이션된 형식](types-migrated-from-wpf-to-system-xaml.md)
