---
title: HttpWebRequest._CoreResponse Field
ms.date: 01/29/2018
topic_type:
- apiref
api_name:
- System.Net.HttpWebRequest._CoreResponse
api_location:
- System.dll
api_type:
- Assembly
author: stevewhims
ms.openlocfilehash: 3627c9bf0d72ccec3a0d6d9c7c89b62f83dcd4b4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61706067"
---
# <a name="httpwebrequestcoreresponse-field"></a>HttpWebRequest 합니다. \_CoreResponse 필드

`HttpWebRequest._CoreResponse` 개체 (중 하나를 [CoreResponseData](coreresponsedata.md) 요소나 <xref:System.Exception>) HTTP 응답을 구문 분석 결과 포함 하 합니다.

## <a name="syntax"></a>구문
  
```csharp
private object _CoreResponse
```

> [!WARNING]
> 코드에서 직접 사용할이 API는 사용 하는 것이 아닙니다. 대신 사용 해야는 <xref:System.Diagnostics.DiagnosticSource> 네트워킹 코드를 연결 합니다. 참조 [DiagnosticSource 사용자 가이드](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md)합니다.
> 
> Microsoft는 어떤 상황에서 프로덕션 응용 프로그램에서이 클래스의 사용을 지원 하지 않습니다.

## <a name="requirements"></a>요구 사항

**네임스페이스:** <xref:System.Net>

**어셈블리:** 시스템 (에: System.dll)

**.NET framework 버전:** 2.0부터 사용할 수 있습니다.
