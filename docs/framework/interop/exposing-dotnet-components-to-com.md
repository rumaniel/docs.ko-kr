---
title: .NET 구성 요소를 COM에 공개
ms.date: 03/30/2017
helpviewer_keywords:
- exposing .NET Framework components to COM
- interoperation with unmanaged code, exposing .NET Framework components
- COM interop, exposing COM components
ms.assetid: e42a65f7-1e61-411f-b09a-aca1bbce24c6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: db4380e97cf4d556248f42981b350160710f1dd8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051811"
---
# <a name="exposing-net-components-to-com"></a>.NET 구성 요소를 COM에 공개

.NET 형식을 작성하고 비관리 코드에서 해당 형식을 사용하는 것은 개발자들에게 독특한 활동입니다. 이 섹션에서는 COM 클라이언트와 통합되는 관리 코드를 작성하기 위한 몇 가지 팁을 설명합니다.

- [상호 운용할 .NET 형식을 정규화합니다](../../standard/native-interop/qualify-net-types-for-interoperation.md).

     COM에 노출할 모든 관리되는 형식, 메서드, 속성, 필드 및 이벤트는 공용이어야 합니다. 형식에는 COM을 통해 호출될 수 있는 유일한 생성자인 공용 매개 변수가 없는 생성자가 있어야 합니다.

- [Interop 특성을 적용합니다](../../standard/native-interop/apply-interop-attributes.md).

     관리 코드 내의 사용자 지정 특성은 구성 요소의 상호 운용성을 개선할 수 있습니다.

- [COM에 대한 어셈블리를 패키지합니다](packaging-an-assembly-for-com.md).

     COM 개발자는 어셈블리를 참조 및 배포하는 작업에 관련된 단계를 요약하도록 요구할 수 있습니다.

 또한 이 섹션에서는 COM 클라이언트에서 관리되는 형식을 사용하는 것과 관련된 작업을 확인합니다.

## <a name="to-consume-a-managed-type-from-com"></a>COM에서 관리되는 형식을 사용하려면

1. [COM에 어셈블리를 등록합니다](registering-assemblies-with-com.md).

     어셈블리의 형식(및 형식 라이브러리)은 디자인 타임에 등록되어야 합니다. 설치 관리자가 어셈블리를 등록하지 않으면 COM 개발자에게 Regasm.exe를 사용하도록 지시합니다.

2. [COM에서 .NET 형식을 참조합니다](how-to-reference-net-types-from-com.md).

     COM 개발자는 현재 사용하는 동일한 도구와 기술을 통해 어셈블리에서 형식을 참조할 수 있습니다.

3. [.NET 개체를 호출합니다](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8hw8h46b(v=vs.100)).

     COM 개발자는 관리되는 형식에서 메서드를 호출하는 동일한 방법으로 .NET 개체에서 메서드를 호출할 수 있습니다. 예를 들어 COM **CoCreateInstance** API는 .NET 개체를 활성화합니다.

4. [COM 액세스를 위해 애플리케이션을 배포합니다](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/c2850st8(v=vs.100)).

     강력한 이름의 어셈블리는 전역 어셈블리 캐시에 설치할 수 있고 게시자의 시그니처가 필요합니다. 강력한 이름이 아닌 어셈블리는 클라이언트의 애플리케이션 디렉터리에 설치해야 합니다.

## <a name="see-also"></a>참고 항목

- [비관리 코드와의 상호 운용](index.md)
- [COM Interop 샘플: COM 클라이언트 및 .NET 서버](com-interop-sample-com-client-and-net-server.md)
