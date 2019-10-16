---
title: 지역화 특성 및 주석
ms.date: 03/30/2017
helpviewer_keywords:
- localization [WPF], attributes
- localization [WPF], comments
ms.assetid: ead2d9ac-b709-4ec1-a924-39927a29d02f
ms.openlocfilehash: 4f9c2700d8163988b7ea1e75bec1427778cf571c
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004899"
---
# <a name="localization-attributes-and-comments"></a>지역화 특성 및 주석
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 지역화 주석은 개발자가 지역화를 위한 규칙과 힌트를 제공 하기 위해 제공 하는 XAML 소스 코드 내 속성입니다. [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 지역화 주석에는 두 가지 정보 집합(지역화 가능성 특성 및 자유 형식 지역화 주석)이 포함됩니다. 지역화 가능성 특성은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 지역화 API가 사용하여 지역화할 리소스를 나타냅니다. 자유 형식 주석은 애플리케이션 작성자가 포함하려고 하는 정보입니다.  

<a name="Localizer_Comments_"></a>   
## <a name="localization-comments"></a>지역화 주석  
 태그 응용 프로그램 작성자가 텍스트 길이, 글꼴 패밀리 또는 글꼴 크기에 대 한 제약 조건과 같이 XAML의 특정 요소에 대 한 요구 사항이 있는 경우 XAML 코드의 주석을 사용 하 여이 정보를 지역화 담당자에 게 전달할 수 있습니다. 주석을 소스 코드에 추가하는 절차는 다음과 같습니다.  
  
1. 응용 프로그램 개발자는 지역화 주석을 XAML 소스 코드에 추가 합니다.  
  
2. 빌드 프로세스 중에 자유 형식 지역화 주석을 어셈블리에 남길지, 주석의 일부를 제거할지, 모든 주석을 제거할지 여부를 .proj 파일에서 지정할 수 있습니다. 제거된 주석은 별도의 파일에 기록됩니다. `LocalizationDirectivesToLocFile` 태그를 사용하여 옵션을 지정합니다. 예를 들면 다음과 같습니다.  
  
     `<LocalizationDirectivesToLocFile>` *값* `</LocalizationDirectivesToLocFile>`  
  
3. 할당할 수 있는 값은 다음과 같습니다.  
  
    - **None** - 주석과 특성이 모두 어셈블리 안에 유지되고 별도의 파일이 생성되지 않습니다.  
  
    - **CommentsOnly** - 어셈블리에서 주석만 제거하고 별도의 LocFile 파일에 둡니다.  
  
    - **All** - 주석과 특성을 어셈블리에서 모두 제거하고 둘 다 별도의 LocFile에 둡니다.  
  
4. 지역화 가능한 리소스를 BAML에서 추출할 경우 지역화 가능성 특성은 BAML 지역화 API에 의해 적용 됩니다.  
  
5. 자유 형식 주석만 포함하는 지역화 주석 파일은 나중에 지역화 프로세스에 통합됩니다.  
  
 다음 예제에서는 XAML 파일에 지역화 주석을 추가 하는 방법을 보여 줍니다.  
  
 `<TextBlock x:Id = "text01"`  
  
 `FontFamily = "Microsoft Sans Serif"`  
  
 `FontSize = "12"`  
  
 `Localization.Attributes = "$Content (Unmodifiable Readable Text)`  
  
 `FontFamily (Unmodifiable Readable)"`  
  
 `Localization.Comments = "$Content (Trademark)`  
  
 `FontSize (Trademark font size)" >`  
  
 `Microsoft`  
  
 `</TextBlock>`  
  
 위 샘플에서 Localization.Attributes 섹션에는 지역화 특성이 포함되어 있고 Localization.Comments 섹션에는 자유 형식 주석이 포함되어 있습니다. 다음 표에서는 특성 및 주석과 함께 지역화 담당자에게 어떤 의미가 있는지를 보여 줍니다.  
  
|지역화 특성|의미|  
|-----------------------------|-------------|  
|$Content (Unmodifiable Readable Text)|TextBlock 요소의 콘텐츠를 수정할 수 없습니다. 지역화 담당자는 “Microsoft” 단어를 변경할 수 없습니다. 콘텐츠는 지역화 담당자가 볼 수 있습니다(읽기 가능). 콘텐츠의 범주는 텍스트입니다.|  
|FontFamily (Unmodifiable Readable)|TextBlock 요소의 글꼴 패밀리 속성은 변경할 수 없지만 지역화 담당자가 볼 수 있습니다.|  
  
|지역화 자유 형식 주석|의미|  
|--------------------------------------|-------------|  
|$Content (Trademark)|애플리케이션 작성자는 TextBlock 요소의 콘텐츠가 상표라는 것을 지역화 담당자에게 알립니다.|  
|FontSize (Trademark font size)|애플리케이션 작성자는 글꼴 크기 속성을 표준 상표 크기에 맞춰야 한다는 것을 가리킵니다.|  
  
### <a name="localizability-attributes"></a>지역화 가능성 특성  
 Localization.Attributes의 정보에는 대상 값 이름과 연관된 지역화 가능성 값이 쌍으로 된 목록이 포함됩니다. 대상 이름은 속성 이름 또는 특수한 $Content 이름일 수 있습니다. 속성 이름인 경우 대상 값은 속성의 값입니다. $Content인 경우 대상 값은 요소의 콘텐츠입니다.  
  
 다음 세 가지 형식의 특성이 있습니다.  
  
- **Category** 지역화 담당자 도구에서 값을 수정할 수 있어야 하는지 여부를 지정합니다. <xref:System.Windows.LocalizabilityAttribute.Category%2A>을 참조하세요.  
  
- **가독성**. 지역화 담당자 도구에서 값을 읽고 표시해야 하는지 여부를 지정합니다. <xref:System.Windows.LocalizabilityAttribute.Readability%2A>을 참조하세요.  
  
- **수정 가능성**. 지역화 담당자 도구에서 값 수정을 허용하는지 여부를 지정합니다. <xref:System.Windows.LocalizabilityAttribute.Modifiability%2A>을 참조하세요.  
  
 이러한 특성은 공백으로 구분하여 임의의 순서로 지정할 수 있습니다. 중복된 특성이 지정된 경우 마지막 특성이 이전 특성을 재정의합니다. 예를 들어 Localization.Attributes = “Unmodifiable Modifiable”은 Modifiability를 마지막 값인 Modifiable로 설정합니다.  
  
 Modifiability 및 Readability는 이름만으로도 해당 의미를 이해할 수 있습니다. Category 특성은 지역화 담당자가 텍스트를 번역할 때 도움이 되는 미리 정의된 범주를 제공합니다. Text, Label 및 Title과 같은 범주는 텍스트를 번역하는 방법에 대한 정보를 지역화 담당자에게 제공합니다. 특수 범주도 있습니다. None, Inherit, Ignore 및 NeverLocalize입니다.  
  
 다음 표에서는 특수한 범주의 의미를 보여 줍니다.  
  
|Category|의미|  
|--------------|-------------|  
|없음|대상 값에 정의된 범주가 없습니다.|  
|상속|대상 값은 부모로부터 해당 범주를 상속합니다.|  
|무시|대상 값은 지역화 프로세스에서 무시됩니다. Ignore는 현재 값에만 영향을 줍니다. 자식 노드에 영향을 주지는 않습니다.|  
|NeverLocalize|현재 값을 지역화할 수 없습니다. 이 범주는 요소의 자식에 의해 상속됩니다.|  
  
<a name="Localization_Comments"></a>   
## <a name="localization-comments"></a>지역화 주석  
 Localization.Comments에는 대상 값에 대한 자유 형식 문자열이 포함됩니다. 애플리케이션 개발자는 애플리케이션 텍스트를 번역하는 방법에 대한 힌트를 지역화 담당자에게 제공하는 정보를 추가할 수 있습니다. 주석 형식은 “()”로 묶인 문자열일 수 있습니다. 문자를 이스케이프하려면 ‘\\’를 사용합니다.  
  
## <a name="see-also"></a>참조

- [WPF의 전역화](globalization-for-wpf.md)
- [자동 레이아웃을 사용하여 단추 만들기](how-to-use-automatic-layout-to-create-a-button.md)
- [자동 레이아웃에 그리드 사용](how-to-use-a-grid-for-automatic-layout.md)
- [애플리케이션 지역화](how-to-localize-an-application.md)
