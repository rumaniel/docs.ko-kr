---
title: .NET Framework 애플리케이션의 COM 상호 운용성(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- interoperability, COM and .NET framework objects
- COM interop [Visual Basic]
- shared components
ms.assetid: f5a72143-c268-4dff-a019-974ad940e17d
ms.openlocfilehash: 758f065d2e0e7f8200529ef171dc89f94950b46e
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68627095"
---
# <a name="com-interoperability-in-net-framework-applications-visual-basic"></a>.NET Framework 애플리케이션의 COM 상호 운용성(Visual Basic)

COM 개체를 사용 하 고 동일한 응용 프로그램에서 개체를 .NET Framework 하려면 개체가 메모리에 존재 하는 방식의 차이를 해결 해야 합니다. .NET Framework 개체는 관리 되는 메모리 (공용 언어 런타임에 의해 제어 되는 메모리)에 있으며 필요에 따라 런타임에 의해 이동 될 수 있습니다. COM 개체는 관리 되지 않는 메모리에 있으며 다른 메모리 위치로 이동할 수 없습니다. Visual Studio 및 .NET Framework는 이러한 관리 되는 구성 요소와 관리 되지 않는 구성 요소의 상호 작용을 제어 하는 도구를 제공 합니다. 관리 코드에 대 한 자세한 내용은 [공용 언어 런타임](../../../standard/clr.md)을 참조 하세요.

.NET 응용 프로그램에서 COM 개체를 사용 하는 것 외에도 Visual Basic를 사용 하 여 COM을 통해 비관리 코드에서 액세스할 수 있는 개체를 개발할 수 있습니다.

이 페이지의 링크는 COM과 .NET Framework 개체 간의 상호 작용에 대 한 세부 정보를 제공 합니다.

## <a name="related-sections"></a>관련 단원

| | |
|---------|---------|
| [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md) | Com 개체, ActiveX 컨트롤, Win32 Dll, 관리 되는 개체 및 COM 개체의 상속을 비롯 하 여 Visual Basic의 COM 상호 운용성을 다루는 항목에 대 한 링크를 제공 합니다. |
| [비관리 코드와의 상호 운용](../../../framework/interop/index.md) | 관리 코드와 비관리 코드 간의 상호 작용 문제 중 일부에 대해 간략하게 설명 하 고 추가 조사를 위한 링크를 제공 합니다. |
| [COM 래퍼](../../../standard/native-interop/com-wrappers.md) | 관리 코드에서 COM 메서드를 호출할 수 있도록 하는 런타임 호출 가능 래퍼와 com 클라이언트에서 .NET 개체 메서드를 호출할 수 있도록 하는 COM 호출 가능 래퍼에 대해 설명 합니다. |
| [고급 COM 상호 운용성](../../../framework/interop/index.md) | 래퍼, 예외, 상속, 스레딩, 이벤트, 변환 및 마샬링과 관련 하 여 COM 상호 운용성을 다루는 항목의 링크를 제공 합니다. |
| [Tlbimp.exe(형식 라이브러리 가져오기)](../../../framework/tools/tlbimp-exe-type-library-importer.md) | COM 형식 라이브러리에 있는 형식 정의를 공용 언어 런타임 어셈블리의 동등한 정의로 변환 하는 데 사용할 수 있는 도구에 대해 설명 합니다. |
