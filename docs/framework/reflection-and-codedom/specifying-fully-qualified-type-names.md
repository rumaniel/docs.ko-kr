---
title: 정규화된 형식 이름 지정
ms.date: 02/21/2019
helpviewer_keywords:
- names [.NET Framework], fully qualified type names
- reflection, fully qualified type names
- names [.NET Framework], assemblies
- tokens
- BNF
- assemblies [.NET Framework], names
- languages, grammar
- fully qualified type names
- type names
- special characters
- IDENTIFIER
ms.assetid: d90b1e39-9115-4f2a-81c0-05e7e74e5580
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 656b82daffc62824ed663ea7080bd6d20cd0dadc
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045823"
---
# <a name="specifying-fully-qualified-type-names"></a>정규화된 형식 이름 지정

다양한 리플렉션 작업에 대한 유효한 입력을 포함하려면 형식 이름을 지정해야 합니다. 정규화된 형식 이름은 어셈블리 이름 사양, 네임스페이스 사양, 형식 이름으로 구성됩니다. 형식 이름 사양은 <xref:System.Type.GetType%2A?displayProperty=nameWithType>, <xref:System.Reflection.Module.GetType%2A?displayProperty=nameWithType>, <xref:System.Reflection.Emit.ModuleBuilder.GetType%2A?displayProperty=nameWithType>, <xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType> 등의 메서드에서 사용됩니다.

