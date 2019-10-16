---
ms.openlocfilehash: 58d1c8cd3aff52703522391c14348bd81c108587
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72237414"
---
### <a name="custom-encoderfallbackbuffer-instances-cannot-fall-back-recursively"></a>사용자 지정 EncoderFallbackBuffer 인스턴스는 재귀적으로 대체될 수 없음

사용자 지정 <xref:System.Text.EncoderFallbackBuffer> 인스턴스는 재귀적으로 대체될 수 없습니다. <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType>를 구현하면 대상 인코딩으로 변환할 수 있는 문자 시퀀스가 생겨야 합니다. 그렇지 않으면 예외가 발생합니다.

#### <a name="change-description"></a>변경 내용 설명

런타임은 문자-바이트 트랜스코딩 작업 도중 형식이 잘못되었거나 변환할 수 없는 UTF-16 시퀀스를 검색하여 해당 문자를 <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> 메서드에 제공합니다. `Fallback` 메서드는 변환할 수 없는 원래 데이터를 대체할 문자를 결정하며, 이러한 문자는 루프에서 <xref:System.Text.EncoderFallbackBuffer.GetNextChar%2A?displayProperty=nameWithType>를 호출하여 드레이닝됩니다.

그런 다음 런타임은 이러한 대체 문자를 대상 인코딩으로 트랜스코딩하려고 합니다. 이 작업이 성공하면 런타임은 원래 입력 문자열에서 중단된 위치에서 트랜스코딩을 계속 실행합니다.

.Net Core 미리 보기 7 버전 이하에서 <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType>에 대한 사용자 지정 구현은 대상 인코딩으로 변환할 수 없는 문자 시퀀스를 반환할 수 있습니다. 대체된 문자를 대상 인코딩으로 변환할 수 없는 경우 런타임은 대체 문자를 사용하여 <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> 메서드를 다시 한 번 호출하여 <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType> 메서드가 새 대체 시퀀스를 반환할 것을 예상합니다. 이 프로세스는 런타임이 올바른 형식의 변환 가능한 대체를 확인하거나 최대 재귀 횟수에 도달할 때까지 계속됩니다.

.Net Core 3.0부터 <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType>에 대한 사용자 지정 구현은 대상 인코딩으로 변환할 수 있는 문자 시퀀스를 반환해야 합니다. 대체된 문자를 대상 인코딩으로 트랜스 코딩할 수 없으면 <xref:System.ArgumentException>이 throw됩니다. 런타임은 더 이상 <xref:System.Text.EncoderFallbackBuffer> 인스턴스에 대한 재귀 호출을 수행하지 않습니다.

이 동작은 다음 조건 중 세 가지를 모두 충족하는 경우에만 적용됩니다.

- 런타임은 잘못된 형식의 UTF-16 시퀀스 또는 대상 인코딩으로 변환할 수 없는 UTF-16 시퀀스를 검색합니다.
- 사용자 지정 <xref:System.Text.EncoderFallback>이 지정되었습니다.
- 사용자 지정 <xref:System.Text.EncoderFallback>은 잘못된 형식이거나 변환할 수 없는 새 UTF-16 시퀀스를 대체하려고 시도합니다.

#### <a name="version-introduced"></a>도입된 버전

3.0

#### <a name="recommended-action"></a>권장 작업

대부분의 개발자는 아무 작업도 수행하지 않아도 됩니다.

애플리케이션이 사용자 지정 <xref:System.Text.EncoderFallback> 및 <xref:System.Text.EncoderFallbackBuffer> 클래스를 사용하는 경우 런타임이 처음 <xref:System.Text.EncoderFallbackBuffer.Fallback%2A> 메서드를 호출할 때 <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> 구현이 대상 인코딩으로 직접 변환할 수 있는 올바른 형식의 UTF-16 데이터로 대체 버퍼를 채우도록 합니다.

#### <a name="category"></a>범주

CoreFx

#### <a name="affected-apis"></a>영향을 받는 API

- <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType>
- <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType>

<!--

### Affected APIs

- `Overload:System.Text.EncoderFallbackBuffer.Fallback`
- `M:System.Text.EncoderFallbackBuffer.GetNextChar`

-->
