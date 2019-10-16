---
title: 형식 라이브러리를 어셈블리로 가져오기
ms.date: 03/30/2017
helpviewer_keywords:
- importing type library
- type metadata
- custom wrappers
- metadata
- exposing COM components to .NET Framework
- Type Library Importer
- interoperation with unmanaged code, importing type library
- interoperation with unmanaged code, exposing COM components
- type libraries
- TypeLibConverter class, importing type library as assembly
- COM interop, importing type library
- COM interop, exposing COM components
ms.assetid: d1898229-cd40-426e-a275-f3eb65fbc79f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: db9571a2d07bcdf9830ef93cd07a5dae912f4677
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051716"
---
# <a name="importing-a-type-library-as-an-assembly"></a>형식 라이브러리를 어셈블리로 가져오기

COM 형식 정의는 일반적으로 형식 라이브러리에 있습니다. 반면 CLS 규격 컴파일러는 어셈블리에서 형식 메타데이터를 생성합니다. 형식 정보의 두 가지 소스는 약간 다릅니다. 이 항목에서는 형식 라이브러리에서 메타데이터를 생성하기 위한 기술을 설명합니다. 결과 어셈블리를 interop 어셈블리라고 하고 포함된 형식 정보를 통해 .NET Framework 애플리케이션이 COM 형식을 사용할 수 있습니다.

이 형식 정보를 애플리케이션에서 사용할 수 있도록 설정하는 두 가지 방법이 있습니다.

- 디자인 타임 전용 interop 어셈블리 사용: .NET Framework 4부터 interop 어셈블리의 형식 정보를 실행 파일에 포함하도록 컴파일러에 지시할 수 있습니다. 컴파일러는 애플리케이션에서 사용하는 형식 정보만 포함합니다. Interop 어셈블리를 애플리케이션에 배포할 필요는 없습니다. 이것이 권장되는 방법입니다.

- interop 어셈블리 배포: interop 어셈블리에 대한 표준 참조를 만들 수 있습니다. 이 경우 interop 어셈블리를 애플리케이션에 배포해야 합니다. 이 방법을 적용하는데 전용 COM 구성 요소를 사용하지 않을 경우 관리 코드에 통합하려는 COM 구성 요소의 작성자가 게시한 PIA(주 interop 어셈블리)를 항상 참조하세요. 주 interop 어셈블리를 생성 및 사용하는 방법에 대한 자세한 내용은 [주 Interop 어셈블리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aax7sdch(v=vs.100))를 참조하세요.

디자인 타임 전용 interop 어셈블리를 사용할 경우 COM 구성 요소의 작성자가 게시한 주 interop 어셈블리의 형식 정보를 포함할 수 있습니다. 그러나 주 interop 어셈블리를 애플리케이션에 배포할 필요는 없습니다.

대부분의 애플리케이션에서는 COM 구성 요소의 일부 기능을 사용하지 않으므로 디자인 타임 전용 interop 어셈블리를 사용하면 애플리케이션 크기가 감소합니다. 컴파일러가 형식 정보를 포함하면 매우 효율적으로 작동합니다. 애플리케이션이 COM 인터페이스에서 일부 메서드만 사용할 경우 컴파일러는 사용되지 않는 메서드를 포함하지 않습니다. 형식 정보가 포함된 애플리케이션이 이와 같은 다른 애플리케이션과 상호 작용하거나 주 interop 어셈블리를 사용하는 애플리케이션과 상호 작용하면 공용 언어 런타임은 형식 동등성 규칙을 사용하여 같은 이름의 두 가지 형식이 동일한 COM 형식을 나타내는지 확인합니다. COM 개체를 사용하기 위해 이러한 규칙을 알 필요는 없습니다. 그러나 규칙에 관심이 있다면 [형식 동등성 및 포함된 Interop 형식](type-equivalence-and-embedded-interop-types.md)을 참조하세요.

## <a name="generating-metadata"></a>메타데이터 생성

