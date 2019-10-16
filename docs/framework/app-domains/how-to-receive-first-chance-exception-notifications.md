---
title: '방법: 첫째 예외 알림 받기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- first-chance exception notifications
- exceptions, first chance notifications
ms.assetid: 66f002b8-a97d-4a6e-a503-2cec01689113
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a17fae64f8cad58b09908212bae4cf62a156ed95
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69921515"
---
# <a name="how-to-receive-first-chance-exception-notifications"></a>방법: 첫째 예외 알림 받기
<xref:System.AppDomain> 클래스의 <xref:System.AppDomain.FirstChanceException> 이벤트를 사용하면 공용 언어 런타임이 예외 처리기 검색을 시작하기 전에 예외가 throw되었다는 알림을 받을 수 있습니다.

 이 이벤트는 애플리케이션 도메인 수준에서 발생합니다. 하나의 실행 스레드가 여러 애플리케이션 도메인을 통과할 수 있으므로 한 애플리케이션 도메인에서 처리되지 않은 예외가 다른 애플리케이션 도메인에서 처리될 수 있습니다. 애플리케이션 도메인이 예외를 처리할 때까지 이벤트 처리기를 추가한 각 애플리케이션 도메인에서 알림이 발생합니다.

 이 문서의 절차 및 예제에서는 애플리케이션 도메인 하나가 있는 간단한 프로그램과 직접 만든 애플리케이션 도메인에서 첫째 예외 알림을 받는 방법을 보여 줍니다.

 여러 애플리케이션 도메인에 걸쳐 있는 좀 더 복잡한 예제의 경우 <xref:System.AppDomain.FirstChanceException> 이벤트에 대한 예제를 참조하세요.

## <a name="receiving-first-chance-exception-notifications-in-the-default-application-domain"></a>기본 애플리케이션 도메인에서 첫째 예외 알림 받기
 다음 절차에서는 애플리케이션에 대한 진입점인 `Main()` 메서드는 기본 애플리케이션 도메인에서 실행됩니다.

#### <a name="to-demonstrate-first-chance-exception-notifications-in-the-default-application-domain"></a>기본 애플리케이션 도메인에서 첫째 예외 알림을 보여 주려면

