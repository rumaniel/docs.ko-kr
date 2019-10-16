---
title: 링크 요청
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [.NET Framework], demands
- demanded permissions
- permissions [.NET Framework], demands
- granting permissions, demands
- code access security, demands
- user demands for permission
- caller security checks
- link demands
ms.assetid: a33fd5f9-2de9-4653-a4f0-d9df25082c4d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f040e1e1706e1f84ced8b253ff3fb15dbcbd6e1e
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70206014"
---
# <a name="link-demands"></a>링크 요청
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 링크 요청으로 인해 Just-In-Time 컴파일 동안 보안 검사를 수행하며 코드의 직접 호출 어셈블리만 검사합니다. 연결은 함수 포인터 참조 및 메서드 호출을 포함하여 코드가 형식 참조에 바인딩된 경우에 발생합니다. 호출 어셈블리에 코드에 연결할 권한이 없는 경우 링크가 허용되지 않으며 코드가 로드 및 실행될 때 런타임 예외가 발생합니다. 코드에서 상속하는 클래스에서 링크 요청을 재정의할 수 있습니다.  
  
 이 형식의 요청에서는 전체 스택 워크가 수행되지 않으며 코드가 여전히 보안 공격에 취약합니다. 예를 들어 어셈블리 A의 메서드가 링크 요청에 의해 보호 되 면 어셈블리 b의 직접 호출자는 어셈블리 B의 권한에 따라 평가 됩니다.  그러나 어셈블리 B의 메서드를 사용 하 여 어셈블리 A에서 메서드를 간접적으로 호출 하는 경우 링크 요청은 어셈블리 C의 메서드를 평가 하지 않습니다. 링크 요청은 직접 호출 어셈블리의 직접 호출자가 코드에 연결 하는 데 필요한 권한만 지정 합니다. 모든 호출자가 코드를 실행하는 데 필요한 권한은 지정하지 않습니다.  
  
 <xref:System.Security.CodeAccessPermission.Assert%2A>, <xref:System.Security.CodeAccessPermission.Deny%2A> 및 <xref:System.Security.CodeAccessPermission.PermitOnly%2A> 스택 워크 한정자는 링크 요청의 평가에 영향을 주지 않습니다.  링크 요청은 스택 워크를 수행하지 않으므로 스택 워크 한정자가 링크 요청에 영향을 주지 않습니다.  
  
 [리플렉션을](../reflection-and-codedom/reflection.md)통해 링크 요청에 의해 보호 되는 메서드에 액세스 한 경우 링크 요청은 리플렉션을 통해 액세스 되는 코드의 직접 실행 호출자를 확인 합니다. 이는 리플렉션을 사용하여 수행된 메서드 호출 및 메서드 검색 둘 다에 적용됩니다. 예를 들어 코드에서 리플렉션을 사용 하 여 링크 <xref:System.Reflection.MethodInfo> 요청으로 보호 되는 메서드를 나타내는 개체를 반환한 다음 개체를 사용 하 여 원래 메서드를 호출 하는 다른 코드에 **MethodInfo** 개체를 전달 한다고 가정 합니다. 이 경우 링크 요청 검사는 **MethodInfo** 개체를 반환 하는 코드에 대해 한 번, 그리고 호출 하는 코드의 경우 한 번 수행 됩니다.  
  
> [!NOTE]
> 정적 생성자는 애플리케이션 코드 실행 경로 외부의 시스템에서 호출되므로 정적 클래스 생성자에서 수행되는 링크 요청은 생성자를 보호하지 않습니다. 따라서 링크 요청이 전체 클래스에 적용되는 경우 클래스의 나머지 부분은 보호하지만 정적 생성자에 대한 액세스를 보호할 수 없습니다.  
  
 다음 코드 조각에서는 `ReadData` 메서드에 연결하는 코드에 `CustomPermission` 권한이 있어야 함을 선언적으로 지정합니다. 이 권한은 가상의 사용자 지정 권한이며 .NET Framework에 존재하지 않습니다. 요청은 **SecurityAction** 플래그를에 `CustomPermissionAttribute`전달 하 여 수행 됩니다.  
  
```vb  
<CustomPermissionAttribute(SecurityAction.LinkDemand)> _  
Public Shared Function ReadData() As String  
    ' Access a custom resource.  
End Function    
```  
  
```csharp  
[CustomPermissionAttribute(SecurityAction.LinkDemand)]  
public static string ReadData()  
{  
    // Access a custom resource.  
}  
```  
  
## <a name="see-also"></a>참고자료

- [특성](../../standard/attributes/index.md)
- [코드 액세스 보안](code-access-security.md)
