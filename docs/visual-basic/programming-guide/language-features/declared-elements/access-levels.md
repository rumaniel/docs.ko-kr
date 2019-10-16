---
title: Visual Basic의 액세스 수준
ms.date: 05/10/2018
helpviewer_keywords:
- members [Visual Basic], accessing in Visual Basic
- Friend access modifier
- access levels, declared elements
- access levels
- access modifiers
- Public access modifier
- Protected access modifier
- Protected Friend access modifier
- Private Protected access modifier
- Private access modifier
- declared elements [Visual Basic], access level
ms.assetid: 6e06c1ab-fd78-47f0-83a8-1152780b5e1a
ms.openlocfilehash: d8f2f16d2fb15f2e840f13f177d3fea83fda315e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61828102"
---
# <a name="access-levels-in-visual-basic"></a>Visual Basic의 액세스 수준
합니다 *액세스 수준* 것에 액세스할 수 있도록 범위를 읽거나 쓸 수 있는 권한이 있는 코드, 선언 된 요소입니다. 요소 자체를 선언한 방법 뿐만 아니라 요소의 컨테이너의 액세스 수준에 따라 결정 됩니다. 포함 하는 요소에 액세스할 수 없는 코드에 액세스할 수 없는 포함 된 요소의 이더라도로 선언 `Public`합니다. 예를 들어를 `Public` 변수는 `Private` 구조 아닌 하지만 해당 구조체를 포함 하는 클래스 내에서 액세스할 수 있습니다 해당 클래스 외부에서.  
  
## <a name="public"></a>Public  
 합니다 [공용](../../../../visual-basic/language-reference/modifiers/public.md) 선언문에서 키워드는 같은 프로젝트의 코드에서 해당 프로젝트를 참조 하는 다른 프로젝트 및 프로젝트에서 빌드된 어셈블리에 있는 요소에 액세스할 수 있는지를 지정 합니다. 다음 코드 예제를 보여 줍니다. `Public` 선언 합니다.  
  
```vb  
Public Class classForEverybody  
```  
  
 사용할 수 있습니다 `Public` 모듈, 인터페이스 또는 네임 스페이스 수준 에서만. 즉, 소스 파일 또는 네임 스페이스 또는 인터페이스, 모듈, 클래스 또는 구조체 내에서 아니라 프로시저 수준에서 공용 요소를 선언할 수 있습니다.  
  
## <a name="protected"></a>보호됨  
 합니다 [보호 된](../../../../visual-basic/language-reference/modifiers/protected.md) 선언문에서 키워드는 같은 클래스 내에서 또는이 클래스에서 파생 된 클래스에서 요소 에서만 액세스할 수 있는지를 지정 합니다. 다음 코드 예제를 보여 줍니다. `Protected` 선언 합니다.  
  
```vb  
Protected Class classForMyHeirs  
```  
  
 사용할 수 있습니다 `Protected` 클래스 에서만 수준 및만 선언 하면 클래스의 멤버입니다. 즉, 클래스에서 하지만 수준이 아닌 소스 파일 또는 네임 스페이스 또는 인터페이스, 모듈, 구조체 또는 프로시저 내에서 보호 된 요소를 선언할 수 있습니다.  
  
## <a name="friend"></a>Friend  
 [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) 선언문에서 키워드를 제외한 아닌 동일한 어셈블리 내에서 요소에 액세스할 수 있는지 지정 어셈블리 외부에 있습니다. 다음 코드 예제를 보여 줍니다. `Friend` 선언 합니다.  
  
```vb  
Friend stringForThisProject As String  
```  
  
 사용할 수 있습니다 `Friend` 모듈, 인터페이스 또는 네임 스페이스 수준 에서만. 즉, 소스 파일 또는 네임 스페이스 또는 인터페이스, 모듈, 클래스 또는 구조체 내에서 아니라 프로시저 수준에서 friend 요소를 선언할 수 있습니다.  
  
