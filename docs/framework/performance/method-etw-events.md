---
title: 메서드 ETW 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- ETW, method events (CLR)
- method events [.NET Framework]
ms.assetid: 167a4459-bb6e-476c-9046-7920880f2bb5
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 48e1c2271d6d011296d347e7d74fb363cc4d8527
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834546"
---
# <a name="method-etw-events"></a>메서드 ETW 이벤트

<a name="top"></a> 이들 이벤트는 메서드와 관련된 정보를 수집합니다. 이들 이벤트의 페이로드는 기호 확인을 위해 필요합니다. 또한 이들 이벤트는 메서드를 호출한 횟수와 같은 유용한 정보를 제공합니다.

모든 메서드 이벤트에는 "정보 제공(4)" 수준이 있습니다. 모든 메서드 자세한 정보 표시 이벤트에는 "자세한 정보 표시(5)" 수준이 있습니다.

모든 메서드 이벤트는 런타임 공급자에서 `JITKeyword` (0x10) 키워드 또는 `NGenKeyword` (0x20) 키워드에 의해 발생하거나 런다운 공급자에서 `JitRundownKeyword` (0x10) 또는 `NGENRundownKeyword` (0x20)에 의해 발생합니다.

CLR 메서드 이벤트는 추가로 다음과 같이 구분됩니다.

