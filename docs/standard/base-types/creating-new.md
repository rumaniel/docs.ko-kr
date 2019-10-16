---
title: .NET에서 새 문자열 만들기
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CopyTo method
- Join method
- Format method
- Concat method
- strings [.NET Framework], creating
- Insert method
ms.assetid: 06fdf123-2fac-4459-8904-eb48ab908a30
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 50750b23af9e9cfca79b0f7db9d272e8e24971ab
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591408"
---
# <a name="creating-new-strings-in-net"></a>.NET에서 새 문자열 만들기
.NET Framework에서는 간단한 할당을 사용하여 문자열을 만들 수 있으며, 클래스 생성자를 오버로드하여 여러 다양한 매개 변수를 사용한 문자열 생성도 지원합니다. 또한 .NET Framework에서는 여러 문자열, 문자열 배열 또는 개체를 결합하여 새 문자열 개체를 만드는 여러 메서드를 <xref:System.String?displayProperty=nameWithType> 클래스에서 제공합니다.  
  
## <a name="creating-strings-using-assignment"></a>할당을 사용하여 문자열 만들기  
 새 <xref:System.String> 개체를 만드는 가장 쉬운 방법은 간단히 <xref:System.String> 개체에 문자열 리터럴을 할당하는 것입니다.  
  
## <a name="creating-strings-using-a-class-constructor"></a>클래스 생성자를 사용하여 문자열 만들기  
 <xref:System.String> 클래스 생성자의 오버로드를 사용하여 문자 배열에서 문자열을 만들 수 있습니다. 특정 문자를 지정된 횟수만큼 복제하여 새 문자열을 만들 수도 있습니다.  
  
## <a name="methods-that-return-strings"></a>문자열을 반환하는 메서드  
 다음 표에서는 새 문자열 개체를 반환하는 여러 유용한 메서드를 보여 줍니다.  
  
|메서드 이름|기능|  
|-----------------|---------|  
|<xref:System.String.Format%2A?displayProperty=nameWithType>|입력 개체 집합에서 형식이 지정된 문자열을 작성합니다.|  
|<xref:System.String.Concat%2A?displayProperty=nameWithType>|둘 이상의 문자열에서 문자열을 작성합니다.|  
|<xref:System.String.Join%2A?displayProperty=nameWithType>|문자열 배열을 결합하여 새 문자열을 작성합니다.|  
|<xref:System.String.Insert%2A?displayProperty=nameWithType>|기존 문자열의 지정된 인덱스에 문자열을 삽입하여 새 문자열을 작성합니다.|  
|<xref:System.String.CopyTo%2A?displayProperty=nameWithType>|문자열의 지정된 문자를 문자 배열의 지정된 위치에 복사합니다.|  
  
### <a name="format"></a>서식  
 **String.Format** 메서드를 사용하여 서식이 지정된 문자열을 만들고 여러 개체를 나타내는 문자열을 연결할 수 있습니다. 이 메서드는 전달된 모든 개체를 문자열로 자동으로 변환합니다. 예를 들어 애플리케이션이 **Int32** 값과 **DateTime** 값을 사용자에게 표시해야 하는 경우 **Format** 메서드를 사용하여 이러한 값을 나타내는 문자열을 쉽게 생성할 수 있습니다. 이 메서드에서 사용되는 형식 지정 규칙에 대한 자세한 내용은 [복합 형식 지정](../../../docs/standard/base-types/composite-formatting.md) 섹션을 참조하세요.  
  
 다음 예제에서는 **Format** 메서드를 통해 정수 변수를 사용하는 문자열을 만듭니다.  
  
 [!code-csharp[Strings.Creating#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#1)]
 [!code-vb[Strings.Creating#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#1)]  
  
 이 예제에서 <xref:System.DateTime.Now%2A?displayProperty=nameWithType>는 현재 스레드와 연결된 문화권에서 지정된 방식으로 현재 날짜와 시간을 표시합니다.  
  
### <a name="concat"></a>Concat  
 **String.Concat** 메서드를 사용하여 둘 이상의 기존 개체에서 새 문자열 개체를 쉽게 만들 수 있습니다. 문자열을 연결하는 언어 독립적인 방법을 제공합니다. 이 메서드는 **System.Object**에서 파생된 모든 클래스를 허용합니다. 다음 예제에서는 두 개의 기존 문자열 개체와 구분 문자에서 문자열을 만듭니다.  
  
 [!code-csharp[Strings.Creating#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#2)]
 [!code-vb[Strings.Creating#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#2)]  
  
### <a name="join"></a>Join  
 **String.Join** 메서드는 문자열 배열 및 구분 기호 문자열에서 새 문자열을 만듭니다. 이 메서드는 여러 문자열을 함께 연결하여 쉼표 등으로 구분된 목록을 만들려는 경우에 유용합니다.  
  
 다음 예제에서는 공백을 사용하여 문자열 배열을 바인딩합니다.  
  
 [!code-csharp[Strings.Creating#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#3)]
 [!code-vb[Strings.Creating#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#3)]  
  
### <a name="insert"></a>Insert  
 **String.Insert** 메서드는 다른 문자열의 지정된 위치에 문자열을 삽입하여 새 문자열을 만듭니다. 이 메서드는 0부터 시작하는 인덱스를 사용합니다. 다음 예제에서는 `MyString`의 다섯 번째 인덱스 위치에 문자열을 삽입하고 이 값으로 새 문자열을 만듭니다.  
  
 [!code-csharp[Strings.Creating#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#4)]
 [!code-vb[Strings.Creating#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#4)]  
  
### <a name="copyto"></a>CopyTo  
 **String.CopyTo** 메서드는 문자열의 일부를 문자 배열에 복사합니다. 기존 문자열의 시작 인덱스와 복사할 문자 수를 둘 다 지정할 수 있습니다. 이 메서드는 소스 인덱스, 문자 배열, 대상 인덱스 및 복사할 문자 수를 사용합니다. 모든 인덱스는 0부터 시작합니다.  
  
 다음 예제에서는 **CopyTo** 메서드를 사용하여 “Hello” 단어의 문자를 문자열 개체에서 문자 배열의 첫 번째 인덱스 위치로 복사합니다.  
  
 [!code-csharp[Strings.Creating#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#5)]
 [!code-vb[Strings.Creating#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#5)]  
  
## <a name="see-also"></a>참고 항목

- [기본적인 문자열 작업](../../../docs/standard/base-types/basic-string-operations.md)
- [복합 형식 지정](../../../docs/standard/base-types/composite-formatting.md)
