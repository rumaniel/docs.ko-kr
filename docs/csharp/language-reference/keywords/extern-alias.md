---
title: extern 별칭 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- alias_CSharpKeyword
helpviewer_keywords:
- extern alias keyword [C#]
- aliases [C#], extern keyword
- aliases, extern keyword
ms.assetid: f487bf4f-c943-4fca-851b-e540c83d9027
ms.openlocfilehash: a701ae02adebfa2dda8fb65053dbf2ebbe83328b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924690"
---
# <a name="extern-alias-c-reference"></a>extern alias(C# 참조)
정규화된 형식 이름이 동일한 어셈블리의 두 버전을 참조해야 할 수 있습니다. 예를 들어 동일한 애플리케이션에서 어셈블리 버전을 두 개 이상 사용해야 할 수 있습니다. 외부 어셈블리 별칭을 사용하면 각 어셈블리의 네임스페이스를 별칭으로 명명된 루트 수준 네임스페이스 내에서 래핑하여 동일한 파일에서 사용하도록 할 수 있습니다.  
  
> [!NOTE]
> [extern](./extern.md) 키워드는 메서드 한정자로도 사용되어 비관리 코드로 작성된 메서드를 선언합니다.  
  
 정규화된 형식 이름이 동일한 두 어셈블리를 참조하려면 다음과 같이 명령 프롬프트에서 별칭을 지정해야 합니다.  
  
 `/r:GridV1=grid.dll`  
  
 `/r:GridV2=grid20.dll`  
  
 그러면 외부 별칭 `GridV1` 및 `GridV2`가 생성됩니다. 프로그램 내에서 이러한 별칭을 사용하려면 `extern` 키워드를 사용하여 참조합니다. 예:  
  
 `extern alias GridV1;`  
  
 `extern alias GridV2;`  
  
 각 extern alias 선언에서는 전역 네임스페이스와 병렬이지만 전역 네임스페이스 내에 있지 않는 추가 루트 수준 네임스페이스를 소개합니다. 따라서 각 어셈블리의 형식은 적절한 namespace-alias에서 시작되는 정규화된 이름을 사용하여 명확하게 참조할 수 있습니다.  
  
 이전 예제에서 `GridV1::Grid`는 `grid.dll`의 표 컨트롤이 되고 `GridV2::Grid`는 `grid20.dll`의 표 컨트롤이 됩니다.  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](./index.md)
- [:: 연산자](../operators/namespace-alias-qualifier.md)
- [/reference(C# 컴파일러 옵션)](../compiler-options/reference-compiler-option.md)
