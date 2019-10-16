---
title: C# 언어 및 .NET Framework 소개
description: C# 및 .NET의 기본 사항에 대해 알아봅니다. C# 언어 및 .NET 에코시스템에 대한 개요를 확인합니다.
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, about C# language
- Visual C#, about
ms.assetid: 0a2dff4e-cd84-42ff-8141-e89889b24081
ms.openlocfilehash: 995362667ed0a203112744f03a036eabbcb784c8
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69608305"
---
# <a name="introduction-to-the-c-language-and-the-net-framework"></a>C# 언어 및 .NET Framework 소개

유연하고 형식이 안전한 개체 지향 언어인 C#은 개발자가 .NET Framework에서 실행되는 안전하고 강력한 여러 애플리케이션을 빌드할 수 있도록 지원합니다. C#을 사용하여 Windows 클라이언트 애플리케이션, XML Web services, 분산 구성 요소, 클라이언트-서버 애플리케이션, 데이터베이스 애플리케이션 등을 만들 수 있습니다. Visual C#에서는 고급 코드 편집기, 편리한 사용자 인터페이스 디자이너, 통합 디버거 및 다른 많은 도구를 제공하여 C# 언어 및 .NET Framework에 따라 보다 쉽게 애플리케이션을 개발할 수 있습니다.  
  
> [!NOTE]
> Visual C# 설명서에서는 사용자가 기본적인 프로그래밍 개념을 이해하고 있다고 간주합니다. 완전 초보 사용자인 경우 웹에서 사용할 수 있는 Visual C#을 살펴볼 수도 있습니다. C#에 대한 설명서 및 웹 리소스를 활용하여 실제 프로그래밍 기술을 배울 수도 있습니다.  
  
## <a name="c-language"></a>C# 언어

 C# 구문은 다양한 표현 기능을 갖추면서도 간편하고 쉽게 배울 수 있습니다. C#의 중괄호 구문은 C, C++ 또는 Java에 익숙한 사용자라면 누구나 바로 알아볼 수 있습니다. 이러한 언어에 익숙한 개발자는 일반적으로 매우 짧은 시간 내에 C#으로 생산적인 작업을 수행할 수 있습니다. C# 구문은 C++의 복잡성을 획기적으로 단순화하고 Java에는 없는 null 허용 값 형식, 열거형, 대리자, 람다 식 및 직접 메모리 액세스와 같은 강력한 기능을 제공합니다. C#은 향상된 형식 안정성 및 성능을 제공하는 제네릭 메서드와 형식을 지원하고, 컬렉션 클래스의 구현을 통해 클라이언트 코드에서 쉽게 사용할 수 있는 사용자 지정 반복 동작을 정의할 수 있도록 하는 반복기를 지원합니다. [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)] 식은 강력한 형식의 쿼리를 최고의 언어 구문으로 만들어줍니다.  
  
 개체 지향 언어인 C#은 캡슐화, 상속 및 다형성의 개념을 지원합니다. 애플리케이션의 진입점인 `Main` 메서드를 포함하는 모든 변수 및 메서드가 클래스 정의 내에 캡슐화됩니다. 클래스는 단일 부모 클래스에서 직접 상속될 수 있지만 원하는 수의 인터페이스를 구현할 수 있습니다. 부모 클래스에서 가상 메서드를 재정의하는 메서드에는 우발적인 재정의를 방지하는 방법으로 `override` 키워드가 필요합니다. C#에서 구조체는 같은 클래스와 같습니다. 즉, 인터페이스를 구현할 수 있지만 상속을 지원하지 않는 스택 할당 형식입니다.  
  
 이러한 기본 개체 지향 원칙 외에도, C#은 다음을 포함한 몇 가지 혁신적인 언어 구문을 통해 소프트웨어 구성 요소를 쉽게 개발하도록 지원합니다.  
  
- *대리자*라고 하는 캡슐화된 메서드 시그니처: 형식이 안전한 이벤트 알림을 가능하게 합니다.  
  
- 속성: 전용 멤버 변수에 대한 접근자 역할을 합니다.  
  
- 특성: 런타임에 형식에 대한 선언적 메타데이터를 제공합니다.  
  
- 인라인 XML 문서 주석  
  
