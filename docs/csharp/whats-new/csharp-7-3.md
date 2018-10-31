---
title: C# 7.3의 새로운 기능
description: C# 7.3의 새로운 기능에 대한 개요입니다.
ms.date: 05/16/2018
ms.openlocfilehash: 570da53059242c0242609ddcba5cb23f1728aa9f
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48873802"
---
# <a name="whats-new-in-c-73"></a>C# 7.3의 새로운 기능

C# 7.3 릴리스에는 두 개의 기본 테마가 있습니다. 하나의 테마는 안전한 코드의 성능을 안전하지 않은 코드만큼 향상할 수 있는 기능을 제공합니다. 두 번째 테마는 기존 기능에 대한 점진적인 개선을 제공합니다. 또한 새 컴파일러 옵션이 이 릴리스에 추가되었습니다.

다음 새로운 기능은 안전한 코드에 대해 향상된 성능의 테마를 지원합니다.

- 고정하지 않고 고정 필드에 액세스할 수 있습니다.
- `ref` 지역 변수를 다시 할당할 수 있습니다.
- `stackalloc` 배열에서 이니셜라이저를 사용할 수 있습니다.
- 패턴을 지원하는 모든 형식과 함께 `fixed` 문을 사용할 수 있습니다.
- 추가적인 제네릭 제약 조건을 사용할 수 있습니다.

기존 기능이 다음과 같이 개선되었습니다.

- 튜플 형식으로 `==` 및 `!=`를 테스트할 수 있습니다.
- 더 많은 위치에서 식 변수를 사용할 수 있습니다.
- 자동 구현 속성의 지원 필드에 특성을 연결할 수 있습니다.
- 인수에서 `in`만 다른 경우 메서드 해결이 향상되었습니다.
- 이제 오버로드 해결에 모호한 사례가 감소했습니다.

새 컴파일러 옵션은 다음과 같습니다.

- `-publicsign` - OSS(오픈 소스 소프트웨어) 시그니처를 사용하도록 설정합니다.
- `-pathmap` - 소스 디렉터리에 대한 매핑을 제공합니다.

이 문서의 나머지 부분에서는 각 개선 사항에 대해 자세히 알아보기 위한 세부 정보와 링크를 제공합니다.

## <a name="enabling-more-efficient-safe-code"></a>좀 더 효율적인 안전한 코드 사용

안전하게 실행할 C# 코드 및 안전하지 않은 코드를 작성할 수 있어야 합니다. 안전한 코드를 사용하면 버퍼 오버런, 이상 포인터 및 기타 메모리 액세스 오류와 같은 오류 클래스를 피할 수 있습니다. 이러한 새 기능은 확인 가능한 안전한 코드의 기능을 확장합니다. 안전한 구문을 사용하여 더 많은 코드를 작성하도록 노력하세요. 이러한 기능을 사용하면 이 작업이 더 쉬워집니다.

### <a name="indexing-fixed-fields-does-not-require-pinning"></a>`fixed` 필드 인덱싱에 고정이 필요하지 않음

다음 구조체를 고려합니다.

```csharp
unsafe struct S
{
    public fixed int myFixedField[10];
}
```

이전 버전의 C#에서는 `myFixedField`의 일부인 정수 중 하나에 액세스하려면 변수를 고정해야 했습니다. 이제 다음 코드는 안전한 컨텍스트에서 컴파일됩니다.

```csharp
class C
{
    static S s = new S();

    unsafe public void M()
    {
        int p = s.myFixedField[5];
    }
}
```

`p` 변수는 `myFixedField`의 한 요소에 액세스합니다. 별도의 `int*` 변수를 선언할 필요가 없습니다. `unsafe` 컨텍스트는 계속 필요합니다. 이전 버전의 C#에서는 두 번째 고정된 포인터를 선언해야 합니다.

```csharp
class C
{
    static S s = new S();

    unsafe public void M()
    {
        fixed (int* ptr = s.myFixedField)
        {
            int p = ptr[5];
        }
    }
}
```

자세한 내용은 [`fixed` 문](../language-reference/keywords/fixed-statement.md)에 대한 문서를 참조하세요.

### <a name="ref-local-variables-may-be-reassigned"></a>`ref` 지역 변수를 다시 할당할 수 있음

이제 `ref` 지역 변수를 다시 할당하여 초기화된 후 다른 인스턴스를 참조할 수 있습니다. 이제 다음 코드가 컴파일됩니다.

```csharp
ref VeryLargeStruct refLocal = ref veryLargeStruct; // initialization
refLocal = ref anotherVeryLargeStruct; // reassigned, refLocal refers to different storage.
```