## <a name="protected-friend"></a>Protected Friend  
 합니다 [Protected Friend](../../../language-reference/modifiers/protected-friend.md) 또는 파생 된 클래스에서 내에서 요소에 액세스할 수 있는지 지정 하는 선언문에서 키워드 조합 동일한 어셈블리 또는 둘 다. 다음 코드 예제를 보여 줍니다. `Protected Friend` 선언 합니다.  
  
```vb  
Protected Friend stringForProjectAndHeirs As String  
```  
  
 사용할 수 있습니다 `Protected Friend` 클래스 에서만 수준 및만 선언 하면 클래스의 멤버입니다. 즉, 클래스에서 하지만 수준이 아닌 소스 파일 또는 네임 스페이스 또는 인터페이스, 모듈, 구조체 또는 프로시저 내에서 protected friend 요소를 선언할 수 있습니다.  
  
## <a name="private"></a>Private  
 합니다 [개인](../../../../visual-basic/language-reference/modifiers/private.md) 선언문에서 키워드 요소는 동일한 모듈, 클래스 또는 구조체 내 에서만 액세스할 수 있는지를 지정 합니다. 다음 코드 예제를 보여 줍니다. `Private` 선언 합니다.  
  
```vb  
Private numberForMeOnly As Integer  
```  
  
 `Private`는 모듈 수준에서만 사용할 수 있습니다. 즉, 모듈, 클래스 또는 구조체 내 있지만 소스 파일 또는 네임 스페이스, 인터페이스 또는 프로시저의 수준이 아닌 개인 요소를 선언할 수 있습니다.  
  
 모듈 수준에서의 `Dim` 액세스 수준 키워드 없이 문과 동일는 `Private` 선언 합니다. 그러나 사용 하려는는 `Private` 코드를 더 쉽게 읽고 해석 하는 키워드입니다.  

## <a name="private-protected"></a>Private Protected

합니다 [Private Protected](../../../language-reference/modifiers/private-protected.md) 선언문에서 키워드 조합 지정 요소를 포함 하는 클래스와 동일한 어셈블리의 파생된 클래스와 동일한 클래스 내 에서만 액세스할 수 있습니다. `Private Protected` 액세스 한정자는 Visual Basic 15.5부터 지원 됩니다.

다음 예제는 `Private Protected` 선언 합니다.

```vb
Private Protected internalValue As Integer
```

선언할 수는 `Private Protected` 클래스 내부 에서만 요소입니다. 인터페이스 또는 구조체 내에서 선언할 수 없습니다 나 소스 파일 또는 네임 스페이스, 인터페이스 또는 구조체 내부 또는 프로시저의 수준에서 선언할 수 있습니다.

`Private Protected` 액세스 한정자는 Visual Basic 15.5 이상에 지원 됩니다. 를 사용 하려면 Visual Basic 프로젝트 (*.vbproj) 파일에 다음 요소를 추가 합니다. Visual Basic 15.5 하기만 이상 시스템에 설치 되어, 최신 버전의 Visual Basic 컴파일러를 지 원하는 모든 언어 기능을 활용할 수 있습니다.

```xml
<PropertyGroup>
   <LangVersion>latest</LangVersion>
</PropertyGroup>
```

사용 하는 `Private Protected` 액세스 한정자를 Visual Basic 프로젝트 (*.vbproj) 파일에 다음 요소를 추가 해야 합니다.

```xml
<PropertyGroup>
   <LangVersion>15.5</LangVersion>
</PropertyGroup>
```

자세한 내용은 참조 [Visual Basic 언어 버전을 설정](../../../language-reference/configure-language-version.md)합니다.

## <a name="access-modifiers"></a>액세스 한정자  

액세스 수준을 지정 하는 키워드 라고 *액세스 한정자*합니다. 다음 표에서 액세스 한정자를 비교 합니다.  
  
