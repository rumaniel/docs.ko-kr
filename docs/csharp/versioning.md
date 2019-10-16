---
title: C# 버전 관리 - C# 가이드
description: C# 및 .NET에서 버전 관리의 작동 방식 이해
ms.date: 01/08/2017
ms.assetid: aa8732d7-5cd0-46e1-994a-78017f20d861
ms.openlocfilehash: dcfe373312b88c8ddd8587e27c566a90b25e3c13
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834054"
---
# <a name="versioning-in-c"></a>C\#으로 버전 관리

이 자습서에서는 .NET에서 버전 관리가 어떤 의미인지에 대해 배웁니다. 또한 라이브러리의 버전을 관리할 때 및 라이브러리의 새 버전으로 업그레이드할 때 고려해야 할 요소에 대해 배웁니다.

## <a name="authoring-libraries"></a>라이브러리 작성

공용 .NET 라이브러리를 만든 개발자라면 새로운 업데이트를 출시해야 하는 상황을 겪은 적 있을 것입니다. 이 프로세스의 진행 방법은 기존 코드를 새 버전의 라이브러리로 원활하게 전환해야 하는 경우 매우 중요합니다. 새 릴리스를 만들 때 다음과 같은 몇 가지 사항을 고려해야 합니다.

### <a name="semantic-versioning"></a>유의적 버전