1. 람다 함수를 사용하여 <xref:System.AppDomain.FirstChanceException> 이벤트에 대한 이벤트 처리기를 정의하고 이벤트에 연결합니다. 이 예제에서 이벤트 처리기는 이벤트가 처리된 애플리케이션 도메인의 이름 및 해당 예외의 <xref:System.Exception.Message%2A> 속성을 출력합니다.

     [!code-csharp[System.AppDomain.FirstChanceException_howto_simple#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/cs/example.cs#2)]
     [!code-vb[System.AppDomain.FirstChanceException_howto_simple#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/vb/example.vb#2)]

2. 예외를 throw 및 catch합니다. 런타임에서 예외 처리기를 찾기 전에 <xref:System.AppDomain.FirstChanceException> 이벤트가 발생하고 메시지를 표시합니다. 이 메시지 다음에는 예외 처리기에 의해 표시되는 메시지가 옵니다.

     [!code-csharp[System.AppDomain.FirstChanceException_howto_simple#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/cs/example.cs#3)]
     [!code-vb[System.AppDomain.FirstChanceException_howto_simple#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/vb/example.vb#3)]

3. 예외를 throw하지만 catch하지 않습니다. 런타임에서 예외 처리기를 찾기 전에 <xref:System.AppDomain.FirstChanceException> 이벤트가 발생하고 메시지를 표시합니다. 예외 처리기가 없으므로 애플리케이션이 종료됩니다.

     [!code-csharp[System.AppDomain.FirstChanceException_howto_simple#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/cs/example.cs#4)]
     [!code-vb[System.AppDomain.FirstChanceException_howto_simple#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/vb/example.vb#4)]

     이 절차의 처음 세 단계에 표시된 코드는 완전한 콘솔 애플리케이션을 구성합니다. 애플리케이션의 출력은 .exe 파일의 이름에 따라 달라집니다. 기본 애플리케이션 도메인의 이름이 .exe 파일의 이름 및 확장명으로 구성되기 때문입니다. 샘플 출력은 다음을 참조하세요.

     [!code-csharp[System.AppDomain.FirstChanceException_howto_simple#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/cs/example.cs#5)]
     [!code-vb[System.AppDomain.FirstChanceException_howto_simple#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/vb/example.vb#5)]

## <a name="receiving-first-chance-exception-notifications-in-another-application-domain"></a>다른 애플리케이션 도메인에서 첫째 예외 알림 받기
 프로그램이 둘 이상의 애플리케이션 도메인을 포함하는 경우 알림을 받는 애플리케이션 도메인을 선택할 수 있습니다.

#### <a name="to-receive-first-chance-exception-notifications-in-an-application-domain-that-you-create"></a>직접 만든 애플리케이션 도메인에서 첫째 예외 알림을 받으려면

1. <xref:System.AppDomain.FirstChanceException> 이벤트에 대한 이벤트 처리기를 정의합니다. 이 예제에서는 이벤트가 처리된 애플리케이션 도메인의 이름 및 해당 예외의 `static` 속성을 출력하는 `Shared` 메서드(Visual Basic에서는 <xref:System.Exception.Message%2A> 메서드)를 사용합니다.

     [!code-csharp[System.AppDomain.FirstChanceException_howto#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/cs/example.cs#3)]
     [!code-vb[System.AppDomain.FirstChanceException_howto#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/vb/example.vb#3)]

2. 애플리케이션 도메인을 만들고 해당 애플리케이션 도메인에 대한 <xref:System.AppDomain.FirstChanceException> 이벤트에 이벤트 처리기를 추가합니다. 이 예제에서 애플리케이션 도메인의 이름은 `AD1`입니다.

     [!code-csharp[System.AppDomain.FirstChanceException_howto#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/cs/example.cs#2)]
     [!code-vb[System.AppDomain.FirstChanceException_howto#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/vb/example.vb#2)]

     동일한 방식으로 기본 애플리케이션 도메인에서 이 이벤트를 처리할 수 있습니다. `Main()`의 `static`(Visual Basic에서는 `Shared`) <xref:System.AppDomain.CurrentDomain%2A?displayProperty=nameWithType> 속성을 사용하여 기본 애플리케이션 도메인에 대한 참조를 가져옵니다.

#### <a name="to-demonstrate-first-chance-exception-notifications-in-the-application-domain"></a>애플리케이션 도메인에서 첫째 예외 알림을 보여 주려면

1. 이전 절차에서 만든 애플리케이션 도메인에 `Worker` 개체를 만듭니다. 이 문서의 끝에 있는 전체 예제와 같이 `Worker` 클래스는 public이어야 하고 <xref:System.MarshalByRefObject>에서 파생되어야 합니다.

     [!code-csharp[System.AppDomain.FirstChanceException_howto#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/cs/example.cs#4)]
     [!code-vb[System.AppDomain.FirstChanceException_howto#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/vb/example.vb#4)]

2. 예외를 throw하는 `Worker` 개체의 메서드를 호출합니다. 이 예제에서는 `Thrower` 메서드가 두 번 호출됩니다. 첫 번째 호출에서는 메서드 인수가 `true`이므로 메서드가 자체 예외를 catch합니다. 두 번째 호출에서는 인수가 `false`이며, `Main()` 메서드가 기본 애플리케이션 도메인에서 예외를 catch합니다.

     [!code-csharp[System.AppDomain.FirstChanceException_howto#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/cs/example.cs#6)]
     [!code-vb[System.AppDomain.FirstChanceException_howto#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/vb/example.vb#6)]

3. `Thrower` 메서드에 코드를 배치하여 메서드가 자체 예외를 처리하는지 여부를 제어합니다.

     [!code-csharp[System.AppDomain.FirstChanceException_howto#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/cs/example.cs#5)]
     [!code-vb[System.AppDomain.FirstChanceException_howto#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/vb/example.vb#5)]

## <a name="example"></a>예
 다음 예제에서는 `AD1`이라는 애플리케이션 도메인을 만들고 애플리케이션 도메인의 <xref:System.AppDomain.FirstChanceException> 이벤트에 이벤트 처리기를 추가합니다. 예제에서는 애플리케이션 도메인에서 `Worker` 클래스 인스턴스를 만들고 <xref:System.ArgumentException>을 throw하는 `Thrower` 메서드를 호출합니다. 인수 값에 따라 메서드가 예외를 catch하거나 예외를 처리하지 못합니다.

 `Thrower` 메서드가 `AD1`에서 예외를 throw할 때마다 `AD1`에서 <xref:System.AppDomain.FirstChanceException> 이벤트가 발생하고 이벤트 처리기가 메시지를 표시합니다. 그러면 런타임이 예외 처리기를 찾습니다. 첫 번째 경우에는 예외 처리기가 `AD1`에 있습니다. 두 번째 경우에는 예외가 `AD1`에서 처리되지 않고 기본 애플리케이션 도메인에서 catch됩니다.

> [!NOTE]
> 기본 애플리케이션 도메인의 이름은 실행 파일의 이름과 같습니다.

 기본 애플리케이션 도메인에 <xref:System.AppDomain.FirstChanceException> 이벤트 처리기를 추가하면 기본 애플리케이션 도메인이 예외를 처리하기 전에 이벤트가 발생하고 처리됩니다. 이를 확인하려면 `Main()`의 시작 부분에 C# 코드 `AppDomain.CurrentDomain.FirstChanceException += FirstChanceException;`(Visual Basic에서는 `AddHandler AppDomain.CurrentDomain.FirstChanceException, FirstChanceException`)을 추가합니다.

 [!code-csharp[System.AppDomain.FirstChanceException_howto#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/cs/example.cs#1)]
 [!code-vb[System.AppDomain.FirstChanceException_howto#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/vb/example.vb#1)]

## <a name="see-also"></a>참고 항목

- <xref:System.AppDomain.FirstChanceException>
