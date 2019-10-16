---
title: CLS 규격 인터페이스에는 CLS 규격이 아닌 <membername>을(를) 사용할 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- bc40033
- vbc40033
helpviewer_keywords:
- BC40033
ms.assetid: 060c4b08-798e-40f1-94cf-c05c524f1b8a
ms.openlocfilehash: 68e1fb4f55d9f9b140f1b54cfde2bc5f60952dd2
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592132"
---
# <a name="non-cls-compliant-membername-is-not-allowed-in-a-cls-compliant-interface"></a>비-CLS 규격 \<membername > CLS 규격 인터페이스에 허용 되지 않습니다
속성, 프로시저 또는 인터페이스의 이벤트로 표시 됩니다 `<CLSCompliant(True)>` 인터페이스 자체으로 표시 되 면 `<CLSCompliant(False)>` 되거나 표시 되지 않습니다.  
  
 호환 되어야 하는 인터페이스에 대 한 합니다 [Language Independence and Language-independent Components](../../../standard/language-independence-and-language-independent-components.md) (CLS)와 모든 해당 멤버 규정을 준수 해야 합니다.  
  
 <xref:System.CLSCompliantAttribute>를 프로그래밍 요소에 적용하는 경우 특성의 `isCompliant` 매개 변수를 `True` 또는 `False`로 설정하여 준수 여부를 나타냅니다. 이 매개 변수에는 기본값이 없으며 값을 제공해야 합니다.  
  
 요소에 <xref:System.CLSCompliantAttribute> 를 적용하지 않으면 비규격인 것으로 간주됩니다.  
  
 이 메시지는 기본적으로 경고입니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.  
  
 **오류 ID:** BC40033  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- CLS 규격이 필요 하 고 인터페이스 소스 코드를 제어할 경우 표시 된 인터페이스로 `<CLSCompliant(True)>` 의 모든 멤버는 규정을 준수 하는 경우.  
  
- CLS 규격이 필요 하 고 인터페이스 소스 코드를 제어할 수 없는 경우 또는 호환 되도록 맞지 않을 경우 다른 인터페이스 내에서이 멤버를 정의 합니다.  
  
- 이 멤버는 현재 인터페이스 내에서 유지 하려면를 제거 합니다 <xref:System.CLSCompliantAttribute> 해당 정의에서 표시 하거나 `<CLSCompliant(False)>`합니다.  
  
## <a name="see-also"></a>참고자료

- [Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md)
