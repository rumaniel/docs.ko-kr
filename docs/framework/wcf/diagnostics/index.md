---
title: 관리 및 진단
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation, diagnostics
- Windows Communication Foundation, administration
- diagnostics [WCF]
- WCF, diagnostics
- administration [WCF]
- WCF, administration
ms.assetid: 34c81c08-0e0f-4fbc-9ae8-91948640ee43
ms.openlocfilehash: dfe169cd6c8d9a643e90e98fc9f22bf116d4335f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795982"
---
# <a name="administration-and-diagnostics"></a>관리 및 진단
WCF (Windows Communication Foundation)는 응용 프로그램 수명의 다양 한 단계를 모니터링 하는 데 도움이 되는 다양 한 기능 집합을 제공 합니다. 예를 들어 구성을 사용하여 배포 시 서비스와 클라이언트를 설정할 수 있습니다. WCF는 응용 프로그램의 성능을 측정 하는 데 도움이 되는 다양 한 성능 카운터 집합을 포함 합니다. 또한 WCF는 WCF WMI(Windows Management Instrumentation) (WMI) 공급자를 통해 런타임에 서비스의 검사 데이터를 노출 합니다. 애플리케이션이 실패하거나 실행을 잘못 시작할 때 이벤트 로그를 사용하여 중요한 이벤트가 발생했는지 여부를 확인할 수 있습니다. 메시지 로깅 및 추적을 사용하여 애플리케이션의 엔드투엔드에 발생한 이벤트를 확인할 수도 있습니다. 이러한 기능을 통해 개발자와 IT 전문가는 올바르게 작동 하지 않을 때 WCF 응용 프로그램의 문제를 해결할 수 있습니다.  
  
> [!NOTE]
> 특정 세부 정보 없이 오류를 수신 하는 경우 [ \<servicedebug >](../../configure-apps/file-schema/wcf/servicedebug.md) 구성 요소의 `includeExceptionDetailInFaults` 특성을 사용 하도록 설정 해야 합니다. 이렇게 하면 WCF가 클라이언트에 예외 정보를 보내도록 지시 하 여 고급 진단을 요구 하지 않고도 많은 일반적인 문제를 검색할 수 있습니다. 자세한 내용은 [오류 전송 및 수신](../sending-and-receiving-faults.md)을 참조 하세요.  
  
## <a name="diagnostics-features-provided-by-wcf"></a>WCF에서 제공하는 진단 기능  
 WCF는 다음과 같은 진단 기능을 제공 합니다.  
  
- 엔드투엔드 추적에서는 디버거를 사용하지 않고 애플리케이션 문제 해결을 위한 계측 데이터를 제공합니다. WCF는 프로세스 마일스 톤 및 오류 메시지에 대 한 추적을 출력 합니다. 여기에는 채널 팩터리 열기 또는 서비스 호스트에서 메시지 보내고 받기 등이 포함될 수 있습니다. 실행 중인 애플리케이션에서는 해당 진행률을 모니터링하기 위해 추적을 사용할 수 있습니다. 자세한 내용은 [추적](./tracing/index.md) 항목을 참조 하세요. 추적을 사용 하 여 응용 프로그램을 디버깅 하는 방법을 이해 하려면 [추적을 사용 하 여 응용 프로그램 문제 해결](./tracing/using-tracing-to-troubleshoot-your-application.md) 항목을 참조 하세요.  
  
- 메시지 로깅을 사용하면 전송 이전과 이후에 메시지가 어떻게 표시되는지 볼 수 있습니다. 자세한 내용은 [메시지 로깅](message-logging.md) 항목을 참조 하세요.  
  
- 이벤트 추적은 모든 주요 문제에 대해 이벤트 로그에 이벤트를 기록합니다. 그런 다음 이벤트 뷰어를 사용하여 비정상적인 상태를 검사할 수 있습니다. 자세한 내용은 [이벤트 로깅](./event-logging/index.md) 항목을 참조 하세요.  
  
- 성능 모니터를 통해 노출된 성능 카운터를 통해 사용자는 애플리케이션과 시스템의 상태를 모니터링할 수 있습니다. 자세한 내용은 [성능 카운터](./performance-counters/index.md) 항목을 참조 하세요.  
  
- <xref:System.ServiceModel.Configuration> 네임스페이스를 통해 구성 파일을 로드하고 서비스 또는 클라이언트 엔드포인트를 설정할 수 있습니다. 여러 컴퓨터에 업데이트를 배포해야 하는 경우, 다양한 애플리케이션에 대한 스크립트 변경 사항에 개체 모델을 사용할 수 있습니다. 또는 [구성 편집기 도구 (SvcConfigEditor)](../configuration-editor-tool-svcconfigeditor-exe.md) 를 사용 하 여 GUI 마법사를 사용 하 여 구성 설정을 편집할 수 있습니다. 자세한 내용은 [응용 프로그램 구성](configuring-your-application.md) 항목을 참조 하세요.  
  
- WMI를 사용하면 서비스가 컴퓨터에서 수신하는 내용 및 사용 중인 바인딩을 확인할 수 있습니다. 자세한 내용은 [진단에 WMI(Windows Management Instrumentation) 사용](./wmi/index.md) 항목을 참조 하세요.  
  
 WCF는 또한 WCF 응용 프로그램을 보다 쉽게 만들고 배포 하 고 관리할 수 있도록 여러 GUI 및 명령줄 도구를 제공 합니다. 자세한 내용은 [Windows Communication Foundation 도구](../tools.md)를 참조 하세요. 예를 들어 [구성 편집기 도구 (SvcConfigEditor)](../configuration-editor-tool-svcconfigeditor-exe.md) 를 사용 하 여 XML을 직접 편집 하는 대신 마법사를 사용 하 여 WCF 구성 설정을 만들고 편집할 수 있습니다. [Service Trace Viewer 도구 (svctraceviewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) 를 사용 하 여 추적 메시지를 보고 그룹화 하 고 필터링 하 여 WCF 서비스 문제를 진단, 복구 및 확인할 수도 있습니다.  
  
## <a name="see-also"></a>참고자료

- [애플리케이션 구성](configuring-your-application.md)
- [서비스 배포](deploying-services.md)
- [예외 참조](./exceptions-reference/index.md)
- [이벤트 로깅](./event-logging/index.md)
- [메시지 로깅](message-logging.md)
- [Configuration Editor 도구(SvcConfigEditor.exe)](../configuration-editor-tool-svcconfigeditor-exe.md)
- [Service Trace Viewer 도구(SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md)
- [ServiceModel 등록 도구](servicemodel-registration-tool.md)
- [추적](./tracing/index.md)
- [진단에 WMI(Windows Management Instrumentation) 사용](./wmi/index.md)
- [성능 카운터](./performance-counters/index.md)
- [Windows Communication Foundation 도구](../tools.md)
