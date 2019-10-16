---
title: 명명된 인수와 선택적 인수 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- namedParameter_CSharpKeyword
- cs_namedParameter
helpviewer_keywords:
- parameters [C#], named
- named arguments [C#]
- arguments [C#], named
- optional arguments [C#]
- arguments [C#], optional
- parameters [C#], optional
- named and optional arguments [C#]
ms.assetid: 839c960c-c2dc-4d05-af4d-ca5428e54008
ms.openlocfilehash: ad3f7949e01a387c3c7de2a0702d11b106ea0040
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922205"
---
# <a name="named-and-optional-arguments-c-programming-guide"></a>명명된 인수와 선택적 인수(C# 프로그래밍 가이드)
C# 4에서는 명명된 인수와 선택적 인수가 도입되었습니다. *명명된 인수*를 사용하면 인수를 매개 변수 목록 내의 매개 변수 위치가 아니라 매개 변수 이름과 연결하여 특정 매개 변수에 대한 인수를 지정할 수 있습니다. *선택적 인수*를 사용하면 일부 매개 변수에 대한 인수를 생략할 수 있습니다. 두 기법 모두 메서드, 인덱서, 생성자 및 대리자에 사용할 수 있습니다.  
  
 명명된 인수와 선택적 인수를 사용하는 경우 매개 변수 목록이 아니라 인수 목록에 표시되는 순서대로 인수가 평가됩니다.  
  
 명명된 매개 변수와 선택적 매개 변수를 함께 사용하는 경우 선택적 매개 변수 목록에서 몇 개의 매개 변수에 대해서만 인수를 제공할 수 있습니다. 이 기능은 Microsoft Office 자동화 API와 같은 COM 인터페이스에 대한 호출에 큰 도움이 됩니다.  
  
## <a name="named-arguments"></a>명명된 인수  
 명명된 인수를 사용하면 호출된 메서드의 매개 변수 목록에서 매개 변수의 순서를 기억하거나 조회할 필요가 없습니다. 각 인수에 대한 매개 변수를 매개 변수 이름으로 지정할 수 있습니다. 예를 들어 함수에 정의된 순서의 위치로 인수를 보내서 표준 방법으로 주문 세부 정보(예: 판매자 이름, 주문 번호 및 제품 이름)를 호출할 수 있습니다.
  
 `PrintOrderDetails("Gift Shop", 31, "Red Mug");`
  
 매개 변수의 순서를 기억하지 못하지만 해당 이름을 알고 있는 경우 임의의 순서로 인수를 보낼 수 있습니다.  
  
 `PrintOrderDetails(orderNum: 31, productName: "Red Mug", sellerName: "Gift Shop");`
  
 `PrintOrderDetails(productName: "Red Mug", sellerName: "Gift Shop", orderNum: 31);`
  
 또한 명명된 인수는 각 인수가 무엇을 나타내는지를 식별하여 코드의 가독성을 향상합니다. 아래 예제 메서드에서 `sellerName`은 null 또는 공백일 수 없습니다. `sellerName` 및 `productName`은 모두 문자열 형식이므로, 위치로 인수를 보내는 대신, 명명된 인수를 사용하여 두 코드를 구분하고 코드를 읽는 사람의 혼동을 줄일 수 있습니다.
  
 위치 인수와 함께 사용된 명명된 인수는 

- 그 다음에 위치 인수가 없거나

 `PrintOrderDetails("Gift Shop", 31, productName: "Red Mug");`

- _C# 7.2로 시작하고_ 올바른 위치에 사용되는 한 유효합니다. 아래 예제에서 `orderNum` 매개 변수는 올바른 위치에 있지만 명시적으로 명명되지 않습니다.

 `PrintOrderDetails(sellerName: "Gift Shop", 31, productName: "Red Mug");`
  
 그러나 순서 상관없이 명명된 인수는 그 다음에 위치 인수가 나오는 경우 유효하지 않습니다.

 ```csharp
 // This generates CS1738: Named argument specifications must appear after all fixed arguments have been specified.
 PrintOrderDetails(productName: "Red Mug", 31, "Gift Shop");
 ```
  
## <a name="example"></a>예  
 다음 코드는 몇 가지 추가 코드와 함께 이 섹션의 예제를 구현합니다.  
  
 [!code-csharp[csProgGuideNamedAndOptional#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/program.cs#1)]  
  
## <a name="optional-arguments"></a>선택적 인수  
 메서드, 생성자, 인덱서 또는 대리자의 정의에서 해당 매개 변수를 필수 또는 선택 사항으로 지정할 수 있습니다. 호출 시 모든 필수 매개 변수에 대한 인수를 제공해야 하지만 선택적 매개 변수에 대한 인수는 생략할 수 있습니다.  
  
 각 선택적 매개 변수에는 해당 정의의 일부로 기본값이 있습니다. 해당 매개 변수에 대한 인수가 전송되지 않은 경우 기본값이 사용됩니다. 기본값은 다음 유형의 식 중 하나여야 합니다.  
  
- 상수 식  
  
- `new ValType()` 형태의 식. 여기서 `ValType`은 [enum](../../language-reference/keywords/enum.md) 또는 [struct](./structs.md)와 같은 값 형식입니다.  
  
- [default(ValType)](../../language-reference/operators/default.md) 형태의 식. 여기서 `ValType`은 값 형식입니다.  
  
 선택적 매개 변수는 매개 변수 목록의 끝에서 모든 필수 매개 변수 다음에 정의됩니다. 호출자가 연속된 선택적 매개 변수 중 하나에 대한 인수를 제공하는 경우 이전의 모든 선택적 매개 변수에 대한 인수를 제공해야 합니다. 인수 목록에서 쉼표로 구분된 간격은 지원되지 않습니다. 예를 들어 다음 코드에서 인스턴스 메서드 `ExampleMethod`는 필수 매개 변수 하나와 선택적 매개 변수 두 개로 정의됩니다.  
  
 [!code-csharp[csProgGuideNamedAndOptional#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/optional.cs#15)]  
  
 다음과 같은 `ExampleMethod` 호출에서는 세 번째 매개 변수에 대한 인수가 제공되었지만 두 번째 매개 변수에 대한 인수는 제공되지 않았기 때문에 컴파일러 오류가 발생합니다.  
  
 `//anExample.ExampleMethod(3, ,4);`  
  
 그러나 세 번째 매개 변수의 이름을 알고 있으면 명명된 인수를 사용하여 작업을 수행할 수 있습니다.  
  
 `anExample.ExampleMethod(3, optionalint: 4);`  
  
 IntelliSense는 다음 그림과 같이 대괄호를 사용하여 선택적 매개 변수를 나타냅니다.  
  
 ![ExampleMethod 메서드에 대한 IntelliSense 요약 정보를 보여주는 스크린샷.](./media/named-and-optional-arguments/optional-examplemethod-parameters.png)  
  
> [!NOTE]
> .NET <xref:System.Runtime.InteropServices.OptionalAttribute> 클래스를 사용하여 선택적 매개 변수를 선언할 수도 있습니다. `OptionalAttribute` 매개 변수는 기본값이 필요하지 않습니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 `ExampleClass`에 대한 생성자에 선택 사항인 매개 변수 하나가 있습니다. 인스턴스 메서드 `ExampleMethod`에는 `required`라는 필수 매개 변수 하나와 `optionalstr` 및 `optionalint`라는 선택적 매개 변수 두 개가 있습니다. `Main`의 코드는 생성자와 메서드를 호출할 수 있는 여러 방법을 보여 줍니다.  
  
 [!code-csharp[csProgGuideNamedAndOptional#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/optional.cs#2)]  
  
## <a name="com-interfaces"></a>COM 인터페이스  
 동적 개체 및 기타 향상된 기능에 대한 지원과 더불어 명명된 인수와 선택적 인수는 Office 자동화 API와 같은 COM API와의 상호 운용성을 크게 향상합니다.  
  
 예를 들어 <xref:Microsoft.Office.Interop.Excel.Range.AutoFormat%2A>Microsoft Office Excel<xref:Microsoft.Office.Interop.Excel.Range> 인터페이스의 메서드에는 모두 선택 사항인 매개 변수 7개가 있습니다. 해당 매개 변수는 다음 그림에 표시됩니다.  
  
 ![AutoFormat 메서드에 대한 IntelliSense 요약 정보를 보여주는 스크린샷](./media/named-and-optional-arguments/autoformat-method-parameters.png)  
  
 C# 3.0 및 이전 버전에서는 다음 예제와 같이 각 매개 변수에 대한 인수가 필요합니다.  
  
 [!code-csharp[csProgGuideNamedAndOptional#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/namedandoptcom.cs#3)]  
  
 그러나 C# 4.0에서 도입된 명명된 인수와 선택적 인수를 사용하면 `AutoFormat` 호출을 훨씬 간소화할 수 있습니다. 명명된 인수와 선택적 인수를 사용하면 매개 변수의 기본값을 변경하지 않으려는 경우 선택적 매개 변수에 대한 인수를 생략할 수 있습니다. 다음 호출에서는 7개 매개 변수 중 하나에 대한 값만 지정되었습니다.  
  
 [!code-csharp[csProgGuideNamedAndOptional#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/namedandoptcom.cs#13)]  
  
 자세한 내용과 예제는 [방법: Office 프로그래밍에 명명된 인수와 선택적 인수 사용](./how-to-use-named-and-optional-arguments-in-office-programming.md) 및 [방법: Visual C# 기능을 사용하여 Office Interop 개체에 액세스](../interop/how-to-access-office-onterop-objects.md)를 참조하세요.  
  
## <a name="overload-resolution"></a>Overload Resolution  
 명명된 인수 및 선택적 인수를 사용하면 다음과 같은 방법으로 오버로드 확인에 영향을 줍니다.  
  
- 메서드, 인덱서 또는 생성자는 해당 매개 변수가 각각 선택 사항이거나 이름 또는 위치로 호출하는 문의 단일 인수에 해당하고 이 인수를 매개 변수의 형식으로 변환할 수 있는 경우 실행 후보가 됩니다.  
  
- 둘 이상의 인증서가 있으면 기본 설정 변환에 대한 오버로드 확인 규칙이 명시적으로 지정된 인수에 적용됩니다. 선택적 매개 변수에 대해 생략된 인수는 무시됩니다.  
  
- 두 후보가 똑같이 정상이라고 판단되는 경우 기본적으로 호출에서 인수가 생략된 선택적 매개 변수가 없는 후보가 설정됩니다. 이는 매개 변수가 적은 후보에 대한 오버로드 확인에서 일반적인 기본 설정의 결과입니다.  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [방법: Office 프로그래밍에서 명명된 인수 및 선택적 인수 사용](./how-to-use-named-and-optional-arguments-in-office-programming.md)
- [dynamic 형식 사용](../types/using-type-dynamic.md)
- [생성자 사용](./using-constructors.md)
- [인덱서 사용](../indexers/using-indexers.md)
