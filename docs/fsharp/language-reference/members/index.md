---
title: 멤버
description: 개체 멤버에 대 한 알아봅니다는 F# 프로그래밍 언어입니다.
ms.date: 05/16/2016
ms.openlocfilehash: 0da704b637a9421aa150aa8d8de504bec858e252
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645150"
---
# <a name="members"></a>멤버

이 섹션에서는 F# 개체 형식의 멤버에 대해 설명합니다.

## <a name="remarks"></a>설명

*멤버*는 형식 정의의 일부인 기능이며 `member` 키워드로 선언됩니다. 레코드, 클래스, 구분된 공용 구조체, 인터페이스, 구조체와 같은 F# 개체 형식에서는 멤버를 지원합니다. 자세한 내용은 [레코드](../records.md), [클래스](../classes.md), [구분된 공용 구조체](../discriminated-Unions.md), [인터페이스](../interfaces.md), 및 [구조체](../structures.md)를 참조하세요.

멤버는 일반적으로 특정 형식의 공용 인터페이스를 구성합니다. 이것이 달리 지정된 경우가 아니라면 멤버가 public인 이유입니다. 멤버는 private 또는 internal로 선언될 수도 있습니다. 자세한 내용은 [액세스 제어](../access-Control.md)를 참조하세요. 형식에 대한 시그니처는 특정 형식의 특정 멤버를 노출하거나 노출하지 않는 데에도 사용할 수 있습니다. 자세한 내용은 [시그니처](../signatures.md)를 참조하세요.

Private 필드 및 `do` 바인딩(클래스에만 사용됨)은 특정 형식의 공용 인터페이스의 일부가 아니며 `member` 키워드로 선언되지 않아서 실제 멤버가 아니지만 이 섹션에 설명되어 있습니다.

## <a name="related-topics"></a>관련 항목

|항목|설명|
|-----|-----------|
|[클래스의 `let` 바인딩](let-bindings-in-classes.md)|클래스의 private 필드 및 함수에 대한 정의에 대해 설명합니다.|
|[클래스의 `do` 바인딩](do-bindings-in-classes.md)|개체 초기화 코드의 사양에 대해 설명합니다.|
|[속성](properties.md)|클래스 및 기타 형식의 속성 멤버에 대해 설명합니다.|
|[인덱싱된 속성](indexed-properties.md)|기타 형식 및 클래스의 배열 형식의 속성에 대해 설명합니다.|
|[메서드](methods.md)|특정 형식의 멤버인 함수에 대해 설명합니다.|
|[생성자](constructors.md)|특정 형식의 개체를 초기화하는 특수 함수에 대해 설명합니다.|
|[연산자 오버로드](../operator-overloading.md)|형식에 대한 사용자 지정된 연산자 정의에 대해 설명합니다.|
|[이벤트](events.md)|F#의 이벤트 및 이벤트 처리 지원에 대한 정의에 대해 설명합니다.|
|[명시적 필드: `val` 키워드](explicit-fields-the-val-keyword.md)|특정 형식의 초기화되지 않은 필드에 대한 정의에 대해 설명합니다.|
