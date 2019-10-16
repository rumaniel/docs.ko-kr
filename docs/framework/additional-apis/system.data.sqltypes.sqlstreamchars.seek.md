---
title: SqlStreamChars.Seek (Int64, SeekOrigin) 메서드 (System.Data.SqlTypes)
author: stevestein
ms.author: sstein
ms.date: 12/20/2018
ms.technology: dotnet-data
topic_type:
- apiref
api_name:
- System.Data.SqlTypes.SqlStreamChars.Seek
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: 6b69f87da9fb3829d765dc135de1f6c10765b63a
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65634354"
---
# <a name="sqlstreamcharsseekint64-seekorigin-method"></a>(Int64, SeekOrigin) SqlStreamChars.Seek 메서드

파생 클래스를 재정의될 때 현재 스트림 내의 위치를 설정합니다. 이 메서드를 포함 하는 어셈블리에는 SQLAccess.dll friend 관계를 갖습니다. SQL Server에서 사용할 것입니다. 다른 데이터베이스에 대 한 해당 데이터베이스에서 제공 하는 호스팅 메커니즘을 사용 합니다.

```csharp
public abstract long Seek (long offset, System.IO.SeekOrigin origin);
```

## <a name="parameters"></a>매개 변수

`offset`\
에 상대적인 바이트 오프셋 `origin`합니다.

`origin`\
새 위치를 가져올 참조 위치를 나타내는 열거형 값 중 하나입니다.

## <a name="returns"></a>반환 값

<xref:System.Int32>\
현재 스트림 내의 새 위치입니다.

## <a name="remarks"></a>설명

> [!WARNING]
> `SqlStreamChars.Seek` 메서드가 private 이며 코드에서 직접 사용할 하려고 하지 않습니다.
>
> Microsoft는 어떤 상황에서 프로덕션 응용 프로그램에서이 필드의 사용을 지원 하지 않습니다.

## <a name="requirements"></a>요구 사항

**네임스페이스:** <xref:System.Data.SqlTypes>

**어셈블리:** System.Data (System.Data.dll)

**.NET framework 버전:** 2.0부터 사용할 수 있습니다.
