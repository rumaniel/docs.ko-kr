---
title: XAML의 xml:space 처리
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], xml:space attribute
- XAML [XAML Services], white-space processing
- xml:space attribute [XAML Services]
- white-space processing [XAML Services]
ms.assetid: 5e1814f0-5b30-43d5-8c88-dede335a89d7
ms.openlocfilehash: d15bab1ad9234959048fa7b7c3fa2bbbeca5fe6e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61938725"
---
# <a name="xmlspace-handling-in-xaml"></a>XAML의 xml:space 처리
`xml:space` 특성은 개체 요소 내에서 중요 한 공백 처리 동작을 선언 하는 XML로 정의 된 특성입니다. 이 동작 요소에 포함 된 모든 콘텐츠 (내부 텍스트)와 관련이 있는 `xml:space` 선언 되 고도 범위가 정해 집니다 자식 요소입니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object xml:space="preserve" />  
```  
  
 \- 또는 -  
  
```xaml  
<object xml:space="default" />  
```  
  
## <a name="remarks"></a>설명  
 에 대 한 정의 `xml:space` 가능한 두 값을 포함 하 여 XAML의 특성에서 파생 된 `xml:space` XML에 대 한 W3C 사양 "특수 특성"으로 정의 된 대로 합니다.  
  
 기본값은 `xml:space` 특성은 리터럴 값 `"default"`합니다. 값에 대 한 `"default"`, 또는 `xml:space` 항목에 정의 된 대로 중요 한 공백이 구문 분석의 동작은 기본 처리를 전혀 표시 되지 않습니다 [공백 XAML 처리](whitespace-processing-in-xaml.md)합니다.  
  
 개체 요소 콘텐츠 내에서 공백을 유지 하려면 지정 `xml:space="preserve"` 개체 요소에 해당 합니다.  
  
 대부분의 해석 된 `xml:space` 특성 효과 및 특성은 자식 요소에 범위가 지정 됩니다.  
  
 설명은 공백을 XAML 처리에 대 한 참조 [공백 XAML 처리](whitespace-processing-in-xaml.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [공백에서 XAML 처리](whitespace-processing-in-xaml.md)
- [XAML 개요(WPF)](../wpf/advanced/xaml-overview-wpf.md)
