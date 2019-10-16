---
title: ConfigurationCodeGenerator
ms.date: 03/30/2017
ms.assetid: 3913aae8-165f-4014-9262-7fe426f90cb2
ms.openlocfilehash: f12fae48f1cee198aac22e6f09e616b407b4e9b5
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70990062"
---
# <a name="configurationcodegenerator"></a>ConfigurationCodeGenerator
ConfigurationCodeGenerator는 구성 시스템에 사용자 지정 채널 구현을 노출하는 데 사용할 수 있는 도구입니다. 이를 통해 사용자 지정 채널의 사용자가 `NetTcpBinding`을 사용하여 `TcpTransportBindingElement` 등의 시스템 제공 바인딩이나 사용자 지정 바인딩을 구성하는 것과 같은 방법으로 .config 파일을 사용하여 채널을 구성할 수 있습니다.  
  
 사용자 지정 채널을 써서 새 `BindingElement` 또는 `Binding`을 통해 프로그래밍 모델에 노출할 때에는 일련의 클래스를 만들어 .config 파일을 통해 `BindingElement` 또는 `Binding`을 구성 가능하게 만들어야 합니다. ConfigurationCodeGenerator 도구를 사용하여 이런 클래스를 생성하고 고객의 경험을 향상시킬 수 있습니다.  
  
### <a name="to-build-the-tool"></a>도구를 빌드하려면  
  
1. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.  
  
2. 솔루션을 빌드하면 하나의 파일이 생성 됩니다. ConfigurationCodeGenerator.exe. Samplerun .cmd 파일에는이 도구를 사용 하 여 [전송에 대 한 클래스를 생성 하는 방법을 보여 주는 샘플 명령줄이 있습니다. UDP](../../../../docs/framework/wcf/samples/transport-udp.md) 샘플.  
  
### <a name="to-run-the-tool"></a>도구를 실행하려면  
  
1. 사용자 지정 `BindingElement` 형식과 사용자 지정 `Binding` 형식이 모두 있는 경우 명령 프롬프트에서 다음을 입력합니다.  
  
    ```console  
    ConfigurationCodeGenerator.exe /be:YourCustomBindingElementTypeName /sb:YourCustomStdBindingTypeName /dll:TheAssemblyWhereTheseTypesAreDefined  
    ```  
  
     또는 사용자 지정 `BindingElement` 형식만 있는 경우 다음을 입력합니다.  
  
    ```console  
    ConfigurationCodeGenerator.exe /be:YourCustomBindingElementTypeName /dll: TheAssemblyWhereThisTypeIsDefined  
    ```  
  
     또는 사용자 지정 `Binding` 형식만 있는 경우 다음을 입력합니다.  
  
    ```console  
    ConfigurationCodeGenerator.exe /sb:YourCustomStdBindingTypeName /dll:TheAssemblyWhereThisTypeIsDefined  
    ```  
  
     명령에서는 `BindingElement`(/be: 옵션을 설정한 경우)에 사용할 3개의 .cs 파일, 표준 `Binding`(/sb: 옵션을 지정한 경우)에 사용할 5개의 .cs 파일, 그리고 한 개의 .xml 파일을 생성합니다.  
  
    1. /be 옵션을 사용한 경우 .cs 파일 중 하나에서 바인딩 요소의 `BindingElementExtensionSection`을 구현합니다. 이 코드에서는 다른 사용자 지정 바인딩에서 바인딩 요소를 사용할 수 있도록 구성 시스템에 `BindingElement`를 노출합니다. 다른 파일에는 기본값과 상수를 나타내는 클래스가 있습니다. 파일에는 기본값을 업데이트하도록 상기시키기 위한 `//TODO` 주석이 있습니다.  
  
    2. /sb 옵션을 지정한 경우 2개의 .cs 파일을 각각 구성 시스템에 표준 바인딩을 노출하는 `StandardBindingElement` 및 `StandardBindingCollectionElement`를 구현합니다. 다른 파일에는 기본값과 상수를 나타내는 클래스가 있습니다. 파일에는 기본값을 업데이트하도록 상기시키기 위한 `//TODO` 주석이 있습니다.  
  
         /Sws: 옵션을 지정한*경우 CodeToAddTo*의\<>에는 표준 바인딩을 구현 하는 클래스에 수동으로 추가 해야 하는 코드가 있습니다.  
  
     SampleConfig.xml 파일에는 이전의 1단계 또는 2단계에 정의된 처리기를 등록하는 구성 파일에 추가해야 할 구성 코드가 포함되어 있습니다.  
