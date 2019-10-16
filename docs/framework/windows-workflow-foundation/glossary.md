---
title: .NET Framework 4.5용 Windows Workflow Foundation 용어집
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Workflow Foundation [WF], glossary
- WF [WF], glossary
ms.assetid: ab682b2f-3779-45ca-b831-b7c03d7dbb3a
ms.openlocfilehash: 61d9acab1161302937e240eb8ebb506ca9f1585c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61945628"
---
# <a name="windows-workflow-foundation-glossary-for-net-framework-45"></a>.NET Framework 4.5용 Windows Workflow Foundation 용어집

다음은 Windows Workflow Foundation 설명서에서 사용되는 용어입니다.

## <a name="terms"></a>용어

|용어|정의|
|----------|----------------|
|작업(activity)|Windows Workflow Foundation의 프로그램 동작 단위입니다. 단일 활동을 여러 개 결합하여 보다 복잡한 활동을 작성할 수 있습니다.|
|작업 동작(activity action)|워크플로 및 활동 실행을 위한 콜백을 노출하는 데 사용되는 데이터 구조입니다.|
|인수(argument)|활동 내부/외부로의 데이터 흐름을 정의합니다. 각 인수에는 지정된 방향(입력, 출력 또는 입력/출력)이 있습니다. 이러한 방향은 활동의 입력, 출력 및 입력/출력 매개 변수를 나타냅니다.|
|책갈피(bookmark)|활동을 일시 중단하고 다시 시작할 때까지 대기할 수 있는 지점입니다.|
|보정(compensation)|이전에 완료한 작업을 실행 취소하거나 그 효과를 완화하도록 디자인된 작업 그룹입니다.|
|상관 관계|메시지를 워크플로 또는 서비스 인스턴스로 라우팅하기 위한 메커니즘입니다.|
|expression|하나 이상의 인수를 가져와 인수에 대한 작업을 수행하고 단일 값을 반환하는 구문입니다. 식은 활동을 사용할 수 있는 모든 위치에서 사용할 수 있습니다.|
|순서도(flowchart)|방향 화살표를 사용하여 서로 연결된 기호로 프로그램 구성 요소를 표시하는 널리 사용되는 모델링 패러다임입니다.  .NET Framework 4에서는 순서도 활동을 사용해 워크플로를 순서도로 모델링할 수 있습니다.|
|장기 실행 프로세스(long-running process)|즉시 반환되지 않으며 시스템을 다시 시작할 때까지 계속될 수 있는 프로그램 실행 단위입니다.|
|지속성|워크플로 또는 서비스의 상태를 영구적인 매체에 저장하여 시스템 오류가 발생한 후 메모리에서 언로드하거나 복구할 수 있도록 하는 것입니다.|
|상태 시스템|이벤트 구동 상태 전환을 사용하여 서로 연결된 개별 상태로 프로그램 구성 요소를 표시하는 널리 사용되는 모델링 패러다임입니다.  워크플로는 StateMachine 활동을 사용하여 상태 시스템으로 모델링할 수 있습니다.|
|실체(substance)|공통 식별자 하에서 관련된 책갈피 그룹을 나타내며, 런타임에서 특정 책갈피 다시 시작이 유효하거나 유효해질 수 있는지 여부를 결정할 수 있도록 합니다.|
|형식 변환기(type converter)|CLR 형식은 하나 이상의 System.ComponentModel.TypeConverter 파생 형식과 연결할 수 있습니다. 이 파생 형식을 사용하면 CLR 형식 인스턴스와 다른 형식 인스턴스 간에 변환할 수 있습니다. 형식 변환기는 System.ComponentModel.TypeConverterAttribute 특성을 사용 하 여 CLR 형식과 연결 됩니다.  TypeConverterAttribute는 CLR 형식 또는 속성에서 직접 지정할 수 있습니다. 속성에 대해 지정된 형식 변환기는 항상 속성의 CLR 형식에 대해 지정된 형식 변환기보다 우선적으로 적용됩니다.|
|변수|저장하여 나중에 액세스해야 하는 일부 데이터 스토리지를 나타냅니다.|
|워크플로|호스트 프로세스에서 호출하는 단일 활동 또는 활동 트리입니다.|
|XAML|eXtensible Application Markup Language의 약어입니다.|
