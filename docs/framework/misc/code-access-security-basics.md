---
title: 코드 액세스 보안 기본 사항
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [.NET Framework], code access security
ms.assetid: 4eaa6535-d9fe-41a1-91d8-b437cfc16921
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d77683dde24eeec5de7f1e541a6cc86f3b0c6617
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205623"
---
# <a name="code-access-security-basics"></a>코드 액세스 보안 기본 사항

[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]

공용 언어 런타임을 대상으로 하는 모든 애플리케이션(즉, 관리되는 모든 애플리케이션)은 런타임의 보안 시스템과 상호 작용해야 합니다. 관리되는 애플리케이션이 로드되면 해당 호스트가 자동으로 권한 집합을 부여합니다. 이러한 권한은 호스트의 로컬 보안 설정이나 애플리케이션이 있는 샌드박스에 의해 결정됩니다. 이러한 권한에 따라 애플리케이션이 올바르게 실행되거나 보안 예외를 생성합니다.

데스크톱 애플리케이션에 대한 기본 호스트는 완전 신뢰로 코드를 실행할 수 있도록 합니다. 따라서 애플리케이션이 데스크톱을 대상으로 하는 경우 무제한 권한 집합을 갖습니다. 다른 호스트 또는 샌드박스는 애플리케이션에 대해 제한된 권한 집합을 제공합니다. 호스트마다 권한 집합이 변경될 수 있으므로 대상 호스트에서 허용하는 권한만 사용하도록 애플리케이션을 디자인해야 합니다.

공용 언어 런타임을 대상으로 하는 효과적인 애플리케이션을 작성하려면 다음 코드 액세스 보안 개념을 잘 알고 있어야 합니다.

