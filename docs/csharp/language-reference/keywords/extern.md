---
title: extern 한정자 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- extern_CSharpKeyword
- extern
helpviewer_keywords:
- DllImport attribute
- extern keyword [C#]
ms.assetid: 9c3f02c4-51b8-4d80-9cb2-f2b6e1ae15c7
ms.openlocfilehash: 387ef707166705c4df501bd6740d438683aa2d69
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70203010"
---
# <a name="extern-c-reference"></a>extern(C# 참조)

`extern` 한정자는 외부에서 구현되는 메서드를 선언하는 데 사용됩니다. `extern` 한정자는 일반적으로 Interop 서비스를 사용하여 비관리 코드를 호출할 때 `DllImport` 특성과 함께 사용됩니다. 이 경우 다음 예제에서와 같이 메서드를 `static`으로 선언해야 합니다.

```csharp
[DllImport("avifil32.dll")]
private static extern void AVIFileInit();
```

`extern` 키워드는 외부 어셈블리 별칭도 정의하여 단일 어셈블리 내에서 동일한 구성 요소의 다른 버전을 참조할 수 있도록 합니다. 자세한 내용은 [extern alias](extern-alias.md)를 참조하세요.

[abstract](abstract.md) 및 `extern` 한정자를 함께 사용하여 같은 멤버를 수정할 수는 없습니다. `extern` 한정자는 메서드가 C# 코드 외부에서 구현됨을 나타내고 `abstract` 한정자는 해당 클래스에서 메서드가 구현되지 않음을 나타냅니다.

extern 키워드는 C++보다 C#에서 사용이 제한적입니다. C# 키워드를 C++ 키워드와 비교하려면 extern을 사용하여 C++ 언어 참조에 링크 지정을 참조하십시오.

## <a name="example-1"></a>예제 1

이 예제에서는 프로그램이 사용자로부터 문자열을 수신하여 메시지 상자에 표시합니다. 이 프로그램은 User32.dll 라이브러리에서 가져온 `MessageBox` 메서드를 사용합니다.

[!code-csharp[csrefKeywordsModifiers#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#8)]

## <a name="example-2"></a>예제 2

이 예제는 C 라이브러리(네이티브 DLL)로 호출되는 C# 프로그램을 보여 줍니다.

1. 다음 C 파일을 만들고 이름을 `cmdll.c`로 지정합니다.

    ```c
    // cmdll.c
    // Compile with: -LD
    int __declspec(dllexport) SampleMethod(int i)
    {
      return i*10;
    }
    ```

2. Visual Studio 설치 디렉터리에서 Visual Studio x64(또는 x32) 네이티브 도구 명령 프롬프트 창을 열고 명령 프롬프트에서 **cl -LD cmdll.c**를 입력하여 `cmdll.c` 파일을 컴파일합니다.

3. 같은 디렉터리에서 다음 C# 파일을 만들고 이름을 `cm.cs`로 지정합니다.

    ```csharp
    // cm.cs
    using System;
    using System.Runtime.InteropServices;
    public class MainClass
    {
        [DllImport("Cmdll.dll")]
          public static extern int SampleMethod(int x);

        static void Main()
        {
            Console.WriteLine("SampleMethod() returns {0}.", SampleMethod(5));
        }
    }
    ```

4. Visual Studio 설치 디렉터리에서 Visual Studio x64(또는 x32) 네이티브 도구 명령 프롬프트 창을 열고 명령 프롬프트에서 다음을 입력하여 `cm.cs` 파일을 컴파일합니다.

    > **csc cm.cs**(x64 명령 프롬프트의 경우) —또는— **csc -platform:x86 cm.cs**(x32 명령 프롬프트의 경우)

    이렇게 하면 실행 파일 `cm.exe`가 만들어집니다.

5. `cm.exe`를 실행합니다. `SampleMethod` 메서드가 값 5를 DLL 파일에 전달하면 10을 곱한 값이 반환됩니다.  프로그램에서는 다음이 출력됩니다.

    ```output
    SampleMethod() returns 50.
    ```

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=nameWithType>
- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [한정자](modifiers.md)
