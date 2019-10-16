---
title: CustomChannelsTester
ms.date: 03/30/2017
ms.assetid: ee1fa307-98b1-4647-8860-2e9217ba6082
ms.openlocfilehash: 0d77af319e18868ce7d600269cd9afaa0c4ce2c6
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928640"
---
# <a name="customchannelstester"></a>CustomChannelsTester
`CustomChannelsTester`는 미리 정의된 서비스 계약 집합에 대해 사용자 지정 채널 구현을 테스트하는 데 사용할 수 있는 도구입니다. 서비스 계약 집합을 선택한 다음 XML 파일을 사용하여 이 도구에 전달할 수 있습니다. 그러면 이 도구는 메시지 교환 중에 사용자 지정 채널 구현을 연습하는 서비스와 클라이언트를 생성합니다.  
  
### <a name="to-build-the-tool"></a>도구를 빌드하려면  
  
1. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.  
  
2. 솔루션 빌드는 세 개의 파일을 생성 합니다. CustomChannelsTester, TestSpec .xml 및 SampleRun. Samplerun .cmd 파일에는이 도구를 사용 하 여 [전송을 테스트 하는 방법을 보여 주는 샘플 명령줄이 있습니다. UDP](../../../../docs/framework/wcf/samples/transport-udp.md) 샘플.  
  
### <a name="to-run-the-tool"></a>도구를 실행하려면  
  
- 명령 프롬프트에 다음 명령을 입력합니다.  
  
    ```console  
    CustomChannelsTester.exe /binding:YourCustomBindngName /dll:TheAssemblyWhereThisTypeisDefined /testspec:XmlFileNameWhichContainsTestOptions  
    ```  
  
     `/binding` 옵션은 필수적 요소입니다.  
  
     `/dll`"바인딩"이 Windows Communication Foundation (WCF)에서 제공 하는 시스템 제공 바인딩이 아닌 경우 필요 합니다.  
  
     `/testspec`는 선택적 요소입니다.  
  
     이 명령을 실행하면 테스트 사양 및 바인딩에 따라 서버와 클라이언트가 생성됩니다.  
  
     클라이언트와 서버를 실행하고 결과를 반환합니다.  
  
     다음은 테스트 사양을 설명하는 샘플 XML(testspec.xml)입니다.  
  
    ```xml  
    <TestSpec xmlns="http://WCF/TestSpec" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" >  
    <ServiceContract>  
    <!-- Test a contract which has oneway / twoway operations. If you set ExpandAll = true, both types of contracts are tested -->    <IsOneWay ExpandAll="true">true</IsOneWay>  
    <!-- Test a contract with Asynchronous / Synchronous Operations-->  
        <IsAsync>false</IsAsync>   
    <!-- Test a sessionful / sessionless contract-->      
        <IsSession ExpandAll="true">true</IsSession>  
    <!-- If the Service Contract includes a CallBack Contract-->      
        <IsCallBack ExpandAll="true">true</IsCallBack>  
    </ServiceContract>  
    <TestDetails>  
    <!-- Name of the machine that runs the server - required if you want to run the test crossmachine-->  
        <ServerName>ReplaceThisWithTheServerMachineName</ServerName>  
    <!-- Port Number - Optional-->  
        <Port>8000</Port>  
    <!--URI for the callBack address for the client. The client will receive the messages from the server on this address in case of a CallBack Contract-->  
        <ClientCallBackAddress/>      
    <!-- Duration (in sec) after the server has started, it times out - optional(default = 300sec) -->  
        <ServerTimeout>300</ServerTimeout>  
    <!-- Duration (in sec) before the Client initializes -optional(default = 60sec) -->  
        <ClientTimeout>60</ClientTimeout>  
    <!-- Number of clients for each service - optional(default = 1) -->  
        <NumberOfClients>1</NumberOfClients>  
    <!-- Number of messages each client sends to the service - optional(default = 1) -->  
        <MessagesPerClient>1</MessagesPerClient>  
    </TestDetails>  
    </TestSpec>  
    ```  
