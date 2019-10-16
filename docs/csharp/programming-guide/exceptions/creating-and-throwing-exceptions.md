---
title: 예외 만들기 및 Throw - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- catching exceptions [C#]
- throwing exceptions [C#]
- exceptions [C#], creating
- exceptions [C#], throwing
ms.assetid: 6bbba495-a115-4c6d-90cc-1f4d7b5f39e2
ms.openlocfilehash: 605a28f8f804c11a9a6636c7a17ec5782cc5a429
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590309"
---
# <a name="creating-and-throwing-exceptions-c-programming-guide"></a>예외 만들기 및 Throw(C# 프로그래밍 가이드)
예외는 프로그램을 실행하는 동안 오류가 발생했음을 나타내는 데 사용됩니다. 오류를 설명하는 예외 개체가 만들어지고 [throw](../../language-reference/keywords/throw.md) 키워드를 통해 *throw*됩니다. 그런 다음 런타임에 가장 호환성이 높은 예외 처리기를 검색합니다.  
  
 프로그래머는 다음 조건 중 하나 이상에 해당할 경우 예외를 throw해야 합니다.  
  
- 메서드가 정의된 기능을 완료할 수 없는 경우.  
  
     예를 들어 메서드에 대한 매개 변수에 잘못된 값이 포함된 경우입니다.  
  
     [!code-csharp[csProgGuideExceptions#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#12)]  
  
- 개체 상태에 따라 개체에 대한 부적절한 호출이 이루어진 경우.  
  
     한 가지 예는 읽기 전용 파일에 쓰려고 시도하는 경우입니다. 개체 상태가 작업을 허용하지 않을 경우 이 클래스의 파생에 따라 <xref:System.InvalidOperationException>의 인스턴스 또는 개체를 throw합니다. 다음은 <xref:System.InvalidOperationException> 개체를 throw하는 메서드의 예제입니다.  
  
     [!code-csharp[csProgGuideExceptions#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#13)]  
  
- 메서드에 대한 인수가 예외를 일으키는 경우.  
  
     이 경우 원래 예외가 catch되고 <xref:System.ArgumentException> 인스턴스가 만들어져야 합니다. 원래 예외를 <xref:System.ArgumentException>의 생성자에 <xref:System.Exception.InnerException%2A> 매개 변수로 전달해야 합니다.  
  
     [!code-csharp[csProgGuideExceptions#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#14)]  
  
 예외에 이름이 <xref:System.Exception.StackTrace%2A>인 속성이 포함되어 있습니다. 이 문자열에는 현재 콜 스택에 대한 메서드의 이름과 각 메서드에 대해 예외가 throw된 파일 이름 및 줄 번호가 포함됩니다. <xref:System.Exception.StackTrace%2A> 개체는 `throw` 문의 지점에서 CLR(공용 언어 런타임)에 의해 자동으로 만들어지므로 해당 예외는 스택 추적이 시작되는 지점에서 throw되어야 합니다.  
  
 모든 예외에 이름이 <xref:System.Exception.Message%2A>인 속성이 포함되어 있습니다. 예외의 이유를 설명하려면 이 문자열을 설정해야 합니다. 보안이 중요한 정보는 메시지 텍스트에 넣으면 안 됩니다. <xref:System.Exception.Message%2A> 외에 <xref:System.ArgumentException>에는 예외를 throw한 인수의 이름으로 설정해야 하는 <xref:System.ArgumentException.ParamName%2A> 속성이 포함되어 있습니다. 속성 setter의 경우 <xref:System.ArgumentException.ParamName%2A>을 `value`로 설정해야 합니다.  
  
 public 및 protected 메서드는 의도한 함수를 완료할 수 없을 때마다 예외를 throw해야 합니다. throw된 예외 클래스는 오류 조건에 맞을 수 있는 가장 구체적인 예외여야 합니다. 이러한 예외는 클래스 기능의 일부로 문서화해야 하고 파생 클래스 또는 원래 클래스의 업데이트는 이전 버전과의 호환성을 위해 같은 동작을 유지해야 합니다.  
  
## <a name="things-to-avoid-when-throwing-exceptions"></a>예외를 throw할 때 피해야 하는 작업  
 다음 목록은 예외를 throw할 때 피해야 할 사례를 나타냅니다.  
  
- 프로그램 흐름을 일반 예외의 일부로 변경하는 데는 예외를 사용하면 안 됩니다. 오류 조건을 보고하고 처리하는 데만 예외를 사용해야 합니다.  
  
- 예외는 throw하는 대신 반환 값 또는 매개 변수로 반환하면 안 됩니다.  
  
- 고유한 소스 코드에서 의도적으로 <xref:System.Exception?displayProperty=nameWithType>, <xref:System.SystemException?displayProperty=nameWithType>, <xref:System.NullReferenceException?displayProperty=nameWithType> 또는 <xref:System.IndexOutOfRangeException?displayProperty=nameWithType>을 throw하지 마세요.  
  
- 릴리스 모드가 아닌 디버그 모드에서 throw될 수 있는 예외를 만들지 마세요. 개발 단계에서 런타임 오류를 식별하려면 대신 디버그 어설션을 사용하세요.  
  
## <a name="defining-exception-classes"></a>예외 클래스 정의  
 프로그램에서는 <xref:System> 네임스페이스의 미리 정의된 예외 클래스를 throw하거나(이전에 언급한 위치 제외) <xref:System.Exception>에서 파생시켜 자체 예외 클래스를 만들 수 있습니다. 파생 클래스는 매개 변수 없는 생성자, 메시지 속성을 설정하는 생성자, <xref:System.Exception.Message%2A> 및 <xref:System.Exception.InnerException%2A> 속성을 설정하는 생성자 두 개를 포함하여 네 개 이상의 생성자를 정의해야 합니다. 네 번째 생성자는 예외를 serialize하는 데 사용됩니다. 새 예외 클래스는 serialize할 수 있어야 합니다. 예:  
  
 [!code-csharp[csProgGuideExceptions#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#15)]  
  
 새로운 속성이 제공하는 데이터가 예외 확인에 유용할 경우에만 해당 속성을 예외 클래스에 추가해야 합니다. 새 속성이 파생 예외 클래스에 추가되면 추가된 정보를 반환하기 위해 `ToString()`을 재정의해야 합니다.  
  
## <a name="c-language-specification"></a>C# 언어 사양  

자세한 내용은 [C# 언어 사양](../../language-reference/language-specification/index.md)의 [예외](~/_csharplang/spec/exceptions.md) 및 [throw 문](~/_csharplang/spec/statements.md#the-throw-statement)을 참조하세요. 언어 사양은 C# 구문 및 사용법에 대 한 신뢰할 수 있는 소스 됩니다.
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [예외 및 예외 처리](./index.md)
- [예외 계층](../../../standard/exceptions/index.md)
- [예외 처리](./exception-handling.md)