- [CLR 메서드 이벤트](#clr_method_events)

- [CLR 메서드 표식 이벤트](#clr_method_marker_events)

- [CLR 메서드 자세한 정보 표시 이벤트](#clr_method_verbose_events)

- [MethodJittingStarted 이벤트](#methodjittingstarted_event)

<a name="clr_method_events"></a>

## <a name="clr-method-events"></a>CLR 메서드 이벤트

다음 표에서는 키워드와 수준을 보여 줍니다. 자세한 내용은 [CLR ETW 키워드 및 수준](clr-etw-keywords-and-levels.md)을 참조 하세요.

|이벤트를 발생시키기 위한 키워드|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) 런타임 공급자|정보(4)|
|`NGenKeyword` (0x20) 런타임 공급자|정보(4)|
|`JitRundownKeyword` (0x10) 런다운 공급자|정보(4)|
|`NGENRundownKeyword` (0x20) 런다운 공급자|정보(4)|

다음 표에서는 이벤트 정보를 보여 줍니다.

|이벤트|이벤트 ID|설명|
|-----------|--------------|-----------------|
|`MethodLoad_V1`|136|메서드가 JIT(Just-In-Time) 로드되거나 NGEN 이미지가 로드될 때 발생합니다. 동적 및 제네릭 메서드는 메서드 로드에 대해 이 버전을 사용하지 않습니다. JIT 도우미는 이 버전을 사용하지 않습니다.|
|`MethodUnLoad_V1`|137|모듈이 언로드되거나 애플리케이션 도메인이 삭제될 때 발생합니다. 동적 메서드는 메서드 언로드에 대해 이 버전을 사용하지 않습니다.|
|`MethodDCStart_V1`|137|시작 런다운 중에 메서드를 열거합니다.|
|`MethodDCEnd_V1`|138|끝 런다운 중에 메서드를 열거합니다.|

다음 표에서는 이벤트 데이터를 보여 줍니다.

|필드 이름|데이터 형식|설명|
|----------------|---------------|-----------------|
|MethodID|win:UInt64|메서드의 고유 식별자입니다. JIT 도우미 메서드에 대한 이 필드는 메서드의 시작 주소로 설정됩니다.|
|ModuleID|win:UInt64|이 메서드가 속한 모듈의 식별자입니다(JIT 도우미의 경우 0).|
|MethodStartAddress|win:UInt64|메서드의 시작 주소입니다.|
|MethodSize|win:UInt32|메서드의 크기입니다.|
|MethodToken|win:UInt32|동적 메서드 및 JIT 도우미의 경우 0입니다.|
|MethodFlags|win:UInt32|0x1: 동적 메서드입니다.<br /><br /> 0x2: 제네릭 메서드입니다.<br /><br /> 0x4: JIT 컴파일된 코드 메서드 (그렇지 않은 경우 NGEN 네이티브 이미지 코드).<br /><br /> 0x8: 도우미 메서드입니다.|
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|

[맨 위로 이동](#top)

<a name="clr_method_marker_events"></a>

## <a name="clr-method-marker-events"></a>CLR 메서드 표식 이벤트

이들 이벤트는 런다운 공급자에서만 발생하고 시작 또는 끝 런다운 중에 메서드 열거형의 끝을 나타냅니다. 즉, 이들 이벤트는 `NGENRundownKeyword`, `JitRundownKeyword`, `LoaderRundownKeyword`또는 `AppDomainResourceManagementRundownKeyword` 키워드가 사용될 때 발생합니다.

다음 표에서는 키워드와 수준을 보여 줍니다.

|이벤트를 발생시키기 위한 키워드|Level|
|-----------------------------------|-----------|
|`AppDomainResourceManagementRundownKeyword` (0x800) 런다운 공급자|정보(4)|
|`JitRundownKeyword` (0x10) 런다운 공급자|정보(4)|
|`NGENRundownKeyword` (0x20) 런다운 공급자|정보(4)|

다음 표에서는 이벤트 정보를 보여 줍니다.

|이벤트|이벤트 ID|설명|
|-----------|--------------|----------------|
|`DCStartInit_V1`|147|시작 런다운 중에 열거가 시작하기 전에 전송됩니다.|
|`DCStartComplete_V1`|145|시작 런다운 중에 열거가 끝날 때 전송됩니다.|
|`DCEndInit_V1`|148|끝 런다운 중에 열거가 시작하기 전에 전송됩니다.|
|`DCEndComplete_V1`|146|끝 런다운 중에 열거가 끝날 때 전송됩니다.|

다음 표에서는 이벤트 데이터를 보여 줍니다.

|필드 이름|데이터 형식|설명|
|----------------|---------------|-----------------|
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|

[맨 위로 이동](#top)

<a name="clr_method_verbose_events"></a>

## <a name="clr-method-verbose-events"></a>CLR 메서드 자세한 정보 표시 이벤트

다음 표에서는 키워드와 수준을 보여 줍니다.

|이벤트를 발생시키기 위한 키워드|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) 런타임 공급자|자세한 정보 표시(5)|
|`NGenKeyword` (0x20) 런타임 공급자|자세한 정보 표시(5)|
|`JitRundownKeyword` (0x10) 런다운 공급자|자세한 정보 표시(5)|
|`NGENRundownKeyword` (0x20) 런다운 공급자|자세한 정보 표시(5)|

다음 표에서는 이벤트 정보를 보여 줍니다.

|이벤트|이벤트 ID|설명|
|-----------|--------------|-----------------|
|`MethodLoadVerbose_V1`|143|메서드가 JIT 로드되거나 NGEN 이미지가 로드될 때 발생합니다. 동적 및 제네릭 메서드는 항상 메서드 로드에 대해 이 버전을 사용합니다. JIT 도우미는 항상 이 버전을 사용합니다.|
|`MethodUnLoadVerbose_V1`|144|동적 메서드가 삭제되거나, 모듈이 언로드되거나, 애플리케이션 도메인이 삭제될 때 발생합니다. 동적 메서드는 항상 메서드 언로드에 대해 이 버전을 사용합니다.|
|`MethodDCStartVerbose_V1`|141|시작 런다운 중에 메서드를 열거합니다.|
|`MethodDCEndVerbose_V1`|142|끝 런다운 중에 메서드를 열거합니다.|

다음 표에서는 이벤트 데이터를 보여 줍니다.

|필드 이름|데이터 형식|설명|
|----------------|---------------|-----------------|
|MethodID|win:UInt64|메서드의 고유 식별자입니다. JIT 도우미 메서드의 경우 메서드의 시작 주소로 설정합니다.|
|ModuleID|win:UInt64|이 메서드가 속한 모듈의 식별자입니다(JIT 도우미의 경우 0).|
|MethodStartAddress|win:UInt64|시작 주소입니다.|
|MethodSize|win:UInt32|메서드 길이입니다.|
|MethodToken|win:UInt32|동적 메서드 및 JIT 도우미의 경우 0입니다.|
|MethodFlags|win:UInt32|0x1: 동적 메서드입니다.<br /><br /> 0x2: 제네릭 메서드입니다.<br /><br /> 0x4: JIT 컴파일된 메서드 (그렇지 않은 경우 Ngen.exe에서 생성 됨)<br /><br /> 0x8: 도우미 메서드입니다.|
|MethodNameSpace|win:UnicodeString|메서드와 연결된 전체 네임스페이스 이름입니다.|
|MethodName|win:UnicodeString|메서드와 연결된 전체 클래스 이름입니다.|
|MethodSignature|win:UnicodeString|메서드의 서명입니다(쉼표로 구분된 형식 이름 목록).|
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|

[맨 위로 이동](#top)

<a name="methodjittingstarted_event"></a>

## <a name="methodjittingstarted-event"></a>MethodJittingStarted 이벤트

다음 표에서는 키워드와 수준을 보여 줍니다.

|이벤트를 발생시키기 위한 키워드|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) 런타임 공급자|자세한 정보 표시(5)|
|`NGenKeyword` (0x20) 런타임 공급자|자세한 정보 표시(5)|
|`JitRundownKeyword` (0x10) 런다운 공급자|자세한 정보 표시(5)|
|`NGENRundownKeyword` (0x20) 런다운 공급자|자세한 정보 표시(5)|

다음 표에서는 이벤트 정보를 보여 줍니다.

|이벤트|이벤트 ID|설명|
|-----------|--------------|-----------------|
|`MethodJittingStarted`|145|메서드가 JIT로 컴파일되는 동안 발생합니다.|

다음 표에서는 이벤트 데이터를 보여 줍니다.

|필드 이름|데이터 형식|설명|
|----------------|---------------|-----------------|
|MethodID|win:UInt64|메서드의 고유 식별자입니다.|
|ModuleID|win:UInt64|이 메서드가 속한 모듈의 식별자입니다.|
|MethodToken|win:UInt32|동적 메서드 및 JIT 도우미의 경우 0입니다.|
|MethodILSize|win:UInt32|JIT로 컴파일되는 메서드에 대한 MSIL(Microsoft Intermediate Language)의 크기입니다.|
|MethodNameSpace|win:UnicodeString|메서드와 연결된 전체 클래스 이름입니다.|
|MethodName|win:UnicodeString|메서드의 이름입니다.|
|MethodSignature|win:UnicodeString|메서드의 서명입니다(쉼표로 구분된 형식 이름 목록).|
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|

## <a name="see-also"></a>참조

- [CLR ETW 이벤트](clr-etw-events.md)
