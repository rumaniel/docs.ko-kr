---
title: 비동기 개요
description: 비동기 프로그래밍이 다중 코어에서 차단 I/O 및 동시 작업을 간단하게 처리할 수 있게 해주는 주요 기술이 되는 방법을 알아봅니다.
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.technology: dotnet-standard
ms.assetid: 1e38e9d9-8284-46ee-a15f-199adc4f26f4
ms.openlocfilehash: 2f76eb7d2b769b59809bec81aefacb7cec90a450
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106696"
---
# <a name="async-overview"></a>비동기 개요

얼마 전만 해도 최신 PC 또는 서버를 구입하기만 해도 앱 속도가 빨라졌지만 이러한 추세는 중단되었습니다. 사실 반대가 되었다고 해야 맞습니다. 1ghz 싱글 코어 ARM 칩이 탑재되고 서버 작업이 VM으로 전환된 휴대폰이 출시되었습니다. 그래도 사용자는 여전히 응답성이 뛰어난 UI를 원하고 비즈니스 소유자는 비즈니스에 맞게 확장되는 서버를 원합니다. 모바일 및 클라우드로의 전환과 인터넷 연결 사용자 수가 30억 명을 넘어서면서 일련의 새로운 소프트웨어 패턴이 생겼습니다. 

- 클라이언트 애플리케이션은 항상 켜져 있고, 항상 연결되어 있으며, 지속적으로 사용자 조작(예: 터치)에 빠르게 응답해야 하고, 앱 스토어 등급이 높아야 합니다.
- 서비스는 적절하게 확장 및 축소하여 트래픽 급증을 처리해야 합니다. 

비동기 프로그래밍은 다중 코어에서 차단 I/O 및 동시 작업을 간단하게 처리할 수 있게 해주는 주요 기술입니다. .NET에서는 앱과 서비스가 C#, VB 및 F#으로 작성된 사용하기 쉬운 언어 수준의 비동기 프로그래밍 모델을 사용하여 응답성 및 탄력성을 유지할 수 있습니다.

## <a name="why-write-async-code"></a>비동기 코드를 작성하는 이유

최신 앱은 파일 및 네트워킹 I/O를 광범위하게 사용합니다. 이전에는 I/O API가 기본적으로 차단되어, 어려운 패턴을 배우고 사용하지 않을 경우 사용자 환경 및 하드웨어 사용률이 좋지 않았습니다. 작업 기반 비동기 API 및 언어 수준의 비동기 프로그래밍 모델은 이 모델을 뒤집어 새로운 개념을 배우지 않고도 기본적으로 비동기 실행을 사용할 수 있게 합니다.

비동기 코드에는 다음과 같은 특성이 있습니다.

- I/O 요청이 반환되기를 기다리는 동안 추가 요청을 처리할 수 있도록 스레드를 양도하여 더 많은 서버 요청을 처리합니다.
- I/O 요청을 기다리는 동안 UI 조작에 스레드를 양도하고 장기 실행 작업을 다른 CPU 코어로 전환하여 UI 응답성을 개선합니다.
- 대부분의 최신 .NET API는 비동기입니다.
- .NET에서 비동기 코드를 작성하는 것은 쉽습니다.

## <a name="whats-next"></a>새로운 기능

자세한 내용은 [비동기에 대한 자세한 설명](async-in-depth.md) 항목을 참조하세요.

[비동기 프로그래밍 패턴](asynchronous-programming-patterns/index.md) 항목은 .NET에서 지원되는 세 가지 비동기 프로그래밍 패턴에 대한 개요를 제공합니다.  
  
- [APM(비동기 프로그래밍 모델)](asynchronous-programming-patterns/asynchronous-programming-model-apm.md)(레거시)  
  
- [EAP(이벤트 기반 비동기 패턴)](asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)(레거시)  
  
- [TAP(작업 기반 비동기 패턴)](asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)(새로운 개발에 권장)  

권장 작업 기반 프로그래밍 모델에 대한 자세한 내용은 [작업 기반 비동기 프로그래밍](parallel-programming/task-based-asynchronous-programming.md) 항목을 참조하세요.
