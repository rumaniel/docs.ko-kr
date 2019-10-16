---
title: CoreResponseData.m_ResponseHeaders 필드
ms.date: 01/29/2018
topic_type:
- apiref
api_name:
- System.Net.CoreResponseData.m_ResponseHeaders
api_location:
- System.dll
api_type:
- Assembly
author: stevewhims
ms.openlocfilehash: ea93b70ae8e1a710b4208050d7ec823a28b218b7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61705976"
---
# <a name="coreresponsedatamresponseheaders-field"></a>CoreResponseData.m\_ResponseHeaders 필드

`CoreResponseData.m_ResponseHeaders` 가 <xref:System.Net.WebHeaderCollection> 서버 응답과 관련 된 헤더입니다.

## <a name="syntax"></a>구문
  
```csharp
public WebHeaderCollection m_ResponseHeaders
```

> [!WARNING]
> 코드에서 직접 사용할이 API는 사용 하는 것이 아닙니다. 대신 사용 해야는 <xref:System.Diagnostics.DiagnosticSource> 네트워킹 코드를 연결 합니다. 참조 [DiagnosticSource 사용자 가이드](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md)합니다.
> 
> Microsoft는 어떤 상황에서 프로덕션 응용 프로그램에서이 클래스의 사용을 지원 하지 않습니다.

## <a name="requirements"></a>요구 사항

**네임스페이스:** <xref:System.Net>

**어셈블리:** 시스템 (에: System.dll)

**.NET framework 버전:** 2.0부터 사용할 수 있습니다.
