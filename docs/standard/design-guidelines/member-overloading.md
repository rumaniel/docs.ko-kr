---
title: 멤버 오버로드
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- default arguments
- members [.NET Framework], overloaded
- member design guidelines [.NET Framework], overloading
- overloaded members
- signatures, members
ms.assetid: 964ba19e-8b94-4b5b-b1e3-5a0b531a0bb1
author: KrzysztofCwalina
ms.openlocfilehash: 4caa0ae78d168b23fd2862153bef0e3960d3ea42
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392951"
---
# <a name="member-overloading"></a>멤버 오버로드
멤버 오버 로드는 매개 변수의 개수나 형식만 다르고 이름이 동일한 동일한 형식으로 둘 이상의 멤버를 만드는 것을 의미 합니다. 예를 들어, 다음에서 `WriteLine` 메서드는 오버 로드 됩니다.  
  
```csharp  
public static class Console {  
    public void WriteLine();  
    public void WriteLine(string value);  
    public void WriteLine(bool value);  
    ...  
}  
```  
  
 메서드, 생성자 및 인덱싱된 속성만 매개 변수를 가질 수 있으므로 해당 멤버만 오버 로드 될 수 있습니다.  
  
 오버 로드는 유용성, 생산성 및 재사용 가능한 라이브러리의 가독성을 향상 시키기 위한 가장 중요 한 기술 중 하나입니다. 매개 변수 수를 오버 로드 하면 더 간단한 버전의 생성자와 메서드를 제공할 수 있습니다. 매개 변수 형식에 대 한 오버 로드를 사용 하면 선택한 다른 형식 집합에 대해 동일한 작업을 수행 하는 멤버에 대해 동일한 멤버 이름을 사용할 수 있습니다.  
  
 **✓ DO** 짧은 오버 로드에서 사용 되는 기본값을 나타내기 위해 설명 매개 변수 이름을 사용 하려고 합니다.  
  
 **X AVOID** 임의의 여러 오버 로드에 매개 변수 이름입니다. 한 오버 로드의 매개 변수가 다른 오버 로드의 매개 변수와 동일한 입력을 나타내는 경우 매개 변수의 이름이 같아야 합니다.  
  
 **X AVOID** 오버 로드 된 멤버의 매개 변수 순서에 일관 되지 않은 것입니다. 이름이 같은 매개 변수는 모든 오버 로드에서 동일한 위치에 표시 되어야 합니다.  
  
 **✓ DO** (확장 기능이 필요) 하는 경우 가상 가장 긴 오버 로드를 확인 합니다. 짧은 오버 로드는 단순히를 통해 보다 긴 오버 로드를 호출 해야 합니다.  
  
 **X DO NOT** 사용 `ref` 또는 `out` 한정자를 멤버를 오버 로드 합니다.  
  
 일부 언어에서는 다음과 같은 오버 로드에 대 한 호출을 확인할 수 없습니다. 또한 이러한 오버 로드는 일반적으로 완전히 다른 의미 체계를 가지 며 오버 로드를 제외 하 고 별도의 두 메서드를 대신 하 여 사용할 수 있습니다.  
  
 **X DO NOT** 서로 다른 의미 체계 하면서도 동일한 위치와 유사한 형식 매개 변수를 사용 하는 오버 로드를 갖고 있습니다.  
  
 **✓ DO** 허용 `null` 선택적 인수를 전달 하도록 합니다.  
  
 **✓ DO** 멤버 기본 인수가 있는 멤버를 정의 하는 대신 오버 로드를 사용 합니다.  
  
 기본 인수는 CLS 규격이 아닙니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 @no__t-[Framework 디자인 지침에서 피어슨 교육부, Inc.의 권한으로 0Reprinted. 다시 사용할 수 있는 .NET 라이브러리에 대 한 규칙, 관용구 및 패턴, Microsoft Windows 개발 @no__t 시리즈의 일부로 Addison-Wesley Professional에서 2008 no__t, Krzysztof Cwalina 및 Brad Abrams 성  
  
## <a name="see-also"></a>참조

- [멤버 디자인 지침](../../../docs/standard/design-guidelines/member.md)
- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
