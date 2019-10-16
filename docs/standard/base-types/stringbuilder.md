---
title: .NET에서 StringBuilder 클래스 사용
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Remove method
- strings [.NET Framework], capacities
- StringBuilder object
- Replace method
- AppendFormat method
- Append method
- Insert method
- strings [.NET Framework], StringBuilder object
ms.assetid: 5c14867c-9a99-45bc-ae7f-2686700d377a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2f18bdfaee1d79ce84a5b2822d52231f4bed098c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54620060"
---
# <a name="using-the-stringbuilder-class-in-net"></a>.NET에서 StringBuilder 클래스 사용
<xref:System.String> 개체는 변경할 수 없습니다. <xref:System.String?displayProperty=nameWithType> 클래스에서 메서드 중 하나를 사용할 때마다 메모리에 새 문자열 개체가 생성되므로, 새 개체에 대한 공간을 새로 할당해야 합니다. 문자열을 반복적으로 수정해야 하는 경우 새로운 <xref:System.String> 개체 생성과 관련된 오버헤드로 인해 비용이 증가할 수 있습니다. 새 개체를 만들지 않고 문자열을 수정하려는 경우 <xref:System.Text.StringBuilder?displayProperty=nameWithType> 클래스를 사용할 수 있습니다. 예를 들어 <xref:System.Text.StringBuilder> 클래스를 사용하면 루프에서 많은 문자열을 연결할 때 성능이 향상될 수 있습니다.  
  