- **형식이 안전한 코드**: 형식 안전 코드는 잘 정의 된 허용 되는 방식 으로만 형식에 액세스 하는 코드입니다. 예를 들어 유효한 개체 참조가 지정된 경우 형식이 안전한 코드는 실제 필드 멤버에 해당하는 고정된 오프셋의 메모리에 액세스할 수 있습니다. 코드가 공개적으로 노출된 해당 개체의 필드에 속하는 메모리 범위를 벗어난 임의 오프셋의 메모리에 액세스하는 경우에는 형식이 안전하지 않습니다. 코드가 코드 액세스 보안을 활용할 수 있게 하려면 형식 안정성이 확인된 코드를 생성하는 컴파일러를 사용해야 합니다. 자세한 내용은이 항목의 뒷부분에 있는 [안정형 형식 안전 코드 작성](#typesafe_code) 섹션을 참조 하십시오.

- **명령적 및 선언적 구문**: 공용 언어 런타임을 대상으로 하는 코드는 권한을 요청 하 고, 호출자에 게 권한을 지정 하 고, 특정 보안 설정 (충분 한 권한이 부여 됨)을 재정의 하 여 보안 시스템과 상호 작용할 수 있습니다. 선언적 구문 및 명령적 구문의 두 가지 구문 형식은 사용하여 .NET Framework 보안 시스템과 프로그래밍 방식으로 상호 작용합니다. 선언적 호출은 특성을 사용하여 수행되고, 명령적 호출은 코드 내에서 클래스의 새 인스턴스를 사용하여 수행됩니다. 명령적으로만 수행할 수 있는 호출도 있고, 선언적으로만 수행할 수 있는 호출도 있고, 두 가지 방식 중 하나로 수행할 수 있는 호출도 있습니다.

- **보안 클래스 라이브러리**: 보안 클래스 라이브러리는 보안 요구를 사용 하 여 라이브러리의 호출자에 게 라이브러리가 노출 하는 리소스에 액세스할 수 있는 권한이 있는지 확인 합니다. 예를 들어 보안 클래스 라이브러리에 호출자에게 파일을 만들 수 있는 권한이 있도록 요구하는 파일 생성 메서드가 있을 수 있습니다. .NET Framework는 보안 클래스 라이브러리로 구성되어 있습니다. 코드에서 사용하는 라이브러리에 액세스하는 데 필요한 권한을 알고 있어야 합니다. 자세한 내용은이 항목의 뒷부분에 있는 [보안 클래스 라이브러리 사용](#secure_library) 단원을 참조 하십시오.

- **투명 코드**: .NET Framework 4부터 특정 사용 권한을 식별 하는 것 외에도 코드를 보안 투명으로 실행할지 여부도 결정 해야 합니다. 보안 투명 코드는 보안에 중요한 것으로 식별된 형식이나 멤버를 호출할 수 없습니다. 이 규칙은 완전 신뢰 애플리케이션과 부분적으로 신뢰할 수 있는 애플리케이션에 적용됩니다. 자세한 내용은 [보안 투명 코드](security-transparent-code.md)를 참조 하세요.

<a name="typesafe_code"></a>

## <a name="writing-verifiably-type-safe-code"></a>형식 안정성이 확인된 코드 작성

JIT(Just-In-Time) 컴파일은 코드를 검사하고 코드의 형식이 안전한지 여부를 확인하려고 하는 검증 프로세스를 수행합니다. 확인 하는 동안 형식이 안전한 것으로 입증 된 코드를 *안정형 형식 안전 코드*라고 합니다. 코드 형식이 안전해도 검증 프로세스나 컴파일러의 제한 사항 때문에 형식 안전성이 아직 확인되지 않았을 수 있습니다. 모든 언어가 형식이 안전한 것은 아니며, Microsoft Visual C++와 같은 일부 언어 컴파일러는 형식 안전성이 확인된 관리 코드를 생성할 수 없습니다. 사용하는 언어 컴파일러가 형식 안전성이 확인된 코드를 생성하는지 여부를 확인하려면 컴파일러의 설명서를 참조하세요. 특정 언어 구문을 사용 하지 않는 경우에만 확인 가능한 형식 안전 코드를 생성 하는 언어 컴파일러를 사용 하는 경우 [PEVerify 도구](../tools/peverify-exe-peverify-tool.md) 를 사용 하 여 코드의 형식이 안전한 지 여부를 확인 하는 것이 좋습니다.

보안 정책에서 검증을 건너뛸 수 있도록 허용하는 경우 형식 안전성이 확인되지 않은 코드가 실행을 시도할 수 있습니다. 그러나 형식 안전성은 런타임의 어셈블리 격리 메커니즘에서 필수 부분이므로 코드가 형식 안전성 규칙을 위반하는 경우 보안을 안정적으로 적용할 수 없습니다. 기본적으로 형식이 안전하지 않은 코드는 로컬 컴퓨터에서 시작된 경우에만 실행할 수 있습니다. 따라서 모바일 코드는 형식이 안전해야 합니다.

<a name="secure_library"></a>

## <a name="using-secure-class-libraries"></a>보안 클래스 라이브러리 사용

코드가 클래스 라이브러리에 필요한 권한을 요청하고 부여된 경우 라이브러리에 액세스할 수 있으며, 라이브러리에서 노출하는 리소스가 무단 액세스로부터 보호됩니다. 코드에 적절한 권한이 없는 경우 클래스 라이브러리에 액세스할 수 없으며, 악성 코드가 코드를 사용하여 보호된 리소스에 간접적으로 액세스할 수 없습니다. 코드를 호출하는 다른 코드에도 라이브러리에 액세스할 수 있는 권한이 있어야 합니다. 권한이 없는 경우 코드 실행도 제한됩니다.

코드 액세스 보안은 코드를 작성하는 사람의 오류 가능성을 제거하지 않습니다. 그러나 애플리케이션이 보안 클래스 라이브러리를 사용하여 보호된 리소스에 액세스하는 경우 클래스 라이브러리에서 잠재적인 보안 문제가 철저히 검사되기 때문에 애플리케이션 코드의 보안 위험이 감소합니다.

## <a name="declarative-security"></a>선언적 보안

선언적 보안 구문에서는 [특성](../../standard/attributes/index.md) 을 사용 하 여 보안 정보를 코드의 [메타 데이터로](../../standard/metadata-and-self-describing-components.md) 저장 합니다. 어셈블리, 클래스 또는 멤버 수준에 특성을 배치하여 사용할 요청, 요구 또는 재정의 형식을 나타낼 수 있습니다. 요청은 애플리케이션이 요구하거나 원하지 않는 권한에 대해 런타임 보안 시스템에 알리기 위해 공용 언어 런타임을 대상으로 하는 애플리케이션에서 사용됩니다. 요구와 재정의는 호출자로부터 리소스를 보호하거나 기본 보안 동작을 재정의하기 위해 라이브러리에서 사용됩니다.

> [!NOTE]
> .NET Framework 4에서는 .NET Framework 보안 모델 및 용어에 대 한 중요 한 변경 내용이 있습니다. 이러한 변경 내용에 대 한 자세한 내용은 [보안 변경 내용](../security/security-changes.md)을 참조 하세요.

선언적 보안 호출을 사용하려면 필요한 특정 형식의 권한을 나타내도록 권한 개체의 상태 데이터를 초기화해야 합니다. 모든 기본 제공 권한에는 수행할 보안 작업 형식을 설명하는 <xref:System.Security.Permissions.SecurityAction> 열거형이 전달되는 특성이 있습니다. 그러나 권한은 고유한 전용 매개 변수도 수락합니다.

다음 코드 조각에서는 코드의 호출자에게 `MyPermission`이라는 사용자 지정 권한이 있도록 요청하는 선언적 구문을 보여 줍니다. 이 권한은 가상의 사용자 지정 권한이며 .NET Framework에 존재하지 않습니다. 이 예제에서 선언적 호출은 클래스 정의 바로 앞에 배치되며 이 권한이 클래스 수준에 적용되도록 지정합니다. 이 특성에는 호출자가를 실행 하기 위해이 권한이 있어야 하도록 지정 하기 위해 **SecurityAction** 구조가 전달 됩니다.

```vb
<MyPermission(SecurityAction.Demand, Unrestricted = True)> Public Class MyClass1

   Public Sub New()
      'The constructor is protected by the security call.
   End Sub

   Public Sub MyMethod()
      'This method is protected by the security call.
   End Sub

   Public Sub YourMethod()
      'This method is protected by the security call.
   End Sub
End Class
```

```csharp
[MyPermission(SecurityAction.Demand, Unrestricted = true)]
public class MyClass
{
   public MyClass()
   {
      //The constructor is protected by the security call.
   }

   public void MyMethod()
   {
      //This method is protected by the security call.
   }

   public void YourMethod()
   {
      //This method is protected by the security call.
   }
}
```

## <a name="imperative-security"></a>명령적 보안

명령적 보안 구문은 호출할 권한 개체의 새 인스턴스를 만들어 보안 호출을 실행합니다. 명령적 구문을 사용하여 요구 및 재정의를 수행할 수 있지만 요청은 수행할 수 없습니다.

보안 호출을 수행하기 전에 필요한 특정 형식의 권한을 나타내도록 권한 개체의 상태 데이터를 초기화해야 합니다. 예를 들어 <xref:System.Security.Permissions.FileIOPermission> 개체를 만들 때 생성자를 사용 하 여 모든 파일에 대 한 무제한 액세스 또는 파일에 대 한 액세스 권한 없음을 나타내도록 **FileIOPermission** 개체를 초기화할 수 있습니다. 또는 다른 **FileIOPermission** 개체를 사용 하 여 개체에서 나타낼 액세스 형식 (즉, 읽기, 추가 또는 쓰기) 및 개체에서 보호할 파일을 나타내는 매개 변수를 전달할 수 있습니다.

명령적 보안 구문을 사용하여 단일 보안 개체를 호출하는 것은 물론 권한 집합에 있는 권한 그룹을 초기화할 수도 있습니다. 예를 들어이 기술은 한 방법으로 여러 권한에 대해 [assert](using-the-assert-method.md) 호출을 안정적으로 수행 하는 유일한 방법입니다. <xref:System.Security.PermissionSet> 및 <xref:System.Security.NamedPermissionSet> 클래스를 사용하여 권한 그룹을 만든 다음 적절한 메서드를 호출하여 원하는 보안 호출을 호출합니다.

명령적 구문을 사용하여 요구 및 재정의를 수행할 수 있지만 요청은 수행할 수 없습니다. 권한 상태를 초기화하기 위해 필요한 정보가 런타임에만 알려지는 경우 선언적 구문 대신 명령적 구문을 요구 및 재정의에 사용할 수 있습니다. 예를 들어 호출자에게 특정 파일을 읽을 수 있는 권한이 있도록 해야 하지만 런타임까지 해당 파일의 이름을 알 수 없는 경우 명령적 요구를 사용합니다. 런타임에 조건이 유지되는지 및 테스트 결과에 따라 보안 요구를 수행할지 여부를 결정해야 하는 경우 선언적 검사 대신 명령적 검사를 사용하도록 선택할 수도 있습니다.

다음 코드 조각에서는 코드의 호출자에게 `MyPermission`이라는 사용자 지정 권한이 있도록 요청하는 명령적 구문을 보여 줍니다. 이 권한은 가상의 사용자 지정 권한이며 .NET Framework에 존재하지 않습니다. `MyPermission`의 새 인스턴스가 `MyMethod`에서 생성되어 이 메서드만 보안 호출을 통해 보호합니다.

```vb
Public Class MyClass1

   Public Sub New()

   End Sub

   Public Sub MyMethod()
      'MyPermission is demanded using imperative syntax.
      Dim Perm As New MyPermission()
      Perm.Demand()
      'This method is protected by the security call.
   End Sub

   Public Sub YourMethod()
      'YourMethod 'This method is not protected by the security call.
   End Sub
End Class
```

```csharp
public class MyClass {
   public MyClass(){

   }

   public void MyMethod() {
       //MyPermission is demanded using imperative syntax.
       MyPermission Perm = new MyPermission();
       Perm.Demand();
       //This method is protected by the security call.
   }

   public void YourMethod() {
       //This method is not protected by the security call.
   }
}
```

## <a name="using-managed-wrapper-classes"></a>관리되는 래퍼 클래스 사용

대부분의 애플리케이션과 구성 요소(보안 라이브러리 제외)는 비관리 코드를 직접 호출하면 안 됩니다. 여기에는 여러 가지 이유가 있습니다. 코드에서 비관리 코드를 직접 호출하는 경우 네이티브 코드를 호출하기 위해 코드에 높은 신뢰 수준이 부여되어야 하기 때문에 실행할 수 없는 경우가 많습니다. 이러한 애플리케이션의 실행을 허용하도록 정책을 수정하면 시스템의 보안을 훨씬 약화되어 애플리케이션이 거의 모든 작업을 자유롭게 수행할 수 있게 됩니다.

또한 비관리 코드에 액세스할 수 있는 권한을 가진 코드에서 관리되지 않는 API를 호출하여 거의 모든 작업을 수행할 수 있습니다. 예를 들어 비관리 코드를 호출할 수 있는 권한이 있는 코드는 파일 <xref:System.Security.Permissions.FileIOPermission> 에 액세스할 필요가 없으며, **FileIOPermission**이 필요한 관리 되는 파일 api를 우회 하 여 관리 되지 않는 (Win32) 파일 api를 직접 호출할 수 있습니다. 관리 코드에 비관리 코드를 호출할 수 있는 권한이 있고 비관리 코드를 직접 호출하는 경우 런타임이 비관리 코드에 보안 제한을 적용할 수 없기 때문에 보안 시스템에서 이러한 제한을 안정적으로 적용할 수 없습니다.

애플리케이션에서 비관리 코드에 액세스해야 하는 작업을 수행하려는 경우 필요한 기능을 래핑하는 신뢰할 수 있는 관리되는 클래스를 통해 수행해야 합니다(이러한 클래스가 있는 경우). 보안 클래스 라이브러리에 이미 있는 경우 래퍼 클래스를 직접 만들지 마세요. 비관리 코드를 호출할 수 있도록 높은 신뢰 수준이 부여되어야 하는 래퍼 클래스는 호출자에게 적절한 권한이 있도록 요구해야 합니다. 래퍼 클래스를 사용하는 경우 코드에서 요청하기만 하면 래퍼 클래스가 요구하는 권한이 부여됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Security.PermissionSet>
- <xref:System.Security.Permissions.FileIOPermission>
- <xref:System.Security.NamedPermissionSet>
- <xref:System.Security.Permissions.SecurityAction>
- [Assert](using-the-assert-method.md)
- [코드 액세스 보안](code-access-security.md)
- [코드 액세스 보안 기본 사항](code-access-security-basics.md)
- [특성](../../standard/attributes/index.md)
- [메타데이터 및 자동 기술 구성 요소](../../standard/metadata-and-self-describing-components.md)
