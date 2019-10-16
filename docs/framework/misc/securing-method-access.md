---
title: 메서드 액세스 보안
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- code security, method access
- secure coding, method access
- security [.NET Framework], method access
- method access security
ms.assetid: f7c2d6ec-3b18-4e0e-9991-acd97189d818
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 74327e10e57c2f63519a3336ab2a600ad2b0a6b8
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70971051"
---
# <a name="securing-method-access"></a>메서드 액세스 보안
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 몇몇 메서드는 임의의 신뢰할 수 없는 코드 호출을 허용하는 데 적합하지 않을 수 있습니다. 이러한 메서드는 여러 가지 위험을 발생 시킵니다. 메서드는 몇 가지 제한 된 정보를 제공할 수 있습니다. 여기에 전달 된 모든 정보를 생각할 수 있습니다. 매개 변수에 대 한 오류 검사를 수행 하지 않을 수 있습니다. 또는 잘못 된 매개 변수를 사용 하는 경우 제대로 작동 하지 않거나 해로운 문제가 발생할 수 있습니다. 이들 경우에 대해 알고 있어야 하고 메서드 보호를 도와주는 조치를 취해야 합니다.  
  
 경우에 따라 공용으로 제공되지 않지만 공용으로 사용되어야 하는 메서드를 제한해야 할 수 있습니다. 예를 들어 자체 DLL에서 호출되어야 하고 공용으로도 사용되어야 하는 인터페이스를 포함하지만, 이 인터페이스를 고객이 사용하지 않도록 하고 악성 코드가 구성 요소에 대한 진입점으로 악용하지 못하도록 방지하기 위해 이 인터페이스를 공개적으로 노출하지 않고자 할 수 있습니다. 공용으로 제공되지 않은 메서드를 제한하는 또 다른 일반적인 이유는 완전히 내부적인 인터페이스일 수 있는 내용을 문서화하고 지원할 필요가 없도록 하려는 것입니다.  
  
 관리 코드는 메서드 액세스를 제한하는 여러 가지 방법을 제공합니다.  
  
- 액세스 가능성 범위를 신뢰할 수 있는 클래스, 어셈블리 또는 파생 클래스로 제한합니다. 이는 메서드 액세스를 제한하는 가장 간단한 방법입니다. 일반적으로 파생 클래스는 자신이 파생된 소스 클래스보다 신뢰도가 더 낮지만 경우에 따라 부모 클래스의 ID를 공유할 수 있습니다. 특히 보안 컨텍스트에서 반드시 사용 되는 것은 아니므로 **protected**키워드에서 트러스트를 유추 하지 마십시오.  
  
- 지정 된 id의 호출자에 대 한 액세스 권한을 제한 합니다. 기본적으로 특정 [증명 정보](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7y5x1hcd%28v=vs.100%29) (강력한 이름, 게시자, 영역 등)를 선택 합니다.  
  
- 메서드 액세스를 선택한 권한을 가진 호출자로 제한합니다.  
  
 마찬가지로 선언적 보안을 통해 클래스 상속을 제어할 수 있습니다. **InheritanceDemand** 를 사용 하 여 다음을 수행할 수 있습니다.  
  
- 지정된 ID 또는 권한을 포함할 파생 클래스가 필요합니다.  
  
- 지정된 ID 또는 권한을 포함하도록 특정 메서드를 재정의하는 파생 클래스가 필요합니다.  
  
 다음 예제에서는 특정 강력한 이름을 통해 호출자에 서명하도록 요구하여 제한된 액세스용 공용 클래스를 보호하도록 도와주는 방법을 보여 줍니다. 이 예제에서는 강력한 <xref:System.Security.Permissions.StrongNameIdentityPermissionAttribute> 이름에 대 한 **요청과** 함께를 사용 합니다. 강력한 이름을 사용 하 여 어셈블리에 서명 하는 방법에 대 한 작업 기반 정보는 [강력한 이름의 어셈블리 만들기 및 사용](../../standard/assembly/create-use-strong-named.md)을 참조 하세요.  
  
