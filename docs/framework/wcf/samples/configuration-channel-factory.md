---
title: 구성 채널 팩터리
ms.date: 03/30/2017
ms.assetid: 3b749493-bd8a-4ccb-893e-5948901a1486
ms.openlocfilehash: 1b74c15599ebc932a2a0ed46d646b54bec986794
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045651"
---
# <a name="configuration-channel-factory"></a>구성 채널 팩터리
이 샘플에서는 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>의 사용법에 대해 설명합니다. 에서는 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> WCF 클라이언트 구성의 중앙 관리를 수행할 수 있습니다. 애플리케이션 도메인의 로드 이후 구성이 선택되었거나 변경된 경우에도 유용합니다.

## <a name="demonstrates"></a>세부 항목
 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>

## <a name="discussion"></a>토론
 이 샘플에서는 기본 애플리케이션 구성 파일을 사용할 필요 없이 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>를 사용하여 클라이언트 애플리케이션에 특정 구성 파일을 추가하는 방법을 보여 줍니다.

 이 샘플은 두 프로젝트로 구성되어 있습니다. 첫 번째 프로젝트는 클라이언트가 보내는 메시지에 회신하기 위해 실행되는 간단한 서비스입니다. 두 번째 프로젝트는 Test.config 구성 파일에 대해 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>을 사용하여 두 개의 <xref:System.Configuration.ExeConfigurationFileMap> 개체를 빌드하고 이 개체를 사용하여 서비스와 통신하는 클라이언트 애플리케이션입니다. 두 클라이언트 모두 Test.config에 지정된 구성을 사용하여 서비스와 통신합니다.

 다음 코드에서는 클라이언트 애플리케이션에 사용자 지정 구성 파일을 추가합니다.

```csharp
ExeConfigurationFileMap fileMap = new ExeConfigurationFileMap();
fileMap.ExeConfigFilename = "Test.config";
Configuration newConfiguration = ConfigurationManager.OpenMappedExeConfiguration(fileMap, ConfigurationUserLevel.None);

ConfigurationChannelFactory<ICalculatorChannel> factory1 = new ConfigurationChannelFactory<ICalculatorChannel>("endpoint1", newConfiguration, new EndpointAddress("http://localhost:8000/servicemodelsamples/service"));
ICalculatorChannel client1 = factory1.CreateChannel();
```

#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. 관리자 권한으로 Visual Studio 2012을 엽니다.

2. ConfigurationChannelFactory 솔루션 (프로젝트 2 개)을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다.

3. **공용 속성**에서 **시작 프로젝트**를 선택한 다음 **여러 개의 시작 프로젝트**를 클릭 합니다.

4. **서비스** 프로젝트를 **' start ' 작업**을 사용 하 여 목록의 시작 부분으로 이동한 다음 클라이언트 프로젝트를 **' 시작 ' 작업**을 사용 하 여 **서비스** 프로젝트 뒤에 이동 하 여 **클라이언트** 프로젝트를 실행 합니다. **서비스** 프로젝트 후

5. **확인**을 클릭 한 다음 F5 키 (또는 CTRL + F5)를 눌러 샘플을 실행 합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\ConfigurationChannelFactory`
