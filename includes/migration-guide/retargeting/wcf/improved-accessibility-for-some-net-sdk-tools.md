---
ms.openlocfilehash: 79005f19ac31ba32e7e468ef61eb867a052eff40
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858947"
---
### <a name="improved-accessibility-for-some-net-sdk-tools"></a>일부 .NET SDK 도구에 대해 향상된 액세스 가능성

|   |   |
|---|---|
|설명|.NET Framework SDK 4.7.1에서 다양한 액세스 가능성 문제를 수정하여 SvcConfigEditor.exe 및 SvcTraceViewer.exe 도구가 개선되었습니다. 이들 중 대부분은 정의되지 않은 이름이나 특정 UI 자동화 패턴이 올바르게 구현되지 않은 것과 같은 사소한 문제였습니다. 많은 사용자가 이러한 잘못된 값을 인식하지 못하지만, 화면 판독기와 같은 보조 기술을 사용하는 고객은 이러한 SDK 도구를 보다 쉽게 사용할 수 있습니다. 물론 이러한 수정은 키보드 포커스 순서와 같은 이전 동작을 변경합니다. 이 도구에서 모든 액세스 가능성을 수정하기 위해 app.config 파일에서 다음을 수행할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.7.1|
|형식|대상 변경|