```vb  
<StrongNameIdentityPermissionAttribute(SecurityAction.Demand, PublicKey := "…hex…", Name := "App1", Version := "0.0.0.0")>  _  
Public Class Class1  
End Class  
```  
  
```csharp  
[StrongNameIdentityPermissionAttribute(SecurityAction.Demand, PublicKey="…hex…", Name="App1", Version="0.0.0.0")]  
public class Class1  
{  
  
}   
```  
  
## <a name="excluding-classes-and-members-from-use-by-untrusted-code"></a>신뢰할 수 없는 코드에 의한 클래스 및 멤버 사용 방지  
 이 섹션에 표시된 선언을 사용하여 특정 클래스와 메서드 및 속성과 이벤트가 부분 신뢰 코드에서 사용되지 않도록 방지합니다. 이들 선언을 클래스에 적용하여 모든 메서드, 속성 및 이벤트에 보호를 적용하지만, 필드 액세스는 선언적 보안의 영향을 받지 않습니다. 또한 링크 요청은 직접 실행 호출자 차단에만 도움이 되고 유인 공격의 대상이 될 수 있습니다.  
  
> [!NOTE]
> 새 투명도 모델은 .NET Framework 4에서 도입 되었습니다. [보안 투명 코드, 수준 2](security-transparent-code-level-2.md) 모델은 <xref:System.Security.SecurityCriticalAttribute> 특성을 사용 하 여 보안 코드를 식별 합니다. 보안에 중요한 코드에서는 호출자와 상속자를 둘 다 완전히 신뢰할 수 있어야 합니다. 이전 .NET Framework 버전에서 코드 액세스 보안 규칙에 따라 실행 중인 어셈블리는 수준 2 어셈블리를 호출할 수 있습니다. 이 경우 보안에 중요한 특성은 완전 신뢰를 위해 링크 요청으로 처리됩니다.  
  
 강력한 이름의 어셈블리에서 [LinkDemand](link-demands.md) 는 완전히 신뢰할 수 있는 호출자에 게 사용을 제한 하기 위해 공개적으로 액세스할 수 있는 모든 메서드, 속성 및 이벤트에 적용 됩니다. 이 기능을 사용하지 않도록 설정하려면 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 특성을 적용해야 합니다. 따라서 신뢰할 수 없는 호출자를 제외하도록 클래스에 명시적으로 표시하는 작업은 서명되지 않은 어셈블리나 이 특성이 포함된 어셈블리에만 필요합니다. 이들 선언을 사용하여 신뢰할 수 없는 호출자로 제공되지 않은 형식 하위 집합을 표시할 수 있습니다.  
  
 다음 예제에서는 클래스와 멤버가 신뢰할 수 없는 코드에서 사용되지 않도록 방지하는 방법을 보여 줍니다.  
  
 봉인되지 않은 공용 클래스의 경우:  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name := "FullTrust"), _   
System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _  
Public Class CanDeriveFromMe  
End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
public class CanDeriveFromMe  
{  
}  
```  
  
 봉인된 공용 클래스의 경우:  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _  
NotInheritable Public Class CannotDeriveFromMe  
End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
public sealed class CannotDeriveFromMe  
{  
}  
```  
  
 공용 추상 클래스의 경우:  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name := "FullTrust"), _  
System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _  
MustInherit Public Class CannotCreateInstanceOfMe_CanCastToMe  
End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
public abstract class CannotCreateInstanceOfMe_CanCastToMe {}  
```  
  
 공용 가상 함수의 경우:  
  
```vb  
Class Base1   
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _  
    Public Overridable Sub CanOverrideOrCallMe()  
    End Sub 'CanOverrideOrCallMe  
