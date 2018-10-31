---
title: '방법: 동시 작업을 배리어와 동기화'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Barrier, how to use
ms.assetid: e1a253ff-e0fb-4df8-95ff-d01a90d4cb19
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 16dc60fa9cd8782efbe1b6028413138b5991839e
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48025350"
---
# <a name="how-to-synchronize-concurrent-operations-with-a-barrier"></a>방법: 동시 작업을 배리어와 동기화
다음 예제는 <xref:System.Threading.Barrier>와 동시 작업을 동기화하는 방법을 보여줍니다.  
  
## <a name="example"></a>예  
 다음 프로그램의 목적은 무작위 알고리즘을 사용하여 단어를 다시 섞어서 동일한 단계에서 두 스레드가 솔루션의 절반을 서로 찾는 데 필요한 반복(또는 단계) 수를 계산하는 것입니다. 각 스레드가 해당 단어를 섞은 후 장벽 사후 단계 작업은 두 결과를 비교하여 전체 문장이 올바른 단어 순서로 렌더링되었는지 확인합니다.  
  
 [!code-csharp[CDS_Barrier#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_barrier/cs/barrier.cs#01)]
 [!code-vb[CDS_Barrier#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_barrier/vb/barrier_vb.vb#01)]  
  
 <xref:System.Threading.Barrier>는 모든 작업이 장벽에 도달할 때까지 병렬 작업의 개별 작업이 계속되는 것을 방지하는 개체입니다. 이 개체는 병렬 작업이 단계에서 발생하는 경우에 유용하며, 각 단계에서는 작업 간 동기화가 필요합니다. 이 예제에서, 작업의 단계는 두 개입니다. 첫 번째 단계에서 각 작업은 데이터를 사용하여 버퍼의 섹션을 채웁니다. 각 작업이 해당 섹션 채우기를 완료하면 작업은 장벽에 계속할 준비가 되었음을 알리는 신호를 보낸 후 대기합니다. 모든 작업이 장벽에 신호를 보내면 장벽이 잠금 해제되고 두 번째 단계가 시작됩니다. 두 번째 단계에서는 각 작업이 이 지점까지 생성된 모든 데이터에 액세스해야 하므로 장벽이 필요합니다. 장벽이 없으면 완료할 첫 번째 작업이 다른 작업에 의해 아직 채워지지 않은 버퍼에서 읽으려고 할 수 있습니다. 이런 방식으로 개수와 관계없이 모든 단계를 동기화할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [병렬 프로그래밍을 위한 데이터 구조](../../../docs/standard/parallel-programming/data-structures-for-parallel-programming.md)
