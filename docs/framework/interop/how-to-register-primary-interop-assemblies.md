---
title: '방법: 주 Interop 어셈블리 등록'
ms.date: 03/30/2017
helpviewer_keywords:
- registering primary interop assemblies
- primary interop assemblies, registering
ms.assetid: 4b2fcf8a-429d-43ce-8334-e026040be8bb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e0eeaee969eda5e4d0ea1a119991456668c7d44f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051735"
---
# <a name="how-to-register-primary-interop-assemblies"></a>방법: 주 Interop 어셈블리 등록

클래스는 COM interop에 의해서만 마샬링될 수 있으며 항상 인터페이스로 마샬링됩니다. 클래스를 마샬링하는 데 사용되는 인터페이스를 클래스 인터페이스라고 하는 경우도 있습니다. 선택한 인터페이스로 클래스 인터페이스를 재정의하는 방법에 대한 자세한 내용은 [COM 호출 가능 래퍼](../../standard/native-interop/com-callable-wrapper.md)를 참조하세요.

 .NET Framework 애플리케이션에서 COM 형식을 사용하려는 모든 개발자가 interop 어셈블리를 생성할 수 있지만 이 경우 문제가 발생합니다. 개발자가 COM 형식 라이브러리를 가져오고 서명할 때마다 다른 개발자가 가져오고 서명한 형식과 호환되지 않는 고유한 형식 집합이 생성됩니다. 이러한 형식 비호환성 문제에 대한 해결 방법은 각 개발자가 공급업체에서 제공하고 서명한 주 interop 어셈블리를 가져오는 것입니다.

 타사 COM 형식을 다른 애플리케이션에 노출하려는 경우 항상 정의하는 형식 라이브러리와 동일한 게시자가 제공한 주 interop 어셈블리를 사용합니다. 보장된 형식 호환성을 제공할 뿐 아니라 주 interop 어셈블리는 상호 운용성을 향상시키기 위해 공급업체에서 사용자 지정되는 경우도 많습니다.

 타사 COM 형식을 노출하지 않으려는 경우에도 주 interop 어셈블리를 사용하면 COM 구성 요소와의 상호 운용 작업이 쉬워질 수 있습니다. 그러나 이 전략은 공급업체가 주 interop 어셈블리에서 정의된 형식에 대해 수행할 수 있는 변경 내용으로부터 단절을 제공하지 않습니다. 애플리케이션에 이러한 단절이 필요한 경우 주 interop 어셈블리를 사용하는 대신 고유한 interop 어셈블리를 생성합니다.

 Visual Studio를 사용하여 참조하려면 먼저 가져온 모든 주 interop 어셈블리를 개발 컴퓨터에 등록해야 합니다. Visual Studio는 COM 형식 라이브러리의 형식을 처음 참조할 때 주 interop 어셈블리를 찾아서 사용합니다. Visual Studio가 형식 라이브러리와 연결된 주 interop 어셈블리를 찾을 수 없는 경우 가져오거나 대신 interop 어셈블리를 만들라는 메시지가 표시됩니다. 마찬가지로, [형식 라이브러리 가져오기(Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md)도 레지스트리를 사용하여 주 interop 어셈블리를 찾습니다.

 Visual Studio를 사용하려는 경우가 아니면 주 interop 어셈블리를 등록할 필요는 없지만 등록 시 다음과 같은 두 가지 이점이 있습니다.

- 등록된 주 interop 어셈블리가 원래 형식 라이브러리의 레지스트리 키 아래에 명확하게 표시됩니다. 등록이 컴퓨터에서 주 interop 어셈블리를 찾는 최상의 방법입니다.

- 나중에 Visual Studio를 사용하여 등록되지 않은 주 interop 어셈블리가 있는 형식을 참조할 경우 실수로 새 interop 어셈블리를 생성 및 사용하는 것을 방지할 수 있습니다.

[어셈블리 등록 도구(Regasm.exe)](../tools/regasm-exe-assembly-registration-tool.md)를 사용하여 주 interop 어셈블리를 등록할 수 있습니다.

## <a name="to-register-a-primary-interop-assembly"></a>주 Interop 어셈블리를 등록하려면

1. 명령 프롬프트에서 다음을 입력합니다.

     **regasm** *assemblyname*

     이 명령에서 *assemblyname*은 등록된 어셈블리의 파일 이름입니다. Regasm.exe는 원래 형식 라이브러리와 동일한 레지스트리 키 아래에 주 interop 어셈블리에 대한 항목을 추가합니다.

## <a name="example"></a>예제
 다음 예제에서는 `CompanyA.UtilLib.dll` 주 interop 어셈블리를 등록합니다.

```console
regasm CompanyA.UtilLib.dll
```

## <a name="see-also"></a>참고 항목

- [주 Interop 어셈블리를 사용한 프로그래밍](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/baxfadst(v=vs.100))
- [주 Interop 어셈블리 찾기](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/y06sxw56(v=vs.100))
- [기본 Interop 어셈블리 재배포](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w0dt2w20(v=vs.100))