|액세스 한정자|부여 된 액세스 수준|이 액세스 수준을 가진 선언할 수 있습니다 요소|이 한정자를 사용할 수 있는 선언 컨텍스트|  
|---------------------|--------------------------|-----------------------------------------------------|----------------------------------------------------------------|  
|`Public`|무제한:<br /><br /> 공용 요소를 볼 수 있는 코드에서 액세스할 수 있습니다.|인터페이스<br /><br /> 모듈<br /><br /> 클래스<br /><br /> 구조체<br /><br /> 구조체 멤버<br /><br /> 절차<br /><br /> 속성<br /><br /> 멤버 변수<br /><br /> 상수<br /><br /> 열거형<br /><br /> 이벤트<br /><br /> 외부 선언<br /><br /> 대리자|소스 파일<br /><br /> 네임스페이스<br /><br /> 인터페이스<br /><br /> Module<br /><br /> 클래스<br /><br /> 구조체|  
|`Protected`|파생 합니다.<br /><br /> 보호 된 요소나에서 파생 된 클래스 요소에 액세스할 수를 선언 하는 클래스의 코드|인터페이스<br /><br /> 클래스<br /><br /> 구조체<br /><br /> 절차<br /><br /> 속성<br /><br /> 멤버 변수<br /><br /> 상수<br /><br /> 열거형<br /><br /> 이벤트<br /><br /> 외부 선언<br /><br /> 대리자|클래스|  
|`Friend`|어셈블리:<br /><br /> Friend 요소에 액세스할 수를 선언 하는 어셈블리의 코드|인터페이스<br /><br /> 모듈<br /><br /> 클래스<br /><br /> 구조체<br /><br /> 구조체 멤버<br /><br /> 절차<br /><br /> 속성<br /><br /> 멤버 변수<br /><br /> 상수<br /><br /> 열거형<br /><br /> 이벤트<br /><br /> 외부 선언<br /><br /> 대리자|소스 파일<br /><br /> 네임스페이스<br /><br /> 인터페이스<br /><br /> Module<br /><br /> 클래스<br /><br /> 구조체|  
|`Protected` `Friend`|공용 구조체 `Protected` 고 `Friend`:<br /><br /> 동일한 클래스에서 protected friend 요소 또는 요소의 클래스에서 파생 된 클래스 내에서 동일한 어셈블리의 코드에서 액세스할 수 있습니다|인터페이스<br /><br /> 클래스<br /><br /> 구조체<br /><br /> 절차<br /><br /> 속성<br /><br /> 멤버 변수<br /><br /> 상수<br /><br /> 열거형<br /><br /> 이벤트<br /><br /> 외부 선언<br /><br /> 대리자|클래스|  
|`Private`|선언 컨텍스트.<br /><br /> 포함된 형식 내에서 코드를 포함 하 여 개인 요소를 선언 하는 형식에서 코드 요소에 액세스할 수 있습니다.|인터페이스<br /><br /> 클래스<br /><br /> 구조체<br /><br /> 구조체 멤버<br /><br /> 절차<br /><br /> 속성<br /><br /> 멤버 변수<br /><br /> 상수<br /><br /> 열거형<br /><br /> 이벤트<br /><br /> 외부 선언<br /><br /> 대리자|Module<br /><br /> 클래스<br /><br /> 구조체|
|`Private Protected`|Private protected 요소를 선언 하는 클래스의 코드 또는 bas 클래스와 동일한 어셈블리에 있는 파생된 클래스에서 코드입니다.|인터페이스<br /><br /> 클래스<br /><br /> 구조체<br /><br /> 절차<br /><br /> 속성<br /><br /> 멤버 변수<br /><br /> 상수<br /><br /> 열거형<br /><br /> 이벤트<br /><br /> 외부 선언<br /><br /> 대리자|클래스|
  
## <a name="see-also"></a>참고자료

- [Dim 문](../../../../visual-basic/language-reference/statements/dim-statement.md)
- [정적](../../../../visual-basic/language-reference/modifiers/static.md)
- [선언 요소 이름](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [선언된 요소 참조](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [선언 요소의 특징](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)
- [Visual Basic의 수명](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)
- [Visual Basic의 범위](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)
- [방법: 변수의 사용 가능성 제어](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-availability-of-a-variable.md)
- [변수](../../../../visual-basic/programming-guide/language-features/variables/index.md)
- [변수 선언](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
