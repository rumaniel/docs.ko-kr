---
title: .NET 성능 팁
ms.date: 03/30/2017
helpviewer_keywords:
- C# language, performance
- performance [C#]
- Visual Basic, performance
- performance [Visual Basic]
ms.assetid: ae275793-857d-4102-9095-b4c2a02d57f4
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 14ed06bbd09d7551707628060b460584816e4711
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046292"
---
# <a name="net-performance-tips"></a>.NET 성능 팁
*성능*이라는 용어는 일반적으로 프로그램의 실행 속도를 나타냅니다. 경우에 따라 소스 코드에서 특정 기본 규칙을 따라 실행 속도를 높일 수 있습니다. 일부 프로그램에서는 코드를 자세히 검사하고 프로파일러를 사용하여 최대한 빠르게 실행 중인지 확인하는 작업을 해야 합니다. 다른 프로그램에서는 코드가 작성된 대로 만족스럽게 실행되므로 이러한 최적화를 수행하지 않아도 됩니다. 이 문서에서는 성능이 떨어질 수 있는 몇 가지 일반적인 영역과 성능 향상 팁 및 추가 성능 항목에 대한 링크를 나열합니다. 성능 계획 및 측정에 대한 자세한 내용은 [성능](index.md)을 참조하세요.  
  
## <a name="boxing-and-unboxing"></a>boxing 및 unboxing  
 예를 들어 <xref:System.Collections.ArrayList?displayProperty=nameWithType>와 같이 제네릭이 아닌 컬렉션 클래스에서 상당히 많은 횟수로 boxing되어야 하는 경우 값 형식을 사용하지 않는 것이 좋습니다. <xref:System.Collections.Generic.List%601?displayProperty=nameWithType>와 같은 제네릭 컬렉션을 사용하는 경우 값 형식을 boxing하지 않을 수 있습니다. Boxing 및 unboxing은 계산을 많이 해야 하는 프로세스입니다. 값 형식이 boxing되면 완전히 새로운 개체가 생성되어야 합니다. 이 작업은 단순 참조 할당보다 20배나 오래 걸립니다. unboxing 시 캐스팅 프로세스는 할당의 4배에 달하는 시간이 소요될 수 있습니다. 자세한 내용은 [boxing 및 unboxing](../../csharp/programming-guide/types/boxing-and-unboxing.md)을 참조하세요.  
  
## <a name="strings"></a>문자열  
 예를 들어 연속 루프에서 다수의 문자열 변수를 연결하는 경우 C# [+ 연산자](../../csharp/language-reference/operators/addition-operator.md) 또는 Visual Basic [연결 연산자](../../visual-basic/language-reference/operators/concatenation-operators.md)가 아니라 <xref:System.Text.StringBuilder?displayProperty=nameWithType>를 대신 사용합니다. 자세한 내용은 [방법: Visual Basic에서 여러](../../csharp/how-to/concatenate-multiple-strings.md) 문자열과 [연결 연산자](../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)를 연결 합니다.  
  
## <a name="destructors"></a>소멸자  
 빈 소멸자는 사용할 수 없습니다. 클래스에 소멸자가 포함되어 있으면 Finalize 큐에서 항목이 생성됩니다. 소멸자를 호출하면 가비지 수집기가 호출되어 큐를 처리합니다. 소멸자가 비어 있으면 성능이 저하됩니다. 자세한 내용은 [소멸자](../../csharp/programming-guide/classes-and-structs/destructors.md) 및 [개체 수명을 참조 하세요. 개체를 만들고 제거](../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)하는 방법입니다.  
  
## <a name="other-resources"></a>기타 리소스  
  
- [더 빠른 관리 코드 작성: 작업 비용 파악](https://go.microsoft.com/fwlink/?LinkId=99294)  
  
- [고성능 관리 되는 응용 프로그램 작성: 입문](https://go.microsoft.com/fwlink/?LinkId=99295)  
  
- [가비지 수집기 기본 및 성능 힌트](https://go.microsoft.com/fwlink/?LinkId=99296)  
  
- [.NET 애플리케이션에서의 성능 팁과 요량](https://go.microsoft.com/fwlink/?LinkId=99297)  

- [Rico Mariani의 성능 정보](https://go.microsoft.com/fwlink/?LinkId=115679)  

- [Vance Morrison의 블로그](https://blogs.msdn.microsoft.com/vancem/)
  
## <a name="see-also"></a>참고자료

- [성능](index.md)
- [Visual Basic 프로그래밍 가이드](../../visual-basic/programming-guide/index.md)
- [C# 프로그래밍 가이드](../../csharp/programming-guide/index.md)
