---
title: '방법: Parallel.Invoke를 사용하여 병렬 작업 실행'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- task parallelism in .NET
- parallel programming, task parallelism
ms.assetid: 6b3ecd79-dec9-4ce1-abf4-62e5392a59c6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c0192e12c86b21eb126293bbd220e093b334768b
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48837065"
---
# <a name="how-to-use-parallelinvoke-to-execute-parallel-operations"></a>방법: Parallel.Invoke를 사용하여 병렬 작업 실행

이 예제에서는 작업 병렬 라이브러리의 <xref:System.Threading.Tasks.Parallel.Invoke%2A>을 사용하여 작업을 병렬 처리하는 방법을 보여 줍니다. 세 가지 작업이 공유 데이터 소스에 대해 수행됩니다. 소스를 수정하는 작업이 없기 때문에 간단하게 병렬로 실행할 수 있습니다.

> [!NOTE]
> 이 문서에서는 람다 식을 사용하여 TPL에 대리자를 정의합니다. C# 또는 Visual Basic의 람다 식을 잘 모르는 경우 [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)을 참조하세요.

## <a name="example"></a>예

[!code-csharp[TPL_Parallel#06](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallelinvoke.cs#06)]
[!code-vb[TPL_Parallel#06](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/parallelinvoke.vb#06)]

<xref:System.Threading.Tasks.Parallel.Invoke%2A>에서 동시에 실행하려는 작업을 표시하기만 하면 런타임에서 호스트 컴퓨터의 코드 수에 맞게 자동으로 크기 조정을 포함하여 모든 스레드 예약 세부 정보를 처리합니다.

이 예제에서는 데이터가 아니라 작업을 병렬 처리합니다. 대체 방법으로 PLINQ를 사용하여 LINQ 쿼리를 병렬 처리하고 쿼리를 순차적으로 실행할 수 있습니다. 또는 PLINQ를 사용하여 데이터를 병렬 처리할 수 있습니다. 다른 옵션은 쿼리와 작업을 둘 다 병렬 처리하는 것입니다. 결과로 생성된 오버헤드로 인해 프로세서가 비교적 적은 호스트 컴퓨터에서는 성능이 저하될 수도 있지만 프로세서가 많은 컴퓨터에서는 훨씬 효율적으로 크기가 조정됩니다.

## <a name="compile-the-code"></a>코드 컴파일

전체 예제를 복사하여 Microsoft Visual Studio 프로젝트에 붙여넣고 **F5** 키를 누릅니다.

## <a name="see-also"></a>참고 항목

- [병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)
- [방법: 작업 및 해당 자식 취소](../../../docs/standard/parallel-programming/how-to-cancel-a-task-and-its-children.md)
- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
