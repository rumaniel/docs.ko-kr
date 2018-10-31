---
title: 네임스페이스 사용(C# 프로그래밍 가이드)
ms.date: 07/20/2015
f1_keywords:
- cs.names
helpviewer_keywords:
- fully qualified names [C#]
- namespaces [C#], how to use
ms.assetid: 1fe8bf39-addc-438a-bd9e-86410e32381d
ms.openlocfilehash: 81876d1818a6e82764e4aea0ae2b6f9e091f0ba3
ms.sourcegitcommit: 15d99019aea4a5c3c91ddc9ba23692284a7f61f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49123399"
---
# <a name="using-namespaces-c-programming-guide"></a>네임스페이스 사용(C# 프로그래밍 가이드)
네임스페이스는 C# 프로그램 내에서 두 가지 방법으로 많이 사용됩니다. 첫째, .NET Framework 클래스는 네임스페이스를 사용하여 많은 클래스를 구성합니다. 둘째, 고유한 네임스페이스를 선언하면 대규모 프로그래밍 프로젝트에서 클래스 및 메서드 이름의 범위를 제어할 수 있습니다.  
  
## <a name="accessing-namespaces"></a>네임스페이스 액세스  
 대부분의 C# 응용 프로그램은 `using` 지시문 섹션으로 시작합니다. 이 섹션에는 응용 프로그램이 자주 사용하는 네임스페이스가 나열되어, 프로그래머가 내부에 포함된 메서드를 사용할 때마다 정규화된 이름을 지정할 필요가 없도록 합니다.  
  
 예를 들어 다음 줄을 포함할 수 있습니다.  
  
 [!code-csharp[csProgGuide#1](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/using-namespaces_1.cs)]  
  
 프로그램의 시작 부분에서 프로그래머는 다음 코드를 사용할 수 있습니다.  
  
 [!code-csharp[csProgGuide#31](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/using-namespaces_2.cs)]  
  
 위 코드를 아래 코드 대신 사용합니다.  
  
 [!code-csharp[csProgGuide#30](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/using-namespaces_3.cs)]  
  
## <a name="namespace-aliases"></a>네임스페이스 별칭  
 [using 지시문](../../../csharp/language-reference/keywords/using-directive.md)을 사용하여 [namespace](../../../csharp/language-reference/keywords/namespace.md)의 별칭을 만들 수도 있습니다. 예를 들어 중첩 네임스페이스가 포함된 이전에 작성한 네임스페이스를 사용하는 경우, 다음 예제와 같이 특정 네임스페이스를 약식으로 참조하는 별칭을 선언할 수 있습니다.  
  
 [!code-csharp[csProgGuideNamespaces#7](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_4.cs)]  
  
## <a name="using-namespaces-to-control-scope"></a>네임스페이스를 사용하여 범위 제어  
 `namespace` 키워드는 범위를 선언하는 데 사용됩니다. 프로젝트 내에서 범위를 만드는 기능은 코드 구성에 도움이 되며, 전역적으로 고유한 형식을 만들 수 있게 해줍니다. 다음 예제에서 `SampleClass`라는 클래스는 서로 중첩된 두 개의 네임스페이스에 정의되어 있습니다. [ 연산자](../../../csharp/language-reference/operators/member-access-operator.md)는 호출되는 메서드를 구분하는 데 사용됩니다.  
  
 [!code-csharp[csProgGuideNamespaces#8](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_5.cs)]  
  
## <a name="fully-qualified-names"></a>정규화된 이름  
 네임스페이스 및 형식에는 논리적 계층 구조를 나타내는 정규화된 이름으로 설명된 고유한 제목이 있습니다. 예를 들어 `A.B` 문은 `A`는 네임스페이스 또는 형식의 이름이고 `B`는 그 안에 중첩됨을 암시합니다.  
  
 다음 예제에서는 중첩된 클래스 및 네임스페이스가 있습니다. 정규화된 이름이 각 엔터티 뒤에 주석으로 표시됩니다.  
  
 [!code-csharp[csProgGuideNamespaces#9](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_6.cs)]  
  
 앞의 코드 세그먼트에서:  
  
-   `N1` 네임스페이스는 전역 네임스페이스의 멤버입니다. 정규화된 이름은 `N1`입니다.  
  
-   `N2` 네임스페이스는 `N1`의 멤버입니다. 정규화된 이름은 `N1.N2`입니다.  
  
-   `C1` 클래스는 `N1`의 멤버입니다. 정규화된 이름은 `N1.C1`입니다.  
  
-   이 코드에서는 클래스 이름 `C2`가 두 번 사용되었습니다. 그러나 정규화된 이름은 고유합니다. `C2`의 첫 번째 인스턴스는 `C1` 내에서 선언되었으므로 정규화된 이름이 `N1.C1.C2`입니다. `C2`의 두 번째 인스턴스는 `N2` 네임스페이스 내에서 선언되었으므로 정규화된 이름이 `N1.N2.C2`입니다.  
  
 앞의 코드 세그먼트를 사용하여 다음과 같이 `N1.N2` 네임스페이스에 새 클래스 멤버 `C3`를 추가할 수 있습니다.  
  
 [!code-csharp[csProgGuideNamespaces#10](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_7.cs)]  
  
 일반적으로 `::`을 사용하여 네임스페이스 별칭을 참조하거나, `global::`을 사용하여 전역 네임스페이스를 참조하고 `.`를 사용하여 형식 또는 멤버를 한정합니다.  
  
 네임스페이스 대신 형식을 참조하는 별칭과 함께 `::`을 사용하면 오류가 발생합니다. 예:  
  
 [!code-csharp[csProgGuideNamespaces#11](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_8.cs)]  
  
 [!code-csharp[csProgGuideNamespaces#12](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_9.cs)]  
  
 `global` 단어는 미리 정의된 별칭이 아니므로 `global.X`에 특별한 의미가 없습니다. `::`과 함께 사용하는 경우에만 특별한 의미가 있습니다.  
  
 `global::`은 항상 별칭이 아니라 전역 네임스페이스를 참조하기 때문에 global이란 별칭을 정의할 경우 컴파일러 경고 CS0440이 생성됩니다. 예를 들어 다음 줄에서는 경고가 생성됩니다.  
  
 [!code-csharp[csProgGuideNamespaces#13](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_10.cs)]  
  
 별칭과 함께 `::`을 사용하는 것은 좋은 방법이며, 예기치 않은 추가 형식의 도입을 방지합니다. 예를 들어 다음 예제를 고려해보세요.  
  
 [!code-csharp[csProgGuideNamespaces#14](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_11.cs)]  
  
 [!code-csharp[csProgGuideNamespaces#15](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_12.cs)]  
  
 이 예제는 작동하지만, `Alias`라는 형식을 이후에 도입할 경우 `Alias.`가 해당 형식에 대신 바인딩합니다. `Alias::Exception`을 사용하면 `Alias`가 네임스페이스 별칭으로 처리되며 형식으로 잘못 인식되지 않습니다.  
  
 `global` 별칭과 관련된 자세한 내용은 [방법: 전역 네임스페이스 별칭 사용](../../../csharp/programming-guide/namespaces/how-to-use-the-global-namespace-alias.md) 항목을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [네임스페이스](../../../csharp/programming-guide/namespaces/index.md)  
- [네임스페이스 키워드](../../../csharp/language-reference/keywords/namespace-keywords.md)  
- [. 연산자](../../../csharp/language-reference/operators/member-access-operator.md)  
- [:: 연산자](../../../csharp/language-reference/operators/namespace-alias-qualifer.md)  
- [extern](../../../csharp/language-reference/keywords/extern.md)
