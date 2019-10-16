---
title: '방법: 리플렉션 전용 컨텍스트에 어셈블리 로드'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- reflection, reflection-only loader context
- assemblies [.NET Framework], loading for reflection
- attributes [.NET Framework], retrieving
- assemblies [.NET Framework], reflection-only loader context
- reflection-only loader context
ms.assetid: 9818b660-52f5-423d-a9af-e75163aa7068
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8e22dcf7db5ec2c78a79e574604e0b39b4962727
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68971851"
---
# <a name="how-to-load-assemblies-into-the-reflection-only-context"></a>방법: 리플렉션 전용 컨텍스트에 어셈블리 로드

리플렉션 전용 로드 컨텍스트를 사용하면 다른 플랫폼이나 다른 버전의 .NET Framework에 대해 컴파일된 어셈블리를 검사할 수 있습니다. 이 컨텍스트에 로드된 코드는 검사할 수만 있고 실행할 수 없습니다. 즉, 생성자를 실행할 수 없기 때문에 개체를 만들 수 없습니다. 코드를 실행할 수 없기 때문에 종속성이 자동으로 로드되지 않습니다. 종속성을 검사하려면 직접 로드해야 합니다.

## <a name="to-load-an-assembly-into-the-reflection-only-load-context"></a>리플렉션 전용 로드 컨텍스트에 어셈블리를 로드하려면

1. 표시 이름이 지정된 경우 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%28System.String%29> 메서드 오버로드를 사용하여 어셈블리를 로드하고, 해당 경로가 지정된 경우 <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> 메서드를 사용하여 어셈블리를 로드합니다. 어셈블리가 이진 이미지인 경우 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%28System.Byte%5B%5D%29> 메서드 오버로드를 사용합니다.

    > [!NOTE]
    > 리플렉션 전용 컨텍스트를 사용하여 실행 컨텍스트에 있는 버전 이외의 .NET Framework 버전에서 mscorlib.dll 버전을 로드할 수 없습니다.

2. 어셈블리에 종속성이 있는 경우 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A> 메서드는 종속성을 로드하지 않습니다. 종속성을 검사하려면 직접 로드해야 합니다.

3. 어셈블리의 <xref:System.Reflection.Assembly.ReflectionOnly%2A> 속성을 사용하여 어셈블리를 리플렉션 전용 컨텍스트에 로드할지 여부를 확인합니다.

4. 어셈블리 또는 어셈블리의 형식에 특성이 적용된 경우 <xref:System.Reflection.CustomAttributeData> 클래스를 통해 이러한 특성을 검사하여 리플렉션 전용 컨텍스트에서 코드를 실행하지 않도록 합니다. <xref:System.Reflection.CustomAttributeData.GetCustomAttributes%2A?displayProperty=nameWithType> 메서드의 적절한 오버로드를 사용하여 어셈블리, 멤버, 모듈 또는 매개 변수에 적용된 특성을 나타내는 <xref:System.Reflection.CustomAttributeData> 개체를 가져옵니다.

    > [!NOTE]
    > 어셈블리에 또는 해당 내용에 적용되는 특성은 어셈블리에서 정의되거나, 리플렉션 전용 컨텍스트에 로드된 다른 어셈블리에서 정의될 수 있습니다. 특성이 정의되어 있는 위치를 미리 확인할 수는 없습니다.

## <a name="example"></a>예

다음 코드 예제에서는 리플렉션 전용 컨텍스트에 로드된 어셈블리에 적용된 특성을 검사하는 방법을 보여 줍니다.

이 코드 예제는 생성자 두 개와 속성 하나를 사용하여 사용자 지정 특성을 정의합니다. 어셈블리, 어셈블리에 선언된 형식, 형식의 메서드, 메서드의 매개 변수에 특성이 적용됩니다. 실행할 경우 어셈블리는 리플렉션 전용 컨텍스트에 자동으로 로드되고 어셈블리와 어셈블리에 포함된 형식 및 멤버에 적용된 사용자 지정 특성에 대한 정보를 표시합니다.

> [!NOTE]
> 코드 예제를 단순화하기 위해 어셈블리가 자동으로 로드 및 검사됩니다. 일반적으로 실행 컨텍스트와 리플렉션 전용 컨텍스트에 동일한 어셈블리가 로드되는 경우는 없습니다.

[!code-cpp[CustomAttributeData#1](../../../samples/snippets/cpp/VS_Snippets_CLR/CustomAttributeData/CPP/source.cpp#1)]
[!code-csharp[CustomAttributeData#1](../../../samples/snippets/csharp/VS_Snippets_CLR/CustomAttributeData/CS/source.cs#1)]
[!code-vb[CustomAttributeData#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CustomAttributeData/VB/source.vb#1)]

## <a name="see-also"></a>참고 항목

- <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A>
- <xref:System.Reflection.Assembly.ReflectionOnly%2A>
- <xref:System.Reflection.CustomAttributeData>