## <a name="importing-the-systemtext-namespace"></a>System.Text 네임스페이스 가져오기  
 <xref:System.Text.StringBuilder> 클래스는 <xref:System.Text> 네임스페이스에 있습니다.  코드에서 정규화된 형식 이름을 제공할 필요가 없도록 하려면 <xref:System.Text> 네임스페이스를 가져올 수 있습니다.  
  
 [!code-cpp[Conceptual.StringBuilder#11](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#11)]
 [!code-csharp[Conceptual.StringBuilder#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#11)]
 [!code-vb[Conceptual.StringBuilder#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#11)]  
  
## <a name="instantiating-a-stringbuilder-object"></a>StringBuilder 개체 인스턴스화  
 다음 예제와 같이 오버로드된 생성자 메서드 중 하나로 변수를 초기화하여 <xref:System.Text.StringBuilder> 클래스의 새 인스턴스를 만들 수 있습니다.  
  
 [!code-cpp[Conceptual.StringBuilder#1](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#1)]
 [!code-csharp[Conceptual.StringBuilder#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#1)]
 [!code-vb[Conceptual.StringBuilder#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#1)]  
  
## <a name="setting-the-capacity-and-length"></a>용량 및 길이 설정  
 <xref:System.Text.StringBuilder>는 캡슐화되는 문자열에서 문자 수를 확장할 수 있는 동적 개체이지만, 보관할 수 있는 최대 문자 수 값을 지정할 수 있습니다. 이 값을 개체의 용량이라고 하며, 현재 <xref:System.Text.StringBuilder>에 보관된 문자열의 길이와 혼동해서는 안 됩니다. 예를 들어 길이가 5인 “Hello” 문자열을 사용하여 <xref:System.Text.StringBuilder> 클래스의 새 인스턴스를 만들고 개체의 최대 용량을 25로 지정할 수 있습니다. <xref:System.Text.StringBuilder>를 수정할 경우 용량에 도달할 때까지 자체 크기를 다시 할당할 수 없습니다. 이 경우 새 공간이 자동으로 할당되고 용량이 두 배로 증가합니다. 오버로드된 생성자 중 하나를 사용하여 <xref:System.Text.StringBuilder> 클래스의 용량을 지정할 수 있습니다. 다음 예에서는 `myStringBuilder` 개체를 최대 25개 공간으로 확장할 수 있도록 지정합니다.  
  
 [!code-cpp[Conceptual.StringBuilder#2](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#2)]
 [!code-csharp[Conceptual.StringBuilder#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#2)]
 [!code-vb[Conceptual.StringBuilder#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#2)]  
  
 또한 읽기/쓰기 <xref:System.Text.StringBuilder.Capacity%2A> 속성을 사용하여 개체의 최대 길이를 설정할 수 있습니다. 다음 예에서는 **Capacity** 속성을 사용하여 최대 개체 길이를 정의합니다.  
  
 [!code-cpp[Conceptual.StringBuilder#3](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#3)]
 [!code-csharp[Conceptual.StringBuilder#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#3)]
 [!code-vb[Conceptual.StringBuilder#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#3)]  
  
 <xref:System.Text.StringBuilder.EnsureCapacity%2A> 메서드를 사용하여 현재 **StringBuilder**의 용량을 확인할 수 있습니다. 용량이 전달된 값보다 크면 변경되지 않고, 용량이 전달된 값보다 작으면 현재 용량이 전달된 값과 일치하도록 변경됩니다.  
  
 <xref:System.Text.StringBuilder.Length%2A> 속성을 보거나 설정할 수도 있습니다. **Length** 속성을 **Capacity** 속성보다 큰 값으로 설정하면 **Capacity** 속성이 **Length** 속성과 동일한 값으로 자동으로 변경됩니다. **Length** 속성을 현재 **StringBuilder** 내의 문자열 길이보다 작은 값으로 설정하면 문자열이 단축됩니다.  
  
## <a name="modifying-the-stringbuilder-string"></a>StringBuilder 문자열 수정  
 다음 표에서는 **StringBuilder**의 내용을 수정하는 데 사용할 수 있는 메서드를 보여 줍니다.  
  
|메서드 이름|사용|  
|-----------------|---------|  
|<xref:System.Text.StringBuilder.Append%2A?displayProperty=nameWithType>|현재 **StringBuilder**의 끝에 정보를 추가합니다.|  
|<xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType>|문자열에 전달된 서식 지정자를 서식 있는 텍스트로 바꿉니다.|  
|<xref:System.Text.StringBuilder.Insert%2A?displayProperty=nameWithType>|현재 **StringBuilder**의 지정된 인덱스에 문자열 또는 개체를 삽입합니다.|  
|<xref:System.Text.StringBuilder.Remove%2A?displayProperty=nameWithType>|현재 **StringBuilder**에서 지정된 수의 문자를 제거합니다.|  
|<xref:System.Text.StringBuilder.Replace%2A?displayProperty=nameWithType>|지정된 인덱스에서 지정된 문자를 바꿉니다.|  
  
### <a name="append"></a>추가  
 **Append** 메서드를 사용하여 현재 **StringBuilder**에 표시되는 문자열의 끝에 개체의 문자열 표현이나 텍스트를 추가할 수 있습니다. 다음 예에서는 **StringBuilder**를 "Hello World"로 초기화한 다음 개체의 끝에 일부 텍스트를 추가합니다. 필요한 경우 공간이 자동으로 할당됩니다.  
  
 [!code-cpp[Conceptual.StringBuilder#4](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#4)]
 [!code-csharp[Conceptual.StringBuilder#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#4)]
 [!code-vb[Conceptual.StringBuilder#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#4)]  
  
### <a name="appendformat"></a>AppendFormat  
 <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType> 메서드는 <xref:System.Text.StringBuilder> 개체의 끝에 텍스트를 추가합니다. 또한 서식 지정할 개체의 <xref:System.IFormattable> 구현을 호출하여 복합 서식 지정 기능을 지원합니다. 자세한 내용은 [복합 서식 지정](../../../docs/standard/base-types/composite-formatting.md)을 참조하세요. 따라서 숫자, 날짜 및 시간, 열거형 값에 대한 표준 서식 문자열, 숫자, 날짜 및 시간 값에 대한 사용자 지정 서식 문자열, 사용자 지정 형식에 대해 정의된 서식 문자열을 허용합니다. 서식 지정에 대한 자세한 내용은 [서식 지정 형식](../../../docs/standard/base-types/formatting-types.md)을 참조하세요. 이 메서드를 사용하여 변수의 서식을 사용자 지정하고 해당 값을 <xref:System.Text.StringBuilder>에 추가할 수 있습니다. 다음 예에서는 <xref:System.Text.StringBuilder.AppendFormat%2A> 메서드를 사용하여 통화 값으로 서식 지정된 정수 값을 <xref:System.Text.StringBuilder> 개체의 끝에 배치합니다.  
  
 [!code-cpp[Conceptual.StringBuilder#5](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#5)]
 [!code-csharp[Conceptual.StringBuilder#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#5)]
 [!code-vb[Conceptual.StringBuilder#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#5)]  
  
### <a name="insert"></a>Insert  
 <xref:System.Text.StringBuilder.Insert%2A> 메서드는 현재 <xref:System.Text.StringBuilder> 개체의 지정된 위치에 문자열 또는 개체를 추가합니다. 다음 예에서는 이 메서드를 사용하여 <xref:System.Text.StringBuilder> 개체의 여섯 번째 위치에 단어를 삽입합니다.  
  
 [!code-cpp[Conceptual.StringBuilder#6](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#6)]
 [!code-csharp[Conceptual.StringBuilder#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#6)]
 [!code-vb[Conceptual.StringBuilder#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#6)]  
  
### <a name="remove"></a>제거  
 **Remove** 메서드를 사용하여 지정된 0부터 시작하는 인덱스를 기준으로 현재 <xref:System.Text.StringBuilder> 개체에서 지정된 수의 문자를 제거할 수 있습니다. 다음 예에서는 **Remove** 메서드를 사용하여 <xref:System.Text.StringBuilder> 개체를 단축합니다.  
  
 [!code-cpp[Conceptual.StringBuilder#7](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#7)]
 [!code-csharp[Conceptual.StringBuilder#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#7)]
 [!code-vb[Conceptual.StringBuilder#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#7)]  
  
### <a name="replace"></a>바꾸기  
 **Replace** 메서드는 <xref:System.Text.StringBuilder> 개체 내의 문자를 다른 지정된 문자로 바꾸는 데 사용할 수 있습니다. 다음 예에서는 **Replace** 메서드를 사용하여 <xref:System.Text.StringBuilder> 개체에서 느낌표 문자(!)의 모든 인스턴스를 검색한 다음, 물음표 문자(?)로 바꿉니다.  
  
 [!code-cpp[Conceptual.StringBuilder#8](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#8)]
 [!code-csharp[Conceptual.StringBuilder#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#8)]
 [!code-vb[Conceptual.StringBuilder#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#8)]  
  
## <a name="converting-a-stringbuilder-object-to-a-string"></a>StringBuilder 개체를 문자열로 변환  
 <xref:System.Text.StringBuilder> 개체에 표시되는 문자열을 <xref:System.String> 매개 변수를 가진 메서드에 전달하거나 사용자 인터페이스에 표시하려면 <xref:System.Text.StringBuilder> 개체를 <xref:System.String> 개체로 변환해야 합니다. <xref:System.Text.StringBuilder.ToString%2A?displayProperty=nameWithType> 메서드를 호출하여 이 변환을 수행합니다. 다음 예에서는 다양한 <xref:System.Text.StringBuilder> 메서드를 호출한 다음, <xref:System.Text.StringBuilder.ToString?displayProperty=nameWithType> 메서드를 호출하여 문자열을 표시합니다.  
  
 [!code-csharp[Conceptual.StringBuilder#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/tostringexample1.cs#10)]
 [!code-vb[Conceptual.StringBuilder#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/tostringexample1.vb#10)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Text.StringBuilder?displayProperty=nameWithType>
- [기본적인 문자열 작업](../../../docs/standard/base-types/basic-string-operations.md)
- [형식 서식 지정](../../../docs/standard/base-types/formatting-types.md)
