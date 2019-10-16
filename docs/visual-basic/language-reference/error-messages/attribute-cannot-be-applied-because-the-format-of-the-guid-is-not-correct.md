---
title: "'GUID '<attribute>'의 형식이 올바르지 않으므로 '<number>'을(를) 적용할 수 없습니다."
ms.date: 07/20/2015
f1_keywords:
- vbc32500
- bc32500
helpviewer_keywords:
- BC32500
ms.assetid: 6fa34c55-368e-4d7d-b488-07a3fffe045f
ms.openlocfilehash: d27c326b6a88271ba4abf0144e71027f6671b17e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62054382"
---
# <a name="attribute-cannot-be-applied-because-the-format-of-the-guid-number-is-not-correct"></a>'\<특성 >' 때문에 적용할 수 없습니다. GUID의 형식은 '\<수 >' 올바르지 않습니다
`COMClassAttribute` 특성 블록 GUID에 대 한 적절 한 형식에 맞지 않는 전역적으로 고유 식별자 (GUID)를 지정 합니다. `COMClassAttribute` Guid를 사용 하 여 클래스, 인터페이스 및 생성 이벤트를 고유 하 게 식별 합니다.  
  
 GUID는 16바이트로 구성되며, 그중에서 처음 8바이트는 숫자이고 마지막 8바이트는 이진입니다. Uuidgen.exe와 같은 Microsoft 유틸리티에서 생성 하 고 시간과 공간에서 고유성이 보장 됩니다.  
  
 **오류 ID:** BC32500  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. COM 개체를 식별 하는 데 필요한 올바른 GUID를 결정 합니다.  
  
2. `COMClassAttribute` 특성 블록에 제공되는 GUID 문자열이 올바르게 복사되었는지 확인합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Guid>
- [특성 개요](../../../visual-basic/programming-guide/concepts/attributes/index.md)
