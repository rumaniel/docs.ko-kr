---
title: "F# 형식"
description: "F # 및 F # 형식 어떻게 명명 및 설명 대 한 사용 되는 형식에 알아봅니다."
keywords: "visual f#, f#, 함수형 프로그래밍"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: c7272a0d-5ab6-4eae-bceb-e49af498b917
ms.openlocfilehash: 9b7235637f301f91ae2cc8fbc59adc27cdfd5bd0
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2017
---
# <a name="f-types"></a><span data-ttu-id="41e7c-104">F# 형식</span><span class="sxs-lookup"><span data-stu-id="41e7c-104">F# Types</span></span>

<span data-ttu-id="41e7c-105">이 항목에서는 F # 및 F # 형식 어떻게 명명 및 설명 대 한 사용 되는 형식에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-105">This topic describes the types that are used in F# and how F# types are named and described.</span></span>


## <a name="summary-of-f-types"></a><span data-ttu-id="41e7c-106">F # 형식 요약</span><span class="sxs-lookup"><span data-stu-id="41e7c-106">Summary of F# Types</span></span>
<span data-ttu-id="41e7c-107">일부 형식은 간주 됩니다 *기본 형식*, 예: 부울 형식 `bool` 및 바이트 수와 문자에 대 한 형식을 포함 하는 다양 한 크기의 정수 계열 및 부동 소수점 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-107">Some types are considered *primitive types*, such as the Boolean type `bool` and integral and floating point types of various sizes, which include types for bytes and characters.</span></span> <span data-ttu-id="41e7c-108">이러한 형식은에 설명 된 [기본 형식](primitive-types.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-108">These types are described in [Primitive Types](primitive-types.md).</span></span>

<span data-ttu-id="41e7c-109">다른 언어에 내장 된 튜플, 목록, 배열, 시퀀스, 레코드, 포함 형식과 구별 된 공용 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-109">Other types that are built into the language include tuples, lists, arrays, sequences, records, and discriminated unions.</span></span> <span data-ttu-id="41e7c-110">다른.NET 언어와 경험이 F # 학습 하는 경우 이러한 각 형식에 대 한 항목은 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-110">If you have experience with other .NET languages and are learning F#, you should read the topics for each of these types.</span></span> <span data-ttu-id="41e7c-111">에 포함 된 이러한 형식에 대 한 자세한 정보에 대 한 링크는 [관련 항목](https://msdn.microsoft.com/library/#rel) 이 항목의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-111">Links to more information about these types are included in the [Related Topics](https://msdn.microsoft.com/library/#rel) section of this topic.</span></span> <span data-ttu-id="41e7c-112">이러한 F #-특정 형식을 함수형 프로그래밍 언어에 공통적인 프로그래밍의 스타일을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-112">These F#-specific types support styles of programming that are common to functional programming languages.</span></span> <span data-ttu-id="41e7c-113">이 형식의 대부분 연결한 F # 라이브러리에서 이러한 형식에서 일반적인 작업을 지 원하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-113">Many of these types have associated modules in the F# library that support common operations on these types.</span></span>

<span data-ttu-id="41e7c-114">함수 형식의 매개 변수 형식에 대 한 정보를 포함 및 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-114">The type of a function includes information about the parameter types and return type.</span></span>

<span data-ttu-id="41e7c-115">.NET Framework에는 개체 형식, 인터페이스 형식, 대리자 형식 및 다른 사용자의 원인입니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-115">The .NET Framework is the source of object types, interface types, delegate types, and others.</span></span> <span data-ttu-id="41e7c-116">다른.NET 언어의 경우와 마찬가지로 사용자 고유의 개체 형식을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-116">You can define your own object types just as you can in any other .NET language.</span></span>

