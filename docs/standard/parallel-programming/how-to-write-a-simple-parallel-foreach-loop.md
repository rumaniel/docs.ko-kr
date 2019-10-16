---
title: Parallel.ForEach를 사용하여 단순 병렬 프로그램 작성
ms.date: 02/14/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- foreach, parallel version
- parallel programming, foreach
ms.assetid: cb5fab92-1c19-499e-ae91-8b7525dd875f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9d54f06c1fc774a2e73b3b99a7d5bb24dd8baf3f
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71835270"
---
# <a name="how-to-write-a-simple-parallelforeach-loop"></a>방법: 간단한 Parallel.ForEach 루프 작성

이 예제는 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 루프를 사용하여 <xref:System.Collections.IEnumerable?displayProperty=nameWithType> 또는 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> 데이터 소스에 대해 데이터 병렬 처리를 사용하는 방법을 보여줍니다.

> [!NOTE]
> 이 문서에서는 람다 식을 사용하여 PLINQ에 대리자를 정의합니다. C# 또는 Visual Basic의 람다 식을 잘 모르는 경우 [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)을 참조하세요.

## <a name="example"></a>예

이 예제에서는 *C:\Users\Public\Pictures\Sample Pictures* 폴더에 여러 .jpg 파일이 있다고 가정하고 *Modified*라는 새 하위 폴더를 만듭니다. 예제를 실행할 때 *Sample Pictures*의 각 .jpg 이미지를 회전시키고 *Modified*에 저장합니다. 필요에 따라 두 경로를 수정할 수 있습니다.

[!code-csharp[TPL_Parallel#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/simpleforeach.cs#03)]
[!code-vb[TPL_Parallel#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/simpleforeach.vb#03)]

<xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 루프는 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 루프처럼 작동합니다. 해당 루프는 원본 컬렉션을 분할하고 시스템 환경에 따라 여러 스레드에서 작업을 예약합니다. 시스템에 프로세서가 많을수록 병렬 메서드가 더 빠르게 실행됩니다. 일부 원본 컬렉션의 경우 원본의 크기 및 수행되는 루프 작업의 종류에 따라 순차 루프가 더 빠를 수 있습니다. 성능에 대한 자세한 내용은 [데이터 및 작업 병렬 처리에서 발생할 수 있는 문제](potential-pitfalls-in-data-and-task-parallelism.md)를 참조하세요.

병렬 루프에 대한 자세한 내용은 [방법: 간단한 Parallel.For 루프 작성](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-for-loop.md)을 참조하세요.

제네릭이 아닌 컬렉션에 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType>를 사용하려면 다음 예제와 같이 <xref:System.Linq.Enumerable.Cast%2A?displayProperty=nameWithType> 확장 메서드를 사용하여 컬렉션을 일반 컬렉션으로 변환할 수 있습니다.

[!code-csharp[TPL_Parallel#07](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/nongeneric.cs#07)]
[!code-vb[TPL_Parallel#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/nongeneric.vb#07)]

병렬 LINQ(PLINQ)를 사용하여 <xref:System.Collections.Generic.IEnumerable%601> 데이터 소스의 처리를 병렬 처리할 수도 있습니다. PLINQ를 통해 선언 쿼리 구문을 사용하여 루프 동작을 표현할 수 있습니다. 자세한 내용은 [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)를 참조하세요.

## <a name="compile-and-run-the-code"></a>코드 컴파일 및 실행

.NET Framework의 콘솔 애플리케이션 또는 .NET Core의 콘솔 애플리케이션으로 코드를 컴파일할 수 있습니다.

Visual Studio에는 Windows Desktop 및 .NET Core용 Visual Basic 및 C# 콘솔 애플리케이션 템플릿이 있습니다.

명령줄에서 .NET Core 및 CLI 도구 중 하나를 사용할 수 있습니다(예: `dotnet new console` 또는 `dotnet new console -lang vb`). 또는 .NET Framework 애플리케이션에서 파일을 만들고 명령줄 컴파일러를 사용할 수 있습니다.

.NET Core 프로젝트에서 **System.Drawing.Common** NuGet 패키지를 참조해야 합니다. Visual Studio에서 NuGet 패키지 관리자를 사용하여 패키지를 설치합니다. 혹은 \*.csproj 또는 \*.vbproj 파일에서 패키지에 대한 참조를 추가할 수 있습니다.
 
```xml
<ItemGroup>
     <PackageReference Include="System.Drawing.Common" Version="4.5.1" />
</ItemGroup>
```

명령줄의 .NET Core 콘솔 애플리케이션을 실행하려면 애플리케이션이 포함된 폴더에서 `dotnet run`을 사용하세요.

Visual Studio에서 콘솔 애플리케이션을 실행하려면 **F5** 키를 누르세요.

## <a name="see-also"></a>참고 항목

- [데이터 병렬 처리](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)
- [병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)
- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