End Class 'Base1  
```  
  
```csharp  
class Base1   
{  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
    public virtual void CanOverrideOrCallMe() {}  
}  
```  
  
 공용 추상 함수의 경우:  
  
```vb  
MustInherit Class Base2  
    <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _  
    Public Sub MustOverrideMe()  
    End Sub  
End Class 'Base2  
```  
  
```csharp  
abstract class Base2 {  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
public abstract void MustOverrideMe();  
}  
```  
  
 기본 클래스가 완전 신뢰를 요청하지 않는 공용 재정의 함수의 경우:  
  
```vb  
Class Derived  
    Inherits Base1  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.Demand, Name:="FullTrust")> _  
    Public Overrides Sub CanOverrideOrCallMe()  
        MyBase.CanOverrideOrCallMe()  
    End Sub 'CanOverrideOrCallMe  
End Class 'Derived  
```  
  
```csharp  
class Derived : Base1  
{     
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.Demand, Name="FullTrust")]      
    public override void CanOverrideOrCallMe()   
    {  
        base.CanOverrideOrCallMe();  
    }  
}  
```  
  
 기본 클래스가 완전 신뢰를 요청하는 공용 재정의 함수의 경우:  
  
```vb  
Class Derived  
    Inherits Base1  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _  
    Public Overrides Sub CanOverrideOrCallMe()  
        MyBase.CanOverrideOrCallMe()  
    End Sub 'CanOverrideOrCallMe   
End Class 'Derived  
```  
  
```csharp  
class Derived : Base1  
{     
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]      
    public override void CanOverrideOrCallMe()   
    {  
        base.CanOverrideOrCallMe();  
    }  
}  
```  
  
 공용 인터페이스의 경우:  
  
```vb  
Public Interface ICanCastToMe  
    <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust")> _  
    Sub CanImplementMe()  
End Interface 'ICanCastToMe  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust")> _  
Class Implemented  
    Implements ICanCastToMe  
    Public Sub CanImplementMe()  
    End Sub 'CanImplementMe  
```  
  
```csharp  
public interface ICanCastToMe   
{  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")]  
void CanImplementMe();  
}  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")]  
class Implemented : ICanCastToMe  
{  
    public void CanImplementMe()  
    {  
    }  
}  
```  
  
## <a name="virtual-internal-overrides-or-overloads-overridable-friend"></a>Virtual Internal 재정의 또는 Overloads Overridable Friend  
  
> [!NOTE]
> 이 섹션에서는 메서드를 `virtual` 및 `internal` (`Overloads` `Overridable` VisualBasic)로선언할때발생하는보안문제에대해경고합니다.`Friend` 이 경고는 .NET Framework 버전 1.0 및 1.1에만 적용 되 고 이후 버전에는 적용 되지 않습니다.  
  
 .NET Framework 버전 1.0 및 1.1에서는 다른 어셈블리에서 코드를 사용할 수 없다는 것을 확인 하는 경우 형식 시스템 액세스 가능성의 nuance에 대해 알고 있어야 합니다. **가상** 및 **내부** (Visual Basic의**재정의 가능한 Friend** )로 선언 된 메서드는 부모 클래스의 vtable 항목을 재정의할 수 있으며 내부 이기 때문에 동일한 어셈블리 내 에서만 사용할 수 있습니다. 그러나 재정의할 수 있는 액세스 가능성은 **virtual** 키워드에 의해 결정 되며, 해당 코드가 클래스 자체에 액세스할 수 있는 한 다른 어셈블리에서 재정의할 수 있습니다. 재정의가 문제를 발생 시킬 가능성이 있는 경우 선언적 보안을 사용 하 여 문제를 해결 하거나, 꼭 필요 하지 않은 경우 **가상** 키워드를 제거 합니다.  
  
 언어 컴파일러에서 컴파일 오류 때문에 이 재정의가 차단되더라도 다른 컴파일러로 작성된 코드는 재정의될 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [보안 코딩 지침](../../standard/security/secure-coding-guidelines.md)
