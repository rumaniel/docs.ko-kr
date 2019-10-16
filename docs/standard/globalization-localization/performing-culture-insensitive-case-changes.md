---
title: Culture를 구분하지 않는 대/소문자 변경 수행
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- String.ToLower method
- culture, case sensitivity
- Char.ToLower method
- case, changing in culture-insensitive strings
- Char.ToUpper method
- culture-insensitive string operations, case changes
- String.ToUpper method
- culture parameter
ms.assetid: 822d551c-c69a-4191-82f4-183d82c9179c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 04601ac0e6b1bc3289be36ce3e1a144ce57ccefb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54550515"
---
# <a name="performing-culture-insensitive-case-changes"></a>Culture를 구분하지 않는 대/소문자 변경 수행
<xref:System.String.ToUpper%2A?displayProperty=nameWithType>, <xref:System.String.ToLower%2A?displayProperty=nameWithType>, <xref:System.Char.ToUpper%2A?displayProperty=nameWithType> 및 <xref:System.Char.ToLower%2A?displayProperty=nameWithType> 메서드는 매개 변수를 허용하지 않는 오버로드를 제공합니다. 기본적으로 매개 변수가 없는 이러한 오버로드는 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>의 값에 따라 대/소문자 변경을 수행합니다. 이렇게 하면 문화권에 따라 달라질 수 있는 대/소문자 구분 결과가 생성됩니다. 대/소문자 변경에 문화권을 구분할지 또는 문화권을 구분하지 않을지 명확하게 하려면 `culture` 매개 변수를 명시적으로 지정하도록 요구하는 이러한 메서드의 오버로드를 사용해야 합니다. 문화권을 구분하는 대/소문자 변경의 경우 `culture` 매개 변수에 대해 `CultureInfo.CurrentCulture`를 지정합니다. 문화권을 구분하지 않는 대/소문자 변경의 경우 `culture` 매개 변수에 대해 `CultureInfo.InvariantCulture`를 지정합니다.  
  
 흔히 나중에 더 쉽게 조회할 수 있도록 문자열을 표준 케이스(대/소문자)로 변환합니다. 이 방식으로 문자열을 사용하는 경우 대/소문자가 변경된 시간과 조회가 발생하는 시간 사이에 <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType>의 값이 잠재적으로 변경될 수 있으므로 `culture` 매개 변수에 대해 `CultureInfo.InvariantCulture`를 지정해야 합니다.  
  
 보안 결정이 대/소문자 변경 작업을 기반으로 하는 경우 해당 작업이 문화권을 구분하지 않아야 `CultureInfo.CurrentCulture` 값의 영향을 받지 않는 결과를 얻을 수 있습니다. 문화권 구분 문자열 작업으로 인해 어떻게 일관되지 않은 결과가 나타날 수 있는지에 대한 예제를 보려면 [문자열 사용에 대한 모범 사례](../../../docs/standard/base-types/best-practices-strings.md) 문서의 “현재 문화권을 사용하는 문자열 비교” 섹션을 참조하세요.  
  
## <a name="using-the-stringtoupper-and-stringtolower-methods"></a>String.ToUpper 및 String.ToLower 메서드 사용  
 코드를 명확히 하기 위해 항상 `culture` 매개 변수를 명시적으로 지정할 수 있게 하는 `String.ToUpper` 및 `String.ToLower` 메서드의 오버로드를 사용하는 것이 좋습니다. 예를 들어 다음 코드에서는 ID 조회를 수행합니다. `key.ToLower` 작업은 기본적으로 문화권을 구분하지만, 이 동작은 코드 읽기에서 명확하지 않습니다.  
  
### <a name="example"></a>예제  
  
```vb  
Shared Function LookupKey(key As String) As Object  
   Return internalHashtable(key.ToLower())  
End Function  
```  
  
```csharp  
static object LookupKey(string key)   
{  
    return internalHashtable[key.ToLower()];  
}  
```  
  
 `key.ToLower` 작업이 문화권을 구분하지 않도록 설정하려는 경우 앞의 예제를 다음과 같이 변경하여 대/소문자를 변경할 때 `CultureInfo.InvariantCulture`를 명시적으로 사용해야 합니다.  
  
```vb  
Shared Function LookupKey(key As String) As Object  
    Return internalHashtable(key.ToLower(CultureInfo.InvariantCulture))  
End Function  
```  
  
```csharp  
static object LookupKey(string key)   
{  
    return internalHashtable[key.ToLower(CultureInfo.InvariantCulture)];  
}  
```  
  
## <a name="using-the-chartoupper-and-chartolower-methods"></a>Char.ToUpper 및 Char.ToLower 메서드 사용  
 `Char.ToUpper` 및 `Char.ToLower` 메서드는 특징이 `String.ToUpper` 및 `String.ToLower` 메서드와 동일하지만 터키어(터키) 및 아제르바이잔어(라틴 문자, 아제르바이잔) 문화권에만 영향을 줍니다. 이러한 두 문화권만 단일 문자 대/소문자 구분 차이가 있습니다. 이러한 독특한 대/소문자 매핑에 대한 자세한 내용은 <xref:System.String> 클래스 항목의 "대/소문자 구분" 섹션을 참조하십시오. 코드를 명확히 하고 일관성 있는 결과를 얻으려면 항상 `culture` 매개 변수를 명시적으로 지정할 수 있게 하는 이러한 메서드의 오버로드를 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.String.ToUpper%2A?displayProperty=nameWithType>
- <xref:System.String.ToLower%2A?displayProperty=nameWithType>
- <xref:System.Char.ToUpper%2A?displayProperty=nameWithType>
- <xref:System.Char.ToLower%2A?displayProperty=nameWithType>
- [Culture의 영향을 받지 않는 문자열 작업 수행](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)
