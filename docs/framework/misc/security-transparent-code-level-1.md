---
title: 보안 투명 코드, 수준 1
ms.date: 03/30/2017
helpviewer_keywords:
- transparent
- SecurityTreatAsSafeAttribute
- SecurityTransparentAttribute
- SecurityCriticalAttribute
- security-transparent code
- security [.NET Framework], security-transparent code
ms.assetid: 5fd8f46d-3961-46a7-84af-2eb1f48e75cf
author: mairaw
ms.author: mairaw
ms.openlocfilehash: efd3954b63a6683e04bd9143ca3523cdbace506d
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894532"
---
# <a name="security-transparent-code-level-1"></a>보안 투명 코드, 수준 1
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 투명도를 통해 개발자는 부분적으로 신뢰할 수 있는 코드에 기능을 노출하는 더 안전한 .NET Framework 라이브러리를 작성할 수 있습니다. 수준 1 투명도는 .NET Framework 버전 2.0에서 새로 추가되었고 주로 Microsoft 내에서만 사용됩니다. .NET Framework 4부터 [수준 2 투명도](security-transparent-code-level-2.md)를 사용할 수 있습니다. 그러나 이전 보안 규칙을 사용 하 여 실행 해야 하는 레거시 코드를 식별할 수 있도록 수준 1 투명도는 유지 되었습니다.  
  
