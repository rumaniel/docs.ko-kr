---
title: PLINQ(병렬 LINQ)
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- PLINQ, overview
ms.assetid: 3d4d0cd3-bde4-490b-99e7-f4e41be96455
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1fe7edffd53023cba6dac1454e620d6e0d7e9513
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48582270"
---
# <a name="parallel-linq-plinq"></a>PLINQ(병렬 LINQ)
PLINQ(병렬 LINQ)는 LINQ to Objects의 병렬 구현입니다. PLINQ는 LINQ 표준 쿼리 연산자의 전체 집합을 <xref:System.Linq> 네임스페이스의 확장 메서드로 구현하고, 병렬 작업을 위한 추가 연산자를 포함합니다. PLINQ는 LINQ의 간편성과 가독성을 병렬 프로그래밍의 기능과 결합합니다. 작업 병렬 라이브러리를 대상으로 하는 코드와 마찬가지로 PLINQ 쿼리는 호스트 컴퓨터의 기능에 따라 동시성 수준 규모를 조정합니다.  
  
 대부분의 시나리오에서 PLINQ는 호스트 컴퓨터에서 사용 가능한 모든 코어를 보다 효율적으로 사용하여 LINQ to Objects 쿼리 속도를 상당히 높일 수 있습니다. 이렇게 향상된 성능으로 고성능 컴퓨팅 기능을 데스크탑에 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [PLINQ 소개](../../../docs/standard/parallel-programming/introduction-to-plinq.md)  
  
 [PLINQ의 속도 향상 이해](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)  
  
 [PLINQ에서 순서 유지](../../../docs/standard/parallel-programming/order-preservation-in-plinq.md)  
  
 [PLINQ의 병합 옵션](../../../docs/standard/parallel-programming/merge-options-in-plinq.md)  
  
 [방법: 간단한 PLINQ 쿼리 만들기 및 실행](../../../docs/standard/parallel-programming/how-to-create-and-execute-a-simple-plinq-query.md)  
  
 [방법: PLINQ 쿼리의 순서 제어](../../../docs/standard/parallel-programming/how-to-control-ordering-in-a-plinq-query.md)  
  
 [방법: 병렬 및 순차적 LINQ 쿼리 결합](../../../docs/standard/parallel-programming/how-to-combine-parallel-and-sequential-linq-queries.md)  
  
 [방법: PLINQ 쿼리의 예외 처리](../../../docs/standard/parallel-programming/how-to-handle-exceptions-in-a-plinq-query.md)  
  
 [방법: PLINQ 쿼리 취소](../../../docs/standard/parallel-programming/how-to-cancel-a-plinq-query.md)  
  
 [방법: 사용자 지정 PLINQ 집계 함수 작성](../../../docs/standard/parallel-programming/how-to-write-a-custom-plinq-aggregate-function.md)  
  
 [방법: PLINQ에 실행 모드 지정](../../../docs/standard/parallel-programming/how-to-specify-the-execution-mode-in-plinq.md)  
  
 [방법: PLINQ에서 병합 옵션 지정](../../../docs/standard/parallel-programming/how-to-specify-merge-options-in-plinq.md)  
  
 [방법: PLINQ를 사용하여 파일 디렉터리 열거](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-plinq.md)  
  
 [방법: PLINQ 쿼리 성능 측정](../../../docs/standard/parallel-programming/how-to-measure-plinq-query-performance.md)  
  
 [PLINQ 데이터 샘플](../../../docs/standard/parallel-programming/plinq-data-sample.md)  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Linq.ParallelEnumerable>  
- [병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)  
- [LINQ(Language-Integrated Query)](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)
