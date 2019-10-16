---
title: CLR ETW 공급자
ms.date: 03/30/2017
helpviewer_keywords:
- ETW, CLR providers
- CLR ETW providers
ms.assetid: 0beafad4-b2c8-47f4-b342-83411d57a51f
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 93a0271c521de6e390e323d92e93a5e7bf94444f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046732"
---
# <a name="clr-etw-providers"></a>CLR ETW 공급자
CLR(공용 언어 런타임)에는 런타임 공급자 및 런다운 공급자라는 두 개의 공급자가 있습니다.  
  
 런타임 공급자는 사용하도록 설정된 키워드(이벤트 범주)에 따라 이벤트를 발생시킵니다. 예를 들어 `LoaderKeyword` 키워드를 사용하도록 설정하면 로더 이벤트를 수집할 수 있습니다.  
  
 ETW (ETW(Windows용 이벤트 추적)) 이벤트는 확장명이 .etl 인 파일에 기록 되며, 나중에 필요에 따라 쉼표로 구분 된 값 (.csv) 파일에서 나중에 처리 될 수 있습니다. .etl 파일을 .csv 파일로 변환하는 방법에 대한 자세한 내용은 [.NET Framework 로깅 제어](controlling-logging.md)를 참조하세요.  
  
## <a name="the-runtime-provider"></a>런타임 공급자  
 런타임 공급자는 기본 CLR ETW 공급자입니다.  
  
 CLR 런타임 공급자 GUID는 e13c0d23-ccbc-4e12-931b-d9cc2eee27e4입니다.  
  
 일반적으로 사용 가능한 도구를 사용하여 CLR ETW 이벤트를 기록하고 보는 방법의 예제는 [.NET Framework 로깅 제어](controlling-logging.md)를 참조하세요.  
  
 `LoaderKeyword` 등의 키워드 사용 외에도 너무 자주 발생할 수 있는 이벤트를 기록하기 위해 키워드를 사용하도록 설정해야 할 수도 있습니다. 이러한 이벤트는 `StartEnumerationKeyword` 및 `EndEnumerationKeyword` 키워드에 의해 활성화되며 두 키워드는 [CLR ETW 키워드 및 수준](clr-etw-keywords-and-levels.md)에 요약되어 있습니다.  
  
## <a name="the-rundown-provider"></a>런다운 공급자  
 특별한 용도에 사용하려면 런다운 공급자를 켜야 합니다. 그러나 대부분의 사용자는 런타임 공급자로 충분합니다.  
  
 CLR 런다운 공급자 GUID는 A669021C-C450-4609-A035-5AF59AF4DF18입니다.  
  
 일반적으로 ETW 로깅은 프로세스가 시작되기 전에 사용되고, 프로세스가 종료된 후 로깅이 꺼집니다. 그러나 프로세스를 실행하는 동안 ETW 로깅이 켜져 있는 경우 프로세스에 대한 추가 정보가 필요합니다. 예를 들어 기호를 확인하려면 로깅을 켜기 전에 이미 로드된 메서드에 대한 메서드 이벤트를 기록해야 합니다.  
  
 `DCStart` 및 `DCEnd` 이벤트는 데이터 수집이 시작 및 중지될 때 프로세스의 상태를 캡처합니다. 상태는 JIT(Just-In-Time) 컴파일된 메서드 및 로드된 어셈블리를 포함하여 개괄적인 정보를 참조합니다. 이러한 두 이벤트는 프로세스에서 이미 발생한 사항(예: JIT 컴파일된 메서드 등)에 대한 정보를 제공할 수 있습니다.  
  
 `DC`, `DCStart`, `DCEnd` 또는 `DCInit`가 이름에 포함된 이벤트만 런다운 공급자 아래에서 발생합니다. 또한 이들 이벤트는 런다운 공급자에서만 발생합니다.  
  
 이벤트 키워드 필터 외에도 런다운 공급자는 대상 필터링을 제공하는 `StartRundownKeyword` 및 `EndRundownKeyword` 키워드도 지원합니다.  
  
### <a name="start-rundown"></a>시작 런다운  
 시작 런다운은 런다운 공급자 아래의 로깅이 `StartRundownKeyword` 키워드로 활성화된 경우에 트리거됩니다. 이 경우 `DCStart`가 발생하고 시스템 상태가 캡처됩니다. 열거를 시작하기 전에 `DCStartInit` 이벤트가 발생합니다. 열거형의 끝에는 `DCStartComplete` 이벤트가 발생하여 데이터 수집이 정상적으로 종료되었음을 컨트롤러에 알립니다.  
  
