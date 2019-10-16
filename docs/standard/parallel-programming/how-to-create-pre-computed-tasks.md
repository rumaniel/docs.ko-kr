---
title: '방법: 미리 계산된 작업 만들기'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, creating pre-computed
ms.assetid: a73eafa2-1f49-4106-a19e-997186029b58
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5e68465b6fae39089600457414e7f2a2328f725b
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65593127"
---
# <a name="how-to-create-pre-computed-tasks"></a>방법: 미리 계산된 작업 만들기
이 문서에서는 <xref:System.Threading.Tasks.Task.FromResult%2A?displayProperty=nameWithType> 메서드를 사용하여 캐시에 저장된 비동기 다운로드 작업의 결과를 검색하는 방법을 설명합니다. <xref:System.Threading.Tasks.Task.FromResult%2A> 메서드는 제공된 값을 <xref:System.Threading.Tasks.Task%601> 속성으로 포함하는 완료된 <xref:System.Threading.Tasks.Task%601.Result%2A> 개체를 반환합니다. 이 메서드는 <xref:System.Threading.Tasks.Task%601> 개체가 반환되는 비동기 작업을 수행하고 해당 <xref:System.Threading.Tasks.Task%601> 개체의 결과가 계산되어 있을 때 유용합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 웹에서 문자열을 다운로드합니다. 이 예제에서는 `DownloadStringAsync` 메서드를 정의합니다. 이 메서드는 웹에서 문자열을 비동기적으로 다운로드합니다. 또한 이 예제에서는 <xref:System.Collections.Concurrent.ConcurrentDictionary%602>개체를 사용하여 이전 작업의 결과를 캐시합니다. 입력 주소가 이 캐시에 저장된 경우 `DownloadStringAsync`는 <xref:System.Threading.Tasks.Task.FromResult%2A> 메서드를 사용하여 해당 주소의 콘텐츠를 포함하는 <xref:System.Threading.Tasks.Task%601> 개체를 생성합니다. 그렇지 않은 경우에는 `DownloadStringAsync`가 웹에서 파일을 다운로드하고 결과를 캐시에 추가합니다.  
  
 [!code-csharp[TPL_CachedDownloads#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_cacheddownloads/cs/cacheddownloads.cs#1)]
 [!code-vb[TPL_CachedDownloads#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_cacheddownloads/vb/cacheddownloads.vb#1)]  
  
 이 예제에서는 여러 문자열을 두 번 다운로드하는 데 필요한 시간을 계산합니다. 결과가 캐시에 저장되기 때문에 다운로드 작업의 두 번째 집합은 첫 번째 집합보다 시간이 덜 걸려야 합니다. <xref:System.Threading.Tasks.Task.FromResult%2A> 메서드는 `DownloadStringAsync` 메서드가 이러한 미리 계산된 결과를 포함하는 <xref:System.Threading.Tasks.Task%601> 개체를 만들 수 있도록 합니다.  
  
## <a name="see-also"></a>참고 항목

- [작업 기반 비동기 프로그래밍](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)
