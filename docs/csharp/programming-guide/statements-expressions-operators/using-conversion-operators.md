---
title: 변환 연산자 사용(C# 프로그래밍 가이드)
ms.date: 07/20/2015
helpviewer_keywords:
- conversions [C#], operators
- conversion operators [C#]
- operators [C#], conversion
- user-defined conversions [C#]
- implicit conversion operators [C#]
- explicit conversion operators [C#]
ms.assetid: caf36e89-c6c0-4b87-9f9e-85780a45c9a4
ms.openlocfilehash: 17a722f7160ae9cd03caa2dff9c4436fcf0f9d9e
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2018
ms.locfileid: "48845917"
---
# <a name="using-conversion-operators-c-programming-guide"></a>변환 연산자 사용(C# 프로그래밍 가이드)
쉽게 사용할 수 있는 `implicit` 변환 연산자 또는 코드를 읽는 사람에게 형식을 변환함을 명확하게 나타내는 `explicit` 변환 연산자를 사용할 수 있습니다. 이 항목에서는 두 형식의 변환 연산자를 모두 보여 줍니다.  
  
> [!NOTE]
>  단순 형식 변환에 대한 자세한 내용은 [방법: 문자열을 숫자로 변환](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md), [방법: 바이트 배열을 정수로 변환](../../../csharp/programming-guide/types/how-to-convert-a-byte-array-to-an-int.md), [방법: 16진수 문자열과 숫자 형식 간 변환](../../../csharp/programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md) 또는 <xref:System.Convert>를 참조하세요.  
  
## <a name="example"></a>예  
 명시적 변환 연산자의 예입니다. 이 연산자는 <xref:System.Byte> 형식에서 `Digit`라는 값 형식으로 변환합니다. 일부 바이트는 숫자로 변환할 수 없기 때문에 변환이 명시적이므로 `Main` 메서드와 같이 캐스트를 사용해야 합니다.  
  
 [!code-csharp[csProgGuideStatements#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-conversion-operators_1.cs)]  
  
## <a name="example"></a>예  
 이 예제에서는 앞의 예제에서 수행한 작업을 실행 취소하는 변환 연산자를 정의하여 암시적 변환 연산자를 보여 줍니다. 이 연산자는 `Digit`라는 값 클래스에서 정수 <xref:System.Byte> 형식으로 변환합니다. 모든 숫자를 <xref:System.Byte>로 변환할 수 있으므로 사용자에게 변환을 명시적으로 지정하도록 요구할 필요가 없습니다.  
  
 [!code-csharp[csProgGuideStatements#12](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-conversion-operators_2.cs)]  
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../../../csharp/language-reference/index.md)  
- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [변환 연산자](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md)  
- [is](../../../csharp/language-reference/keywords/is.md)