### <a name="end-rundown"></a>끝 런다운  
 끝 런다운은 런다운 공급자 아래의 로깅이 `EndRundownKeyword` 키워드로 활성화된 경우에 트리거됩니다. 끝 런다운은 계속 실행되는 프로세스에 대한 프로파일링을 중지합니다. `DCEnd` 이벤트는 프로파일링이 중지될 때의 시스템 상태를 캡처합니다.  
  
 열거를 시작하기 전에 `DCEndInit` 이벤트가 발생합니다. 열거형의 끝에는 `DCEndComplete` 이벤트가 발생하여 데이터 수집이 정상적으로 종료되었음을 소비자에게 알립니다. 시작 런다운 및 끝 런다운은 주로 관리되는 기호 확인에 사용됩니다. 시작 런다운은 프로파일링 세션이 시작되기 전에 이미 JIT 컴파일된 메서드에 대한 주소 범위 정보를 제공할 수 있습니다. 끝 런다운은 프로파일링을 끌 때 JIT 컴파일된 모든 메서드에 대한 주소 범위 정보를 제공할 수 있습니다.  
  
 끝 런다운은 프로파일링 세션을 중지할 때 자동으로 발생하지 않습니다. 대신, 프로파일링이 중지되기 직전에 관리되는 기호 확인을 수행하려는 도구가 `EndRundownKeyword` 키워드를 사용하여 CLR 런다운 공급자 세션을 명시적으로 호출해야 합니다.  
  
 시작 런다운 또는 끝 런다운은 관리되는 기호 확인을 위해 메서드 주소 범위 정보를 제공할 수 있지만 `StartRundownKeyword` 키워드(`DCStart` 이벤트 제공) 대신 `EndRundownKeyword` 키워드(`DCEnd` 이벤트 제공)를 사용하는 것이 좋습니다. `StartRundownKeyword`를 사용하면 프로파일링 세션 중에 런다운이 발생하며 프로파일링된 시나리오를 방해할 수 있습니다.  
  
## <a name="etw-data-collection-using-runtime-and-rundown-providers"></a>런타임 및 런다운 공급자를 사용한 ETW 데이터 수집  
 다음 예제에서는 프로세스가 프로파일링된 창 내부 또는 외부에서 시작 또는 종료되는지에 관계없이 최소한의 영향으로 관리되는 프로세스의 기호 확인을 허용하는 방식으로 CLR 런다운 공급자를 사용하는 방법을 보여 줍니다.  
  
1. CLR 런타임 공급자를 사용하여 ETW 로깅 켜기:  
  
    ```console
    xperf -start clr -on e13c0d23-ccbc-4e12-931b-d9cc2eee27e4:0x1CCBD:0x5 -f clr1.etl      
    ```  
  
     로그는 clr1.etl 파일에 저장됩니다.  
  
2. 프로세스를 계속 실행하는 동안 프로파일링을 중지하려면 런다운 공급자를 시작하여 `DCEnd` 이벤트를 캡처합니다.  
  
    ```console
    xperf -start clrRundown -on A669021C-C450-4609-A035-5AF59AF4DF18:0xB8:0x5 -f clr2.etl      
    ```  
  
     이렇게 하면 `DCEnd` 이벤트 컬렉션이 런다운 세션을 시작할 수 있습니다. 모든 이벤트가 수집되도록 30-60초 기다려야 할 수도 있습니다. 로그는 clr1.et2 파일에 저장됩니다.  
  
3. 모든 ETW 프로파일링 끄기:  
  
    ```console
    xperf -stop clrRundown   
    xperf -stop clr  
    ```  
  
4. 프로필을 병합하여 하나의 로그 파일 만들기:  
  
    ```console
    xperf -merge clr1.etl clr2.etl merged.etl  
    ```  
  
     merged.etl 파일에는 런타임 및 런다운 공급자 세션의 이벤트가 포함됩니다.  
  
 도구는 사용자가 프로파일링 중지를 요청할 때 프로파일링을 즉시 끄지 않고 2단계와 3단계(런다운 세션을 시작한 다음 프로파일링 종료)를 실행할 수 있습니다. 도구에서 4단계를 실행할 수도 있습니다.  
  
## <a name="see-also"></a>참고자료

- [공용 언어 런타임의 ETW 이벤트](etw-events-in-the-common-language-runtime.md)