자세한 내용은 [`ref` 반환 및 `ref` 지역](../programming-guide/classes-and-structs/ref-returns.md)에 대한 아티클 및 [`foreach`](../language-reference/keywords/foreach-in.md)에 대한 아티클을 참조하세요.

### <a name="stackalloc-arrays-support-initializers"></a>`stackalloc` 배열이 이니셜라이저를 지원함

초기화할 때 배열의 요소 값을 지정할 수 있었습니다.

```csharp
var arr = new int[3] {1, 2, 3};
var arr2 = new int[] {1, 2, 3};
```

이제 `stackalloc`로 선언된 배열에 동일한 구문을 적용할 수 있습니다.

```csharp
int* pArr = stackalloc int[3] {1, 2, 3};
int* pArr2 = stackalloc int[] {1, 2, 3};
Span<int> arr = stackalloc [] {1, 2, 3};
```

자세한 내용은 언어 참조에서 [`stackalloc` 문](../language-reference/keywords/stackalloc.md) 문서를 참조하세요.

### <a name="more-types-support-the-fixed-statement"></a>더 많은 형식이 `fixed` 문을 지원함

`fixed` 문은 제한된 형식 집합을 지원했습니다. C# 7.3부터 `ref T` 또는 `ref readonly T`를 반환하는 `GetPinnableReference()` 메서드를 포함하는 모든 형식이 `fixed`일 수 있습니다. 이 기능을 추가하면 `fixed`를 <xref:System.Span%601?displayProperty=nameWithType> 및 관련 형식과 함께 사용할 수 있습니다.

자세한 내용은 언어 참조에서 [`fixed` 문](../language-reference/keywords/fixed-statement.md) 문서를 참조하세요.

### <a name="enhanced-generic-constraints"></a>향상된 제네릭 제약 조건

이제 형식 매개 변수에 대한 기본 클래스 제약 조건으로 <xref:System.Enum?displayProperty=nameWithType> 또는 <xref:System.Delegate?displayProperty=nameWithType> 형식을 지정할 수 있습니다.

또한 새 `unmanaged` 제약 조건을 사용하여 형식 매개 변수가 **관리되지 않는 형식**이 되도록 지정할 수 있습니다. **관리되지 않는 형식**은 참조 형식이 아니고 모든 중첩 수준의 참조 형식을 포함하지 않는 형식입니다.

자세한 내용은 [`where` 제네릭 제약 조건](../language-reference/keywords/where-generic-type-constraint.md) 및 [형식 매개 변수 제약 조건](../programming-guide/generics/constraints-on-type-parameters.md)에 대한 문서를 참조하세요.

