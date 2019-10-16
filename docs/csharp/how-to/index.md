---
title: 방법 문서(C# 가이드)
description: 유용한 팁 및 간단하고 집중된 코드 샘플의 컬렉션
ms.date: 12/20/2017
ms.openlocfilehash: f764bd0183e3881bfb81ebda7d3c7dd49a4cbdde
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71591604"
---
# <a name="how-to-c"></a>방법(C#)

C# 가이드의 방법 섹션에서 일반적인 질문에 대한 빠른 답변을 찾을 수 있습니다. 경우에 따라 문서는 여러 섹션에 나타날 수 있습니다. 여러 검색 경로를 쉽게 찾을 수 있도록 했습니다.

## <a name="general-c-concepts"></a>일반 C# 개념

일반적인 C# 개발자 사례인 몇 가지 유용한 정보가 있습니다.

- [개체 이니셜라이저를 사용하여 개체를 초기화합니다](../programming-guide/classes-and-structs/how-to-initialize-objects-by-using-an-object-initializer.md).
- [메서드에 구조체를 전달하는 것과 클래스를 전달하는 것의 차이점에 대해 알아보세요](../programming-guide/classes-and-structs/how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method.md).
- [연산자 오버로드를 사용합니다](../language-reference/operators/operator-overloading.md).
- [사용자 지정 확장 메서드를 구현하고 호출합니다](../programming-guide/classes-and-structs/how-to-implement-and-call-a-custom-extension-method.md).
- C# 프로그래머조차도 [VB에서 `My` 네임스페이스를 사용](../programming-guide/namespaces/how-to-use-the-my-namespace.md)하려 할 수 있습니다.
- [확장 메서드를 사용하여 `enum` 형식에 대해 새 메서드를 만듭니다](../programming-guide/classes-and-structs/how-to-create-a-new-method-for-an-enumeration.md).

### <a name="class-and-struct-members"></a>클래스 및 구조체 멤버

구조체 및 클래스를 만들어 프로그램을 구현합니다. 이러한 기술은 클래스 또는 구조체를 작성할 때 자주 사용됩니다.

- [자동 구현 속성을 선언합니다](../programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties.md).
- [읽기/쓰기 속성을 선언하고 사용합니다](../programming-guide/classes-and-structs/how-to-declare-and-use-read-write-properties.md).
- [상수를 정의합니다](../programming-guide/classes-and-structs/how-to-define-constants.md).
- [`ToString` 메서드를 재정의하여 문자열 출력을 제공합니다](../programming-guide/classes-and-structs/how-to-override-the-tostring-method.md).
- [추상 속성을 정의합니다](../programming-guide/classes-and-structs/how-to-define-abstract-properties.md).
- [XML 문서 기능을 사용하여 코드를 문서화합니다](../programming-guide/xmldoc/how-to-use-the-xml-documentation-features.md).
- [인터페이스 멤버를 명시적으로 구현하여](../programming-guide/interfaces/how-to-explicitly-implement-interface-members.md) 공용 인터페이스 간소화를 유지합니다.
- [두 인터페이스의 멤버를 명시적으로 구현합니다](../programming-guide/interfaces/how-to-explicitly-implement-members-of-two-interfaces.md).

### <a name="working-with-collections"></a>컬렉션으로 작업

이러한 문서를 통해 데이터의 컬렉션으로 작업할 수 있습니다.

- [컬렉션 이니셜라이저를 사용하여 사전을 초기화합니다](../programming-guide/classes-and-structs/how-to-initialize-a-dictionary-with-a-collection-initializer.md).

## <a name="working-with-strings"></a>문자열 작업

문자열은 텍스트를 표시하거나 조작하는 데 사용되는 기본 데이터 형식입니다. 이러한 문서는 문자열이 포함된 일반적인 사례를 보여줍니다.

- [문자열을 비교합니다](compare-strings.md).
- [문자열의 내용을 수정합니다](modify-string-contents.md).
- [문자열이 숫자를 나타내는지 여부를 확인합니다](../programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md).
- [`String.Split`를 사용하여 문자열을 구분합니다](parse-strings-using-split.md).
- [여러 문자열을 하나로 결합합니다](concatenate-multiple-strings.md).
- [문자열 내에서 텍스트를 검색합니다](search-strings.md).

## <a name="convert-between-types"></a>형식 변환

한 개체를 다른 형식으로 변환해야 하는 경우가 있습니다.

- [문자열이 숫자를 나타내는지 여부를 확인합니다](../programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md).
- [16진수를 나타내는 문자열과 숫자 사이를 변환합니다](../programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md).
- [문자열을 `DateTime`로 변환합니다](../../standard/base-types/parsing-datetime.md).
- [바이트 배열을 정수로 변환합니다](../programming-guide/types/how-to-convert-a-byte-array-to-an-int.md).
- [문자열을 숫자로 변환합니다](../programming-guide/types/how-to-convert-a-string-to-a-number.md).
- [패턴 일치, `as` 및 `is` 연산자를 사용하여 안전하게 다른 형식으로 캐스팅합니다](../how-to/safely-cast-using-pattern-matching-is-and-as-operators.md).
- [사용자 지정 형식 변환을 정의합니다](../language-reference/operators/user-defined-conversion-operators.md).
- [형식이 nullable 값 형식인지 여부를 확인합니다](../programming-guide/nullable-types/how-to-identify-a-nullable-type.md).
- [nullable과 비 nullable 값 형식 사이를 변환합니다](../programming-guide/nullable-types/using-nullable-types.md#conversion-from-a-nullable-value-type-to-an-underlying-type).

## <a name="equality-and-ordering-comparisons"></a>같음 및 순서 비교

같음에 대한 자체 규칙을 정의하거나 해당 형식의 개체 간의 자연 정렬을 정의하는 형식을 만들 수 있습니다.

- [참조 기반 같음을 테스트합니다](../programming-guide/statements-expressions-operators/how-to-test-for-reference-equality-identity.md).
- [형식에 대해 값 기반 값음을 정의합니다](../programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md).

## <a name="exception-handling"></a>예외 처리

.NET 프로그램은 메서드가 예외를 throw하여 작업을 성공적으로 완료되지 않았음을 보고합니다. 이 문서에서는 예외를 사용하는 방법에 대해 살펴보겠습니다.

- [`try` 및 `catch`를 사용하여 예외를 처리합니다](../programming-guide/exceptions/how-to-handle-an-exception-using-try-catch.md).
- [`finally` 절을 사용하여 리소스를 정리합니다](../programming-guide/exceptions/how-to-execute-cleanup-code-using-finally.md).
- [비 CLS(공용 언어 사양) 예외에서 복구합니다](../programming-guide/exceptions/how-to-catch-a-non-cls-exception.md).

## <a name="delegates-and-events"></a>대리자 및 이벤트

대리인과 이벤트는 느슨하게 결합된 코드 블록을 포함하는 전략에 대한 기능을 제공합니다.

- [대리자를 선언하고, 인스턴스화하고, 사용합니다](../programming-guide/delegates/how-to-declare-instantiate-and-use-a-delegate.md).
- [멀티캐스트 대리자를 결합합니다](../programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md).

이벤트는 알림을 구독하거나 게시하는 메커니즘을 제공합니다.

- [이벤트를 구독하거나 구독 취소합니다](../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).
- [인터페이스에서 선언된 이벤트를 구현합니다](../programming-guide/events/how-to-implement-interface-events.md).
- [코드가 이벤트를 게시할 때 .NET Framework 지침을 준수합니다](../programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md).
- [파생된 클래스로부터 기본 클래스에서 정의된 이벤트를 발생시킵니다](../programming-guide/events/how-to-raise-base-class-events-in-derived-classes.md).
- [사용자 지정 이벤트 접근자를 구현합니다](../programming-guide/events/how-to-implement-custom-event-accessors.md).

## <a name="linq-practices"></a>LINQ 사례

LINQ를 사용하면 LINQ 쿼리 식 패턴을 지원하는 데이터 소스를 쿼리하는 코드를 작성할 수 있습니다. 이러한 문서는 패턴을 이해하고 다른 데이터 원본으로 작업하는 데 도움이 됩니다.

- [컬렉션을 쿼리합니다](../programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md).
- [쿼리에서 람다 식을 사용합니다](../programming-guide/statements-expressions-operators/how-to-use-lambda-expressions-in-a-query.md).
- [쿼리 식에서 `var`를 사용합니다](../programming-guide/classes-and-structs/how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression.md).
- [쿼리에서 요소 속성의 하위 집합을 반환합니다](../programming-guide/classes-and-structs/how-to-return-subsets-of-element-properties-in-a-query.md).
- [복합 필터링으로 쿼리를 작성합니다](../programming-guide/concepts/linq/how-to-write-queries-with-complex-filtering.md).
- [데이터 원본의 요소를 정렬합니다](../programming-guide/concepts/linq/how-to-sort-elements.md).
- [여러 키로 요소를 정렬합니다](../programming-guide/concepts/linq/how-to-sort-elements-on-multiple-keys.md).
- [프로젝션 형식을 제어합니다](../programming-guide/concepts/linq/how-to-control-the-type-of-a-projection.md).
- [소스 시퀀스에서 값의 발생 수를 카운트합니다](../programming-guide/concepts/linq/how-to-count-occurrences-of-a-word-in-a-string-linq.md).
- [중간 값을 계산합니다](../programming-guide/concepts/linq/how-to-calculate-intermediate-values.md).
- [여러 원본의 데이터를 병합합니다](../programming-guide/concepts/linq/how-to-populate-object-collections-from-multiple-sources-linq.md).
- [두 시퀀스 간의 차집합을 반환합니다](../programming-guide/concepts/linq/how-to-find-the-set-difference-between-two-lists-linq.md).
- [빈 쿼리 결과를 디버깅합니다](../programming-guide/concepts/linq/how-to-debug-empty-query-results-sets.md).
- [사용자 지정 메서드를 LINQ 쿼리에 추가합니다](../programming-guide/concepts/linq/how-to-add-custom-methods-for-linq-queries.md).

## <a name="multiple-threads-and-async-processing"></a>여러 스레드 및 비동기 처리

최신 프로그램은 종종 비동기 작업을 사용합니다. 이러한 문서를 통해 이러한 기법을 사용하는 방법을 배울 수 있습니다.

- [`System.Threading.Tasks.Task.WhenAll`를 사용하여 비동기 성능을 개선합니다](../programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md).
- [`async` 및 `await`를 사용하여 여러 웹을 동시에 요청합니다](../programming-guide/concepts/async/how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md).
- [스레드 풀을 사용합니다](../../standard/threading/the-managed-thread-pool.md#using-the-thread-pool).

## <a name="command-line-args-to-your-program"></a>프로그램에 대한 명령줄 인수

일반적으로 C# 프로그램에는 명령줄 인수가 있습니다. 이 문서에서는 이러한 명령줄 인수를 액세스하고 처리하는 방법을 배울 수 있습니다.

- [`for`가 포함된 모든 명령줄 인수를 검색합니다](../programming-guide/main-and-command-args/how-to-display-command-line-arguments.md).
