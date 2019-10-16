---
title: '방법: 자식 작업이 부모 작업에 연결되지 않도록 방지'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, preventing attachments
ms.assetid: c0fb85d4-9e80-4905-9f65-29acc54201c4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 55b9c6c7175d8c7c33d8bfa03330c8e4b8816531
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592017"
---
# <a name="how-to-prevent-a-child-task-from-attaching-to-its-parent"></a>방법: 자식 작업이 부모 작업에 연결되지 않도록 방지
이 문서에서는 자식 작업이 부모 작업에 연결하는 것을 방지하는 방법을 보여 줍니다. 자식 작업이 부모에 연결하는 것을 방지하는 방법은 타사가 작성하고 마찬가지로 작업을 사용하는 구성 요소를 호출하는 경우 유용합니다. 예를 들어 <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent?displayProperty=nameWithType> 옵션을 사용하여 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 개체를 만드는 타사 구성 요소는 오래 실행되는 경우 코드에서 문제를 유발하거나 처리되지 않은 예외를 throw할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 기본 옵션의 효과와 자식 작업이 부모에 연결하는 것을 방지하는 효과를 비교합니다. 이 예제에서는 마찬가지로 <xref:System.Threading.Tasks.Task> 개체를 사용하는 타사 라이브러리를 호출하는 <xref:System.Threading.Tasks.Task> 개체를 만듭니다. 타사 라이브러리는 <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent> 옵션을 사용하여 <xref:System.Threading.Tasks.Task> 개체를 만듭니다. 애플리케이션은 <xref:System.Threading.Tasks.TaskCreationOptions.DenyChildAttach?displayProperty=nameWithType> 옵션을 사용하여 부모 작업을 만듭니다. 이 옵션은 자식 작업에서 <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent> 지정을 제거하도록 런타임에 지시합니다.  
  
 [!code-csharp[TPL_DenyChildAttach#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_denychildattach/cs/denychildattach.cs#1)]
 [!code-vb[TPL_DenyChildAttach#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_denychildattach/vb/denychildattach.vb#1)]  
  
 부모 작업은 자식 작업이 모두 완료될 때까지 완료되지 않기 때문에 오래 실행되는 자식 작업은 전체적인 애플리케이션의 성능을 저하시킬 수 있습니다. 이 예제에서 애플리케이션이 기본 옵션을 사용하여 부모 작업을 만들 때 자식 작업은 부모 작업이 완료되기 전에 완료되어야 합니다. 애플리케이션에서 <xref:System.Threading.Tasks.TaskCreationOptions.DenyChildAttach?displayProperty=nameWithType> 옵션을 사용하는 경우 자식은 부모에 연결되지 않습니다. 따라서 애플리케이션은 부모 작업이 완료된 후와 자식 작업이 완료되기를 기다려야 하기 전에 추가 작업을 수행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [작업 기반 비동기 프로그래밍](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)