- [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)]: 다양한 데이터 소스에 대한 기본 제공 쿼리 기능을 제공합니다.  
  
 COM 개체 또는 네이티브 Win32 DLL 등의 다른 Windows 소프트웨어와 상호 작용해야 하는 경우 C#에서 “Interop”라는 프로세스를 통해 작업할 수 있습니다. Interop을 사용하면 네이티브 C++ 애플리케이션에서 수행할 수 있는 거의 모든 작업을 C# 프로그램으로 수행할 수 있습니다. C#은 직접 메모리 액세스가 절대적으로 중요한 경우를 위한 "안전하지 않은" 코드 개념 및 포인터까지도 지원합니다.  
  
 C# 빌드 프로세스는 C 및 C++과 비교해서 비교적 간단하며 Java의 경우보다 좀 더 유연합니다. 별도 헤더 파일이 없으며, 메서드 및 형식을 특정 순서로 선언할 필요도 없습니다. C# 소스 파일은 원하는 수의 클래스, 구조체, 인터페이스 및 이벤트를 정의할 수 있습니다.  
  
 다음은 추가적인 C# 리소스입니다.  
  
- 언어에 대한 일반적이면서 유용한 소개 정보는 [C# 언어 사양](../language-reference/language-specification/index.md), 1장을 참조하세요.  
  
- C# 언어의 특정 측면에 대한 자세한 내용은 [C# 참조](../language-reference/index.md)를 참조하세요.  
  
- [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]에 대한 자세한 내용은 [LINQ(언어 통합 쿼리)](../programming-guide/concepts/linq/index.md)를 참조하세요.  

## <a name="net-framework-platform-architecture"></a>.NET Framework 플랫폼 아키텍처

 C# 프로그램은 CLR(공용 언어 런타임)이라고 하는 가상 실행 시스템과 통합된 클래스 라이브러리 세트를 포함하는 Windows의 통합 구성 요소인 .NET Framewor에서 실행됩니다. CLR은 언어 및 라이브러리가 원활하게 함께 작동하는 실행 및 개발 환경을 만들기 위한 기준이 되는 국제 표준인 CLI(공용 언어 인프라)를 Microsoft에서 상업적으로 구현한 것입니다.  
  
 C#으로 작성된 소스 코드는 CLI 사양을 준수하는 [IL(중간 언어)](../../standard/managed-code.md)로 컴파일됩니다. IL 코드 및 리소스(예: 비트맵 및 문자열)는 일반적으로 확장명이 .exe 또는 .dll인 어셈블리라는 실행 파일로 디스크에 저장됩니다. 어셈블리는 어셈블리의 형식, 버전, 문화권 및 보안 요구 사항에 대한 정보를 제공하는 매니페스트를 포함합니다.  
  
 C# 프로그램이 실행될 경우 어셈블리가 CLR에 로드되어 매니페스트의 정보를 기준으로 다양한 작업을 수행할 수 있습니다. 그런 다음 보안 요구 사항을 충족되면 CLR은 JIT(Just-In-Time) 컴파일을 수행하여 IL 코드를 네이티브 기계어 명령으로 변환합니다. 또한 CLR은 자동 가비지 수집, 예외 처리 및 리소스 관리와 관련된 다른 서비스도 제공합니다. CLR에서 실행되는 코드는 "관리 코드"라고도 합니다. 즉, 특정 시스템을 대상으로 하는 네이티브 기계어로 컴파일되는 "비관리 코드"와는 반대됩니다. 다음 다이어그램은 C# 소스 코드 파일, .NET Framework 클래스 라이브러리, 어셈블리 및 CLR의 컴파일 타임 및 런타임 관계를 보여 줍니다.  
  
 ![C&#35; 소스 코드부터 머신 실행까지](./media/introduction-to-the-csharp-language-and-the-net-framework/net-architecture-relationships.png)  
  
 언어 상호 운용성은 .NET Framework의 주요 기능입니다. C# 컴파일러에서 생성된 IL 코드는 CTS(공용 형식 사양)을 준수하므로 C#에서 생성된 IL 코드는 .NET 버전의 Visual Basic, Visual C++ 또는 20개 이상의 다른 CTS 규격 언어에서 생성된 코드와 상호 작용할 수 있습니다. 단일 어셈블리는 다른 .NET 언어로 작성된 여러 모듈을 포함할 수 있고 형식은 마치 같은 언어로 작성된 것처럼 서로를 참조할 수 있습니다.  
  
 .NET Framework에는 런타임 서비스 외에, 파일 입/출력부터 문자열 조작, XML 구문 분석, Windows Forms 컨트롤에 이르는 모든 항목에 대해 다양하고 유용한 기능을 제공하는 네임스페이스로 구성된 4,000개가 넘는 광범위한 클래스 라이브러리도 포함됩니다. 일반적인 C# 애플리케이션은 .NET Framework 클래스 라이브러리를 광범위하게 사용하여 일반적인 "배관" 작업을 처리합니다.  
  
 .NET Framework에 대한 자세한 내용은 [Microsoft.NET Framework 개요](../../framework/get-started/overview.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [C#](../index.md)
- [Visual C# 및 Visual Basic 시작](/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic)