[유의적 버전](https://semver.org/)(줄여서 SemVer)은 특정 중요 시점 이벤트를 나타내기 위해 라이브러리의 버전에 적용되는 명명 규칙입니다.
라이브러리에 제공하는 버전 정보를 이용해 개발자가 동일한 라이브러리의 이전 버전을 사용하는 프로젝트와의 호환성을 확인하는 것이 가장 바람직합니다.

SemVer에 대한 가장 기본적인 접근법은 3개 구성 요소 형식 `MAJOR.MINOR.PATCH`입니다. 여기서:

- `MAJOR`은 호환되지 않는 API 변경 사항이 있을 때 증가합니다.
- `MINOR`는 이전 버전과 호환성 방식으로 기능을 추가할 때 증가합니다.
- `PATCH`는 이전 버전과 호환성 버그 수정을 만들 때 증가합니다.

.NET 라이브러리에 버전 정보를 적용할 때 시험판 버전 등과 같은 기타 시나리오를 지정할 수도 있습니다.

### <a name="backwards-compatibility"></a>이전 버전과의 호환성

라이브러리의 새 버전을 릴리스하면 이전 버전과의 호환성이 주요 관심사 중 하나가 될 것입니다.
이전 버전에 종속된 코드가 다시 컴파일할 때 새 버전과 작동하는 경우, 라이브러리의 새 버전은 이전 버전과 소스가 호환됩니다. 이전 버전을 사용하는 애플리케이션이 다시 컴파일하지 않고도 새 버전과 작동하는 경우 라이브러리의 새 버전은 이진 호환됩니다.

라이브러리 이전 버전과의 호환성을 유지하고자 할 경우 다음 사항을 고려해야 합니다.

- 가상 메서드: 새 버전에서 가상 메서드를 가상이 아닌 상태로 만들 경우, 해당 메서드를 재정의하는 프로젝트를 업데이트해야 합니다. 여기에는 엄청난 변화가 따르므로 권장하지 않습니다.
- 메서드 시그니처: 메서드 동작 업데이트 시 시그니처도 변경해야 하는 경우, 해당 메서드에 대한 코드 호출이 계속 작동하도록 오버로드를 대신 만들어야 합니다.
구현의 일관성이 유지되도록 항상 이전 메서드 시그니처를 조작하여 새 메서드 시그니처를 호출할 수 있습니다.
- [Obsolete 특성](programming-guide/concepts/attributes/common-attributes.md#Obsolete): 사용되지 않는 클래스 또는 클래스 멤버를 지정하고 이후 버전에서 제거되도록 하려면 코드에 이 특성을 사용할 수 있습니다. 이렇게 하면 라이브러리를 활용하는 개발자가 큰 변화에 더 잘 대비할 수 있습니다.
- 선택적 메서드 인수: 전에는 선택 사항이었던 메서드 인수를 필수로 만들거나 기본값을 변경하는 경우, 해당 인수를 제공하지 않는 모든 코드를 업데이트해야 합니다.

> [!NOTE]
> 필수 인수를 선택 사항으로 만드는 것은 특히 메서드의 동작을 변경하지 않을 경우 거의 영향을 미치지 않습니다.

라이브러리의 새 버전으로 업그레이드하는 방법이 쉬울수록 사용자가 더 빨리 업그레이드할 가능성이 높아집니다.

### <a name="application-configuration-file"></a>애플리케이션 구성 파일

.NET 개발자는 대부분의 프로젝트 형식에서 [`app.config` 파일](../framework/configure-apps/file-schema/index.md)을 발견할 가능성이 매우 높습니다.
이 간단한 구성 파일은 새로운 업데이트 출시를 개선하는 데 큰 도움이 될 수 있습니다. 일반적으로 라이브러리를 설계할 때 정기적으로 변경될 가능성이 있는 정보를 `app.config` 파일에 저장하도록 해야 합니다. 이렇게 하면 해당 정보가 업데이트될 때 라이브러리를 다시 컴파일하지 않고 이전 버전의 구성 파일을 새로운 파일로 바꾸기만 하면 됩니다.

## <a name="consuming-libraries"></a>라이브러리 사용

다른 개발자가 만든 .NET 라이브러리를 사용하는 개발자는 라이브러리의 새 버전이 자신의 프로젝트와 완전히 호환되지 않을 수 있으며 그러한 변경 사항에 적응하기 위해 자신의 코드를 업데이트해야 상황에 종종 처하게 된다는 사실을 알고 있을 것입니다.

다행히 C# 및 .NET 에코시스템에는 큰 변화가 생긴 새로운 라이브러리 버전과 작동하도록 앱을 손쉽게 업데이트할 수 있는 기능과 기술이 마련되어 있습니다.

### <a name="assembly-binding-redirection"></a>어셈블리 바인딩 리디렉션

앱이 사용하는 라이브러리의 버전을 업데이트하기 위해 *app.config* 파일을 사용할 수 있습니다. [*바인딩 리디렉션*](../framework/configure-apps/redirect-assembly-versions.md)을 추가하면 앱을 다시 컴파일하지 않고도 새 라이브러리 버전을 사용할 수 있습니다. 다음 예제에서는 원래 컴파일된 `1.0.0` 버전 대신 `ReferencedLibrary`의 `1.0.1` 패치 버전을 사용하도록 앱의 *app.config* 파일을 업데이트하는 방법을 보여 줍니다.

```xml
<dependentAssembly>
    <assemblyIdentity name="ReferencedLibrary" publicKeyToken="32ab4ba45e0a69a1" culture="en-us" />
    <bindingRedirect oldVersion="1.0.0" newVersion="1.0.1" />
</dependentAssembly>
```

> [!NOTE]
> 이 방법은 `ReferencedLibrary`의 새 버전이 앱과 이진 호환되는 경우에만 적용됩니다.
> 호환성을 결정할 때 확인해야 할 변경 사항은 위의 [이전 버전과 호환성](#backwards-compatibility) 섹션을 참조하세요.

### <a name="new"></a>new

상속된 기본 클래스의 멤버를 숨기려면 `new` 한정자를 사용합니다. 이것은 파생 클래스가 기본 클래스의 업데이트에 응답할 수 있는 한 방법입니다.

다음 예제를 참조하세요.

[!code-csharp[Sample usage of the 'new' modifier](~/samples/csharp/versioning/new/Program.cs#sample)]

**출력**

```console
A base method
A derived method
```

위의 예제에서는 `DerivedClass`가 `BaseClass`에 있는 `MyMethod` 메서드를 숨기는 방법을 확인할 수 있습니다.
즉, 라이브러리의 새 버전에 있는 기본 클래스가 파생 클래스에 이미 있는 멤버를 추가하면 파생 클래스 멤버에 `new` 한정자를 사용하여 기본 클래스 멤버를 숨길 수 있습니다.

`new` 한정자를 지정하지 않으면 파생 클래스는 기본 클래스에서 충돌하는 멤버를 기본적으로 숨깁니다. 컴파일러 경고가 생성되지만 코드는 여전히 컴파일됩니다. 즉, 기존 클래스에 새 멤버를 추가하기만 하면 라이브러리의 새 버전이 소스와 이진 모두 여기에 종속된 코드와 호환됩니다.

### <a name="override"></a>재정의

`override` 한정자를 사용하면 파생된 구현은 기본 클래스 멤버의 구현을 숨기는 대신 확장합니다. 기본 클래스 멤버에 `virtual` 한정자를 적용해야 합니다.

[!code-csharp[Sample usage of the 'override' modifier](../../samples/csharp/versioning/override/Program.cs#sample)]

**출력**

```console
Base Method One: Method One
Derived Method One: Derived Method One
```

`override` 한정자는 컴파일 시간에 평가되며, 재정의할 가상 멤버를 찾지 못하면 컴파일러에서 오류가 발생합니다.

라이브러리 버전 간을 더욱 간편하게 전환하려면 여기서 설명한 방법을 익히고 어떤 상황에서 이를 사용해야 할지를 이해해야 합니다.
