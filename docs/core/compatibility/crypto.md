---
title: 암호화 관련 호환성이 손상되는 변경, 버전 2.2-3.0 - .NET Core
description: .NET Core, ASP.NET Core, EF Core 버전 2.2에서 버전 3.0으로의 호환성이 손상되는 변경 사항 사항을 나열합니다.
ms.date: 09/10/2019
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 44caf042404d44ec4c5cb7b7e25883d8460efeb5
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216944"
---
# <a name="breaking-changes-for-migration-from-version-22-to-30"></a>버전 2.2에서 3.0으로 마이그레이션 시 호환성이 손상되는 변경 내용

> [!IMPORTANT]
> 이 문서는 작성 중입니다. 이것은 .NET Core 호환성이 손상되는 변경 사항의 완전한 목록이 아닙니다. .NET Core 호환성이 손상되는 변경 사항에 대한 자세한 내용은 GitHub의 dotnet/docs 리포지토리에 있는 개별 [호환성이 손상되는 변경 문제](https://github.com/dotnet/docs/issues?q=is%3Aissue+is%3Aopen+label%3Abreaking-change)에서 검토할 수 있습니다. 

.NET Core, ASP.NET Core 또는 EF Core 버전 2.2에서 버전 3.0으로 마이그레이션하는 경우, 앱에 영향을 줄 수 있는 호환성이 손상되는 변경에 대한 다음 항목을 검토하세요.

## <a name="corefx"></a>CoreFx

[!INCLUDE[APIs that report version now report product and not file version](~/includes/core-changes/corefx/version-information-changes.md)]

***

[!INCLUDE[Custom EncoderFallbackBuffer instances cannot fall back recursively](~/includes/core-changes/corefx/custom-encoderfallbackbuffer-cannot-be-recursive.md)]

***

[!INCLUDE[Floating point formatting and parsing behavior changes](~/includes/core-changes/corefx/floating-point-changes.md)]

***

[!INCLUDE[InvalidAsynchronousStateException moved to another assembly](~/includes/core-changes/corefx/move-invalidasynchronousstateexception.md)]

***

[!INCLUDE[NET Core 3.0 follows Unicode best practices when replacing ill-formed UTF-8 byte sequences](~/includes/core-changes/corefx/net-core-3-0-follows-unicode-utf8-best-practices.md)]

***

[!INCLUDE[TypeDescriptionProviderAttribute moved to another assembly](~/includes/core-changes/corefx/move-typedescriptionproviderattribute.md)]

***

[!INCLUDE[ZipArchiveEntry no longer handles archives with inconsistent entry sizes](~/includes/core-changes/corefx/ziparchiveentry-and-inconsistent-entry-sizes.md)]

## <a name="cryptography"></a>암호화

[!INCLUDE[EnvelopedCms defaults to AES-256 encryption](~/includes/core-changes/cryptography/envelopedcms-defaults-to-aes256.md)]

***

[!INCLUDE[Minimum size for RSAOpenSsl key generation has increased](~/includes/core-changes/cryptography/minimum-rsaopenssl-key-size-change.md)]

***

[!INCLUDE[.NET Core 3.0 prefers OpenSSL 1.1.x to OpenSSL 1.0.x](~/includes/core-changes/cryptography/net-core-3-0-prefers-openssl-1-1-x.md)]

## <a name="globalization"></a>전역화

[!INCLUDE["C" locale maps to the invariant locale](~/includes/core-changes/globalization/c-locale-maps-to-invariant-locale.md)]

## <a name="visual-basic"></a>Visual Basic

[!INCLUDE[vbNewLine is obsolete](~/includes/core-changes/visualbasic/vbnewline-is-obsolete.md)]

## <a name="entity-framework-core"></a>Entity Framework Core

[Entity Framework Core 호환성이 손상되는 변경 사항](/ef/core/what-is-new/ef-core-3.0/breaking-changes)
