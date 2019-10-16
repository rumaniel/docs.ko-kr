---
ms.openlocfilehash: db1d09c8c9e606b5327a42977a74a74703282d84
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72237413"
---
### <a name="net-core-30-follows-unicode-best-practices-when-replacing-ill-formed-utf-8-byte-sequences"></a>.NET Core 3.0이 잘못된 형식의 UTF-8 바이트 시퀀스를 대체할 때 유니코드 모범 사례를 적용

<xref:System.Text.UTF8Encoding> 클래스는 바이트-문자 트랜스코딩을 수행하는 동안 잘못된 형식의 UTF-8 바이트 시퀀스가 발견되면 출력 문자열에서 해당 시퀀스를 ‘�' 문자(U+FFFD 대체 문자)로 바꿉니다. .NET Core 3.0은 이전 버전의 .NET Core 및 .NET Framework와 달리 트랜스코딩 작업 도중 이 대체를 수행하기 위해 유니코드 모범 사례를 따릅니다.

이는 새로운 <xref:System.Text.Unicode.Utf8?displayProperty=nameWithType> 및 <xref:System.Text.Rune?displayProperty=nameWithType> 형식을 포함하여 .NET 전체에서 UTF-8 처리를 향상하기 위해 기울인 보다 많은 노력의 일환입니다. <xref:System.Text.UTF8Encoding> 형식에는 새로 도입된 형식과 일치하는 출력을 생성하도록 향상된 오류 처리 메커니즘이 적용되었습니다.

#### <a name="change-description"></a>변경 내용 설명

.Net Core 3.0부터 바이트를 문자로 트랜스코딩하는 경우 <xref:System.Text.UTF8Encoding> 클래스는 유니코드 모범 사례를 기반으로 문자 대체를 수행합니다. 사용되는 대체 메커니즘은 _최대 하위 부분의 U+FFFD 대체_ 항목의 [유니코드 표준 버전 12.0, 섹션 3.9(PDF)](https://www.unicode.org/versions/Unicode12.0.0/ch03.pdf)에서 설명합니다.

이 동작은 입력 바이트 시퀀스에 잘못된 형식의 UTF-8 데이터가 포함된 _경우에만_ 적용됩니다. 또한 <xref:System.Text.UTF8Encoding> 인스턴스가 `throwOnInvalidBytes: true`를 사용하여 생성된 경우([UTF8Encoding 생성자 설명서] 참조)(<xref:System.Text.UTF8Encoding.%23ctor(System.Boolean,System.Boolean)>) `UTF8Encoding` 인스턴스는 U+FFFD 대체를 수행하는 대신 잘못된 입력에 대해 계속 throw합니다.

다음은 이 변경이 잘못된 3바이트 입력에 미치는 영향입니다.

|잘못된 형식의 3바이트 입력|.NET Core 3.0 이하의 출력|.NET Core 3.0 이상의 출력|
|---|---|---|
| `[ ED A0 90 ]` | `[ FFFD FFFD ]`(2자 출력)| `[ FFFD FFFD FFFD ]`(3자 출력)|

이 3자 출력은 위에 링크된 유니코드 표준 PDF의 _표 3-9_에 따라 선호되는 출력입니다.

#### <a name="version-introduced"></a>도입된 버전

3.0

#### <a name="recommended-action"></a>권장 작업

개발자는 아무 작업도 수행하지 않아도 됩니다.

#### <a name="category"></a>범주

CoreFx

#### <a name="affected-apis"></a>영향을 받는 API

- <xref:System.Text.UTF8Encoding.GetCharCount%2A?displayProperty=nameWithType>
- <xref:System.Text.UTF8Encoding.GetChars%2A?displayProperty=nameWithType>
- <xref:System.Text.UTF8Encoding.GetString(System.Byte[],System.Int32,System.Int32)?displayProperty=nameWithType>

<!--

### Affected APIs

- `Overload:System.Text.UTF8Encoding.GetCharCount`
- `Overload:System.Text.UTF8Encoding.GetChars`
- `M:System.Text.UTF8Encoding.GetString(System.Byte[],System.Int32,System.Int32)`

-->
