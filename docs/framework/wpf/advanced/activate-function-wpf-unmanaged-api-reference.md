---
title: Activate 함수 (F 관리 되지 않는 API 참조)
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- Activate
api_location:
- PresentationHost_v0400.dll
ms.assetid: 1400329c-b598-465f-80f2-e3dabf044811
ms.openlocfilehash: ee231653815bd5ef75d58979034e3b3be9f5ba54
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61777171"
---
# <a name="activate-function-wpf-unmanaged-api-reference"></a>Activate 함수 (F 관리 되지 않는 API 참조)

이 API는 Windows Presentation Foundation (WPF) 인프라를 지원 하며 코드에서 직접 사용할 수 없습니다.

Windows 관리에 대 한 Windows Presentation Foundation (WPF) 인프라에서 사용 합니다.

## <a name="syntax"></a>구문

```cpp
void Activate(
    const ActivateParameters* pParameters,
    __deref_out_ecount(1) LPUNKNOWN* ppInner,
    );
```

## <a name="parameters"></a>매개 변수

`pParameters`\
활성화 매개 변수 창에 대 한 포인터입니다.

`ppInner`\
에 대 한 포인터를 포함 하는 단일 요소 버퍼의 주소에 대 한 포인터를 <xref:Microsoft.VisualStudio.OLE.Interop.IOleDocument> 개체입니다.

## <a name="requirements"></a>요구 사항

**플랫폼:** 참조 [.NET Framework 시스템 요구 사항](../../get-started/system-requirements.md)합니다.

**DLL:**

.NET framework 3.0 및 3.5. PresentationHostDLL.dll

.NET framework 4 이상: PresentationHost_v0400.dll

**.NET framework 버전:** [!INCLUDE[net_current_v30plus](../../../../includes/net-current-v30plus-md.md)]

## <a name="see-also"></a>참고자료

- [F 관리되지 않는 API 참조](wpf-unmanaged-api-reference.md)
