---
title: 메서드에서 쿼리 반환
description: 쿼리를 반환하는 방법.
ms.date: 11/30/2016
ms.assetid: db220f79-c35b-41f2-886c-cd068672d42d
ms.openlocfilehash: fe2192a3edb683d7284ffae3b66cb9f70e8854b1
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54519101"
---
# <a name="how-to-return-a-query-from-a-method-c-programming-guide"></a>방법: 메서드에서 쿼리 반환(C# 프로그래밍 가이드)
이 예제는 메서드에서 반환 값 및 `out` 매개 변수로서 쿼리를 반환하는 방법을 보여 줍니다.  
  
 쿼리 개체는 구성 가능하므로 메서드에서 쿼리를 반환할 수 있습니다. 쿼리를 나타내는 개체는 결과 컬렉션을 저장하지 않고, 대신 필요할 때 결과를 생성하는 단계를 저장합니다. 메서드에서 쿼리 개체를 반환하는 경우 메서드를 추가로 작성하거나 수정할 수 있다는 이점이 있습니다. 따라서 쿼리를 반환하는 메서드의 반환 값 또는 `out` 매개 변수도 해당 형식을 가지고 있어야 합니다. 메서드가 쿼리를 구체적인 <xref:System.Collections.Generic.List%601> 또는 <xref:System.Array> 형식으로 구체화하는 경우 쿼리 자체가 아니라 쿼리 결과를 반환하는 것으로 간주됩니다. 메서드에서 반환되는 쿼리 변수는 여전히 구성 또는 수정 가능합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서 첫 번째 메서드는 쿼리를 반환 값으로 반환하고 두 번째 메서드는 쿼리를 `out` 매개 변수로 반환합니다. 두 경우 모두 쿼리 결과가 아니라 쿼리가 반환됩니다.  
  
 [!code-csharp[csProgGuideLINQ#80](~/samples/snippets/csharp/concepts/linq/how-to-return-a-query-from-a-method_1.cs)]  

## <a name="see-also"></a>참고 항목

- [LINQ(Language-Integrated Query)](index.md)
