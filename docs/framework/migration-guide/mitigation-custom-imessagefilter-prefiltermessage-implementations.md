---
title: '완화: 사용자 지정 IMessageFilter.PreFilterMessage 구현'
ms.date: 03/30/2017
ms.assetid: 9cf47c5b-0bb2-45df-9437-61cd7e7c2f4d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2af81468c5c4c4caf2f09725d6c7c4723084e35c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779438"
---
# <a name="mitigation-custom-imessagefilterprefiltermessage-implementations"></a>완화: 사용자 지정 IMessageFilter.PreFilterMessage 구현

.NET Framework 4.6.1부터 .NET Framework 버전을 대상으로 하는 Windows Forms 앱에서는 <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType> 구현이 다음에 해당하는 경우 <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType> 메서드를 호출할 때 사용자 지정 <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType> 구현이 메시지를 안전하게 필터링할 수 있습니다.

- 다음 중 하나 또는 두 가지 모두를 수행합니다.

  - <xref:System.Windows.Forms.Application.AddMessageFilter%2A> 메서드를 호출하여 메시지 필터 추가

  - <xref:System.Windows.Forms.Application.RemoveMessageFilter%2A> 메서드를 호출하여 메시지 필터 제거 메서드를 재정의합니다.

- **그와 동시에** <xref:System.Windows.Forms.Application.DoEvents%2A?displayProperty=nameWithType> 메서드를 호출하여 메시지를 펌핑하는 경우

## <a name="impact"></a>영향

이 변경은 .NET Framework 4.6.1부터 .NET Framework 버전을 대상으로 하는 Windows Forms 앱에만 영향을 줍니다.

이전 버전의 .NET Framework를 대상으로 하는 Windows Forms 앱에서는 경우에 따라 <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType> 메서드를 호출할 때 이러한 구현이 <xref:System.IndexOutOfRangeException> 예외를 throw할 수 있습니다.

## <a name="mitigation"></a>완화

이러한 변경을 원치 않는 경우 .NET Framework 4.6.1 이상 버전을 대상으로 하는 앱은 앱 구성 파일의 [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) 섹션에 다음 구성 설정을 추가하여 이 동작을 사용하지 않을 수 있습니다.

```xml
<runtime>
    <AppContextSwitchOverrides value="Switch.System.Windows.Forms.DontSupportReentrantFilterMessage=true" />
</runtime>
```

또한 이전 버전의 .NET Framework를 대상으로 하지만 .NET Framework 4.6.1 이상 버전에서 실행되는 앱은 앱 구성 파일의 [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) 섹션에 다음 구성 설정을 추가하여 이 동작을 옵트인(opt in)할 수 있습니다.

```xml
<runtime>
    <AppContextSwitchOverrides value="Switch.System.Windows.Forms.DontSupportReentrantFilterMessage=false" />
</runtime>
```

## <a name="see-also"></a>참고 항목

- [대상 다시 지정 변경 내용](retargeting-changes-in-the-net-framework-4-6-1.md)
