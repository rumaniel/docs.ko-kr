---
title: 비동기 작업
ms.date: 03/30/2017
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.openlocfilehash: 55cb9472c23f09b3f0f248a795dbad62af8ff37f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782610"
---
# <a name="asynchronous-operations"></a>비동기 작업
명령 실행 등의 일부 데이터베이스 작업은 완료하는 데 시간이 오래 걸릴 수 있습니다. 이 경우 단일 스레드 애플리케이션에서는 다른 작업을 차단하고 명령이 종료되기를 기다린 다음 자신의 작업을 계속 수행할 수 있습니다. 그러나 장기 실행 작업을 배경 스레드에 할당할 수 있으면 작업을 수행하는 동안 전경 스레드를 계속 활성화된 상태로 유지할 수 있습니다. 예를 들어, Windows 애플리케이션에서 장기 실행 작업을 배경 스레드에 위임하면 작업을 실행하면서 사용자 인터페이스 스레드가 응답을 유지할 수 있습니다.  
  
 .NET Framework에서는 여러 가지 표준 비동기 디자인 패턴을 제공합니다. 이를 사용하여 개발자가 배경 스레드를 활용하는 것은 물론 사용자 인터페이스나 우선 순위가 높은 스레드에서 얼마든지 다른 작업을 완료할 수 있습니다. ADO.NET은 해당 <xref:System.Data.SqlClient.SqlCommand> 클래스에서 이와 동일한 디자인 패턴을 지원합니다. 특히, <xref:System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:System.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> 및 <xref:System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> 메서드와 쌍을 이루는 <xref:System.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>, <xref:System.Data.SqlClient.SqlCommand.EndExecuteReader%2A> 및 <xref:System.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A> 메서드에서 이와 같은 비동기 작업을 지원합니다.  
  
> [!NOTE]
> 비동기 프로그래밍은 .NET Framework의 핵심 기능이며 ADO.NET에서는 표준 디자인 패턴을 최대한 활용합니다. 개발자에 게 제공 되는 다양 한 비동기 기술에 대 한 자세한 내용은 [동기 메서드를 비동기적으로 호출](../../../../standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)을 참조 하세요.  
  
 비동기 기법을 ADO.NET 기능과 함께 사용하더라도 특별히 고려해야 할 사항은 없지만 앞으로 .NET Framework의 다른 영역보다 ADO.NET의 비동기 기능을 사용하는 개발자의 수가 점차 늘어날 것으로 보입니다. 따라서 다중 스레드 애플리케이션을 만드는 데 대한 이점과 문제점을 반드시 알아두어야 합니다. 이 단원의 뒷부분에 나오는 예제에서는 개발자가 다중 스레드 기능이 통합된 애플리케이션을 빌드할 때 고려해야 할 몇 가지 중요한 문제에 대해 살펴 봅니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [콜백을 사용하는 Windows 애플리케이션](windows-applications-using-callbacks.md)  
 비동기 명령을 안전하게 실행하여 별도의 스레드에서 폼 및 해당 내용과의 상호 작용을 올바르게 처리하는 방법을 보여 주는 예제를 제공합니다.  
  
 [대기 핸들을 사용한 ASP.NET 애플리케이션](aspnet-apps-using-wait-handles.md)  
 ASP.NET 페이지에서 여러 동시 명령을 실행하고 대기 핸들을 사용하여 모든 명령이 완료될 때 작업을 관리하는 방법을 보여 주는 예제를 제공합니다.  
  
 [콘솔 애플리케이션에서 폴링](polling-in-console-applications.md)  
 폴링을 사용하여 콘솔 애플리케이션에서 비동기 명령 실행이 완료되기를 기다리는 방법을 보여 주는 예제를 제공합니다. 이 기법은 클래스 라이브러리나 사용자 인터페이스가 없는 다른 애플리케이션에도 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [SQL Server 및 ADO.NET](index.md)
- [동기 메서드를 비동기 방식으로 호출](../../../../standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)
- [ADO.NET 개요](../ado-net-overview.md)
