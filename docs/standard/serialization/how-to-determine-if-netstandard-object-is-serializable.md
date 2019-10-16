---
title: .NET Standard 개체를 직렬화 가능 인지 확인 하는 방법
description: .NET 표준 형식이 런타임에 serialize 할 수 있는지 여부를 확인 하는 방법을 보여 줍니다.
ms.date: 10/20/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- serializing objects
- objects, serializing steps
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 196e99ab1f1a0baae53c6a1dc295b135e36fbfe0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62018764"
---
# <a name="how-to-determine-if-a-net-standard-object-is-serializable"></a>.NET Standard 개체를 직렬화 가능 인지 확인 하는 방법

.NET Standard는 형식 및 해당 버전의 표준 준수 하는 특정.NET 구현에 있어야 하는 멤버를 정의 하는 사양입니다. 그러나.NET Standard 정의 하지 않습니다는 형식이 직렬화 가능 인지 합니다. .NET 표준 라이브러리에서 정의 된 형식으로 표시 되어 있지는 <xref:System.SerializableAttribute> 특성입니다. 대신.NET Framework 및.NET Core와 같은 특정.NET 구현에는 특정 형식의 직렬화 가능 인지 여부를 확인 무료입니다. 

개발한 경우 라이브러리를 대상으로 하는.NET Standard,.NET Standard를 지 원하는 모든.NET 구현에서 라이브러리를 사용할 수 있습니다. 즉,는 알 수 없습니다 사전에 특정 형식 인지 직렬화 할 수 있습니다. 만 런타임에 직렬화 될 지 여부를 확인할 수 있습니다.

개체의 값을 검색 하 여 런타임 시 직렬화 가능 인지 여부를 확인할 수 있습니다 합니다 <xref:System.Type.IsSerializable> 의 속성을 <xref:System.Type> 해당 개체의 형식을 나타내는 개체입니다. 다음 예제에는 하나의 구현을 제공합니다. 정의 `IsSerializable(Object)` 확장 메서드를 나타내는 있는지 여부를 <xref:System.Object> 인스턴스를 serialize 할 수 있습니다.

[!code-csharp[is-a-type-serializable](~/samples/snippets/standard/serialization/is-serializable/csharp/program.cs#2)]
[!code-vb[is-a-type-serializable](~/samples/snippets/standard/serialization/is-serializable/vb/library.vb#2)]

그런 다음 여부를 고 수 serialize 및 deserialize 될 현재.NET 구현에서 다음 예와 같이 결정할 메서드에 개체를 전달할 수 있습니다.

[!code-csharp[test-is-a-type-serializable](~/samples/snippets/standard/serialization/is-serializable/csharp/program.cs#1)]
[!code-vb[test-is-a-type-serializable](~/samples/snippets/standard/serialization/is-serializable/vb/program.vb#1)]

## <a name="see-also"></a>참고자료

- [이진 serialization](binary-serialization.md)
- <xref:System.SerializableAttribute?displayProperty=nameWithType>
- <xref:System.Type.IsSerializable?displayProperty=nameWithType>
