---
title: 형식 멤버의 이름
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- events [.NET Framework], names
- methods [.NET Framework], names
- type members
- properties [.NET Framework], names
- fields, names
- field names
- names [.NET Framework], type members
- members [.NET Framework], type
ms.assetid: af5a0903-36af-4c2a-b848-cf959affeaa5
author: KrzysztofCwalina
ms.openlocfilehash: b4da14575d29582814d32a3050087b7acc0da802
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353714"
---
# <a name="names-of-type-members"></a>형식 멤버의 이름
형식은 메서드, 속성, 이벤트, 생성자 및 필드 등의 멤버로 이루어집니다. 다음 섹션에서는 형식 멤버 이름 지정에 대한 지침을 설명합니다.  
  
## <a name="names-of-methods"></a>메서드 이름  
 메서드가 작업을 수행하는 수단이기 때문에 디자인 지침에서는 메서드 이름이 동사 또는 동사구여야 합니다. 또한 이 지침을 따르면 명사 또는 형용사구인 속성 및 형식 이름과 메서드 이름을 구분할 수 있습니다.  
  
 **✓ DO**를 통해 동사 또는 동사구인 메서드 이름을 지정합니다.  
  
```csharp  
public class String {  
    public int CompareTo(...);  
    public string[] Split(...);  
    public string Trim();  
}  
```  
  
## <a name="names-of-properties"></a>속성 이름  
 다른 멤버와 달리 속성은 명사구 또는 형용사 이름이 지정되어야 합니다. 속성이 데이터를 나타내기 때문에 속성 이름은 이를 반영해야 합니다. PascalCasing은 속성 이름에 항상 사용됩니다.  
  
 **✓ DO**는 명사, 명사구 또는 형용사를 사용하여 속성 이름을 지정합니다.  
  
 **X DO NOT**에는 다음 예제와 같이 "Get" 메서드의 이름과 일치하는 속성이 있습니다.  
  
 `public string TextWriter { get {...} set {...} }`  
 `public string GetTextWriter(int value) { ... }`  
  
 이 패턴은 일반적으로 속성이 실제로 메서드임을 나타냅니다.  
  
 **✓ DO**는 뒤에 "List" 또는 "Collection"이 붙은 단일 구를 사용하는 대신 컬렉션에서 항목을 설명하는 복수 구를 사용하여 컬렉션 속성의 이름을 지정합니다.  
  
 **✓ DO**는 긍정 구문(`CantSeek` 대신 `CanSeek`)을 사용하여 부울 속성의 이름을 지정합니다. 또한 필요에 따라 부울 속성에 "Is," "Can," 또는 "Has"를 전치사로 지정할 수 있지만 여기에 값을 추가해야 합니다.  
  
 **✓ CONSIDER**는 속성에 해당 형식으로 동일한 이름을 지정합니다.  
  
 예를 들어, 다음 속성은 현재 올바르게 `Color`라는 열거형 값을 설정하므로 속성 이름은 `Color`입니다.  
  
```csharp  
public enum Color {...}  
public class Control {  
    public Color Color { get {...} set {...} }  
}  
```  
  
## <a name="names-of-events"></a>이벤트 이름  
 이벤트는 발생 중인 작업 또는 발생한 작업 중 하나를 가리킵니다. 따라서 메서드와 마찬가지로 이벤트는 동사를 사용하여 명명하고 동사 시제는 이벤트가 발생할 시간을 나타내는 데 사용됩니다.  
  
 **✓ DO**는 동사 또는 동사구를 사용하여 이벤트의 이름을 지정합니다.  
  
 예를 들면 `Clicked`, `Painting`, `DroppedDown` 등입니다.  
  
 **✓ DO**를 통해 현재 및 과거 시제를 사용하여 이전 및 이후 개념을 포함한 이벤트 이름을 지정합니다.  
  
 예를 들어 창이 닫히기 전에 발생하는 닫기 이벤트는 `Closing`이라고 하고 창이 닫힌 후에 발생하는 닫기 이벤트는 `Closed`라고 합니다.  
  
 **X DO NOT**은 "Before" 또는 "After" 접두사 또는 접미사를 사용하여 사전 및 사후 이벤트를 나타냅니다. 위에서 설명한 대로 현재 및 과거 시제를 사용합니다.  
  
 **✓ DO**는 다음 예제와 같이 "EventHandler" 접미사를 사용하여 이벤트 처리기(이벤트 형식으로 사용된 대리자)의 이름을 지정합니다.  
  
 `public delegate void ClickedEventHandler(object sender, ClickedEventArgs e);`  
  
 **✓ DO**는 이벤트 처리기에서 `sender` 및 `e`라는 두 개의 매개 변수를 사용합니다.  
  
 보낸 사람 매개 변수는 이벤트를 발생시킨 개체를 나타냅니다. 보낸 사람 매개 변수는 보다 구체적인 형식을 적용할 수 있더라도 일반적으로 `object` 형식입니다.  
  
 **✓ DO**는 "EventArgs" 접미사를 사용하여 이벤트 인수 클래스의 이름을 지정합니다.  
  
## <a name="names-of-fields"></a>필드 이름  
 필드 명명 지침은 공용 및 보호된 고정 필드에 적용됩니다. 내부 및 개인 필드는 지침에서 다루지 않고 공용 또는 보호된 인스턴스 필드는 [멤버 디자인 지침](../../../docs/standard/design-guidelines/member.md)에서 허용하지 않습니다.  
  
 **✓ DO**는 필드 이름에 PascalCasing을 사용합니다.  
  
 **✓ DO**는 명사, 명사구 또는 형용사를 사용하여 필드 이름을 지정합니다.  
  
 **X DO NOT**은 필드 이름에 접두사를 사용합니다.  
  
 예를 들어 "g_" 또는 "s_"를 사용하여 고정 필드를 나타내지 마십시오.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 @no__t-[Framework 디자인 지침에서 피어슨 교육부, Inc.의 권한으로 0Reprinted. 다시 사용할 수 있는 .NET 라이브러리에 대 한 규칙, 관용구 및 패턴, Microsoft Windows 개발 @no__t 시리즈의 일부로 Addison-Wesley Professional에서 2008 no__t, Krzysztof Cwalina 및 Brad Abrams 성  
  
## <a name="see-also"></a>참조

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
- [명명 지침](../../../docs/standard/design-guidelines/naming-guidelines.md)
