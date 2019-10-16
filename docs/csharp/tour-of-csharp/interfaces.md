---
title: C# 인터페이스 - C# 언어 둘러보기
description: 인터페이스는 C#의 형식이 구현하는 계약을 정의합니다.
ms.date: 08/10/2016
ms.assetid: a9bf82f4-efd1-4216-bd34-4ef0fa48c968
ms.openlocfilehash: 240ddfb321c5a89c8aada4353845915d0e242ae0
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65634549"
---
# <a name="interfaces"></a>인터페이스

***인터페이스***는 클래스 및 구조체에서 구현될 수 있는 계약을 정의합니다. 인터페이스는 메서드, 속성, 이벤트 및 인덱서를 포함할 수 있습니다. 인터페이스는 정의하는 멤버의 구현을 제공하지 않으며 단순히 인터페이스를 구현하는 클래스 또는 구조체에서 제공해야 하는 멤버를 지정합니다.

인터페이스는 ***다중 상속***을 사용할 수 있습니다. 다음 예제에서 인터페이스 `IComboBox`는 `ITextBox` 및 `IListBox`를 둘 다 상속합니다.

[!code-csharp[InterfacesOne](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L5-L17)]

클래스 및 구조체는 여러 인터페이스를 구현할 수 있습니다. 다음 예제에서 클래스 `EditBox`는 `IControl` 및 `IDataBound`를 둘 다 구현합니다.

[!code-csharp[InterfacesTwo](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L19-L27)]

클래스 또는 구조체가 특정 인터페이스를 구현하는 경우 해당 클래스 또는 구조체의 인스턴스를 해당 인터페이스 형식으로 암시적으로 변환할 수 있습니다. 예

[!code-csharp[InterfacesThree](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L33-L35)]

인스턴스가 정적으로 특정 인터페이스를 구현하는 것으로 알려지지 않은 경우 동적 형식 캐스팅을 사용할 수 있습니다. 예를 들어 다음 문에서는 동적 형식 캐스팅을 사용하여 개체의 `IControl` 및 `IDataBound` 인터페이스 구현을 획득합니다. 개체의 실제 런타임 형식이 `EditBox`이므로 캐스팅은 성공합니다.

[!code-csharp[InterfacesFour](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L40-L42)]

이전 `EditBox` 클래스에서 `IControl` 인터페이스의 `Paint` 메서드와 에서 `IDataBound` 인터페이스의 `Bind` 메서드는 공용 멤버를 사용하여 구현됩니다. 또한 C#에서는 명시적 ***인터페이스 멤버 구현***을 지원하여 클래스 또는 구조체가 멤버를 공용으로 만들지 못하게 합니다. 명시적 인터페이스 멤버 구현은 정규화된 인터페이스 멤버 이름을 사용하여 작성됩니다. 예를 들어 `EditBox` 클래스는 다음과 같이 명시적 인터페이스 멤버 구현을 사용하여 `IControl.Paint` 및 `IDataBound.Bind` 메서드를 구현할 수 있습니다.

[!code-csharp[InterfacesFive](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L60-L64)]

명시적 인터페이스 멤버는 인터페이스 형식을 통해서만 액세스할 수 있습니다. 예를 들어 이전 EditBox 클래스가 제공한 `IControl.Paint`의 구현은 먼저 `EditBox` 참조를 `IControl` 인터페이스 형식으로 변환해야만 호출할 수 있습니다.

[!code-csharp[InterfacesFive](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L71-L74)]

>[!div class="step-by-step"]
>[이전](arrays.md)
>[다음](enums.md)