<span data-ttu-id="41e7c-117">F # 코드에서 라는 별칭을 정의할 수는 또한 *형식 약어*, 하는 형식에 대 한 대체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-117">Also, F# code can define aliases, which are named *type abbreviations*, that are alternative names for types.</span></span> <span data-ttu-id="41e7c-118">형식을 나중에 변경 될 수 있습니다 및 형식에 의존 하는 코드를 변경 하지 못하도록 할 때 형식 약어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-118">You might use type abbreviations when the type might change in the future and you want to avoid changing the code that depends on the type.</span></span> <span data-ttu-id="41e7c-119">또는 코드를 읽고 이해 하기 쉽게 만들 수 있는 형식에 대 한 이름으로 형식 약어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-119">Or, you might use a type abbreviation as a friendly name for a type that can make code easier to read and understand.</span></span>

<span data-ttu-id="41e7c-120">F # 함수형 프로그래밍을 염두에 두고 설계 되는 유용한 컬렉션 형식을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-120">F# provides useful collection types that are designed with functional programming in mind.</span></span> <span data-ttu-id="41e7c-121">이러한 컬렉션 형식은 사용 코드 스타일의 기능적를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-121">Using these collection types helps you write code that is more functional in style.</span></span> <span data-ttu-id="41e7c-122">자세한 내용은 참조 [F # 컬렉션 형식](fsharp-collection-types.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-122">For more information, see [F# Collection Types](fsharp-collection-types.md).</span></span>


## <a name="syntax-for-types"></a><span data-ttu-id="41e7c-123">형식에 대 한 구문</span><span class="sxs-lookup"><span data-stu-id="41e7c-123">Syntax for Types</span></span>
<span data-ttu-id="41e7c-124">F # 코드에서는 형식 이름을 작성 해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-124">In F# code, you often have to write out the names of types.</span></span> <span data-ttu-id="41e7c-125">모든 형식에 구문 형식 및 형식 주석을, 추상 메서드 선언, 대리자 선언, 서명 및 기타 구문에서 이러한 구문 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-125">Every type has a syntactic form, and you use these syntactic forms in type annotations, abstract method declarations, delegate declarations, signatures, and other constructs.</span></span> <span data-ttu-id="41e7c-126">인터프리터의 새 프로그램 구조를 선언 하면 때마다 해당 형식에 대 한 구문 및 구문의 이름을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-126">Whenever you declare a new program construct in the interpreter, the interpreter prints the name of the construct and the syntax for its type.</span></span> <span data-ttu-id="41e7c-127">이 구문은 기본 제공 식별자에 대 한 이러한 또는 사용자 정의 형식에 대 한 식별자로만 될 수 있습니다 `int` 또는 `string`만 더 복잡 한 형식에 대 한 구문은 더 복잡 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-127">This syntax might be just an identifier for a user-defined type or a built-in identifier such as for `int` or `string`, but for more complex types, the syntax is more complex.</span></span>

<span data-ttu-id="41e7c-128">다음 표에서 F # 형식에 대 한 구문 측면을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-128">The following table shows aspects of the type syntax for F# types.</span></span>



