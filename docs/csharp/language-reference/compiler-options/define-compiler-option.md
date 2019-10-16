---
title: -define(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /define
helpviewer_keywords:
- -define compiler option [C#]
- /define compiler option [C#]
- -d compiler option [C#]
- define compiler option [C#]
- /d compiler option [C#]
- d compiler option [C#]
ms.assetid: f17d7b4d-82d0-4133-8563-68cced1cac6e
ms.openlocfilehash: cb9de387b319ff4b81dcd1ccc37f04d8b6b3123a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924789"
---
# <a name="-define-c-compiler-options"></a>-define(C# 컴파일러 옵션)
**-define** 옵션은 프로그램의 모든 소스 코드 파일에서 `name`을 기호로 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-define:name[;name2]  
```  
  
## <a name="arguments"></a>인수  
 `name`, `name2`  
 정의하려는 하나 이상의 기호 이름입니다.  
  
## <a name="remarks"></a>설명  
 **-define** 옵션은 컴파일러 옵션이 프로젝트의 모든 파일에 적용된다는 점을 제외하고는 [#define](../preprocessor-directives/preprocessor-define.md) 전처리기 지시문을 사용하는 것과 효과가 동일합니다. 소스 파일의 [#undef](../preprocessor-directives/preprocessor-undef.md) 지시문이 정의를 제거할 때까지 기호는 소스 파일에 정의된 상태로 유지됩니다. -define 옵션을 사용하는 경우 한 파일의 `#undef` 지시문이 프로젝트의 다른 소스 코드 파일에는 영향을 주지 않습니다.  
  
 이 옵션으로 만든 기호를 [#if](../preprocessor-directives/preprocessor-if.md), [#else](../preprocessor-directives/preprocessor-else.md), [#elif](../preprocessor-directives/preprocessor-elif.md), [#endif](../preprocessor-directives/preprocessor-endif.md)와 함께 사용하면 소스 파일을 조건부 컴파일할 수 있습니다.  
  
 **-d**는 **-define**의 약식 형태입니다.  
  
 세미콜론 또는 쉼표를 사용해서 기호 이름을 구분하여 **-define**으로 여러 기호를 정의할 수 있습니다. 예:  
  
```console  
-define:DEBUG;TUESDAY  
```  
  
 C# 컴파일러 자체는 소스 코드에서 사용할 수 있는 기호 또는 매크로를 정의하지 않습니다. 모든 기호 정의는 사용자가 정의해야 합니다.  
  
> [!NOTE]
> C# `#define`에서는 C++와 같은 언어에서처럼 기호에 값을 지정할 수 없습니다. 예를 들어 `#define`을 사용하여 매크로를 만들거나 상수를 정의할 수 없습니다. 상수를 정의해야 하는 경우 `enum` 변수를 사용합니다. C++ 스타일 매크로를 만들려는 경우 제네릭과 같은 다른 방식을 고려해 보세요. 매크로는 오류가 발생할 가능성이 크므로 C#에서는 매크로를 사용할 수 없으며 더 안전한 방식이 사용됩니다.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1. 프로젝트 **속성** 페이지를 엽니다.  
  
2. **빌드** 탭의 **조건부 컴파일 기호** 상자에 정의할 기호를 입력합니다. 예를 들어 다음 코드 예제를 사용하는 경우 텍스트 상자에 `xx`를 입력합니다.  
  
 이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DefineConstants%2A>을 참조하세요.  
  
## <a name="example"></a>예  
  
```csharp  
// preprocessor_define.cs  
// compile with: -define:xx  
// or uncomment the next line  
// #define xx  
using System;  
public class Test   
{  
    public static void Main()   
    {  
        #if (xx)   
            Console.WriteLine("xx defined");  
        #else  
            Console.WriteLine("xx not defined");  
        #endif  
    }  
}  
```  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
