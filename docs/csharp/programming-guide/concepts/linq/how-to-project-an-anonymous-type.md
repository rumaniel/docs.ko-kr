---
title: '방법: 익명 형식 프로젝션(C#)'
ms.date: 07/20/2015
ms.assetid: 5cb9be13-5ac4-4373-a034-b3520a5b2dec
ms.openlocfilehash: 3ed14ae6e7bc4b84ae9dc416b76e37443b831c73
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253515"
---
# <a name="how-to-project-an-anonymous-type-c"></a>방법: 익명 형식 프로젝션(C#)
새 형식을 잠깐 동안만 사용할 경우에도 필요에 따라 쿼리를 해당 형식으로 프로젝션하려고 할 수 있습니다. 프로젝션에서만 사용하기 위해 새 형식을 만드는 것은 비효율적입니다. 이 경우 더 효율적인 방법은 익명 형식을 프로젝션하는 것입니다. 익명 형식을 사용하면 클래스를 정의한 다음 클래스의 이름을 지정하지 않고도 클래스의 개체를 선언하고 초기화할 수 있습니다.  
  
 무명 형식은 *튜플*이라는 수학적 개념의 C# 구현입니다. 수학 용어인 튜플은 단일(single), 이중(double), 3중(triple), 4중(quadruple), 5중(quintuple), n중(n-tuple)에서 유래되었습니다. 튜플은 각각 특정 형식으로 되어 있는 개체의 유한 시퀀스를 의미합니다. 이를 이름/값 쌍의 목록이라고 하기도 합니다. 예를 들어 [샘플 XML 파일: 일반적인 구매 주문(LINQ to XML)](./sample-xml-file-typical-purchase-order-linq-to-xml-1.md) XML 문서에 있는 주소의 내용은 다음과 같이 표현될 수 있습니다.  
  
```text  
Name: Ellen Adams  
Street: 123 Maple Street  
City: Mill Valley  
State: CA  
Zip: 90952  
Country: USA  
```  
  
 익명 형식의 인스턴스를 만드는 경우 n번째 튜플을 만드는 것으로 생각하면 편리합니다. `select` 절에서 튜플을 만드는 쿼리를 작성하면 쿼리에서 튜플의 `IEnumerable`을 반환합니다.  
  
## <a name="example"></a>예  
 이 예제에서 `select` 절은 익명 형식을 프로젝션한 다음 `var`을 사용하여 `IEnumerable` 개체를 만듭니다. `foreach` 루프에서 반복 변수는 쿼리 식에서 만든 익명 형식의 인스턴스가 됩니다.  
  
 이 예제에서는 XML 문서로을 사용합니다. [샘플 XML 파일: Customers 및 Orders(LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md).  
  
```csharp  
XElement custOrd = XElement.Load("CustomersOrders.xml");  
var custList =  
    from el in custOrd.Element("Customers").Elements("Customer")  
    select new {  
        CustomerID = (string)el.Attribute("CustomerID"),  
        CompanyName = (string)el.Element("CompanyName"),  
        ContactName = (string)el.Element("ContactName")  
    };  
foreach (var cust in custList)  
    Console.WriteLine("{0}:{1}:{2}", cust.CustomerID, cust.CompanyName, cust.ContactName);  
```  
  
 이 코드의 결과는 다음과 같습니다.  
  
```output  
GREAL:Great Lakes Food Market:Howard Snyder  
HUNGC:Hungry Coyote Import Store:Yoshi Latimer  
LAZYK:Lazy K Kountry Store:John Steel  
LETSS:Let's Stop N Shop:Jaime Yorres  
```  
  