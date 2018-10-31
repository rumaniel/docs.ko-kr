---
title: 버전 2.0에서 System.Uri 네임스페이스 변경 내용
ms.date: 03/30/2017
ms.assetid: 35883fe9-2d09-4d8b-80ca-cf23a941e459
ms.openlocfilehash: 987010b8367069e8089df3f809d23f258bb68f2b
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50188438"
---
# <a name="changes-to-the-systemuri-namespace-in-version-20"></a>버전 2.0에서 System.Uri 네임스페이스 변경 내용

<xref:System.Uri?displayProperty=nameWithType> 클래스에 몇 가지 변경 내용이 적용되었습니다. 이러한 변경 내용은 잘못된 동작을 수정하고, 유용성을 개선하고, 보안을 강화했습니다.

## <a name="obsolete-and-deprecated-members"></a>더 이상 사용되지 않는 멤버

 생성자:

- `dontEscape` 매개 변수가 있는 모든 생성자.

 메서드:

- <xref:System.Uri.CheckSecurity%2A>

- <xref:System.Uri.Escape%2A>

- <xref:System.Uri.Canonicalize%2A>

- <xref:System.Uri.Parse%2A>

- <xref:System.Uri.IsReservedCharacter%2A>

- <xref:System.Uri.IsBadFileSystemCharacter%2A>

- <xref:System.Uri.IsExcludedCharacter%2A>

- <xref:System.Uri.EscapeString%2A>

## <a name="changes"></a>변경 내용

- 쿼리 부분(file, ftp 등)이 없는 것으로 알려진 URI 체계에서는 ‘?’ 문자가 항상 이스케이프되고 <xref:System.Uri.Query%2A> 부분의 시작으로 간주되지 않습니다.

- 암시적 파일 URI(`c:\directory\file@name.txt` 형식)의 경우 전체 이스케이프 취소가 요청되거나 <xref:System.Uri.LocalPath%2A>가 `true`인 경우가 아니면 조각 문자(‘#’)가 항상 이스케이프됩니다.

- UNC 호스트 이름 지원이 제거되었습니다. 국제 호스트 이름을 나타내기 위한 IDN 사양이 채택되었습니다.

- <xref:System.Uri.LocalPath%2A>는 항상 완전히 이스케이프 해제된 문자열을 반환합니다.

- <xref:System.Uri.ToString%2A>은 이스케이프된 ‘%’, ‘?’ 또는 ‘#’ 문자의 이스케이프를 해제하지 않습니다.

- 이제 <xref:System.Uri.Equals%2A>의 동등성 검사에 <xref:System.Uri.Query%2A> 부분이 포함됩니다.

- 연산자 “= =” 및 “!=”가 재정의되고 <xref:System.Uri.Equals%2A> 메서드에 연결됩니다.

- 이제 <xref:System.Uri.IsLoopback%2A>에서 일관된 결과를 생성합니다.

- URI “`file:///path`”가 더 이상 `file://path`로 변환되지 않습니다.

- 아재 “#”이 호스트 이름 종결자로 인식됩니다. 즉, `http://contoso.com#fragment`는 이제 `http://contoso.com/#fragment`로 변환됩니다.

- 기본 URI와 조각을 결합할 때 발생하는 버그가 수정되었습니다.

- <xref:System.Uri.HostNameType%2A>의 버그가 수정되었습니다.

- NNTP 구문 분석의 버그가 수정되었습니다.

- 이제 HTTP:contoso.com 형식의 URI가 구문 분석 예외를 throw합니다.

- 프레임워크에서 URI의 사용자 정보를 올바르게 처리합니다.

- 끊어진 URI가 루트 위의 파일 시스템을 트래버스할 수 없도록 URI 경로 압축이 수정되었습니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Uri?displayProperty=nameWithType>
