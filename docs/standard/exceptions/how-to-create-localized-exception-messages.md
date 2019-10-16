---
title: '방법: 지역화된 예외 메시지를 사용하여 사용자 정의 예외 만들기'
description: '방법: 지역화된 예외 메시지를 사용하여 사용자 정의 예외 만드는 방법 알아보기'
author: Youssef1313
ms.author: ronpet
ms.date: 09/13/2019
ms.openlocfilehash: b4aa567fccda9354bc5959d6b9838d678d53abef
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696712"
---
# <a name="how-to-create-user-defined-exceptions-with-localized-exception-messages"></a>방법: 지역화된 예외 메시지를 사용하여 사용자 정의 예외 만들기

이 문서에서는 위성 어셈블리를 사용하여 지역화된 예외 메시지로 기본 <xref:System.Exception> 클래스에서 상속되는 사용자 정의 예외를 만드는 방법을 설명합니다.

## <a name="create-custom-exceptions"></a>사용자 지정 예외 만들기

.NET에는 사용할 수 있는 다양한 예외가 포함되어 있습니다. 그러나 사용자의 요구를 충족하는 항목이 없는 경우에는 사용자 지정 예외를 직접 만들 수 있습니다.

`StudentName` 속성을 포함하는 `StudentNotFoundException`을 만들려고 한다고 가정해 보겠습니다.
사용자 지정 예외를 만들려면 다음 단계를 수행합니다.

1. <xref:System.Exception>에서 상속된 serializable 클래스를 만듭니다. 클래스 이름은 "Exception"으로 끝나야 합니다.

    ```csharp
    [Serializable]
    public class StudentNotFoundException : Exception { }
    ```

1. 기본 생성자를 추가합니다.

    ```csharp
    [Serializable]
    public class StudentNotFoundException : Exception
    {
        public StudentNotFoundException() { }

        public StudentNotFoundException(string message)
            : base(message) { }

        public StudentNotFoundException(string message, Exception inner)
            : base(message, inner) { }
    }
    ```

1. 추가 속성 및 생성자를 정의합니다.

    ```csharp
    [Serializable]
    public class StudentNotFoundException : Exception
    {
        public string StudentName { get; }

        public StudentNotFoundException() { }

        public StudentNotFoundException(string message)
            : base(message) { }

        public StudentNotFoundException(string message, Exception inner)
            : base(message, inner) { }

        public StudentNotFoundException(string message, string studentName)
            : this(message)
        {
            StudentName = studentName;
        }
    }
    ```

## <a name="create-localized-exception-messages"></a>지역화된 예외 메시지 만들기

사용자 지정 예외를 만들고 다음과 같은 코드를 사용하여 어디에서든 throw할 수 있습니다.

```csharp
throw new StudentNotFoundException("The student cannot be found.", "John");
```

이전 줄의 문제는 `"The student cannot be found."`이 상수 문자열에 불과하다는 것입니다. 지역화된 애플리케이션에서는 사용자 문화권에 따라 다른 메시지를 사용할 수 있습니다.
[위성 어셈블리](../../framework/resources/creating-satellite-assemblies-for-desktop-apps.md)는 이 작업을 수행하는 좋은 방법입니다. 위성 어셈블리는 특정 언어에 대한 리소스를 포함하는 .dll입니다. 런타임에 특정 리소스를 요청하면 CLR은 사용자 문화권에 따라 해당 리소스를 찾습니다. 해당 문화권에 대한 위성 어셈블리를 찾을 수 없는 경우에는 기본 문화권의 리소스가 사용됩니다.

지역화된 예외 메시지를 만들려면

1. 리소스 파일을 저장한 *Resources*라는 새 폴더를 만듭니다.
1. 새 리소스 파일을 추가합니다. Visual Studio에서 이렇게 하려면 **솔루션 탐색기**에서 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목** > **리소스 파일**을 선택합니다. 파일 이름을 *ExceptionMessages.resx*입니다. 이 파일은 기본 리소스 파일입니다.
1. 다음 그림에 표시된 것처럼 예외 메시지에 대한 이름/값 쌍을 추가합니다.

   ![기본 문화권에 리소스 추가](media/add-resources-to-default-culture.jpg)

1. 프랑스어의 새 리소스 파일을 추가합니다. 이름을 *ExceptionMessages.fr-FR.resx*로 지정합니다.
1. 예외 메시지에 대한 이름/값 쌍을 다시 추가하지만 이번에는 다음과 같은 프랑스 값을 사용합니다.

   ![fr-FR 문화권에 리소스 추가](media/add-resources-to-fr-culture.jpg)

1. 프로젝트를 빌드하면 빌드 출력 폴더에는 위성 어셈블리인 *.dll* 파일을 포함하는 *fr-FR* 폴더가 있어야 합니다.
1. 다음과 같은 코드를 사용하여 예외를 throw합니다.

    ```csharp
    var resourceManager = new ResourceManager("FULLY_QIALIFIED_NAME_OF_RESOURCE_FILE", Assembly.GetExecutingAssembly());
    throw new StudentNotFoundException(resourceManager.GetString("StudentNotFound"), "John");
    ```

  > [!NOTE]
  > 프로젝트 이름이 `TestProject`이고 리소스 파일 *ExceptionMessages.resx*가 프로젝트의 *Resources* 폴더에 있는 경우 리소스 파일의 정규화된 이름은 `TestProject.Resources.ExceptionMessages`입니다.

## <a name="see-also"></a>참고 항목

- [사용자 정의 예외를 만드는 방법](how-to-create-user-defined-exceptions.md)
- [데스크톱 응용 프로그램용 위성 어셈블리 만들기](../../framework/resources/creating-satellite-assemblies-for-desktop-apps.md)
- [base(C# 참조)](../../csharp/language-reference/keywords/base.md)
- [this(C# 참조)](../../csharp/language-reference/keywords/this.md)