기존 형식에 이러한 제약 조건을 추가하는 것은 [호환되지 않는 변경](version-update-considerations.md#incompatible-changes)입니다. 폐쇄형 제네릭 형식은 더 이상 이러한 새 제약 조건을 충족할 수 없습니다.

## <a name="make-existing-features-better"></a>기존 기능의 향상

두 번째 테마는 언어의 기능에 대한 개선을 제공합니다. 이러한 기능은 C#를 작성할 때 생산성을 개선합니다.

### <a name="tuples-support--and-"></a>튜플은 `==` 및 `!=`를 지원합니다.

C# 튜플 형식은 이제 `==` 및 `!=`를 지원합니다. 자세한 내용은 [튜플](../tuples.md)에 대한 문서에서 [같음](../tuples.md#equality-and-tuples)을 다루는 섹션을 참조하세요.

### <a name="attach-attributes-to-the-backing-fields-for-auto-implemented-properties"></a>자동 구현 속성의 지원 필드에 특성 연결

이제 다음 구문이 지원됩니다.

```csharp
[field: SomeThingAboutFieldAttribute]
public int SomeProperty { get; set; }
```

`SomeThingAboutFieldAttribute` 특성은 `SomeProperty`에 대한 컴파일러 생성 지원 필드에 적용됩니다. 자세한 내용은 C# 프로그래밍 가이드의 [특성](../programming-guide/concepts/attributes/index.md)을 참조하세요.

### <a name="in-method-overload-resolution-tiebreaker"></a>`in` 메서드 오버로드 해결 순위 결정

`in` 인수 한정자가 추가된 경우 이러한 두 메서드로 인해 모호성이 발생합니다.

```csharp
static void M(S arg);
static void M(in S arg);
```

이제 값 기준(이전 예제의 첫 번째) 오버로드가 읽기 전용 참조 기준 버전보다 더 좋습니다. 읽기 전용 참조 인수를 사용하여 버전을 호출하려면 메서드를 호출할 때 `in` 한정자를 포함해야 합니다.

> [!NOTE]
> 이는 버그 수정으로 구현되었습니다. 이것은 언어 버전이 “7.2”로 설정된 경우에도 더 이상 모호하지 않습니다.

자세한 내용은 [`in` 매개 변수 한정자](../language-reference/keywords/in-parameter-modifier.md)에 대한 문서를 참조하세요.

### <a name="extend-expression-variables-in-initializers"></a>이니셜라이저에서 식 변수 확장

`out` 변수 선언이 허용하기 위해 C# 7.0에 추가된 구문은 필드 이니셜라이저, 속성 이니셜라이저, 생성자 이니셜라이저 및 쿼리 절을 포함하도록 확장되었습니다. 이를 통해 다음 예제와 같은 코드를 사용할 수 있습니다.

```csharp
public class B
{
   public B(int i, out int j)
   {
      j = i;
   }
}

public class D : B
{
   public D(int i) : base(i, out var j)
   {
      Console.WriteLine($"The value of 'j' is {j}");
   }
}
```

### <a name="improved-overload-candidates"></a>향상된 오버로드 후보

모든 릴리스에서 오버로드 해결 규칙은 모호한 메서드 호출에 “분명한” 선택이 있는 상황을 해결하도록 업데이트됩니다. 이 릴리스는 컴파일러가 분명한 선택 항목을 선택하도록 도와주는 세 가지 새로운 규칙을 추가합니다.

1. 메서드 그룹에 인스턴스와 정적 멤버가 둘 다 포함되어 있으면 인스턴스 수신기 또는 컨텍스트 없이 호출되는 경우 컴파일러는 인스턴스 멤버를 버립니다. 메서드가 인스턴스 수신기를 통해 호출된 경우 컴파일러는 정적 멤버를 버립니다. 수신기가 없는 경우 컴파일러는 정적 컨텍스트에 정적 멤버만 포함하고, 이외의 경우에는 정적 및 인스턴스 멤버를 둘 다 포함합니다. 수신기가 모호하게 인스턴스 또는 형식인 경우에는 컴파일러가 둘 다 포함합니다. 암시적 `this` 인스턴스 수신기를 사용할 수 없는 정적 컨텍스트에는 정적 멤버와 같이 `this`가 정의되지 않은 멤버의 본문과 필드 이니셜라이저 및 생성자 이니셜라이저와 같이 `this`를 사용할 수 없는 위치가 포함됩니다.
1. 형식 인수가 해당 제약 조건을 충족하지 않는 제네릭 메서드가 메서드 그룹에 포함된 경우 이러한 멤버는 후보 집합에서 제거됩니다.
1. 메서드 그룹 변환의 경우 반환 형식이 대리자의 반환 형식과 일치하지 않는 후보 메서드가 집합에서 제거됩니다.

어떤 메서드가 더 나은지 알고 있으면 모호한 메서드 오버로드에 대한 컴파일러 오류가 감소하므로 이 변경을 알 수 있습니다.

## <a name="new-compiler-options"></a>새로운 컴파일러 옵션

새로운 컴파일러 옵션은 C# 프로그램에 대한 새로운 빌드 및 DevOps 시나리오를 지원합니다.

### <a name="public-or-open-source-signing"></a>공개 또는 오픈 소스 서명

`-publicsign` 컴파일러 옵션은 공개 키를 사용하여 어셈블리에 서명하도록 컴파일러에 지시합니다. 어셈블리는 서명됨으로 표시되지만 시그니처는 공개 키에서 가져옵니다. 이 옵션을 사용하면 공개 키를 사용하여 오픈 소스 프로젝트에서 서명된 어셈블리를 빌드할 수 있습니다.

자세한 내용은 [-publicsign 컴파일러 옵션](../language-reference/compiler-options/publicsign-compiler-option.md) 문서를 참조하세요.

### <a name="pathmap"></a>pathmap

`-pathmap` 컴파일러 옵션은 빌드 환경의 소스 경로를 매핑된 소스 경로로 바꾸도록 컴파일러에 지시합니다. `-pathmap` 옵션은 컴파일러에서 작성된 PDB 파일의 소스 경로 또는 <xref:System.Runtime.CompilerServices.CallerFilePathAttribute>를 제어합니다.

자세한 내용은 [-pathmap 컴파일러 옵션](../language-reference/compiler-options/pathmap-compiler-option.md) 문서를 참조하세요.
