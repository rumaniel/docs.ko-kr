---
title: 메시지 로깅에 대한 보안 고려 사항
ms.date: 03/30/2017
ms.assetid: 21f513f2-815b-47f3-85a6-03c008510038
ms.openlocfilehash: c5efd2990a00045e920c005f6658d5fdfb858481
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795938"
---
# <a name="security-concerns-for-message-logging"></a>메시지 로깅에 대한 보안 고려 사항
이 항목에서는 메시지 로깅에 의해 생성된 이벤트뿐 아니라 중요한 데이터가 메시지 로그에서 노출되지 않도록 보호하는 방법에 대해 설명합니다.  
  
## <a name="security-concerns"></a>보안 고려 사항  
  
### <a name="logging-sensitive-information"></a>중요한 정보 로깅  
 WCF (Windows Communication Foundation)는 응용 프로그램별 헤더 및 본문의 데이터를 수정 하지 않습니다. 또한 WCF는 응용 프로그램별 헤더 또는 본문 데이터에서 개인 정보를 추적 하지 않습니다.  
  
 메시지 로깅을 사용하도록 설정하면 쿼리 문자열 등의 애플리케이션별 헤더와 신용 카드 번호 등의 본문 정보에 있는 개인 정보가 로그에 표시될 수 있습니다. 애플리케이션 배포자는 구성 및 로그 파일에 액세스 제어를 적용하는 작업을 담당합니다. 이런 종류의 정보가 표시되지 않도록 하려면 로깅을 사용하지 않도록 설정하거나 로그를 공유하려는 데이터의 일부를 필터링해야 합니다.  
  
 다음 팁은 로그 파일의 내용이 실수로 노출되지 않도록 보호하는 데 도움이 될 수 있습니다.  
  
- 로그 파일이 웹 호스트 및 자체 호스트 시나리오 둘 다에서 ACL(액세스 제어 목록)을 통해 보호되는지 확인합니다.  
  
- 웹 요청을 사용하여 쉽게 제공될 수 없는 파일 확장명을 선택합니다. 예를 들어 .xml 파일 확장명을 사용하는 것은 안전하지 않습니다. 제공될 수 있는 확장명 목록을 보기 위해 IIS(인터넷 정보 서비스) 관리 설명서를 확인할 수 있습니다.  
  
- 로그 파일 위치의 절대 경로를 지정합니다. 절대 경로는 웹 브라우저를 사용하여 외부 사용자가 해당 파일에 액세스하지 못하도록 웹 호스트 vroot 공용 디렉터리의 외부에 있어야 합니다.  
  
 기본적으로 사용자 이름 및 암호와 같은 PII(개인적으로 식별할 수 있는 정보)와 키는 추적 및 기록된 메시지에 기록되지 않습니다. 그러나 컴퓨터 관리자는 Machine.config 파일의 `enableLoggingKnownPII` 요소에 있는 `machineSettings` 특성을 사용하여 컴퓨터에서 실행되는 애플리케이션이 알려진 PII(개인적으로 식별할 수 있는 정보)를 기록하도록 허용할 수 있습니다. 다음 구성 파일에서 이 작업을 수행하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <system.serviceModel>  
      <machineSettings enableLoggingKnownPii="true"/>  
   </system.serviceModel>  
</configuration>   
```  
  
 그런 다음 애플리케이션 배포자는 App.config 또는 Web.config 파일 중 하나에 있는 `logKnownPii` 특성을 사용하여 다음과 같이 PII 로깅을 사용하도록 설정할 수 있습니다.  
  
```xml  
<system.diagnostics>  
  <sources>  
      <source name="System.ServiceModel.MessageLogging"  
        logKnownPii="true">  
        <listeners>  
                 <add name="messages"  
                 type="System.Diagnostics.XmlWriterTraceListener"  
                 initializeData="c:\logs\messages.svclog" />  
          </listeners>  
      </source>  
    </sources>  
</system.diagnostics>  
```  
  
 두 개의 설정 모두 `true`인 경우에만 PII 로깅을 사용하도록 설정할 수 있습니다. 두 스위치를 조합하면 각 애플리케이션에 대해 알려진 PII를 유연하게 기록할 수 있습니다.  
  
> [!IMPORTANT]
> 또한 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]에서 Web.config 파일 또는 App.config 파일의 `logEntireMessage` 및 `logKnownPii` 플래그를 `true`로 설정하여 다음 예제 `<system.serviceModel><messageLogging logEntireMessage="true" logKnownPii="true" …`와 같이 PII 로깅을 사용하도록 설정해야 합니다.  
  
 하나의 구성 파일에서 두 개 이상의 사용자 지정 소스를 지정할 경우 첫 번째 소스의 특성만 읽는다는 점에 유의해야 합니다. 다른 소스는 무시됩니다. 이는 다음 App.config 파일의 경우, 두 번째 소스에 PII 로깅을 사용하도록 명시적으로 설정되어 있더라도 두 개의 소스 모두에 대해 PII가 기록되지는 않는다는 것을 의미합니다.  
  
```xml  
<system.diagnostics>  
   <sources>  
      <source name="System.ServiceModel.MessageLogging"  
              logKnownPii="false">  
              <listeners>  
                 <add name="messages"  
                      type="System.Diagnostics.XmlWriterTraceListener"  
                      initializeData="c:\logs\messages.svclog" />  
              </listeners>  
            </source>  
      <source name="System.ServiceModel"   
              logKnownPii="true">  
              <listeners>  
                 <add name="traces"  
                      type="System.Diagnostics.XmlWriterTraceListener"  
                      initializeData="c:\logs\traces.svclog" />  
              </listeners>  
      </source>  
   </sources>  