|<span data-ttu-id="41e7c-129">형식</span><span class="sxs-lookup"><span data-stu-id="41e7c-129">Type</span></span>|<span data-ttu-id="41e7c-130">형식 구문</span><span class="sxs-lookup"><span data-stu-id="41e7c-130">Type syntax</span></span>|<span data-ttu-id="41e7c-131">예제</span><span class="sxs-lookup"><span data-stu-id="41e7c-131">Examples</span></span>|
|----|-----------|--------|
|<span data-ttu-id="41e7c-132">기본 형식</span><span class="sxs-lookup"><span data-stu-id="41e7c-132">primitive type</span></span>|<span data-ttu-id="41e7c-133">*형식 이름*</span><span class="sxs-lookup"><span data-stu-id="41e7c-133">*type-name*</span></span>|`int`<br /><br />`float`<br /><br />`string`|
|<span data-ttu-id="41e7c-134">집계 유형 (클래스, 구조체, 공용 구조체, 레코드, 열거형, 및 등)</span><span class="sxs-lookup"><span data-stu-id="41e7c-134">aggregate type (class, structure, union, record, enum, and so on)</span></span>|<span data-ttu-id="41e7c-135">*형식 이름*</span><span class="sxs-lookup"><span data-stu-id="41e7c-135">*type-name*</span></span>|`System.DateTime`<br /><br />`Color`|
|<span data-ttu-id="41e7c-136">형식 약어</span><span class="sxs-lookup"><span data-stu-id="41e7c-136">type abbreviation</span></span>|<span data-ttu-id="41e7c-137">*형식 약어 이름*</span><span class="sxs-lookup"><span data-stu-id="41e7c-137">*type-abbreviation-name*</span></span>|`bigint`|
|<span data-ttu-id="41e7c-138">정규화 된 형식</span><span class="sxs-lookup"><span data-stu-id="41e7c-138">fully qualified type</span></span>|<span data-ttu-id="41e7c-139">*namespaces.type 이름*</span><span class="sxs-lookup"><span data-stu-id="41e7c-139">*namespaces.type-name*</span></span><br /><br /><span data-ttu-id="41e7c-140">또는</span><span class="sxs-lookup"><span data-stu-id="41e7c-140">or</span></span><br /><br /><span data-ttu-id="41e7c-141">*modules.type 이름*</span><span class="sxs-lookup"><span data-stu-id="41e7c-141">*modules.type-name*</span></span><br /><br /><span data-ttu-id="41e7c-142">또는</span><span class="sxs-lookup"><span data-stu-id="41e7c-142">or</span></span><br /><br /><span data-ttu-id="41e7c-143">*namespaces.modules.type 이름*</span><span class="sxs-lookup"><span data-stu-id="41e7c-143">*namespaces.modules.type-name*</span></span>|`System.IO.StreamWriter`|
|<span data-ttu-id="41e7c-144">array</span><span class="sxs-lookup"><span data-stu-id="41e7c-144">array</span></span>|<span data-ttu-id="41e7c-145">*형식 이름*또는</span><span class="sxs-lookup"><span data-stu-id="41e7c-145">*type-name*[] or</span></span><br /><br /><span data-ttu-id="41e7c-146">*형식 이름* 배열</span><span class="sxs-lookup"><span data-stu-id="41e7c-146">*type-name* array</span></span>|`int[]`<br /><br />`array<int>`<br /><br />`int array`|
|<span data-ttu-id="41e7c-147">2 차원 배열</span><span class="sxs-lookup"><span data-stu-id="41e7c-147">two-dimensional array</span></span>|<span data-ttu-id="41e7c-148">*형식 이름*[,]</span><span class="sxs-lookup"><span data-stu-id="41e7c-148">*type-name*[,]</span></span>|`int[,]`<br /><br />`float[,]`|
|<span data-ttu-id="41e7c-149">3 차원 배열</span><span class="sxs-lookup"><span data-stu-id="41e7c-149">three-dimensional array</span></span>|<span data-ttu-id="41e7c-150">*형식 이름*[,]</span><span class="sxs-lookup"><span data-stu-id="41e7c-150">*type-name*[,,]</span></span>|`float[,,]`|
|<span data-ttu-id="41e7c-151">tuple</span><span class="sxs-lookup"><span data-stu-id="41e7c-151">tuple</span></span>|<span data-ttu-id="41e7c-152">*형식 name1* &#42; *형식 name2* ...</span><span class="sxs-lookup"><span data-stu-id="41e7c-152">*type-name1* &#42; *type-name2* ...</span></span>|<span data-ttu-id="41e7c-153">예를 들어 `(1,'b',3)` 형식이`int * char * int`</span><span class="sxs-lookup"><span data-stu-id="41e7c-153">For example, `(1,'b',3)` has type `int * char * int`</span></span>|
|<span data-ttu-id="41e7c-154">제네릭 형식(generic type)</span><span class="sxs-lookup"><span data-stu-id="41e7c-154">generic type</span></span>|<span data-ttu-id="41e7c-155">*형식 매개 변수* *제네릭 형식 이름*</span><span class="sxs-lookup"><span data-stu-id="41e7c-155">*type-parameter* *generic-type-name*</span></span><br /><br /><span data-ttu-id="41e7c-156">또는</span><span class="sxs-lookup"><span data-stu-id="41e7c-156">or</span></span><br /><br /><span data-ttu-id="41e7c-157">*제네릭 형식 이름을*&lt;*형식 매개 변수 목록*&gt;</span><span class="sxs-lookup"><span data-stu-id="41e7c-157">*generic-type-name*&lt;*type-parameter-list*&gt;</span></span>|`'a list`<br /><br />`list<'a>`<br /><br />`Dictionary<'key, 'value>`|
|<span data-ttu-id="41e7c-158">생성 된 형식 (제공 되는 특정 형식 인수가 있는 제네릭 형식)</span><span class="sxs-lookup"><span data-stu-id="41e7c-158">constructed type (a generic type that has a specific type argument supplied)</span></span>|<span data-ttu-id="41e7c-159">*형식 인수* *제네릭 형식 이름*</span><span class="sxs-lookup"><span data-stu-id="41e7c-159">*type-argument* *generic-type-name*</span></span><br /><br /><span data-ttu-id="41e7c-160">또는</span><span class="sxs-lookup"><span data-stu-id="41e7c-160">or</span></span><br /><br /><span data-ttu-id="41e7c-161">*제네릭 형식 이름을*&lt;*유형 인수 목록*&gt;</span><span class="sxs-lookup"><span data-stu-id="41e7c-161">*generic-type-name*&lt;*type-argument-list*&gt;</span></span>|`int option`<br /><br />`string list`<br /><br />`int ref`<br /><br />`option<int>`<br /><br />`list<string>`<br /><br />`ref<int>`<br /><br />`Dictionary<int, string>`|
|<span data-ttu-id="41e7c-162">단일 매개 변수가 있는 함수 형식</span><span class="sxs-lookup"><span data-stu-id="41e7c-162">function type that has a single parameter</span></span>|<span data-ttu-id="41e7c-163">*매개 변수-type1*  - &gt; *반환 형식*</span><span class="sxs-lookup"><span data-stu-id="41e7c-163">*parameter-type1* -&gt; *return-type*</span></span>|<span data-ttu-id="41e7c-164">사용 하는 함수는 `int` 반환는 `string` 형식이`int -> string`</span><span class="sxs-lookup"><span data-stu-id="41e7c-164">A function that takes an `int` and returns a `string` has type `int -> string`</span></span>|
|<span data-ttu-id="41e7c-165">여러 매개 변수가 있는 함수 형식</span><span class="sxs-lookup"><span data-stu-id="41e7c-165">function type that has multiple parameters</span></span>|<span data-ttu-id="41e7c-166">*매개 변수-type1*  - &gt; *매개 변수 type2*  - &gt; ...-&gt; *반환 형식*</span><span class="sxs-lookup"><span data-stu-id="41e7c-166">*parameter-type1* -&gt; *parameter-type2* -&gt; ... -&gt; *return-type*</span></span>|<span data-ttu-id="41e7c-167">사용 하는 함수는 `int` 및 `float` 반환는 `string` 형식이`int -> float -> string`</span><span class="sxs-lookup"><span data-stu-id="41e7c-167">A function that takes an `int` and a `float` and returns a `string` has type `int -> float -> string`</span></span>|
|<span data-ttu-id="41e7c-168">매개 변수로 고차 함수</span><span class="sxs-lookup"><span data-stu-id="41e7c-168">higher order function as a parameter</span></span>|<span data-ttu-id="41e7c-169">(*함수 형식*)</span><span class="sxs-lookup"><span data-stu-id="41e7c-169">(*function-type*)</span></span>|<span data-ttu-id="41e7c-170">`List.map`형식이`('a -> 'b) -> 'a list -> 'b list`</span><span class="sxs-lookup"><span data-stu-id="41e7c-170">`List.map` has type `('a -> 'b) -> 'a list -> 'b list`</span></span>|
|<span data-ttu-id="41e7c-171">대리자(delegate)</span><span class="sxs-lookup"><span data-stu-id="41e7c-171">delegate</span></span>|<span data-ttu-id="41e7c-172">위임 *함수 형식*</span><span class="sxs-lookup"><span data-stu-id="41e7c-172">delegate of *function-type*</span></span>|`delegate of unit -> int`|
|<span data-ttu-id="41e7c-173">유연한 형식</span><span class="sxs-lookup"><span data-stu-id="41e7c-173">flexible type</span></span>|<span data-ttu-id="41e7c-174">#*형식 이름*</span><span class="sxs-lookup"><span data-stu-id="41e7c-174">#*type-name*</span></span>|`#System.Windows.Forms.Control`<br /><br />`#seq<int>`|

