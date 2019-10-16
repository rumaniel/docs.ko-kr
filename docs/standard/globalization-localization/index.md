---
title: .NET 애플리케이션 전역화 및 지역화
ms.date: 06/08/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- international applications [.NET]
- globalization [.NET], encoding
- global applications
- internationalization
- world-ready applications
- application development [.NET], globalization
- multilingual application development
ms.assetid: 9a59696b-d89b-45bd-946d-c75da4732d02
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 501e23656b3a31dc14e0b2213252ef52c598140f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64622637"
---
# <a name="globalizing-and-localizing-net-applications"></a>.NET 애플리케이션 전역화 및 지역화

하나 이상의 언어로 지역화할 수 있는 애플리케이션을 포함하여 지역화 대비 애플리케이션의 개발에는 세계화, 지역화 가능성 검토 및 지역화의 세 가지 단계가 포함됩니다.

[전역화](globalization.md)

이 단계에는 문화적, 언어적으로 중립적이고 지역화된 사용자 인터페이스 및 모든 사용자의 지역 데이터를 지원하는 애플리케이션을 디자인하고 코딩하는 데 과정이 포함됩니다. 문화권별 가정을 기준으로 하지 않는 디자인 및 프로그래밍 결정이 포함됩니다. 전역화된 애플리케이션은 지역화되지 않아도 하나 이상의 언어로 비교적 쉽게 지역화될 수 있도록 설계 및 작성됩니다.

[지역화 가능성 검토](localizability-review.md)

이 단계에는 손쉽게 지역화할 수 있는지 확인하고 지역화하는 데 발생할 수 있는 장애물을 식별하도록 애플리케이션의 코드 및 디자인을 검토하고 애플리케이션의 실행 파일 코드를 리소스와 분리할 수 있는지를 확인하는 데 과정이 포함됩니다. 전역화 단계가 유효한 경우 지역화 검토는 전역화 중에 선택한 디자인과 코딩을 확인합니다. 또한 지역화 가능성 단계에서 남아 있는 문제를 파악하여 지역화 단계에서 애플리케이션의 소스 코드를 수정할 필요가 없도록 할 수 있습니다.

[지역화](localization.md)

이 단계에서는 특정 문화권 또는 지역에 대해 애플리케이션을 사용자 지정합니다. 전역화 및 지역화 가능성 확인 단계가 제대로 수행되었다면 지역화 작업은 주로 사용자 인터페이스의 번역으로 구성됩니다.

다음 세 단계에는 두 가지 장점이 있습니다.

- 미국 영어와 같은 단일 문화권을 지원하도록 설계된 애플리케이션을 추가 문화권을 지원하기 위해 수정할 필요가 없습니다.

- 그 결과, 보다 안정적이며 버그 발생이 적은 지역화된 애플리케이션이 구현됩니다.

.NET에서는 전 세계를 대상으로 지역화되는 애플리케이션 개발을 위해 광범위한 지원을 제공합니다. 특히 .NET 클래스 라이브러리의 많은 형식 멤버는 현재 사용자의 문화권 또는 지정된 문화권의 규약을 반영하는 값을 반환함으로써 전역화를 지원합니다. 또한 .NET은 애플리케이션 지역화 프로세스를 용이하게 하는 위성 어셈블리를 지원합니다.

자세한 내용은 [세계화 설명서](/globalization/)를 참조하세요.

## <a name="in-this-section"></a>단원 내용

[전역화](globalization.md)

문화권과 언어에 중립적인 애플리케이션을 디자인하고 코딩하는 것을 포함하여 지역화 대비 애플리케이션을 만드는 첫 번째 단계를 설명합니다.

[지역화 가능성 검토](localizability-review.md)

지역화하는 데 발생할 수 있는 장애물을 식별하는 것을 포함하여 지역화된 애플리케이션을 만드는 두 번째 단계에 대해 설명합니다.

[지역화](localization.md)

특정 지역 또는 문화권에 대한 애플리케이션 사용자 인터페이스 사용자 지정을 포함하는 지역화된 애플리케이션을 만드는 최종 단계를 설명합니다.

[문화권을 구분하지 않는 문자열 작업](culture-insensitive-string-operations.md)

기본적으로 문화권에 따라 다른 .NET 메서드 및 클래스를 사용하여 문화권을 구분하지 않는 결과를 얻는 방법에 대해 설명합니다.

[지역화 대비 애플리케이션 개발을 위한 최선의 구현 방법](best-practices-for-developing-world-ready-apps.md)

전역화 및 지역화 구현과 world-ready ASP.NET 애플리케이션 개발을 위한 최선의 구현 방법을 소개합니다.

## <a name="reference"></a>참조

- <xref:System.Globalization?displayProperty=nameWithType> 네임스페이스

   언어, 국가/지역, 사용하는 달력, 날짜, 통화 및 숫자 형식 패턴, 문자열 정렬 순서 등의 문화권 관련 정보를 정의하는 클래스를 포함합니다.

- <xref:System.Resources> 네임스페이스

   리소스를 만들고 조작하고 사용하기 위한 클래스를 제공합니다.

- <xref:System.Text> 네임스페이스

   ASCII, ANSI, 유니코드 및 기타 문자 인코딩을 나타내는 클래스를 포함합니다.

- [Resgen.exe(리소스 파일 생성기)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md)

   Resgen.exe를 사용하여 .txt 파일 및 .resx(XML 기반 리소스 형식) 파일을 공용 언어 런타임 바이너리 .resources 파일로 변환하는 방법에 대해 설명합니다.

- [Winres.exe(Windows Forms 리소스 편집기)](../../../docs/framework/tools/winres-exe-windows-forms-resource-editor.md)

   Winres.exe를 사용하여 Windows Forms 폼을 지역화하는 방법을 설명합니다.
