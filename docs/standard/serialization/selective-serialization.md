---
title: 선택적 serialization
ms.date: 08/07/2017
dev_langs:
- CSharp
helpviewer_keywords:
- serialization, selective serialization
- binary serialization, selective serialization
ms.assetid: 39c56635-95d2-4afd-aff1-b022e7649bb3
ms.openlocfilehash: af608031a661037b89c9783ac2451a6b536f9cd4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61712480"
---
# <a name="selective-serialization"></a>선택적 serialization
클래스에는 흔히 직렬화하지 않아야 하는 필드가 있습니다. 예를 들어 클래스가 멤버 변수에 스레드 ID를 저장하는 경우입니다. 클래스가 deserialize되면 클래스가 직렬화된 시점에 대한 ID가 저장된 스레드가 더 이상 실행 중이지 않을 수 있으므로 이 값을 직렬화하는 것은 의미가 없습니다. 다음과 같이 멤버 변수를 [NonSerialized](xref:System.NonSerializedAttribute) 특성으로 표시하여 해당 변수가 직렬화되는 것을 방지할 수 있습니다.  
  
```csharp  
[Serializable]  
public class MyObject   
{  
  public int n1;  
  [NonSerialized] public int n2;  
  public String str;  
}  
```

가능한 경우 보안에 민감한 데이터가 포함될 수 있는 개체는 serialize할 수 없게 만드십시오. 개체를 직렬화할 수 있어야 하는 경우에는 중요한 데이터가 저장되는 특정 필드에 `NonSerialized` 특성을 적용하세요. 이러한 필드를 serialization에서 제외하지 않는 경우에는 저장되는 데이터가 직렬화 권한이 있는 모든 코드에 노출됩니다. 보안 serialization 코드 작성에 대한 자세한 내용은 [보안 및 Serialization](../../../docs/framework/misc/security-and-serialization.md)을 참조하세요.

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]
  
## <a name="see-also"></a>참고자료

- [이진 serialization](binary-serialization.md)
- [XML 및 SOAP serialization](xml-and-soap-serialization.md)
- [보안 및 Serialization](../../../docs/framework/misc/security-and-serialization.md)
