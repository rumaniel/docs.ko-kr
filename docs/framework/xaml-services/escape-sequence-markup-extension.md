---
title: '{}이스케이프 시퀀스 태그 확장'
ms.date: 03/30/2017
f1_keywords:
- '{}'
helpviewer_keywords:
- XAML [XAML Services], quotation mark (")
- '{} escape sequence [XAML Services]'
- XAML [XAML Services], {} escape sequence
- XAML [XAML Services], escape sequence
- quotation mark (") [XAML Services]
- escape sequence [XAML Services]
ms.assetid: 3ce3e2ad-a868-43f9-9c98-b29561cb146e
ms.openlocfilehash: b0646c62a1342eb160d1967e86ac286429013f3c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053869"
---
# <a name="-escape-sequence--markup-extension"></a>{} 이스케이프 시퀀스/태그 확장명
특성 값에 대 한 XAML 이스케이프 시퀀스를 제공 합니다. 이스케이프 시퀀스를 사용 하면 특성의 후속 값이 리터럴로 해석 됩니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object property="{} literalValue" .../>  
```  
  
## <a name="xaml-property-element-usage"></a>XAML 속성 요소 사용  
  
```xaml  
<object>  
  <object.property>  
    {} literalValue  
  </object.property>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|*literalValue*|이스케이프 시퀀스 뒤에 오는 리터럴 문자열입니다. 일반적으로이 문자열에는 여는 중괄호 ({또는})가 포함 됩니다.|  
  
## <a name="remarks"></a>설명  
 이스케이프 시퀀스 ({})는 XAML에서 여는 중괄호 ({)를 리터럴 문자로 사용할 수 있도록 하는 데 사용 됩니다.  
  
 일반적으로 XAML 판독기는 여는 중괄호 ({)를 사용 하 여 태그 확장의 진입점을 나타냅니다. 그러나 먼저 다음 문자를 검사 하 여 닫는 중괄호 (}) 인지 여부를 확인 합니다. 두 중괄호 ({})가 인접 한 경우에만 이스케이프 시퀀스로 간주 됩니다.  
  
 이스케이프 시퀀스가 발생 하는 경우 XAML 판독기는 문자열의 나머지를 문자열로 처리 해야 합니다. 그러나 이스케이프 시퀀스가 형식 변환기를 포함 하는 멤버에 적용 되는 경우에는 XAML 작성기에서 해석 될 때 문자열을 형식으로 변환할 수 있습니다.  
  
 이스케이프 시퀀스가 태그 확장이 아니고 클래스에서 지원 되지 않는 경우 그러나이는 XAML 판독기 (사용자 지정 XAML 판독기 포함)가 따라야 하는 규칙입니다.  
  
 이 방식에서는 따옴표 (")를 이스케이프 시퀀스로 사용할 수 없습니다. 콘텐츠가 아닌 속성의 속성 값으로 따옴표를 설정 해야 하는 경우 속성 요소 구문을 사용 하 고 따옴표를 속성 요소 내에 문자열로 삽입 하거나 XML 문자 엔터티를 사용 합니다. 콘텐츠 속성의 경우 인용 부호는 전체 콘텐츠가 될 수 있습니다.  
  
 이스케이프 시퀀스 ({})는 XAML 태그 확장이 나타날 수 있는 위치에 네임 스페이스 한정자를 포함 해야 하는 XML 형식을 지정할 때 자주 필요 합니다. 여기에는 XAML 특성 값의 시작과 태그 확장의 등호 (=) 바로 다음이 포함 됩니다. 다음 예제에서는 XAML 특성 값의 시작 부분에 표시 되는 XML 네임 스페이스에 대 한 이스케이프 시퀀스를 보여 줍니다.  
  
 [!code-xaml[XLINQExample#StackPanelResources](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#stackpanelresources)]  
  
## <a name="see-also"></a>참고자료

- [XAML을 위한 형식 변환기 및 태그 확장명](type-converters-and-markup-extensions-for-xaml.md)
- [XML 문자 엔터티 및 XAML](xml-character-entities-and-xaml.md)
