---
title: "'<parametername>' 매개 변수의 형식이 CLS 규격이 아닙니다."
ms.date: 07/20/2015
f1_keywords:
- vbc40028
- bc40028
helpviewer_keywords:
- BC40028
ms.assetid: dfa1f6f9-bb88-44ad-b85f-149144363d41
ms.openlocfilehash: 1f671b75972642670e28b9e761a8174d02d39c4e
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65642171"
---
# <a name="type-of-parameter-parametername-is-not-cls-compliant"></a>형식의 매개 변수 '\<parametername >' CLS 규격이 아님
으로 표시 되는 프로시저 `<CLSCompliant(True)>` 로 표시 된 형식과 매개 변수를 선언 하지만 `<CLSCompliant(False)>`는 표시 되지 않았거나, 비규격 형식 이므로 적합 하지 않습니다.  
  
 프로시저가 [언어 독립성 및 언어 독립적 구성 요소](../../../standard/language-independence-and-language-independent-components.md)(CLS)와 호환되려면 CLS 규격 형식만 사용해야 합니다. 이는 매개 변수 형식, 반환 형식 및 모든 로컬 변수 형식에 적용됩니다.  
  
 다음 Visual Basic 데이터 형식은 CLS 규격이 아닙니다.  
  
- [SByte 데이터 형식](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
- [UInteger 데이터 형식](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
- [ULong 데이터 형식](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
- [UShort 데이터 형식](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 <xref:System.CLSCompliantAttribute>를 프로그래밍 요소에 적용하는 경우 특성의 `isCompliant` 매개 변수를 `True` 또는 `False`로 설정하여 준수 여부를 나타냅니다. 이 매개 변수에는 기본값이 없으며 값을 제공해야 합니다.  
  
 요소에 <xref:System.CLSCompliantAttribute> 를 적용하지 않으면 비규격인 것으로 간주됩니다.  
  
 이 메시지는 기본적으로 경고입니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.  
  
 **오류 ID:** BC40028  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 이 특정 형식의 매개 변수가 프로시저를 수행 해야 하는 경우 제거를 <xref:System.CLSCompliantAttribute>입니다. 프로시저는 CLS 규격일 수 없습니다.  
  
- 프로시저가 CLS 규격 이어야 합니다 하는 경우이 매개 변수 형식의 가장 가까운 CLS 규격 형식으로 변경 합니다. 예를 들어 2,147,483,647을 초과하는 값 범위가 필요하지 않은 경우 `UInteger` 대신 `Integer` 을 사용할 수 있습니다. 확장된 범위가 필요한 경우 `UInteger` 를 `Long`으로 바꿀 수 있습니다.  
  
- 자동화 개체나 COM 개체를 사용 하 여 조작 하는 경우.NET Framework의 일부 형식의 데이터 너비가 있는 염두에 둡니다. 예를 들어 `int`는 다른 환경에서 16비트인 경우가 많습니다. 이러한 구성 요소에서 16 비트 정수를 수락 하는 경우로 선언 `Short` 대신 `Integer` 관리 되는 Visual Basic 코드에서.
