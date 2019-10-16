---
title: 이벤트 개요(Windows Forms)
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, event handling
- events [Windows Forms], about events
- delegates [Windows Forms], multicast
- delegates [Windows Forms], events and
- multicast event delegates
- Windows Forms controls, events
ms.assetid: 814a6a43-a312-4791-88d8-f75f9a4f8c4c
ms.openlocfilehash: 92942066b5f08ada0154781ae54b5d8494944ca1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963469"
---
# <a name="events-overview-windows-forms"></a>이벤트 개요(Windows Forms)
이벤트는 코드에서 응답, 즉 "처리"할 수 있는 작업입니다. 마우스를 클릭하거나 키를 누르는 등의 사용자 작업, 프로그램 코드 또는 시스템에 의해 이벤트가 생성될 수 있습니다.

 이벤트 구동 애플리케이션은 이벤트에 대한 응답으로 코드를 실행합니다. 각 폼과 컨트롤은 미리 정의된 이벤트 집합을 표시하며 이러한 이벤트에 대해 프로그래밍을 수행할 수 있습니다. 이러한 이벤트 중 하나가 발생할 때 연결된 이벤트 처리기에 코드가 있으면 해당 코드가 호출됩니다.

 개체에 의해 발생하는 이벤트 형식은 다양하지만 대부분의 형식은 대다수 컨트롤에 공통적으로 적용됩니다. 예를 들어 대부분의 개체는 <xref:System.Windows.Forms.Control.Click> 이벤트를 처리합니다. 사용자가 폼을 클릭하면 폼의 <xref:System.Windows.Forms.Control.Click> 이벤트 처리기에 포함된 코드가 실행됩니다.

> [!NOTE]
> 대부분의 이벤트는 다른 이벤트와 함께 발생합니다. 예를 들어 <xref:System.Windows.Forms.Control.DoubleClick> 이벤트가 발생하는 과정에서는 <xref:System.Windows.Forms.Control.MouseDown>, <xref:System.Windows.Forms.Control.MouseUp> 및 <xref:System.Windows.Forms.Control.Click> 이벤트도 발생합니다.

 이벤트를 발생 시키고 사용 하는 방법에 대 한 자세한 내용은 [이벤트](../../standard/events/index.md)를 참조 하세요.

## <a name="delegates-and-their-role"></a>대리자 및 해당 역할
 대리자는 이벤트 처리 메커니즘을 빌드하기 위해 .NET Framework 내에서 일반적으로 사용 되는 클래스입니다. 대리자는 일반적으로 시각적 C++ 개체 및 기타 개체 지향 언어에서 사용 되는 함수 포인터와 거의 같습니다. 그러나 함수 포인터와는 달리 대리자는 개체 지향적이고 형식이 안전하며 보안이 유지됩니다. 또한 함수 포인터는 특정 함수에 대한 참조만을 포함하지만 대리자는 개체 참조와 해당 개체 내에 있는 하나 이상의 메서드에 대한 참조로 구성됩니다.

 이 이벤트 모델은 *대리자* 를 사용 하 여 이벤트를 처리 하는 데 사용 되는 메서드에 이벤트를 바인딩합니다. 대리자는 처리기 메서드를 지정하여 다른 클래스가 이벤트 알림을 등록할 수 있도록 설정합니다. 이벤트가 발생하면 대리자가 bound 메서드를 호출합니다. 대리자를 정의 하는 방법에 대 한 자세한 내용은 [이벤트](../../standard/events/index.md)를 참조 하세요.

 대리자는 단일 메서드에 바인딩될 수도 있고 여러 메서드에 바인딩(멀티캐스트)될 수도 있습니다. 이벤트에 대 한 대리자를 만들 때 (또는 Windows)는 일반적으로 멀티 캐스트 이벤트를 만듭니다. 이때 논리적으로 이벤트당 여러 번 반복되지 않는 특정 절차(예: 대화 상자 표시)를 수행하는 이벤트가 드물지만 예외적으로 발생할 수 있습니다. 멀티 캐스트 대리자 [를 만드는 방법에 대 한 자세한 내용은 방법: 대리자 조합 (멀티 캐스트 대리자](../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md))

 멀티캐스트 대리자는 바인딩 대상 메서드의 호출 목록을 유지 관리하며, 호출 목록에 메서드를 추가하기 위한 <xref:System.Delegate.Combine%2A> 메서드와 해당 메서드를 제거하기 위한 <xref:System.Delegate.Remove%2A> 메서드를 지원합니다.

 애플리케이션이 이벤트를 기록하면 컨트롤은 해당 이벤트의 대리자를 호출하여 이벤트를 발생시킵니다. 그러면 대리자는 bound 메서드를 호출합니다. 가장 일반적인 경우(멀티캐스트 대리자)에서 대리자는 호출 목록의 각 bound 메서드를 차례로 호출하므로 일대다 알림이 제공됩니다. 이러한 전략이 사용되므로 컨트롤이 이벤트 알림을 위해 대상 개체 목록을 유지하지 않아도 됩니다. 대리자가 모든 등록과 알림을 처리하기 때문입니다.

 또한 대리자는 여러 이벤트를 같은 메서드에 바인딩할 수 있도록 함으로써 다대일 알림도 허용합니다. 예를 들어 단추 클릭 이벤트와 메뉴 명령 클릭 이벤트 모두가 같은 대리자를 호출할 수 있으며, 이 대리자는 단일 메서드를 호출하여 두 개별 이벤트를 같은 방식으로 처리합니다.

 대리자에는 동적 바인딩 메커니즘이 사용되므로 대리자는 런타임에 서명이 이벤트 처리기의 서명과 일치하는 모든 메서드에 바인딩될 수 있습니다. 이 기능을 사용하면 조건에 따라 bound 메서드를 설정하거나 변경하고 이벤트 처리기를 컨트롤에 동적으로 연결할 수 있습니다.

## <a name="see-also"></a>참고자료

- [Windows Forms에서 이벤트 처리기 만들기](creating-event-handlers-in-windows-forms.md)
- [이벤트 처리기 개요](event-handlers-overview-windows-forms.md)
