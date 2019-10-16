---
title: .NET에서 기타 문자열 구문 분석
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Char data type, parsing strings
- enumerations [.NET Framework], parsing strings
- base types, parsing strings
- parsing strings, other strings
- Boolean data type, parsing strings
ms.assetid: d139bc00-3c4e-4d78-ac9a-5c951b258d28
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cf8a7b090b7a54328101478aed7edbbc5efd79ef
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54603627"
---
# <a name="parsing-other-strings-in-net"></a>.NET에서 기타 문자열 구문 분석
숫자 및 <xref:System.DateTime> 문자열 외에도 <xref:System.Char>, <xref:System.Boolean> 및 <xref:System.Enum> 형식을 나타내는 문자열을 데이터 형식으로 구문 분석할 수 있습니다.  
  
## <a name="char"></a>Char  
 **Char** 데이터 형식과 연결된 고정 구문 분석 메서드는 단일 문자를 포함하는 문자열을 해당 유니코드 값으로 변환하는 데 유용합니다. 다음 코드 예제에서는 문자열을 유니코드 문자로 구문 분석합니다.  
  
 [!code-cpp[Conceptual.String.Parse#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.parse/cpp/parse.cpp#2)]
 [!code-csharp[Conceptual.String.Parse#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.parse/cs/parse.cs#2)]
 [!code-vb[Conceptual.String.Parse#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.parse/vb/parse.vb#2)]  
  
## <a name="boolean"></a>부울  
 **부울** 데이터 형식은 부울 값을 나타내는 문자열을 실제 **부울** 형식으로 변환하는 데 사용할 수 있는 **Parse** 메서드를 포함합니다. 이 메서드는 대/소문자를 구분하지 않으며 "True" 또는 "False"를 포함하는 문자열을 성공적으로 구문 분석할 수 있습니다. **부울** 형식과 연결된 **Parse** 메서드는 공백으로 둘러싸인 문자열도 구문 분석할 수 있습니다. 다른 문자열을 전달하면 <xref:System.FormatException>이 throw됩니다.  
  
 다음 코드 예제에서는 **Parse** 메서드를 사용하여 문자열을 부울 값으로 변환합니다.  
  
 [!code-cpp[Conceptual.String.Parse#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.parse/cpp/parse.cpp#3)]
 [!code-csharp[Conceptual.String.Parse#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.parse/cs/parse.cs#3)]
 [!code-vb[Conceptual.String.Parse#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.parse/vb/parse.vb#3)]  
  
## <a name="enumeration"></a>열거형  
 고정 **Parse** 메서드를 사용하여 문자열 값에 대한 열거형 형식을 초기화할 수 있습니다. 이 메서드는 구문 분석하는 열거형 형식, 구문 분석할 문자열 및 구문 분석이 대/소문자를 구분하는지 여부를 나타내는 선택적 부울 플래그를 허용합니다. 구문 분석하는 문자열은 쉼표로 구분된 여러 값을 포함할 수 있으며 앞이나 뒤에는 하나 이상의 빈 공간(공백이라고도 함)이 있을 수 있습니다. 문자열에 여러 값이 포함된 경우 반환된 개체의 값은 비트 OR 연산과 함께 결합된 모든 지정된 값과 같습니다.  
  
 다음 예제에서는 **Parse** 메서드를 사용하여 문자열 표현을 열거형 값으로 변환합니다. <xref:System.DayOfWeek> 열거형은 문자열에서 **목요일**로 초기화됩니다.  
  
 [!code-cpp[Conceptual.String.Parse#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.parse/cpp/parse.cpp#4)]
 [!code-csharp[Conceptual.String.Parse#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.parse/cs/parse.cs#4)]
 [!code-vb[Conceptual.String.Parse#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.parse/vb/parse.vb#4)]  
  
## <a name="see-also"></a>참고 항목

- [Parsing Strings](../../../docs/standard/base-types/parsing-strings.md)
- [형식 서식 지정](../../../docs/standard/base-types/formatting-types.md)
- [.NET에서 형식 변환](../../../docs/standard/base-types/type-conversion.md)
