---
title: '방법: COM Interop 프로그래밍에서 인덱싱된 속성 사용 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- indexed properties [C#]
- Office programming [C#], indexed properties
- properties [C#], indexed
ms.assetid: 756bfc1e-7c28-4d4d-b114-ac9288c73882
ms.openlocfilehash: f1be14ad7ddb6973cc89f10c1735ba2ebce13f97
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70971656"
---
# <a name="how-to-use-indexed-properties-in-com-interop-programming-c-programming-guide"></a>방법: COM Interop 프로그래밍에서 인덱싱된 속성 사용(C# 프로그래밍 가이드)
*인덱싱된 속성*은 매개 변수가 있는 COM 속성이 C# 프로그래밍에서 사용되는 방식을 개선합니다. 인덱싱된 속성은 Visual C#의 다른 기능(예: [명명된 인수 및 선택적 인수](../classes-and-structs/named-and-optional-arguments.md)), 새 형식([dynamic](../../language-reference/keywords/dynamic.md)), [포함된 형식 정보](../../../standard/assembly/embed-types-visual-studio.md)와 함께 작동하여 Microsoft Office 프로그래밍을 개선합니다.  
  
 이전 버전의 C#에서는 `get` 메서드에 매개 변수가 없고 `set` 메서드에 하나의 값 매개 변수가 있는 경우에만 메서드를 속성으로 액세스할 수 있습니다. 그러나 모든 COM 속성이 이러한 제한을 충족하는 것은 아닙니다. 예를 들어 Excel <xref:Microsoft.Office.Interop.Excel.Range.Range%2A> 속성에는 범위 이름에 대한 매개 변수가 필요한 `get` 접근자가 있습니다. 이전에는 `Range` 속성에 직접 액세스할 수 없었기 때문에 다음 예제와 같이 `get_Range` 메서드를 대신 사용해야 했습니다.  
  
 [!code-csharp[csProgGuideIndexedProperties#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#1)]  
  
 인덱싱된 속성을 사용하면 대신 다음과 같이 작성할 수 있습니다.  
  
 [!code-csharp[csProgGuideIndexedProperties#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#2)]  
  
> [!NOTE]
> 또한 앞의 예제에서는 [선택적 인수](../classes-and-structs/named-and-optional-arguments.md) 기능을 사용하므로 `Type.Missing`을 생략할 수 있습니다.  
  
 마찬가지로, C# 3.0 이하에서 <xref:Microsoft.Office.Interop.Excel.Range> 개체의 `Value` 속성 값을 설정하려면 두 개의 인수가 필요합니다. 하나는 범위 값의 형식을 지정하는 선택적 매개 변수의 인수를 제공합니다. 다른 하나는 `Value` 속성의 값을 제공합니다. 다음 예제에서는 이러한 기법을 보여 줍니다. 둘 다 A1 셀의 값을 `Name`으로 설정합니다.
  
 [!code-csharp[csProgGuideIndexedProperties#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#3)]  
  
 인덱싱된 속성을 사용하면 대신 다음 코드와 같이 작성할 수 있습니다.  
  
 [!code-csharp[csProgGuideIndexedProperties#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#4)]  
  
 인덱싱된 속성을 직접 만들 수는 없습니다. 이 기능은 기존 인덱싱된 속성의 사용만을 지원합니다.  
  
## <a name="example"></a>예  
 다음 코드에서는 전체 예제를 보여 줍니다. Office API에 액세스하는 프로젝트를 설정하는 방법에 대한 자세한 내용은 [방법: Visual C# 기능을 사용하여 Office Interop 개체에 액세스](./how-to-access-office-onterop-objects.md)를 참조하세요.  
  
 [!code-csharp[csProgGuideIndexedProperties#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#5)]  
  
## <a name="see-also"></a>참고 항목

- [명명된 인수 및 선택적 인수](../classes-and-structs/named-and-optional-arguments.md)
- [dynamic](../../language-reference/keywords/dynamic.md)
- [dynamic 형식 사용](../types/using-type-dynamic.md)
- [방법: Office 프로그래밍에서 명명된 인수 및 선택적 인수 사용](../classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)
- [방법: Visual C# 기능을 사용하여 Office Interop 개체에 액세스](./how-to-access-office-onterop-objects.md)
- [연습: Office 프로그래밍](./walkthrough-office-programming.md)
