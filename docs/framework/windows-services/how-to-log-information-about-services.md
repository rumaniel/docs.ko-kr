---
title: '방법: 서비스에 대한 정보 로깅'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- AutoLog property
- services, logging information
- Windows Service applications, logging information about
- event logs, service applications
- application event logs, service applications
- logs, service applications
ms.assetid: c0d8140f-c055-4d8e-a2e0-37358a550116
author: ghogen
ms.openlocfilehash: 5556b83346aba5bc48eddb930dedc56f4786bdb5
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48036174"
---
# <a name="how-to-log-information-about-services"></a>방법: 서비스에 대한 정보 로깅
기본적으로 모든 Windows 서비스 프로젝트는  응용 프로그램 이벤트 로그와 상호 작용하고 이 로그에 정보 및 예외를 작성할 수 있습니다. <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> 속성을 사용하여 응용 프로그램에서 이 기능을 표시할지 여부를 나타냅니다. 기본적으로, 로깅은 Windows 서비스 프로젝트 템플릿으로 만드는 모든 서비스에 대해 사용 설정됩니다. <xref:System.Diagnostics.EventLog> 클래스의 정적 형식을 사용하면 <xref:System.Diagnostics.EventLog> 구성 요소의 인스턴스를 만들거나 소스를 수동으로 등록하지 않고도 로그에 서비스 정보를 작성할 수 있습니다.  
  
 서비스가 설치되어 있는 컴퓨터에 로깅이 사용 설정되어 있으면, 서비스 설치 관리자가 응용 프로그램 로그를 사용하여 각 서비스를 유효한 이벤트 소스로 프로젝트에 자동으로 등록합니다. 서비스가 시작, 중지, 일시 중지, 다시 시작, 설치 또는 제거될 때마다 서비스가 정보를 기록합니다. 발생되는 오류도 기록합니다. 기본 동작을 사용하는 경우에는 로그에 항목을 쓰기 위해 코드를 작성할 필요가 없습니다. 서비스가 자동으로 처리합니다.  
  
 응용 프로그램 로그가 아닌 이벤트 로그에 작성하려면 <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> 속성을 `false`로 설정하고, 서비스 코드 내에 사용자 지정 이벤트 로그를 만들고, 해당 로그에 대한 유효한 항목 소스로 서비스를 등록해야 합니다. 그런 다음 원하는 작업이 발생할 때마다 항목을 로그에 기록할 코드를 작성해야 합니다.  
  
> [!NOTE]
>  사용자 지정 이벤트 로그를 사용하고 서비스 응용 프로그램이 이 로그에 기록되도록 구성하는 경우, 코드에서 서비스의 <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> 속성을 설정하기 전에 이벤트 로그에 액세스를 시도하지 않아야 합니다. 서비스가 유효한 이벤트 소스로 등록되려면 이벤트 로그에 이 속성 값이 필요합니다.  
  
### <a name="to-enable-default-event-logging-for-your-service"></a>서비스에 대해 기본 이벤트 로깅을 활성화하려면  
  
-   구성 요소의 <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> 속성을 `true`로 설정합니다.  
  
    > [!NOTE]
    >  기본적으로 이 속성은 `true`로 설정됩니다. 조건을 평가한 다음 조건의 결과를 기반으로 <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> 속성을 설정하는 것과 같이 복잡한 프로세스를 구축하는 경우가 아니라면 이 속성을 명시적으로 설정할 필요가 없습니다.  
  
### <a name="to-disable-event-logging-for-your-service"></a>서비스에 대해 이벤트 로깅을 비활성화하려면  
  
-   구성 요소의 <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> 속성을 `false`로 설정합니다.  
  
     [!code-csharp[VbRadconService#17](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#17)]
     [!code-vb[VbRadconService#17](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#17)]  
  
### <a name="to-set-up-logging-to-a-custom-log"></a>사용자 지정 로그에 로깅을 설정하려면  
  
1.  <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> 속성을 `false`으로 설정합니다.  
  
    > [!NOTE]
    >  사용자 지정 로그를 사용하려면 <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> 를 false로 설정해야 합니다.  
  
2.  Windows 서비스 응용 프로그램에서 <xref:System.Diagnostics.EventLog> 구성 요소의 인스턴스를 설정합니다.  
  
3.  <xref:System.Diagnostics.EventLog.CreateEventSource%2A> 메서드를 호출하고 만들려는 로그 파일의 이름과 소스 문자열을 지정하여 사용자 지정 로그를 만듭니다.  
  
4.  <xref:System.Diagnostics.EventLog.Source%2A> 구성 요소 인스턴스의 <xref:System.Diagnostics.EventLog> 속성을 3단계에서 만든 소스 문자열로 설정합니다.  
  
5.  <xref:System.Diagnostics.EventLog.WriteEntry%2A> 구성 요소 인스턴스의 <xref:System.Diagnostics.EventLog> 메서드에 액세스하여 항목을 작성합니다.  
  
     다음 코드에서는 사용자 지정 로그에 로깅을 설정하는 방법을 보여줍니다.  
  
    > [!NOTE]
    >  이 코드 예제에서 <xref:System.Diagnostics.EventLog> 구성 요소의 인스턴스 이름은 `eventLog1` (Visual Basic의 경우`EventLog1` )입니다. 2단계에서 다른 이름의 인스턴스를 만든 경우에는 그에 따라 코드를 변경합니다.  
  
     [!code-csharp[VbRadconService#14](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#14)]
     [!code-vb[VbRadconService#14](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#14)]  
    [!code-csharp[VbRadconService#15](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#15)]
    [!code-vb[VbRadconService#15](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#15)]  
  
## <a name="see-also"></a>참고 항목  
 [Windows 서비스 응용 프로그램 소개](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)
