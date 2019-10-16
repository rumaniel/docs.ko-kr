---
title: C# 참조
ms.date: 02/14/2017
helpviewer_keywords:
- Visual C#, language reference
- language reference [C#]
- Programmer's Reference for C#
- C# language, reference
- reference, C# language
ms.assetid: 06de3167-c16c-4e1a-b3c5-c27841d4569a
ms.openlocfilehash: df56287d161f7760e136eb80aa1a9171966df794
ms.sourcegitcommit: 992f80328b51b165051c42ff5330788627abe973
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72275807"
---
# <a name="c-reference"></a>C# 참조
이 섹션에서는 C# 키워드, 연산자, 특수 문자, 전처리기 지시문, 컴파일러 옵션 및 컴파일러 오류와 경고에 대한 참조 자료를 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [C# 키워드](./keywords/index.md)  
 C# 키워드 및 구문에 대한 정보 링크를 제공합니다.  
  
 [C# 연산자](./operators/index.md)  
 C# 연산자 및 구문에 대한 정보 링크를 제공합니다.  

 [C# 특수 문자](./tokens/index.md)  
 C#의 특수한 상황에 맞는 문자 및 용도에 대한 정보로 연결되는 링크를 제공합니다.  

 [C# 전처리기 지시문](./preprocessor-directives/index.md)  
 C# 소스 코드에 포함할 컴파일러 명령에 대한 정보 링크를 제공합니다.  
  
 [C# 컴파일러 옵션](./compiler-options/index.md)  
 컴파일러 옵션 및 사용 방법에 대한 정보를 포함합니다.  
  
 [C# 컴파일러 오류](./compiler-messages/index.md)  
 C# 컴파일러 오류 및 경고의 원인과 해결 방법을 보여 주는 코드 조각을 포함합니다.  
  
 [C# 언어 사양](../../../_csharplang/spec/introduction.md)  
 C# 6.0 언어 사양. C# 6.0 언어에 대한 초안 제안입니다. 이 문서는 ECMA C# 표준 위원회와의 협력을 통해 구체화될 예정입니다. 버전 5.0은 2017년 12월에 [표준 ECMA-334 다섯 번째 버전](https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-334.pdf) 문서로 릴리스되었습니다.

6\.0 이후 C# 버전에서 구현된 기능은 언어 사양 제안에 나타납니다. 이 문서는 이러한 새 기능을 추가하기 위해 언어 사양에 대한 델타를 설명합니다. 이는 초안 제안 양식입니다. 이러한 사양은 구체화되어 공식적인 검토를 위해 ECMA 표준 위원회에 제출되며, 이후 버전의 C# 표준으로 통합됩니다.

 [C# 7.0 사양 제안](../../../_csharplang/proposals/csharp-7.0/pattern-matching.md)  
 C# 7.0에서 여러 가지 새로운 기능이 구현되었습니다. 새로운 기능에는 패턴 일치, 로컬 함수, 변수 선언, throw 식, 이진 리터럴 및 숫자 구분 기호가 포함됩니다. 이 폴더에는 각 기능에 대한 사양이 있습니다.
  
 [C# 7.1 사양 제안](../../../_csharplang/proposals/csharp-7.1/async-main.md)  
 C# 7.1에 새로운 기능이 추가되었습니다. 먼저 `Task` 또는 `Task<int>`를 반환하는 `Main` 메서드를 작성할 수 있습니다. 이렇게 하면 `async` 한정자를 `Main`에 추가할 수 있습니다. `default` 식은 형식을 유추할 수 있는 위치에 형식 없이 사용할 수 있습니다. 또한 튜플 멤버 이름을 유추할 수 있습니다. 마지막으로, 패턴 일치는 제네릭과 함께 사용할 수 있습니다.

 [C# 7.2 사양 제안](../../../_csharplang/proposals/csharp-7.2/readonly-ref.md)  
 C# 7.2에 여러 작은 기능을 추가했습니다. `in` 키워드를 사용하여 읽기 전용 참조로 인수를 전달할 수 있습니다. `Span` 및 관련 유형에 대한 컴파일 시간 안정성을 지원하기 위한 여러 가지 하위 수준 변경 내용이 있습니다. 일부 상황에서는 나중에 인수가 위치할 때 명명된 인수를 사용할 수 있습니다. `private protected` 액세스 한정자를 사용하면 호출자가 동일한 어셈블리에 구현된 파생 형식으로 제한되도록 지정할 수 있습니다. `?:` 연산자는 변수에 대한 참조로 확인할 수 있습니다. 선행 숫자 구분 기호를 사용하여 16진수 및 이진 숫자를 포맷할 수도 있습니다.

 [C# 7.3 사양 제안](../../../_csharplang/proposals/csharp-7.3/blittable.md)  
 C# 7.3은 몇 가지 작은 업데이트를 포함하는 또 다른 포인트 릴리스입니다. 제네릭 형식 매개 변수에 대해 새 제약 조건을 사용할 수 있습니다. 다른 변경 내용은 [`stackalloc`](./operators/stackalloc.md) 할당 사용을 포함하여 `fixed` 필드로 작업하는 것을 더 쉽게 만듭니다. `ref` 키워드로 선언된 로컬 변수는 새 스토리지를 참조하도록 다시 할당할 수 있습니다. 컴파일러에서 생성된 지원 필드를 대상으로 하는 자동 구현 속성에 특성을 배치할 수 있습니다. 식 변수는 이니셜라이저에서 사용할 수 있습니다. 튜플은 같음(또는 같지 않음)을 비교할 수 있습니다. 오버로드 확인에도 일부 개선이 있습니다.
  
 [C# 8.0 사양 제안](../../../_csharplang/proposals/csharp-8.0/nullable-reference-types.md)  
 C# 8.0은 .NET Core 3.0에서 사용할 수 있습니다. 이 기능에는 nullable 참조 형식, 재귀 패턴 일치, 기본 인터페이스 메서드, 비동기 스트림, 범위 및 인덱스, 선언을 사용한 패턴, null 병합 할당 및 읽기 전용 인스턴스 멤버가 포함됩니다.
  
## <a name="related-sections"></a>관련 단원  

 [C# 가이드](../index.md)  
 Visual C# 설명서 포털을 제공합니다.  
  
 [C#용 Visual Studio 개발 환경 사용](/visualstudio/get-started/csharp)  
 IDE 및 편집기를 설명하는 개념 및 작업 항목의 링크를 제공합니다.  
  
 [C# 프로그래밍 가이드](../programming-guide/index.md)  
 C# 프로그래밍 언어를 사용하는 방법에 대한 정보를 포함합니다.