COM 형식 라이브러리는 확장명이 .tlb인 독립 실행형 파일일 수 있습니다(예: Loanlib.tlb). 일부 형식 라이브러리는 .dll 또는 .exe 파일의 리소스 섹션에 포함됩니다. 형식 라이브러리 정보의 기타 소스는 .olb 및 .ocx 파일입니다.

대상 COM 형식의 구현이 포함된 형식 라이브러리를 찾은 후 다음 옵션을 사용하여 형식 메타데이터가 포함된 interop 어셈블리를 생성합니다.

- Visual Studio

  Visual Studio는 형식 라이브러리의 COM 형식을 어셈블리의 메타데이터로 자동으로 변환합니다. 자세한 내용은 [방법: 형식 라이브러리에 참조 추가](how-to-add-references-to-type-libraries.md).

- [형식 라이브러리 가져오기(Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md)

  형식 라이브러리 가져오기는 결과 interop 파일에서 메타데이터를 조정하고, 기존 형식 라이브러리에서 형식을 가져오고, interop 어셈블리 및 네임스페이스를 생성하기 위한 명령줄 옵션을 제공합니다. 자세한 내용은 [방법: 형식 라이브러리에서 Interop 어셈블리 생성](how-to-generate-interop-assemblies-from-type-libraries.md)을 참조하세요.

- <xref:System.Runtime.InteropServices.TypeLibConverter?displayProperty=nameWithType> 클래스

  이 클래스는 형식 라이브러리의 coclass 및 인터페이스를 어셈블리 내의 메타데이터로 변환하기 위한 메서드를 제공합니다. 이 클래스는 Tlbimp.exe와 동일한 메타데이터 출력을 생성합니다. 그러나 Tlbimp.exe와 달리 <xref:System.Runtime.InteropServices.TypeLibConverter> 클래스는 메모리 내 형식 라이브러리를 메타데이터로 변환할 수 있습니다.

- 사용자 지정 래퍼

  형식 라이브러리가 사용 불가능하거나 잘못된 경우 한 가지 옵션은 관리 소스 코드에서 클래스 또는 인터페이스에 대한 중복 정의를 만드는 것입니다. 그런 다음 런타임을 대상으로 하는 컴파일러로 소스 코드를 컴파일하여 어셈블리에서 메타데이터를 생성합니다.

  COM 형식을 수동으로 정의하려면 다음 항목에 액세스할 수 있어야 합니다.

  - 정의되는 coclass 및 인터페이스에 대한 자세한 설명.

  - 해당하는 .NET Framework 클래스 정의를 생성할 수 있는 컴파일러(예: C# 컴파일러).

  - 형식 라이브러리-어셈블리 변환 규칙에 대한 이해.

  사용자 지정 래퍼를 작성하는 것은 고급 기술입니다. 사용자 지정 래퍼를 생성하는 방법에 대한 자세한 내용은 [표준 래퍼 사용자 지정](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/h7hx9abd(v=vs.100))을 참조하세요.

 COM interop 가져오기 프로세스에 대한 자세한 내용은 [형식 라이브러리를 어셈블리로 변환 요약](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))을 참조하세요.

## <a name="see-also"></a>참고 항목

- <xref:System.Runtime.InteropServices.TypeLibConverter>
- [.NET Framework에 COM 구성 요소 노출](exposing-com-components.md)
- [형식 라이브러리를 어셈블리로 변환 요약](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))
- [Tlbimp.exe(형식 라이브러리 가져오기)](../tools/tlbimp-exe-type-library-importer.md)
- [표준 래퍼 사용자 지정](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/h7hx9abd(v=vs.100))
- [관리 코드에서 COM 형식 사용](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3y76b69k(v=vs.100))
- [Interop 프로젝트 컴파일](compiling-an-interop-project.md)
- [Interop 애플리케이션 배포](deploying-an-interop-application.md)
- [방법: 형식 라이브러리에 참조 추가](how-to-add-references-to-type-libraries.md)
- [방법: 형식 라이브러리에서 Interop 어셈블리 생성](how-to-generate-interop-assemblies-from-type-libraries.md)
