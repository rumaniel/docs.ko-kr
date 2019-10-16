---
title: C# 열거형 - C# 언어 둘러보기
description: C#의 열거형, 명명된 개별 상수에 대해 자세히 알아보기
ms.date: 08/10/2016
ms.assetid: 7faba1cc-6ea9-4a19-adb9-0335e4b132e5
ms.openlocfilehash: 8c1c29c3c06829da81a9c9be8bb5bd99f1c9e395
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "57843126"
---
# <a name="enums"></a>열거형

***열거형 형식***은 명명된 상수 집합을 갖는 고유 값 형식입니다. 개별 값 집합을 가질 수 있는 형식을 정의해야 할 경우 열거형을 정의합니다. 정수 값 형식 중 하나를 기본 스토리지로 사용합니다. 또한 개별 값에 대해 의미 체계 의미를 제공합니다.

다음 예제에서는 3개의 상수 값, 즉 `Red`, `Green` 및 `Blue`를 갖는 `Color`라는 `enum` 형식을 선언하고 사용합니다.

[!code-csharp[EnumExample](../../../samples/snippets/csharp/tour/enums/Program.cs#L3-L36)]

각 `enum` 형식에는 `enum` 형식의 ***내부 형식***이라고 하는 정수 계열 형식이 있습니다. 내부 형식을 명시적으로 선언하지 않는 `enum` 형식의 내부 형식은 `int`입니다. `enum` 형식의 스토리지 유형 및 가능한 값 범위는 내부 형식에 따라 결정됩니다. `enum` 형식에 적용될 수 있는 값 집합은 해당 `enum` 멤버로 제한되지 않습니다. 특히 `enum`의 모든 내부 형식 값은 `enum` 형식으로 캐스팅될 수 있으며 해당 `enum` 형식을 갖는 유효한 고유 값입니다.

다음 예제에서는 `sbyte`의 내부 형식을 사용하여 `Alignment`라는 `enum` 형식을 선언합니다.

[!code-csharp[EnumStorage](../../../samples/snippets/csharp/tour/enums/Program.cs#L38-L43)]

앞의 예제와 같이 `enum` 멤버 선언에는 멤버의 값을 지정하는 상수 식이 포함될 수 있습니다. 각 `enum` 멤버의 상수 값은 `enum`의 내부 형식 범위 내에 있어야 합니다. `enum` 멤버 선언이 값을 명시적으로 지정하지 않으면 멤버에는 값 0(`enum` 형식의 첫 번째 멤버인 경우) 또는 이전 `enum` 멤버 값 앞에 1을 더한 값이 지정됩니다.

형식 캐스팅을 사용하여 `Enum` 값을 정수로, 그 반대로 변환할 수 있습니다. 예:

[!code-csharp[EnumStorage](../../../samples/snippets/csharp/tour/enums/Program.cs#L49-L50)]

`enum` 형식의 기본값은 `enum` 형식으로 변환된 정수 계열 값 0입니다. 변수가 자동으로 기본값으로 초기화되는 경우 `enum` 형식의 변수에 이 값이 지정됩니다. `enum` 형식의 기본값을 쉽게 사용하도록 하기 위해 리터럴 `0`이 `enum` 형식으로 암시적으로 변환됩니다. 따라서 다음이 허용됩니다.

[!code-csharp[EnumZero](../../../samples/snippets/csharp/tour/enums/Program.cs#L58-L58)]

> [!div class="step-by-step"]
> [이전](interfaces.md)
> [다음](delegates.md)
