---
title: '방법: 병렬 클래스를 사용하여 파일 디렉터리 반복'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel loops, how to iterate directories
ms.assetid: 555e9f48-f53d-4774-9bcf-3e965c732ec5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c1ec270159430434adc074f1fa6ca92ec3c4a455
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2019
ms.locfileid: "56965269"
---
# <a name="how-to-iterate-file-directories-with-the-parallel-class"></a>방법: 병렬 클래스를 사용하여 파일 디렉터리 반복
대부분의 경우 파일 반복은 쉽게 병렬 처리할 수 있는 작업입니다. 항목 [방법: PLINQ를 사용하여 파일 디렉터리 반복](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-plinq.md)은 많은 시나리오에서 이 작업을 수행하는 가장 쉬운 방법을 보여줍니다. 그러나 코드가 파일 시스템에 액세스할 때 발생할 수 있는 많은 예외 형식을 처리해야 할 경우 복잡해질 수 있습니다. 다음 예제는 문제에 대한 하나의 접근 방법을 보여줍니다. 이 방법은 스택 기반 반복을 사용하여 지정된 디렉터리에서 모든 파일과 폴더를 트래버스하고 코드에서 다양한 예외를 catch하여 처리할 수 있습니다. 물론 예외를 처리하는 방법은 사용자가 결정합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 디렉터리를 순차적으로 반복하지만 파일을 병렬로 처리합니다. 이 방법은 파일 대 디렉터리 비율이 큰 경우 가장 적합합니다. 또한 디렉터리 반복을 병렬 처리하고 각 파일에 순차적으로 액세스할 수 있습니다. 많은 프로세서를 사용하는 컴퓨터를 특별히 대상으로 지정하지 않는 한 두 루프를 모두 병렬 처리하는 것은 효율적이지 않을 수 있습니다. 그러나 모든 경우처럼 애플리케이션을 철저히 테스트하여 가장 적합한 방법을 확인해야 합니다.  
  
 [!code-csharp[TPL_Parallel#08](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallel_file.cs#08)]
 [!code-vb[TPL_Parallel#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/fileiteration08.vb#08)]  
  
 이 예제에서 파일 I/O는 동기적으로 수행됩니다. 큰 파일이나 느린 네트워크 연결을 처리할 경우에는 파일에 비동기적으로 액세스하는 것이 좋을 수 있습니다. 비동기 I/O 기술을 병렬 반복과 결합할 수 있습니다. 자세한 내용은 [TPL 및 일반적인 .NET 비동기 프로그래밍](../../../docs/standard/parallel-programming/tpl-and-traditional-async-programming.md)을 참조하세요.  
  
 이 예제에서는 지역 `fileCount` 변수를 사용하여 처리된 총 파일 수를 유지합니다. 이 변수가 여러 작업에서 동시에 액세스될 수 있기 때문에 이 변수에 대한 액세스는 <xref:System.Threading.Interlocked.Add%2A?displayProperty=nameWithType> 메서드를 호출하여 동기화됩니다.  
  
 기본 스레드에서 예외가 throw될 경우 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 메서드를 통해 시작되는 스레드는 계속 실행될 수 있습니다. 이러한 스레드를 중지하려면 예외 처리기에서 부울 변수를 설정하고 병렬 루프의 각 반복에서 해당 값을 확인합니다. 값이 예외가 throw되었음을 나타내는 경우 <xref:System.Threading.Tasks.ParallelLoopState> 변수를 사용하여 루프에서 중지하거나 중단합니다. 자세한 내용은 [방법: Parallel.For 루프 중지 또는 중단](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd460721(v=vs.100))을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [데이터 병렬 처리](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)
