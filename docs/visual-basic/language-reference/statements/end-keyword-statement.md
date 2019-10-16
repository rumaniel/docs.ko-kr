---
title: End <keyword> 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.EndDefinition
helpviewer_keywords:
- End keyword [Visual Basic]
ms.assetid: 42d6e088-ab0f-4cda-88e8-fdce3e5fcf4f
ms.openlocfilehash: 96dc8ce6b0d3b7545f5caeef43358936e426f566
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61638157"
---
# <a name="end-keyword-statement-visual-basic"></a>최종 \<키워드 > 문 (Visual Basic)

추가 키워드 뒤에, 해당 키워드 뒤에 문 블록의 정의가 종료 됩니다.

## <a name="syntax"></a>구문

```vb
End AddHandler
End Class
End Enum
End Event
End Function
End Get
End If
End Interface
End Module
End Namespace
End Operator
End Property
End RaiseEvent  
End RemoveHandler  
End Select
End Set
End Structure
End Sub
End SyncLock
End Try
End While
End With  
```  
  
## <a name="parts"></a>요소

|파트|설명|
|---|---|
|`End`|필수. 프로그래밍 요소의 정의 종료합니다.|
|`AddHandler`|종료 하는 데 필요한를 `AddHandler` 일치 하는 시작 하는 접근자 `AddHandler` 사용자 지정에서 문을 [이벤트 연결 문으로](event-statement.md)합니다.|
|`Class`|일치 하는 시작 클래스 정의 종료 하는 데 필요한 [Class 문](class-statement.md)합니다.|
|`Enum`|일치 하는 시작 된 열거형 정의 종료 하는 데 필요한 [Enum 문](enum-statement.md)합니다.|
|`Event`|종료 하는 데 필요한를 `Custom` 일치 하는 시작 하는 이벤트 정의 [이벤트 연결 문으로](event-statement.md)합니다.|  
|`Function`|종료 하는 데 필요한를 `Function` 일치 하는 시작 하는 프로시저 정의 [Function 문](function-statement.md)합니다. 실행 하는 경우는 `End Function` 문을 컨트롤이 호출 코드에 반환 합니다.|
|`Get`|종료 하는 데 필요한를 `Property` 일치 하는 시작 하는 프로시저 정의 [Get 문은](get-statement.md)합니다. 실행 하는 경우는 `End Get` 문을 컨트롤 속성의 값을 요청 하는 문으로 반환 합니다.|
|`If`|종료 하는 데 필요한는 `If`... `Then`... `Else` 일치 하는 시작 된 정의 차단 `If` 문입니다. 참조 [경우... 다음 중... Else 문](if-then-else-statement.md)합니다.|
|`Interface`|일치 하는 시작 된 인터페이스 정의 종료 하는 데 필요한 [Interface 문](interface-statement.md)합니다.|
|`Module`|일치 하는 시작 모듈 정의 종료 하는 데 필요한 [Module 문](module-statement.md)합니다.|
|`Namespace`|일치 하는 시작 된 네임 스페이스 정의 종료 하는 데 필요한 [Namespace 문](namespace-statement.md)합니다.|
|`Operator`|일치 하는 시작 하는 연산자 정의 종료 하는 데 필요한 [Operator 문](operator-statement.md)합니다.|
|`Property`|일치 하는 시작 속성 정의 종료 하는 데 필요한 [Property 문](property-statement.md)합니다.|
|`RaiseEvent`|종료 하는 데 필요한를 `RaiseEvent` 일치 하는 시작 하는 접근자 `RaiseEvent` 사용자 지정에서 문을 [이벤트 연결 문으로](event-statement.md)합니다.|
|`RemoveHandler`|종료 하는 데 필요한를 `RemoveHandler` 일치 하는 시작 하는 접근자 `RemoveHandler` 사용자 지정에서 문을 [이벤트 연결 문으로](event-statement.md)합니다.|
|`Select`|종료 하는 데 필요한를 `Select`... `Case` 일치 하는 시작 된 정의 차단 `Select` 문입니다. 참조 [선택... Case 문](select-case-statement.md)합니다.  
|`Set`|종료 하는 데 필요한를 `Property` 일치 하는 시작 하는 프로시저 정의 [Set 문을](set-statement.md)합니다. 실행 하는 경우는 `End Set` 문을 컨트롤 속성의 값을 설정 하는 문으로 반환 합니다.  
|`Structure`|일치 하는 시작 된 구조 정의 종료 하는 데 필요한 [Structure 문을](structure-statement.md)합니다.  
|`Sub`|종료 하는 데 필요한를 `Sub` 일치 하는 시작 하는 프로시저 정의 [Sub 문](sub-statement.md)합니다. 실행 하는 경우는 `End Sub` 문을 컨트롤이 호출 코드에 반환 합니다.  
|`SyncLock`|종료 하는 데 필요한를 `SyncLock` 일치 하는 시작 된 정의 차단 `SyncLock` 문입니다. 참조 [SyncLock 문](synclock-statement.md)합니다.  
|`Try`|종료 하는 데 필요한를 `Try`... `Catch`... `Finally` 일치 하는 시작 된 정의 차단 `Try` 문입니다. 참조 [시도 하는 중... Catch 하는 중... Finally 문](try-catch-finally-statement.md)합니다.  
|`While`|종료 하는 데 필요한를 `While` 일치 하는 시작 된 정의 루프 `While` 문입니다. 참조 [하는 동안... While 문 종료](while-end-while-statement.md)합니다.  
|`With`| 종료 하는 데 필요한를 `With` 일치 하는 시작 된 정의 차단 `With` 문입니다. 참조 [사용 하 여는 중... 문을 사용 하 여 종료](with-end-with-statement.md)합니다.  
|||
  
## <a name="directives"></a>지시문

앞에 숫자 기호 (`#`), `End` 키워드는 해당 지시문에 도입 된 전처리 블록을 종료 합니다.  

```vb
#End ExternalSource
#End If
#End Region
```

|파트|설명|
|---|---|
|`#End`|필수. 전처리 블록의 정의 종료합니다.|
|`ExternalSource`|일치 하는 시작 하는 외부 소스 블록을 종료 하는 데 필요한 [#ExternalSource 지시문](../directives/externalsource-directive.md)합니다.|
|`If`|일치 하는 시작 된 조건부 컴파일 블록을 종료 하는 데 필요한 `#If` 지시문입니다. 참조 [#If... Then... #Else 지시문](../directives/if-then-else-directives.md)합니다.|
|`Region`|일치 하는 시작 된 소스 영역 블록을 종료 하는 데 필요한 [#Region 지시문](../directives/region-directive.md)합니다.|
|||

## <a name="remarks"></a>설명

합니다 [End 문](end-statement.md), 추가 키워드, 실행을 즉시 종료 합니다.

## <a name="smart-device-developer-notes"></a>스마트 장치 개발자 노트  

`End` 추가 키워드, 문이 지원 되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [End 문](end-statement.md)
