---
ms.openlocfilehash: 08c16f261338148619de2e484c73046b9d9a6bfe
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858423"
---
### <a name="the-net-framework-46-does-not-use-a-45xx-version-when-registering-itself-in-the-registry"></a>.NET Framework 4.6은 레지스트리에 등록될 때 4.5.x.x 버전을 사용하지 않습니다.

|   |   |
|---|---|
|세부 정보|예상할 수 있듯이 .NET Framework 4.6의 레지스트리(<code>HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\NET Framework Setup\NDP\v4\Full</code>)에 설정된 버전 키는 '4.5'가 아니라 '4.6'으로 시작합니다. 이러한 레지스트리 키를 사용하여 컴퓨터에 설치된 .NET Framework 버전을 확인하는 앱은 4.6이 가능한 새 버전이고 이전 4.5.x 릴리스와 호환된다는 것을 이해하도록 업데이트되어야 합니다.|
|제안|4\.5 레지스트리 키를 검색하여 4.6을 수락하도록 .NET Framework 4.5 설치를 검색하는 앱을 업데이트합니다.|
|범위|Microsoft Edge|
|버전|4.6|
|형식|런타임|