## <a name="grammar-for-type-names"></a>형식 이름의 문법

 문법은 공식 언어의 구문을 정의합니다. 다음 표에서는 유효한 입력을 인식하는 방법을 설명하는 어휘 규칙을 보여 줍니다. 터미널(더 이상 줄일 수 없는 요소)은 모두 대문자로 표시됩니다. 비터미널(더 줄일 수 있는 요소)은 대/소문자가 혼합되어 있거나 작은따옴표가 붙은 문자열로 표시되지만 작은따옴표(')는 구문 자체에 속하지 않습니다. 파이프 문자(&#124;)는 하위 규칙이 있는 규칙을 나타냅니다.

<!-- markdownlint-disable MD010 -->
```antlr
TypeSpec
    : ReferenceTypeSpec
    | SimpleTypeSpec
    ;

ReferenceTypeSpec
    : SimpleTypeSpec '&'
    ;

SimpleTypeSpec
    : PointerTypeSpec
    | GenericTypeSpec
    | TypeName
    ;

GenericTypeSpec
   : SimpleTypeSpec ` NUMBER

PointerTypeSpec
    : SimpleTypeSpec '*'
    ;

ArrayTypeSpec
    : SimpleTypeSpec '[ReflectionDimension]'
    | SimpleTypeSpec '[ReflectionEmitDimension]'
    ;

ReflectionDimension
    : '*'
    | ReflectionDimension ',' ReflectionDimension
    | NOTOKEN
    ;

ReflectionEmitDimension
    : '*'
    | Number '..' Number
    | Number '…'
    | ReflectionDimension ',' ReflectionDimension
    | NOTOKEN
    ;

Number
    : [0-9]+
    ;

TypeName
    : NamespaceTypeName
    | NamespaceTypeName ',' AssemblyNameSpec
    ;

NamespaceTypeName
    : NestedTypeName
    | NamespaceSpec '.' NestedTypeName
    ;

NestedTypeName
    : IDENTIFIER
    | NestedTypeName '+' IDENTIFIER
    ;

NamespaceSpec
    : IDENTIFIER
    | NamespaceSpec '.' IDENTIFIER
    ;

AssemblyNameSpec
    : IDENTIFIER
    | IDENTIFIER ',' AssemblyProperties
    ;

AssemblyProperties
    : AssemblyProperty
    | AssemblyProperties ',' AssemblyProperty
    ;

AssemblyProperty
    : AssemblyPropertyName '=' AssemblyPropertyValue
    ;
```
<!-- markdownlint-enable MD010 -->

## <a name="specifying-special-characters"></a>특수 문자 지정

형식 이름에서 IDENTIFIER는 언어의 규칙에 따라 결정된 유효한 이름입니다.

백슬래시(\\)를 이스케이프 문자로 사용하여 IDENTIFIER의 일부로 사용된 다음 토큰을 구분합니다.

|토큰|의미|
|-----------|-------------|
|\\,|어셈블리 구분 기호.|
|\\+|중첩된 형식 구분 기호.|
|\\&|참조 형식.|
|\\*|포인터 형식.|
|\\[|배열 차원 구분 기호.|
|\\]|배열 차원 구분 기호.|
|\\.|배열 사양에서 마침표가 사용된 경우에만 마침표 앞에 백슬래시를 사용합니다. NamespaceSpec의 마침표는 백슬래시를 사용하지 않습니다.|
|\\\|필요한 경우 백슬래시를 문자열 리터럴로 사용합니다.|

AssemblyNameSpec을 제외한 모든 TypeSpec 구성 요소에서 공백은 관련이 있습니다. AssemblyNameSpec에서는 ',' 구분 기호 앞의 공백은 관련이 있지만 ',' 구분 기호 뒤의 공백은 무시됩니다.

<xref:System.Type.FullName%2A?displayProperty=nameWithType> 등의 리플렉션 클래스는 `MyType.GetType(myType.FullName)`과 같이 반환된 이름을 <xref:System.Type.GetType%2A> 호출에 사용할 수 있도록 바뀐 이름을 반환합니다.

예를 들어 형식의 정규화된 이름이 `Ozzy.OutBack.Kangaroo+Wallaby,MyAssembly`일 수 있습니다.

네임스페이스가 `Ozzy.Out+Back`이면 더하기 기호 앞에 백슬래시가 와야 합니다. 그렇지 않으면 파서가 중첩 구분 기호로 해석합니다. 리플렉션은 이 문자열을 `Ozzy.Out\+Back.Kangaroo+Wallaby,MyAssembly`로 내보냅니다.

## <a name="specifying-assembly-names"></a>어셈블리 이름 지정

어셈블리 이름 사양에 필요한 최소 정보는 어셈블리의 텍스트 이름(IDENTIFIER)입니다. 다음 표에 설명된 대로 속성/값 쌍의 쉼표로 구분된 목록이 IDENTIFIER 뒤에 와야 합니다. IDENTIFIER 이름 지정은 파일 이름 지정 규칙을 따라야 합니다. IDENTIFIER는 대/소문자를 구분하지 않습니다.

|속성 이름|설명|허용 가능한 값|
|-------------------|-----------------|----------------------|
|**버전**|어셈블리 버전 번호|*Major.Minor.Build.Revision*. 여기서 *Major*, *Minor*, *Build*, *Revision*은 0에서 65535 사이의 정수입니다.|
|**PublicKey**|전체 공개 키|16진수 형식인 전체 공개 키의 문자열 값입니다. null 참조(Visual Basic에서는 **Nothing**)를 지정하여 프라이빗 어셈블리를 명시적으로 나타냅니다.|
|**PublicKeyToken**|공개 키 토큰(전체 공개 키의 8바이트 해시)|16진수 형식인 공개 키 토큰의 문자열 값입니다. null 참조(Visual Basic에서는 **Nothing**)를 지정하여 프라이빗 어셈블리를 명시적으로 나타냅니다.|
|**문화권**|어셈블리 문화권|RFC-1766 형식의 어셈블리 문화권 또는 언어 독립적인(비위성) 어셈블리의 경우 "중립"입니다.|
|**사용자 지정**|사용자 지정 BLOB(Binary Large Object)입니다. 현재 [네이티브 이미지 생성기(Ngen)](../tools/ngen-exe-native-image-generator.md)에서 생성된 어셈블리에서만 사용됩니다.|설치되는 어셈블리가 네이티브 이미지이므로 네이티브 이미지 캐시에 설치해야 함을 어셈블리 캐시에 알리기 위해 네이티브 이미지 생성기 도구에서 사용하는 사용자 지정 문자열입니다. zap 문자열이라고도 합니다.|

다음 예제에서는 기본 문화권을 사용하는 단순한 이름의 어셈블리에 대한 **AssemblyName**을 보여 줍니다.

```csharp
com.microsoft.crypto, Culture=""
```

다음 예제에서는 문화권 "en"을 사용하는 강력한 이름의 어셈블리에 대한 완전히 지정된 참조를 보여 줍니다.

```csharp
com.microsoft.crypto, Culture=en, PublicKeyToken=a5d015c7d5a0b012,
    Version=1.0.0.0
```

다음 예제에서는 각각 강력한 이름 또는 단순한 이름의 어셈블리에 의해 충족될 수 있는 부분적으로 지정된 **AssemblyName**을 보여 줍니다.

```csharp
com.microsoft.crypto
com.microsoft.crypto, Culture=""
com.microsoft.crypto, Culture=en
```

다음 예제에서는 각각 단순한 이름의 어셈블리에 의해 충족되어야 하는 부분적으로 지정된 **AssemblyName**을 보여 줍니다.

```csharp
com.microsoft.crypto, Culture="", PublicKeyToken=null
com.microsoft.crypto, Culture=en, PublicKeyToken=null
```

다음 예제에서는 각각 강력한 이름의 어셈블리에 의해 충족되어야 하는 부분적으로 지정된 **AssemblyName**을 보여 줍니다.

```csharp
com.microsoft.crypto, Culture="", PublicKeyToken=a5d015c7d5a0b012
com.microsoft.crypto, Culture=en, PublicKeyToken=a5d015c7d5a0b012,
    Version=1.0.0.0
```

## <a name="specifying-generic-types"></a>제네릭 형식 지정

SimpleTypeSpec\`NUMBER는 1부터 *n*까지의 제네릭 형식 매개 변수를 갖는 개방형 제네릭 형식을 나타냅니다. 예를 들어, 개방형 제네릭 형식 List\<T> 또는 폐쇄형 제네릭 형식 List\<String>의 참조를 가져오려면 ``Type.GetType("System.Collections.Generic.List`1")``을 사용합니다. 제네릭 형식 Dictionary\<TKey,TValue>의 참조를 가져오려면 ``Type.GetType("System.Collections.Generic.Dictionary`2")``를 사용합니다.

## <a name="specifying-pointers"></a>포인터 지정

SimpleTypeSpec*는 관리되지 않는 포인터를 나타냅니다. 예를 들어 MyType 형식에 대한 포인터를 가져오려면 `Type.GetType("MyType*")`을 사용합니다. MyType 형식에 대한 포인터의 포인터를 가져오려면 `Type.GetType("MyType**")`을 사용합니다.

## <a name="specifying-references"></a>참조 지정

SimpleTypeSpec &은 관리되는 포인터나 참조를 나타냅니다. 예를 들어 MyType 형식에 대한 참조를 가져오려면 `Type.GetType("MyType &")`을 사용합니다. 포인터와 달리 참조는 한 수준으로 제한됩니다.

## <a name="specifying-arrays"></a>배열 지정

BNF 문법에서 ReflectionEmitDimension은 <xref:System.Reflection.Emit.ModuleBuilder.GetType%2A?displayProperty=nameWithType>을 사용하여 검색된 불완전한 형식 정의에만 적용됩니다. 불완전한 형식 정의는 <xref:System.Reflection.Emit?displayProperty=nameWithType>을 사용하여 생성되었지만 <xref:System.Reflection.Emit.TypeBuilder.CreateType%2A?displayProperty=nameWithType>이 호출되지 않은 <xref:System.Reflection.Emit.TypeBuilder> 개체입니다. ReflectionDimension을 사용하여 완성된 형식 정의, 즉 로드된 형식을 검색할 수 있습니다.

배열은 배열의 순위를 지정하여 리플렉션에서 액세스합니다.

- `Type.GetType("MyArray[]")`은 하한이 0인 1차원 배열을 가져옵니다.

- `Type.GetType("MyArray[*]")`은 하한을 알 수 없는 1차원 배열을 가져옵니다.
- `Type.GetType("MyArray[][]")`은 2차원 배열의 배열을 가져옵니다.

- `Type.GetType("MyArray[*,*]")` 및 `Type.GetType("MyArray[,]")`은 하한을 알 수 없는 사각형 2차원 배열을 가져옵니다.

런타임 관점에서는 `MyArray[] != MyArray[*]`이지만, 다차원 배열에서는 두 표기법이 동일합니다. 즉, `Type.GetType("MyArray [,]") == Type.GetType("MyArray[*,*]")`은 **true**입니다.

**ModuleBuilder.GetType**의 경우 `MyArray[0..5]`는 크기가 6, 하한이 0인 1차원 배열을 나타냅니다. `MyArray[4…]`는 크기를 알 수 없고 하한이 4인 1차원 배열을 나타냅니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Reflection.AssemblyName>
- <xref:System.Reflection.Emit.ModuleBuilder>
- <xref:System.Reflection.Emit.TypeBuilder>
- <xref:System.Type.FullName%2A?displayProperty=nameWithType>
- <xref:System.Type.GetType%2A?displayProperty=nameWithType>
- <xref:System.Type.AssemblyQualifiedName%2A?displayProperty=nameWithType>
- [형식 정보 보기](viewing-type-information.md)
