---
title: 보안 고려 사항 및 추적에 대한 유용한 정보
ms.date: 03/30/2017
ms.assetid: 88bc2880-ecb9-47cd-9816-39016a07076f
ms.openlocfilehash: d1b2c13cacc792ecedacfc3ede7c38e072841263
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64600045"
---
# <a name="security-concerns-and-useful-tips-for-tracing"></a>보안 고려 사항 및 추적에 대한 유용한 정보
이 항목에서는 WebHost를 사용할 때의 유용한 팁뿐만 아니라 중요한 정보가 노출되지 않도록 보호할 수 있는 방법에 대해 설명합니다.  
  
## <a name="using-a-custom-trace-listener-with-webhost"></a>WebHost에 사용자 지정 추적 수신기 사용  
 고유한 추적 수신기를 작성하는 경우 웹 호스팅 서비스에서는 추적이 손실될 가능성이 있다는 것을 알고 있어야 합니다. WebHost가 재활용되면 복제가 수행되는 동안 활성 프로세스가 종료됩니다. 그러나 두 프로세스에는 같은 리소스에 액세스할 권한이 있어야 하며, 이는 수신기 형식에 따라 다릅니다. 이 경우 `XmlWriterTraceListener`는 두 번째 프로세스에 대한 새 추적 파일을 만들지만, Windows 이벤트 추적은 동일한 세션 내의 여러 프로세스를 관리하고 동일한 파일에 대한 액세스 권한을 부여합니다. 수신기에서 비슷한 기능을 제공하지 않으면 두 프로세스에서 파일을 잠근 경우 추적이 손실될 수 있습니다.  
  
 사용자 지정 추적 수신기에서 원격 데이터베이스와 같은 연결을 통해 추적 및 메시지를 보낼 수 있는지도 알아야 합니다. 애플리케이션 개발자는 적절한 액세스 권한으로 사용자 지정 수신기를 구성해야 합니다. 원격 위치에서 노출될 수 있는 개인 정보에 보안 컨트롤을 적용할 수도 있습니다.  
  
## <a name="logging-sensitive-information"></a>중요한 정보 로깅  
 메시지가 범위 내에 있으면 추적에 메시지 헤더가 포함됩니다. 추적을 사용하도록 설정하면 쿼리 문자열 등의 애플리케이션별 헤더와 신용 카드 번호 등의 본문 정보에 있는 개인 정보가 로그에서 표시될 수 있습니다. 애플리케이션 배포자는 구성 및 추적 파일에 액세스 제어를 적용하는 작업을 담당합니다. 이런 종류의 정보가 표시되지 않도록 하려면 추적을 사용하지 않도록 설정하거나 추적 로그를 공유하려는 데이터의 일부를 필터링해야 합니다.  
  
 다음 팁은 추적 파일의 내용이 실수로 노출되지 않도록 보호하는 데 도움이 될 수 있습니다.  
  
- 로그 파일이 WebHost 및 자체 호스트 시나리오 둘 다에서 ACL(액세스 제어 목록)을 통해 보호되는지 확인합니다.  
  
- 웹 요청을 사용하여 쉽게 제공될 수 없는 파일 확장명을 선택합니다. 예를 들어 .xml 파일 확장명을 사용하는 것은 안전하지 않습니다. 제공될 수 있는 확장명 목록을 보기 위해 IIS 관리 설명서를 확인할 수 있습니다.  
  
- 로그 파일 위치의 절대 경로를 지정합니다. 절대 경로는 웹 브라우저를 사용하여 외부 사용자가 해당 파일에 액세스하지 못하도록 WebHost vroot 공용 디렉터리의 외부에 있어야 합니다.  
  
 기본적으로 사용자 이름 및 암호와 같은 PII(개인적으로 식별할 수 있는 정보)와 키는 추적 및 기록된 메시지에 기록되지 않습니다. 그러나 컴퓨터 관리자는 다음과 같이 Machine.config 파일의 `enableLoggingKnownPII` 요소에 있는 `machineSettings` 특성을 사용하여 컴퓨터에서 실행되는 애플리케이션이 알려진 PII(개인적으로 식별할 수 있는 정보)를 기록하도록 허용할 수 있습니다.  
  
```xml  
<configuration>  
   <system.ServiceModel>  
      <machineSettings enableLoggingKnownPii="Boolean"/>  
   </system.ServiceModel>  
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
            <add name="xml" />  
         </listeners>  
      </source>  
  </sources>  
</system.diagnostics>  
```  
  
 `<machineSettings enableLoggingKnownPii="Boolean"/>` 요소가 Machine.config 파일의 외부에 존재할 경우 시스템은 <xref:System.Configuration.ConfigurationErrorsException>을 throw합니다.  
  
 변경 내용은 애플리케이션이 시작되거나 다시 시작되어야만 적용됩니다. 두 개의 특성이 모두 `true`로 설정된 경우에 시작 시 이벤트가 기록됩니다. `logKnownPii`가 `true`로 설정되어 있지만 `enableLoggingKnownPii`는 `false`인 경우에도 이벤트가 기록됩니다.  
  
 PII 로깅에 대 한 자세한 내용은 참조 하세요. [PII 보안 잠금](../../../../../docs/framework/wcf/samples/pii-security-lockdown.md) 샘플입니다.  
  
 컴퓨터 관리자와 애플리케이션 배포자는 이러한 두 개의 스위치를 사용할 때 특별히 주의를 기울여야 합니다. PII 로깅을 사용하도록 설정하면 보안 키와 PII가 기록됩니다. PII 로깅을 사용하지 않도록 설정해도 중요한 데이터와 애플리케이션별 데이터는 메시지 헤더 및 본문에 기록됩니다. 개인 정보 및 PII 노출 되지 않도록 보호에 대 한 더 상세히 논의 참조 하세요 [사용자 개인 정보 보호](https://go.microsoft.com/fwlink/?LinkID=94647)합니다.  
  
 또한, 연결 지향 전송에 대한 연결마다 한 번, 그리고 그렇지 않게 전송된 메시지마다 한 번 메시지 발신자의 IP 주소가 기록됩니다. 이 작업은 발신자의 동의 없이 수행됩니다. 그러나 이 로깅은 Information 또는 Verbose 추적 수준에서만 발생하며 이러한 수준은 라이브 디버깅을 제외하고 프로덕션에서 기본 추적 수준 또는 권장 추적 수준이 아닙니다.  
  
## <a name="see-also"></a>참고자료

- [추적](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)
