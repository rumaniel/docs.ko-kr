---
title: 보안 및 Serialization
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- code security, serialization
- serialization, security
- secure coding, serialization
- security [.NET Framework], serialization
ms.assetid: b921bc94-bd3a-4c91-9ede-2c8d4f78ea9a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e0b1f8979929dbb6872bbd53e1840b2d0520a31d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69910668"
---
# <a name="security-and-serialization"></a>보안 및 Serialization
다른 방법으로는 액세스할 수 없는 개체 인스턴스 데이터를 직렬화를 통해 다른 코드에서 보거나 수정할 수 있으므로 <xref:System.Security.Permissions.SecurityPermission> 플래그가 지정된 <xref:System.Security.Permissions.SecurityPermissionFlag.SerializationFormatter> 의 직렬화를 수행하려면 코드에 특수 권한이 필요합니다. 기본 정책에 따라 이 권한은 인터넷에서 다운로드한 코드나 인트라넷 코드에는 부여되지 않고 로컬 컴퓨터에 있는 코드에만 부여됩니다.  
  
 일반적으로 개체 인스턴스의 모든 필드가 직렬화되며 이는 해당 데이터가 인스턴스에 대해 직렬화된 데이터로 표시됨을 의미합니다. 멤버의 접근성과 관계 없이, 코드가 형식을 해석하여 데이터 값을 파악할 수 있습니다. 마찬가지로, 접근성 규칙과 관계 없이 역직렬화를 통해 직렬화된 표현에서 데이터를 추출하고 개체 상태를 직접 설정할 수 있습니다.  
  
 보안에 민감한 데이터를 포함할 수 있는 모든 개체는 가능하면 직렬화할 수 없도록 설정해야 합니다. 이러한 개체를 직렬화할 수 있도록 설정해야 하는 경우에는, 민감한 데이터가 포함된 특정 필드를 직렬화할 수 없도록 설정해 보세요. 이렇게 할 수 없는 경우, 직렬화할 수 있는 권한이 있는 모든 코드에 민감한 데이터가 노출되므로 악성 코드가 이러한 권한을 갖지 않도록 주의해야 합니다.  
  
 <xref:System.Runtime.Serialization.ISerializable> 인터페이스는 직렬화 인프라에서만 사용됩니다. 하지만 보호되지 않는 경우에는 중요 중보가 노출될 수 있습니다. **ISerializable**을 구현하여 사용자 지정 직렬화를 제공할 때는 다음 예방 조치를 취해야 합니다.  
  
- <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> SerializationFormatter **권한을 지정하여** SecurityPermission **을 요청하거나 메서드 출력에 중요 정보가 노출되지 않도록 하여** 메서드의 보안을 명시적으로 유지해야 합니다. 예를 들어:  
  
    ```vb  
    Public Overrides<SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter := True)>  _  
    Sub GetObjectData(info As SerializationInfo, context As StreamingContext)  
    End Sub  
    ```  
  
    ```csharp  
    [SecurityPermissionAttribute(SecurityAction.Demand,SerializationFormatter   
    =true)]  
    public override void GetObjectData(SerializationInfo info,   
    StreamingContext context)  
    {  
    }  
    ```  
  
- 직렬화에 사용되는 특수 생성자는 엄격한 입력 유효성 검사를 수행해야 하며 악성 코드가 악용할 수 없도록 보호하거나 비공개로 설정해야 합니다. 클래스를 명시적으로 만들거나 일종의 팩터리를 통해 간접적으로 만드는 경우와 같이 기타 모든 방법으로 이러한 클래스의 인스턴스를 가져오려면 이와 같은 보안 검사 및 권한을 적용해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [보안 코딩 지침](../../standard/security/secure-coding-guidelines.md)
