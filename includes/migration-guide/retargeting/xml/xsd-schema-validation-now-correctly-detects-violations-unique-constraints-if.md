---
ms.openlocfilehash: c0a281b05f453b68495e6fa6fca45f3f36a204a3
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804507"
---
### <a name="xsd-schema-validation-now-correctly-detects-violations-of-unique-constraints-if-compound-keys-are-used-and-one-key-is-empty"></a>복합 키를 사용하고 하나의 키가 비어 있는 경우 XSD 스키마 유효성 검사는 이제 올바르게 UNIQUE 제약 조건 위반을 감지함

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6 이전 버전은 키 중 하나가 비어있는 경우 XSD 유효성 검사가 복합 키에서 UNIQUE 제약 조건을 감지하지 않는 버그가 있었습니다. .NET Framework 4.6에서 이 문제가 수정되었습니다. 이렇게 하면 보다 정확한 유효성 검사가 되지만 이전에 검사되었던 일부 XML이 유효성 검사되지 않는 결과를 발생시킬 수 있습니다.|
|제안|완화된 .NET Framework 4.0 유효성 검사가 필요한 경우 유효성 검사 애플리케이션은 .NET Framework 4.5(또는 이전) 버전을 대상으로 할 수 있습니다. 하지만 .NET Framework 4.6으로 다시 대상을 지정하는 경우 중복 복합 키가 (이 문제 설명에 기술된 것처럼) 유효성 검사되지 않도록 코드 검토를 수행해야 합니다.|
|범위|Microsoft Edge|
|버전|4.6|
|형식|대상 변경|

