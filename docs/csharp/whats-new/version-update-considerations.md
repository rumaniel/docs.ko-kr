---
title: C# 개발자를 위한 버전 및 업데이트 고려 사항
description: 라이브러리에 새로운 언어 기능을 도입하면 해당 라이브러리를 사용하는 코드에 영향을 줄 수 있습니다.
ms.date: 09/19/2018
ms.openlocfilehash: 3ffe2f6fd64a391fddf28233dccb022c95851884
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65634483"
---
# <a name="version-and-update-considerations-for-c-developers"></a>C# 개발자를 위한 버전 및 업데이트 고려 사항

C# 언어에 새로운 기능이 추가되므로 호환성은 매우 중요한 목표입니다. 대부분의 경우 문제없이 새 컴파일러 버전으로 기존 코드를 다시 컴파일할 수 있습니다.

라이브러리에서 새 언어 기능을 채택할 때는 더욱 주의해야 할 수 있습니다. 최신 버전에 있는 기능을 사용하여 새 라이브러리를 만드는 경우 이전 버전의 컴파일러로 빌드된 앱이 새 라이브러리를 사용할 수 있는지 확인해야 합니다. 또는 기존 라이브러리를 업그레이드하는 경우 아직 업그레이드된 버전이 없는 사용자가 많을 수 있습니다. 새 기능을 채택하기로 결정하면 소스 호환 가능 및 이진 호환 가능이라는 두 가지 호환성 변형을 고려해야 합니다.

## <a name="binary-compatible-changes"></a>이진 호환 가능 변경

라이브러리를 사용하는 애플리케이션 및 라이브러리를 다시 빌드하지 않고 업데이트된 라이브러리를 사용할 수 있는 경우 라이브러리 변경은 **이진 호환 가능**합니다. 종속 어셈블리를 다시 빌드하거나 소스 코드를 변경하지 않아도 됩니다. 이진 호환 가능 변경은 소스 호환 가능 변경이기도 합니다.

## <a name="source-compatible-changes"></a>소스 호환 가능 변경

라이브러리를 사용하는 애플리케이션 및 라이브러리에 대해 소스 코드를 변경하지 않아도 되지만 올바르게 작동하려면 새 버전에 대해 소스를 다시 컴파일해야 하는 경우 라이브러리 변경은 **소스 호환 가능**합니다.

## <a name="incompatible-changes"></a>호환되지 않는 변경

변경이 **소스 호환 가능** 또는 **이진 호환 가능**하지 않은 경우 종속 라이브러리 및 애플리케이션에서 소스 코드를 변경하고 다시 컴파일해야 합니다.

## <a name="evaluate-your-library"></a>라이브러리 평가

이러한 호환성 개념은 라이브러리에 대한 public 및 protected 선언에 영향을 주며 내부 구현에는 영향을 주지 않습니다. 내부적으로 새로운 기능을 채택하면 항상 **이진 호환 가능**합니다.  

**이진 호환 가능** 변경은 public 선언에 대해 이전 구문과 동일한 컴파일된 코드를 생성하는 새 구문을 제공합니다. 예를 들어 메서드를 식 본문 멤버로 변경하는 것은 **이진 호환 가능** 변경입니다.

원래 코드:

```csharp
public double CalculateSquare(double value)
{
    return value * value;
}
```

새로운 코드:

```csharp
public double CalculateSquare(double value) => value * value;
```

**소스 호환 가능** 변경은 public 멤버에 대해 컴파일된 코드를 변경하지만 기존 호출 사이트와 호환되는 방식으로 변경하는 구문을 도입합니다. 예를 들어 값 기준 매개 변수에서 `in` 참조 기준 매개 변수로 메서드 시그니처를 변경하는 것은 소스 호환 가능하지만 이진 호환 가능하지는 않습니다.

원래 코드:

```csharp
public double CalculateSquare(double value) => value * value;
```

새로운 코드:

```csharp
public double CalculateSquare(in double value) => value * value;
```

[새로운 기능](index.md) 문서에서는 public 선언에 영향을 주는 기능을 도입하는 것이 소스 호환 가능 또는 이진 호환 가능한지 설명합니다.
