---
title: '방법: PLINQ를 사용하여 파일 디렉터리 반복'
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- PLINQ queries, how to iterate directories
ms.assetid: 354e8ce3-35c4-431c-99ca-7661d1f3901b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5da70cdca16c83b33e525aea588c02c696702ac7
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929149"
---
# <a name="how-to-iterate-file-directories-with-plinq"></a>방법: PLINQ를 사용하여 파일 디렉터리 반복
이 예제는 파일 디렉터리에서 작업을 병렬 처리하는 두 가지 간단한 방법을 보여줍니다. 첫 번째 쿼리는 <xref:System.IO.Directory.GetFiles%2A> 메서드를 사용하여 디렉터리 및 모든 하위 디렉터리에서 파일 이름 배열을 채웁니다. 이 메서드는 전체 배열이 채워질 때까지 반환되지 않으므로 작업 시작 시 지연이 발생할 수 있습니다. 그러나 배열이 채워진 후 PLINQ는 메서드를 매우 빠르게 병렬 처리할 수 있습니다.  
  
 두 번째 쿼리는 결과를 즉시 반환하기 시작하는 정적 <xref:System.IO.Directory.EnumerateDirectories%2A> 및 <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> 메서드를 사용합니다. 첫 번째 쿼리에 비교되는 처리 시간은 많은 요소에 따라 다를 수 있지만 큰 디렉터리 트리를 반복 중일 경우 이 방법이 더 빠를 수 있습니다.  
  
> [!WARNING]
> 이 예제는 사용법을 보여 주기 위해 제공되며 동일한 순차적 LINQ to Objects 쿼리보다 빠르게 실행되지 않을 수 있습니다. 속도 향상에 대한 자세한 내용은 [PLINQ의 속도 향상 이해](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)를 참조하세요.  
  
## <a name="example"></a>예  
 다음 예제는 트리의 모든 디렉터리에 액세스할 수 있고, 파일 크기가 그다지 크지 않고, 액세스 시간이 상당하지 않을 경우 간단한 시나리오에서 파일 디렉터리를 반복하는 방법을 보여줍니다. 이 방법에는 파일 이름 배열이 생성되는 동안 시작 시에 대기 시간이 포함됩니다.  
  
 [!code-csharp[PLINQ#33](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqfileiteration.cs#33)]  
  
## <a name="example"></a>예  
 다음 예제는 트리의 모든 디렉터리에 액세스할 수 있고, 파일 크기가 그다지 크지 않고, 액세스 시간이 상당하지 않을 경우 간단한 시나리오에서 파일 디렉터리를 반복하는 방법을 보여줍니다. 이 방법은 이전 예제보다 빠르게 결과를 생성하기 시작합니다.  
  
 [!code-csharp[PLINQ#34](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqfileiteration.cs#34)]  
  
 <xref:System.IO.Directory.GetFiles%2A>를 사용할 경우 트리의 모든 디렉터리에 충분한 권한이 있는지 확인하세요. 그렇지 않으면 예외가 throw되고 결과가 반환되지 않습니다. PLINQ 쿼리에서 <xref:System.IO.Directory.EnumerateDirectories%2A>를 사용할 경우 반복을 계속할 수 있는 정상적인 방법으로 I/O 예외를 처리하는 것이 어렵습니다. 코드에서 I/O 또는 인증되지 않은 액세스 예외를 처리해야 하는 경우에는 [방법: 병렬 클래스를 사용하여 파일 디렉터리 반복](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-the-parallel-class.md)에 설명된 방법을 고려해야 합니다.  
  
 예를 들어 I/O 지연이 네트워크를 통한 파일 I/O와 관련된 문제인 경우 [TPL 및 일반적인 .NET Framework 비동기 프로그래밍](../../../docs/standard/parallel-programming/tpl-and-traditional-async-programming.md) 및 이 [블로그 게시물](https://devblogs.microsoft.com/pfxteam/parallel-extensions-and-io/)에 설명된 비동기 I/O 기술 중 하나를 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목

- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