> [!IMPORTANT]
> 수준 1 투명도는 호환성 목적으로만 지정해야 합니다. 즉, <xref:System.Security.AllowPartiallyTrustedCallersAttribute>를 사용하거나 투명도 모델을 사용하지 않는 .NET Framework 3.5 이하를 사용하여 개발된 코드에만 수준 1을 지정합니다. 예를 들어 부분적으로 신뢰할 수 있는 호출자(APTCA)의 호출을 허용하는 .NET Framework 2.0 어셈블리에는 수준 1 투명도를 사용합니다. .NET Framework 4 용으로 개발 된 코드의 경우 항상 수준 2 투명도를 사용 합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
- [수준 1 투명도 모델](#the_level_1_transparency_model)  
  
- [투명도 특성](#transparency_attributes)  
  
- [보안 투명성 예제](#security_transparency_examples)  
  
<a name="the_level_1_transparency_model"></a>   
## <a name="the-level-1-transparency-model"></a>수준 1 투명도 모델  
 수준 1 투명도를 사용할 경우 코드를 보안 투명, 보안 안전에 중요 및 보안에 중요 메서드로 구분하는 보안 모델을 사용하는 것입니다.  
  
 전체 어셈블리, 어셈블리의 일부 클래스 또는 클래스의 일부 메서드를 보안 투명으로 표시할 수 있습니다. 보안 투명 코드는 권한을 높일 수 없습니다. 이 제한에 따라 다음 세 가지 결과가 발생합니다.  
  
- 보안 투명 코드는 <xref:System.Security.Permissions.SecurityAction.Assert> 작업을 수행할 수 없습니다.  
  
- 보안 투명 코드로 충족되는 링크 요청은 전체 요청이 됩니다.  
  
- 보안 투명 코드에서 실행되어야 하는 안전하지 않은(확인할 수 없는) 코드로 인해 <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode> 보안 권한에 대한 전체 요청이 발생합니다.  
  
 이들 규칙은 CLR(공용 언어 런타임)에서 실행 중에 적용됩니다. 보안 투명 코드는 호출하는 코드의 모든 보안 요구 사항을 다시 호출자에게 전달합니다. 보안 투명 코드를 통해 전달되는 요청은 권한을 높일 수 없습니다. 조금 신뢰 애플리케이션이 보안 투명 코드를 호출하고 높은 권한에 대한 요청이 발생하면 요청이 다시 조금 신뢰 코드로 전달되고 실패합니다. 보안 투명 코드는 자산 작업을 수행할 수 없으므로 요청을 중지할 수 없습니다. 완전 신뢰 코드에서 같은 보안 투명 코드를 호출하면 요청이 성공합니다.  
  
 보안에 중요는 보안 투명과 반대입니다. 보안에 중요 코드는 완전 신뢰를 기반으로 실행되고 모든 권한 있는 작업을 수행할 수 있습니다. 보안 안전에 중요 코드는 부분적으로 신뢰할 수 있는 호출자가 액세스할 권한이 없는 리소스를 사용하도록 허용하지 않는지 확인하는 폭넓은 보안 감사를 통과한 권한 있는 코드입니다.  
  
 투명도를 명시적으로 적용해야 합니다. 데이터 조작 및 논리를 처리하는 대부분 코드는 일반적으로 보안 투명으로 표시되지만, 권한 상승을 수행하는 더 적은 코드는 보안에 중요 또는 보안 안전에 중요로 표시됩니다.  
  
> [!IMPORTANT]
> 수준 1 투명도는 어셈블리 범위로 제한되고 어셈블리 간에 적용되지 않습니다. 수준 1 투명도는 주로 Microsoft 내에서 보안 감사 목적으로만 사용됩니다. 다른 어셈블리의 보안 투명 코드에서 수준 1 어셈블리 내의 보안에 중요 형식 및 멤버에 액세스할 수 있습니다. 모든 수준 1 보안에 중요 형식 및 멤버에서 완전 신뢰를 위해 링크 요청을 수행해야 합니다. 보안 안전에 중요 형식 및 멤버는 형식 또는 멤버가 액세스하는 보호된 리소스에 대한 권한이 호출자에게 있는지 확인해야 합니다.  
  
 .NET Framework 이전 버전과의 호환성을 위해 투명도 특성을 사용하여 주석 처리되지 않은 모든 멤버는 보안 안전에 중요로 간주합니다. 주석으로 처리되지 않은 모든 형식은 투명으로 간주합니다. 투명도의 유효성을 검사하는 정적 분석 규칙은 없습니다. 따라서 런타임에 투명도 오류를 디버그해야 할 수 있습니다.  
  
<a name="transparency_attributes"></a>   
## <a name="transparency-attributes"></a>투명도 특성  
 다음 표에서는 투명도에 대한 코드를 주석으로 처리하는 데 사용하는 세 가지 특성에 대해 설명합니다.  
  
|특성|Description|  
|---------------|-----------------|  
|<xref:System.Security.SecurityTransparentAttribute>|어셈블리 수준에서만 허용됩니다. 어셈블리의 모든 형식 및 멤버를 보안 투명으로 식별합니다. 어셈블리는 보안에 중요 코드를 포함할 수 없습니다.|  
|<xref:System.Security.SecurityCriticalAttribute>|<xref:System.Security.SecurityCriticalAttribute.Scope%2A> 속성 없이 어셈블리 수준에서 사용될 경우 기본적으로 어셈블리의 모든 코드를 보안 투명으로 식별하지만 어셈블리에 보안에 중요 코드를 포함할 수 있음을 나타냅니다.<br /><br /> 클래스 수준에서 사용될 경우 클래스 또는 메서드를 보안에 중요로 식별하지만 클래스 멤버는 비와 같이 식별하지 않습니다. 모든 멤버를 보안에 중요로 설정하려면 <xref:System.Security.SecurityCriticalAttribute.Scope%2A> 속성을 <xref:System.Security.SecurityCriticalScope.Everything>으로 설정합니다.<br /><br /> 멤버 수준에서 사용될 경우 특성은 해당 멤버에만 적용됩니다.<br /><br /> 보안에 중요로 식별된 클래스 또는 멤버는 권한 상승을 수행할 수 있습니다. **중요:**  수준 1 투명도에서 보안에 중요 형식 및 멤버는 어셈블리 외부에서 호출될 때 보안 안전에 중요로 처리됩니다. 권한이 없는 권한 상승을 방지하려면 완전 신뢰를 위한 링크 요청을 통해 보안에 중요 형식 및 멤버를 보호해야 합니다.|  
|<xref:System.Security.SecuritySafeCriticalAttribute>|어셈블리의 보안 투명 코드에서 액세스할 수 있는 보안에 중요 코드를 식별합니다. 그러지 않으면 보안 투명 코드가 같은 어셈블리의 private 또는 internal 보안에 중요 멤버에 액세스할 수 없습니다. 이렇게 하면 보안에 중요 코드에 영향을 미치고 예기치 않은 권한 상승이 발생할 수 있습니다. 보안 안전에 중요 코드는 엄격한 보안 감사를 통과해야 합니다. **참고:**  보안 안전에 중요 형식 및 멤버는 호출자의 권한을 확인하여 호출자에게 보호된 리소스에 액세스할 권한이 있는지 판별해야 합니다.|  
  
 <xref:System.Security.SecuritySafeCriticalAttribute> 특성을 사용하면 보안 투명 코드가 같은 어셈블리의 보안에 중요 멤버에 액세스할 수 있습니다. 어셈블리에서 보안 투명 및 보안에 중요 코드를 두 어셈블리로 구분하는 것이 좋습니다. 보안 투명 코드는 보안에 중요 코드의 private 또는 internal 멤버를 확인할 수 없습니다. 또한 일반적으로 보안에 중요 코드는 public 인터페이스에 대한 액세스 권한이 있는지 감사됩니다. 사용자는 어셈블리 외부에서 private 또는 internal 상태에 액세스할 수 있다고 예상하지 않고 격리된 상태로 유지하려고 합니다. <xref:System.Security.SecuritySafeCriticalAttribute> 특성은 필요할 때 격리를 재정의하는 기능을 제공하면서 보안 투명 및 보안에 중요 코드 간의 상태 격리를 유지합니다. 보안 투명 코드는 해당 멤버를 <xref:System.Security.SecuritySafeCriticalAttribute>로 표시하지 않으면 private 또는 internal 보안에 중요 코드에 액세스할 수 없습니다. <xref:System.Security.SecuritySafeCriticalAttribute>를 적용하기 전에 공개적으로 노출된 것처럼 해당 멤버를 감사합니다.  
  
### <a name="assembly-wide-annotation"></a>어셈블리 수준 주석  
 다음 표에서는 어셈블리 수준에서 보안 특성을 사용하는 효과에 대해 설명합니다.  
  
|Assembly 특성|어셈블리 상태|  
|------------------------|--------------------|  
|부분적으로 신뢰할 수 있는 어셈블리에 대한 특성 없음|모든 형식 및 멤버가 투명합니다.|  
|완전히 신뢰할 수 있는 어셈블리에 대한 특성 없음(전역 어셈블리 캐시에 포함 또는 `AppDomain`에서 완전 신뢰로 식별됨)|모든 형식은 투명하고 모든 멤버는 보안 안전에 중요합니다.|  
|`SecurityTransparent`|모든 형식 및 멤버가 투명합니다.|  
|`SecurityCritical(SecurityCriticalScope.Everything)`|모든 형식 및 멤버가 보안에 중요합니다.|  
|`SecurityCritical`|모든 코드가 기본적으로 투명으로 설정됩니다. 그러나 개별 형식 및 멤버는 다른 특성을 포함할 수 있습니다.|  
  
<a name="security_transparency_examples"></a>   
## <a name="security-transparency-examples"></a>보안 투명도 예제  
 .NET Framework 2.0 투명도 규칙(수준 1 투명도)을 사용하려면 다음 어셈블리 주석을 사용합니다.  
  
```csharp
[assembly: SecurityRules(SecurityRuleSet.Level1)]  
```  
  
 어셈블리가 중요 코드를 포함하지 않고 권한을 높이지 않음을 나타내도록 전체 어셈블리를 투명하게 설정하려면 다음 특성을 사용하여 어셈블리에 투명도를 명시적으로 추가하면 됩니다.  
  
```csharp  
[assembly: SecurityTransparent]  
```  
  
 같은 어셈블리에서 위험 및 투명 코드를 혼합하려면 먼저 다음과 같이 어셈블리를 <xref:System.Security.SecurityCriticalAttribute> 특성으로 표시하여 어셈블리가 위험 코드를 포함할 수 있음을 나타냅니다.  
  
```csharp  
[assembly: SecurityCritical]  
```  
  
 보안에 위험 작업을 수행하려면 다음 코드 예제와 같이 위험 작업을 수행할 코드를 다른 <xref:System.Security.SecurityCriticalAttribute> 특성으로 명시적으로 표시해야 합니다.  
  
```csharp  
[assembly: SecurityCritical]  
public class A  
{  
    [SecurityCritical]  
    private void Critical()  
    {  
        // critical  
    }  
  
    public int SomeProperty  
    {  
        get {/* transparent */ }  
        set {/* transparent */ }  
    }  
}  
public class B  
{
    internal string SomeOtherProperty  
    {  
        get { /* transparent */ }  
        set { /* transparent */ }  
    }  
}  
```  
  
 명시적으로 보안에 위험으로 표시된 `Critical` 메서드를 제외하고 이전 코드는 투명합니다. 어셈블리 수준 <xref:System.Security.SecurityCriticalAttribute> 특성을 사용해도 투명도는 기본 설정입니다.  
  
## <a name="see-also"></a>참고자료

- [보안 투명 코드, 수준 2](security-transparent-code-level-2.md)
- [보안 변경 내용](../security/security-changes.md)
