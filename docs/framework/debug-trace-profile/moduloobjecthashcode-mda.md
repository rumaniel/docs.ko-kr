---
title: moduloObjectHashcode MDA
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), hashcode modulus
- Modulo object hash code
- moduloObjectHashcode MDA
- hashcode modulus
- MDAs (managed debugging assistants), hashcode modulus
- GetHashCode method
- modulus of hashcodes
ms.assetid: b45366ff-2a7a-4b8e-ab01-537b72e9de68
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1679e283a801044ad5a0baed89f17e6acc74259c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052451"
---
# <a name="moduloobjecthashcode-mda"></a>moduloObjectHashcode MDA
`moduloObjectHashcode` MDA(관리 디버깅 도우미)가 <xref:System.Object> 클래스의 동작을 변경하여 <xref:System.Object.GetHashCode%2A> 메서드에서 반환한 해시 코드에서 모듈로 작업을 수행합니다. 이 MDA의 기본 모듈러스는 1이므로, <xref:System.Object.GetHashCode%2A>에서 모든 개체에 대해 0을 반환합니다.  
  
## <a name="symptoms"></a>증상  
 새로운 버전의 CLR(공용 언어 런타임)로 이동하고 나면 프로그램이 더 이상 올바르게 실행되지 않습니다.  
  
- 프로그램이 <xref:System.Collections.Hashtable>에서 잘못된 개체를 가져옵니다.  
  
- <xref:System.Collections.Hashtable>의 열거형 순서에 프로그램을 중단시키는 변경 내용이 있습니다.  
  
- 서로 같았던 두 개의 개체가 더 이상 같지 않습니다.  
  
- 서로 같지 않았던 두 개의 개체가 이제 같습니다.  
  
## <a name="cause"></a>원인  
 키의 클래스에서 <xref:System.Object.Equals%2A> 메서드를 <xref:System.Collections.Hashtable>에 구현하면 <xref:System.Object.GetHashCode%2A> 메서드 호출 결과와 비교하여 개체의 동일성을 테스트하므로 프로그램이 <xref:System.Collections.Hashtable>에서 잘못된 개체를 가져올 수 있습니다. 각 필드의 값이 서로 달라도 두 개체의 해시 코드는 동일할 수 있으므로 개체의 동일성을 테스트하는 데 해시 코드를 사용하지 않아야 합니다. 해시 코드 충돌은 실제로는 매우 드물지만 발생할 수 있습니다. 이 경우 동일하지 않은 두 개의 키가 동일하게 표시되며 <xref:System.Collections.Hashtable>에서 잘못된 개체가 반환되는 식으로 <xref:System.Collections.Hashtable> 검색에 영향을 미칩니다. 성능상의 이유로 런타임 버전 간에 <xref:System.Object.GetHashCode%2A> 구현이 변경될 수 있으므로 한 버전에서 발생하지 않는 충돌이 후속 버전에서는 발생할 수 있습니다. 이 MDA를 사용하면 해시 코드가 충돌할 때 코드에 버그가 있는지 테스트할 수 있습니다. 이 MDA가 사용되면 <xref:System.Object.GetHashCode%2A> 메서드에서 0을 반환하므로, 모든 해시 코드 충돌의 원인이 됩니다. 이 MDA를 사용하면 프로그램 속도가 저하되는 영향만 미칩니다.  
  
 키의 해시 코드를 컴퓨팅하는 데 사용하는 알고리즘이 변경되면 <xref:System.Collections.Hashtable>의 열거형 순서가 런타임 버전 간 변경될 수 있습니다. 프로그램이 해시 테이블의 값 또는 키의 열거형 순서에 종속되는지 테스트하려면 이 MDA를 사용하도록 설정할 수 있습니다.  
  
## <a name="resolution"></a>해결  
 개체 ID의 대안으로 해시 코드를 사용하지 마세요. 해시 코드를 비교하지 않도록 <xref:System.Object.Equals%2A?displayProperty=nameWithType> 메서드의 재정의를 구현합니다.  
  
 해시 테이블에 있는 값 또는 키의 열거형 순서에 대한 종속성을 만들지 마세요.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA를 사용하면 애플리케이션이 더 느리게 실행됩니다. 이 MDA에서는 반환된 해시 코드를 사용한 다음 모듈러스를 통해 나누는 경우 나머지를 대신 반환합니다.  
  
## <a name="output"></a>출력  
 이 MDA에 대한 출력이 없습니다.  
  
## <a name="configuration"></a>구성  
 `modulus` 특성을 통해 해시 코드에서 사용된 모듈러스를 지정합니다. 기본값은 1입니다.  
  
```xml  
<mdaConfig>  
  <assistants>  
    <moduloObjectHashcode modulus="1" />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Object.GetHashCode%2A?displayProperty=nameWithType>
- <xref:System.Object.Equals%2A?displayProperty=nameWithType>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