## <a name="related-topics"></a><span data-ttu-id="41e7c-175">관련 항목</span><span class="sxs-lookup"><span data-stu-id="41e7c-175">Related Topics</span></span>


|<span data-ttu-id="41e7c-176">항목</span><span class="sxs-lookup"><span data-stu-id="41e7c-176">Topic</span></span>|<span data-ttu-id="41e7c-177">설명</span><span class="sxs-lookup"><span data-stu-id="41e7c-177">Description</span></span>|
|-----|-----------|
|[<span data-ttu-id="41e7c-178">기본 형식</span><span class="sxs-lookup"><span data-stu-id="41e7c-178">Primitive Types</span></span>](primitive-types.md)|<span data-ttu-id="41e7c-179">정수 계열 형식, 부울 형식 및 문자 형식 같은 기본 제공 단순 형식을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-179">Describes built-in simple types such as integral types, the Boolean type, and character types.</span></span>|
|[<span data-ttu-id="41e7c-180">단위 형식</span><span class="sxs-lookup"><span data-stu-id="41e7c-180">Unit Type</span></span>](unit-type.md)|<span data-ttu-id="41e7c-181">설명의 `unit` 형식, 값이 한 하 여 () 표시 되는 형식;에 해당 `void` C# 및 `Nothing` Visual Basic의 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-181">Describes the `unit` type, a type that has one value and that is indicated by (); equivalent to `void` in C# and `Nothing` in Visual Basic.</span></span>|
|[<span data-ttu-id="41e7c-182">튜플</span><span class="sxs-lookup"><span data-stu-id="41e7c-182">Tuples</span></span>](tuples.md)|<span data-ttu-id="41e7c-183">튜플 형식을 쌍, 삼중 쌍, 상관 등에에서 그룹화 된 모든 형식의 연결 된 값으로 구성 된 형식에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-183">Describes the tuple type, a type that consists of associated values of any type grouped in pairs, triples, quadruples, and so on.</span></span>|
|[<span data-ttu-id="41e7c-184">옵션</span><span class="sxs-lookup"><span data-stu-id="41e7c-184">Options</span></span>](options.md)|<span data-ttu-id="41e7c-185">값 중 하나 이거나 비워 둘 수 있는 형식 옵션 종류를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-185">Describes the option type, a type that may either have a value or be empty.</span></span>|
|[<span data-ttu-id="41e7c-186">목록</span><span class="sxs-lookup"><span data-stu-id="41e7c-186">Lists</span></span>](lists.md)|<span data-ttu-id="41e7c-187">목록을 정렬 되 고 변경할 수 없는 일련의 요소는 설명 동일한 형식의 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-187">Describes lists, which are ordered, immutable series of elements all of the same type.</span></span>|
|[<span data-ttu-id="41e7c-188">배열</span><span class="sxs-lookup"><span data-stu-id="41e7c-188">Arrays</span></span>](arrays.md)|<span data-ttu-id="41e7c-189">인접 한 메모리 블록을 차지 하는 고정된 크기는 동일한 형식의 변경 가능한 요소를 정렬 된 배열에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-189">Describes arrays, which are ordered sets of mutable elements of the same type that occupy a contiguous block of memory and are of fixed size.</span></span>|
|[<span data-ttu-id="41e7c-190">시퀀스</span><span class="sxs-lookup"><span data-stu-id="41e7c-190">Sequences</span></span>](sequences.md)|<span data-ttu-id="41e7c-191">논리 일련의 값을 나타내는 시퀀스 유형을 설명합니다 개별 값이 필요한 경우에 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-191">Describes the sequence type, which represents a logical series of values; individual values are computed only as necessary.</span></span>|
|[<span data-ttu-id="41e7c-192">레코드</span><span class="sxs-lookup"><span data-stu-id="41e7c-192">Records</span></span>](records.md)|<span data-ttu-id="41e7c-193">명명 된 값의 작은 집계 레코드 종류를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-193">Describes the record type, a small aggregate of named values.</span></span>|
|[<span data-ttu-id="41e7c-194">구별된 공용 구조체</span><span class="sxs-lookup"><span data-stu-id="41e7c-194">Discriminated Unions</span></span>](discriminated-unions.md)|<span data-ttu-id="41e7c-195">구별 된 공용 구조체 형식의 값을 가진 가능한 형식 집합 중 하나를 사용할 수는 형식에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-195">Describes the discriminated union type, a type whose values can be any one of a set of possible types.</span></span>|
|[<span data-ttu-id="41e7c-196">함수</span><span class="sxs-lookup"><span data-stu-id="41e7c-196">Functions</span></span>](functions/index.md)|<span data-ttu-id="41e7c-197">함수 값에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-197">Describes function values.</span></span>|
|[<span data-ttu-id="41e7c-198">클래스</span><span class="sxs-lookup"><span data-stu-id="41e7c-198">Classes</span></span>](classes.md)|<span data-ttu-id="41e7c-199">.NET 참조 형식에 해당 하는 개체 형식을 클래스 형식에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-199">Describes the class type, an object type that corresponds to a .NET reference type.</span></span> <span data-ttu-id="41e7c-200">클래스 형식 멤버, 속성, 구현 된 인터페이스 및 기본 형식을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-200">Class types can contain members, properties, implemented interfaces, and a base type.</span></span>|
|[<span data-ttu-id="41e7c-201">구조체</span><span class="sxs-lookup"><span data-stu-id="41e7c-201">Structures</span></span>](structures.md)|<span data-ttu-id="41e7c-202">설명의 `struct` 유형,.NET 값 형식에 해당 하는 개체 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-202">Describes the `struct` type, an object type that corresponds to a .NET value type.</span></span> <span data-ttu-id="41e7c-203">`struct` 형식은 일반적으로 데이터의 작은 집계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-203">The `struct` type usually represents a small aggregate of data.</span></span>|
|[<span data-ttu-id="41e7c-204">인터페이스</span><span class="sxs-lookup"><span data-stu-id="41e7c-204">Interfaces</span></span>](interfaces.md)|<span data-ttu-id="41e7c-205">인터페이스 종류는 특정 기능을 제공 하지만 데이터가 포함 되지 않은 멤버의 집합을 나타내는 형식에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-205">Describes interface types, which are types that represent a set of members that provide certain functionality but that contain no data.</span></span> <span data-ttu-id="41e7c-206">인터페이스 형식은 유용 하 게 되려면 개체 유형별로 구현 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-206">An interface type must be implemented by an object type to be useful.</span></span>|
|[<span data-ttu-id="41e7c-207">대리자</span><span class="sxs-lookup"><span data-stu-id="41e7c-207">Delegates</span></span>](delegates.md)|<span data-ttu-id="41e7c-208">함수 개체를 나타내는 대리자 형식을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-208">Describes the delegate type, which represents a function as an object.</span></span>|
|[<span data-ttu-id="41e7c-209">열거형</span><span class="sxs-lookup"><span data-stu-id="41e7c-209">Enumerations</span></span>](enumerations.md)|<span data-ttu-id="41e7c-210">명명 된 값의 집합에 속하는 값을 해당 하는 열거형 형식에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-210">Describes enumeration types, whose values belong to a set of named values.</span></span>|
|[<span data-ttu-id="41e7c-211">특성</span><span class="sxs-lookup"><span data-stu-id="41e7c-211">Attributes</span></span>](attributes.md)|<span data-ttu-id="41e7c-212">다른 형식에 대 한 메타 데이터를 지정 하는 데 사용 되는 특성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-212">Describes attributes, which are used to specify metadata for another type.</span></span>|
|[<span data-ttu-id="41e7c-213">예외 형식</span><span class="sxs-lookup"><span data-stu-id="41e7c-213">Exception Types</span></span>](exception-handling/exception-types.md)|<span data-ttu-id="41e7c-214">오류 정보를 지정 하는 예외를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41e7c-214">Describes exceptions, which specify error information.</span></span>|