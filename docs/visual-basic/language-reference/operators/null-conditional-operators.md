---
title: Null 조건부 연산자 (Visual Basic)
ms.date: 10/19/2018
helpviewer_keywords:
- null-conditional operators [Visual Basic]
- ?. operator [Visual Basic]
- ?[] operator [C#]
- ?[] operator [Visual Basic]
ms.openlocfilehash: 4815fe7ad337634cfb56127fbd24a47a37fdd74b
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65062936"
---
# <a name="-and--null-conditional-operators-visual-basic"></a>?. 및? null 조건부 연산자 () (Visual Basic)

Null에 대 한 왼쪽 피연산자의 값을 테스트 (`Nothing`)는 멤버 액세스를 수행 하기 전에 (`?.`) 또는 인덱스 (`?()`) 작업; 반환 `Nothing` 왼쪽 피연산자가 `Nothing`입니다. 일반적으로 값 형식을 반환 하는 식에서 null 조건부 연산자를 반환 하는 <xref:System.Nullable%601>합니다.

이러한 연산자는 데이터 구조에서 아래로 내려가는 경우에 특히 null 검사를 처리 하는 작은 코드를 작성할 수 있습니다. 예를 들어:

```vb
' Nothing if customers is Nothing  
Dim length As Integer? = customers?.Length  

' Nothing if customers is Nothing
Dim first As Customer = customers?(0)

' Nothing if customers, the first customer, or Orders is Nothing
Dim count As Integer? = customers?(0)?.Orders?.Count()   
```

반면 null 조건부 연산자 없이 이러한 식의 첫 번째에 대 한 대체 코드는 다음과 같습니다.

```vb
Dim length As Integer
If customers IsNot Nothing Then
   length = customers.Length
End If
```

Null 일 수를 해당 개체에 대해 부울 멤버의 값을 기반으로 하는 개체에 대 한 작업을 수행 해야 하는 경우에 따라 (부울 속성을 같은 `IsAllowedFreeShipping` 다음 예제의):

```vb
  Dim customer = FindCustomerByID(123) 'customer will be Nothing if not found.
  
  If customer IsNot Nothing AndAlso customer.IsAllowedFreeShipping Then
   ApplyFreeShippingToOrders(customer)
  End If
```

코드 단축 하 고 수동으로 다음과 같이 null 조건부 연산자를 사용 하 여 null 검사를 방지할 수 있습니다.

```vb
 Dim customer = FindCustomerByID(123) 'customer will be Nothing if not found.
 
 If customer?.IsAllowedFreeShipping Then ApplyFreeShippingToOrders(customer)
```

Null 조건부 연산자는 단락 연산자입니다.  조건부 멤버 액세스 및 인덱스 작업의 체인에 하나의 작업에서 반환 하는 경우 `Nothing`, 나머지 체인의 실행이 중지 됩니다.  다음 예에서 `C(E)` 하는 경우 평가 되지 않습니다 `A`를 `B`, 또는 `C` 로 `Nothing`합니다.

```vb
A?.B?.C?(E);
```

Null 조건부 멤버 액세스에 대 한 또 다른 용도 훨씬 더 적은 코드를 사용 하 여 스레드로부터 안전한 방식으로 대리자를 호출 하는 것입니다.  다음 예제에서는 두 가지 형식 정의 `NewsBroadcaster` 및 `NewsReceiver`합니다. 뉴스 항목에서 수신자에 게 전송 되는 `NewsBroadcaster.SendNews` 위임 합니다.

```vb
Public Module NewsBroadcaster
   Dim SendNews As Action(Of String) 

   Public Sub Main()
      Dim rec As New NewsReceiver()
      Dim rec2 As New NewsReceiver()
      SendNews?.Invoke("Just in: A newsworthy item...")
   End Sub

   Public Sub Register(client As Action(Of String))
      SendNews = SendNews.Combine({SendNews, client})
   End Sub
End Module

Public Class NewsReceiver
   Public Sub New()
      NewsBroadcaster.Register(AddressOf Me.DisplayNews)
   End Sub

   Public Sub DisplayNews(newsItem As String)
      Console.WriteLine(newsItem)
   End Sub
End Class
```

요소가 없을 경우는 `SendNews` 호출 목록에는 `SendNews` throw 대리자는 <xref:System.NullReferenceException>합니다. Null 조건부 연산자를 코드 대리자 호출 목록 없음을 확인 했습니다 다음과 같은 `Nothing`:

```vb  
SendNews = SendNews.Combine({SendNews, client})  
If SendNews IsNot Nothing Then 
   SendNews("Just in...")
End If
```

새로운 방식은 훨씬 더 간단합니다.  

```vb
SendNews = SendNews.Combine({SendNews, client})  
SendNews?.Invoke("Just in...")
```

새로운 방식은 컴파일러가 `SendNews`를 한 번만 평가하는 코드를 생성하고 결과를 임시 변수에 유지하기 때문에 스레드로부터 안전합니다. null 조건부 대리자 호출 구문 `SendNews?(String)`가 없기 때문에 `Invoke` 메서드를 명시적으로 호출해야 합니다.  

## <a name="see-also"></a>참고자료

- [연산자 (Visual Basic)](index.md)
- [Visual Basic 프로그래밍 가이드](../../../visual-basic/programming-guide/index.md)
- [Visual Basic 언어 참조](../../../visual-basic/language-reference/index.md)
