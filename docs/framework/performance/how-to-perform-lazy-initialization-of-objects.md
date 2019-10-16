---
title: '방법: 개체의 초기화 지연 수행'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- lazy initialization in .NET, how to perform
ms.assetid: 8cd68620-dcc3-4f20-8835-c728a6820e71
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6fba47c0ff6425a375715dcd4c08d62e0f7f598c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046473"
---
# <a name="how-to-perform-lazy-initialization-of-objects"></a>방법: 개체의 초기화 지연 수행
<xref:System.Lazy%601?displayProperty=nameWithType> 클래스는 개체의 인스턴스화 및 초기화 지연을 수행하는 작업을 간소화합니다. 지연 방식으로 개체를 초기화하면 개체가 필요하지 않을 경우 개체를 전혀 만들지 않아도 되고, 필요한 경우에도 개체에 처음 액세스할 때까지 초기화를 연기할 수 있습니다. 자세한 내용은 [초기화 지연](lazy-initialization.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Lazy%601>로 값을 초기화하는 방법을 보여 줍니다. `someCondition` 변수를 true 또는 false로 설정하는 일부 기타 코드에 따라 지연 변수가 필요하지 않을 수 있다고 가정합니다.  
  
```vb  
Dim someCondition As Boolean = False  
  
Sub Main()  
    'Initializing a value with a big computation, computed in parallel  
    Dim _data As Lazy(Of Integer) = New Lazy(Of Integer)(Function()  
                                                             Dim result =  
                                                                 ParallelEnumerable.Range(0, 1000).  
                                                                 Aggregate(Function(x, y)  
                                                                               Return x + y  
                                                                           End Function)  
                                                             Return result  
                                                         End Function)  
  
    '  do work that may or may not set someCondition to True  
    ' ...  
    '  Initialize the data only if needed  
    If someCondition = True Then  
  
        If (_data.Value > 100) Then  
  
            Console.WriteLine("Good data")  
        End If  
    End If  
End Sub  
```  
  
```csharp  
  static bool someCondition = false;    
  //Initializing a value with a big computation, computed in parallel  
  Lazy<int> _data = new Lazy<int>(delegate  
  {  
      return ParallelEnumerable.Range(0, 1000).  
          Select(i => Compute(i)).Aggregate((x,y) => x + y);  
  }, LazyExecutionMode.EnsureSingleThreadSafeExecution);  
  
  // Do some work that may or may not set someCondition to true.  
  //  ...  
  // Initialize the data only if necessary  
  if (someCondition)  
  {  
    if (_data.Value > 100)  
      {  
          Console.WriteLine("Good data");  
      }  
  }  
```  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Threading.ThreadLocal%601?displayProperty=nameWithType> 클래스를 사용하여 현재 스레드의 현재 개체 인스턴스에만 표시되는 형식을 초기화하는 방법을 보여 줍니다.  
  
 [!code-csharp[CDS#13](../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/cds2.cs#13)]
 [!code-vb[CDS#13](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/lazyhowto.vb#13)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Threading.LazyInitializer?displayProperty=nameWithType>
- [초기화 지연](lazy-initialization.md)