</system.diagnostics>  
```  
  
 `<machineSettings enableLoggingKnownPii="Boolean"/>` 요소가 Machine.config 파일의 외부에 존재할 경우 시스템은 <xref:System.Configuration.ConfigurationErrorsException>을 throw합니다.  
  
 변경 내용은 애플리케이션이 시작되거나 다시 시작되어야만 적용됩니다. 두 개의 특성이 모두 `true`로 설정된 경우에 시작 시 이벤트가 기록됩니다. `logKnownPii`가 `true`로 설정되어 있지만 `enableLoggingKnownPii`는 `false`인 경우에도 이벤트가 기록됩니다.  
  
 컴퓨터 관리자와 애플리케이션 배포자는 이러한 두 개의 스위치를 사용할 때 특별히 주의를 기울여야 합니다. PII 로깅을 사용하도록 설정하면 보안 키와 PII가 기록됩니다. PII 로깅을 사용하지 않도록 설정해도 중요한 데이터와 애플리케이션별 데이터는 메시지 헤더 및 본문에 기록됩니다. 개인 정보 보호 및 PII의 노출을 방지 하는 방법에 대 한 자세한 내용은 [사용자 개인 정보](https://go.microsoft.com/fwlink/?LinkID=94647)를 참조 하세요.  
  
> [!CAUTION]
> 잘못된 형식의 메시지에서는 PII가 숨겨지지 않습니다. 이와 같은 메시지는 수정 사항 없이 있는 그대로 기록됩니다. 이전에 언급한 특성은 이에 영향을 주지 않습니다.  
  
### <a name="custom-trace-listener"></a>사용자 지정 추적 수신기  
 관리자에 대해서는 메시지 로깅 추적 소스에 사용자 지정 추적 수신기를 추가하는 권한을 제한해야 합니다. 이는 사용자 지정 수신기가 메시지를 원격으로 보내도록 악의적으로 구성될 수 있으며 이를 통해 중요한 정보가 노출될 수 있기 때문입니다. 또한 원격 데이터베이스와 같은 연결을 통해 메시지를 보내도록 사용자 지정 수신기를 구성할 경우, 원격 컴퓨터의 메시지 로그에 적절한 액세스 제어를 적용해야 합니다.  
  
## <a name="events-triggered-by-message-logging"></a>메시지 로깅을 통해 트리거되는 이벤트  
 다음은 메시지 로깅을 통해 내보내지는 모든 이벤트의 목록입니다.  
  
- 메시지 로깅: 구성에서 메시지 로깅을 사용 하도록 설정 하거나 WMI를 통해이 이벤트를 내보냅니다. 이벤트의 내용은 "메시지 로깅이 켜졌습니다. 메시지 본문과 같이 통신 중에 암호화된 경우에도 중요한 정보가 일반 텍스트로 기록됩니다."입니다.  
  
- 메시지 로깅 해제: 이 이벤트는 WMI를 통해 메시지 로깅을 사용 하지 않도록 설정 하면 내보내집니다. 이벤트의 내용은 "메시지 로깅이 꺼졌습니다."입니다.  
  
- 알려진 PII 기록 위치: 이 이벤트는 알려진 PII의 로깅이 사용 하도록 설정 된 경우에 내보내집니다. Machine.config 파일의 `machineSettings` 요소 `enableLoggingKnownPii` 에 있는 특성이로 `true`설정 되 고 app.config 또는 web.config 파일에 있는 `source` 요소의 특성이로 `logKnownPii` `true`설정된경우이오류가발생합니다.  
  
- 알려진 PII 로그를 사용할 수 없음: 이 이벤트는 알려진 PII의 로깅이 허용 되지 않을 때 내보내집니다. 이는 app.config 또는 `logKnownPii` web.config 파일에 `source` 있는 요소의 특성이로 `true` `enableLoggingKnownPii` 설정 되었지만 machine.config 파일의 `machineSettings` 요소에 있는 특성이로 설정 `false`된경우에발생합니다. 예외가 throw되지 않습니다.  
  
 이러한 이벤트는 Windows에 포함된 이벤트 뷰어 도구에서 볼 수 있습니다. 이에 대 한 자세한 내용은 [이벤트 로깅](./event-logging/index.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [메시지 로깅](message-logging.md)
- [보안 고려 사항 및 추적에 대한 유용한 정보](./tracing/security-concerns-and-useful-tips-for-tracing.md)
