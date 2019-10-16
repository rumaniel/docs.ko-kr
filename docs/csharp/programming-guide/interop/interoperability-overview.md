---
title: 상호 운용성 개요 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- COM interop
- C# language, interoperability
- C++ Interop
- interoperability, about interoperability
- platform invoke
ms.assetid: c025b2e0-2357-4c27-8461-118f0090aeff
ms.openlocfilehash: 1342711ca17b0d2bf5122f4c749514e3b96c9ad7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69921822"
---
# <a name="interoperability-overview-c-programming-guide"></a>상호 운용성 개요(C# 프로그래밍 가이드)
이 항목에서는 C# 관리 코드와 비관리 코드 간의 상호 운용성을 사용하도록 설정하는 방법을 설명합니다.  
  
## <a name="platform-invoke"></a>플랫폼 호출  
 *플랫폼 호출*은 관리 코드가 Microsoft Windows API의 함수와 같이 DLL(동적 연결 라이브러리)에서 구현된 관리되지 않는 함수를 호출할 수 있도록 하는 서비스입니다. 이 서비스는 내보낸 함수를 찾아서 호출하고 필요에 따라 상호 운용 경계를 가로질러 인수(정수, 문자열, 배열, 구조체 등)를 마샬링합니다.  
  
 자세한 내용은 [관리되지 않는 DLL 함수 사용](../../../framework/interop/consuming-unmanaged-dll-functions.md) 및 [방법: 플랫폼 호출을 사용하여 웨이브 파일 재생](./how-to-use-platform-invoke-to-play-a-wave-file.md)으르 참조하세요.  
  
> [!NOTE]
> CLR([공용 언어 런타임](../../../standard/clr.md))은 시스템 리소스에 대한 액세스를 관리합니다. CLR 외부에 있는 비관리 코드를 호출하면 이 보안 메커니즘을 우회하므로 보안 위험이 제기됩니다. 예를 들어 비관리 코드는 CLR 보안 메커니즘을 우회하여 비관리 코드의 리소스를 직접 호출할 수 있습니다. 자세한 내용은 [.NET의 보안](../../../standard/security/index.md)을 참조하세요.  
  
## <a name="c-interop"></a>C++ Interop  
 C# 또는 다른 .NET Framework 언어로 작성된 코드에서 사용할 수 있도록 IJW(It Just Works)라고도 하는 C++ interop를 사용하여 네이티브 C++ 클래스를 래핑할 수 있습니다. 이렇게 하려면 C++ 코드를 작성하여 네이티브 DLL 또는 COM 구성 요소를 래핑합니다. 다른 .NET Framework 언어와 달리 Visual C++에는 관리 코드와 비관리 코드가 동일한 애플리케이션 및 동일한 파일에 있을 수 있도록 하는 상호 운용성 지원이 있습니다. 그런 다음 **/clr** 컴파일러 스위치로 관리되는 어셈블리를 생성하여 C++ 코드를 빌드합니다. 마지막으로, C# 프로젝트의 어셈블리에 대한 참조를 추가하고 다른 관리되는 클래스를 사용하는 것처럼 래핑된 개체를 사용합니다.  
  
## <a name="exposing-com-components-to-c"></a>C\#에 COM 구성 요소 노출
 C# 프로젝트에서 COM 구성 요소를 사용할 수 있습니다. 일반적인 단계는 다음과 같습니다.  
  
1. COM 구성 요소를 찾아서 사용하고 등록합니다. regsvr32.exe를 사용하여 COM DLL을 등록하거나 등록을 취소합니다.  
  
2. COM 구성 요소 또는 형식 라이브러리에 대한 참조를 프로젝트에 추가합니다.  
  
     참조를 추가하면 Visual Studio에서는 형식 라이브러리를 입력으로 사용하는 [Tlbimp.exe(형식 라이브러리 가져오기)](../../../framework/tools/tlbimp-exe-type-library-importer.md)를 통해 .NET Framework interop 어셈블리를 출력합니다. RCW(런타임 호출 가능 래퍼)라고도 하는 어셈블리는 형식 라이브러리에 있는 인터페이스 및 COM 클래스를 래핑하는 인터페이스 및 관리되는 클래스를 포함합니다. Visual Studio에서는 생성된 어셈블리에 대한 참조를 프로젝트에 추가합니다.  
  
3. RCW에서 정의된 클래스의 인스턴스를 만듭니다. 그러면 COM 개체의 인스턴스가 생성됩니다.  
  
4. 다른 관리되는 개체와 동일한 방식으로 개체를 사용합니다. 개체가 가비지 수집에 의해 회수되면 COM 개체 인스턴스도 메모리에서 해제됩니다.  
  
 자세한 내용은 [.NET Framework에 COM 구성 요소 노출](../../../framework/interop/exposing-com-components.md)을 참조하세요.  
  
## <a name="exposing-c-to-com"></a>COM에 C# 노출  
 COM 클라이언트는 올바르게 노출된 C# 형식을 사용할 수 있습니다. C# 형식을 노출하는 기본 단계는 다음과 같습니다.  
  
1. C# 프로젝트에서 Interop 특성을 추가합니다.  
  
     Visual C# 프로젝트 속성을 수정하여 어셈블리 COM이 표시되도록 설정할 수 있습니다. 자세한 내용은 [어셈블리 정보 대화 상자](/visualstudio/ide/reference/assembly-information-dialog-box)를 참조하세요.  
  
2. COM 형식 라이브러리를 생성하고 COM 사용을 위해 등록합니다.  
  
     COM interop에 대해 C# 어셈블리를 자동으로 등록하도록 Visual C# 프로젝트 속성을 수정할 수 있습니다. Visual Studio에서는 [Regasm.exe(어셈블리 등록 도구)](../../../framework/tools/regasm-exe-assembly-registration-tool.md)를 사용하며, 관리되는 어셈블리를 입력으로 사용하는 `/tlb` 명령줄 스위치를 통해 형식 라이브러리를 생성합니다. 이 형식 라이브러리는 어셈블리의 `public` 형식을 설명하고, COM 클라이언트가 관리되는 클래스를 만들 수 있도록 레지스트리 항목을 추가합니다.  
  
 자세한 내용은 [.NET Framework 구성 요소를 COM에 노출](../../../framework/interop/exposing-dotnet-components-to-com.md) 및 [예제 COM 클래스](./example-com-class.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [Interop 성능 향상](https://docs.microsoft.com/previous-versions/msp-n-p/ff647812%28v=pandp.10%29)
- [Introduction to Interoperability between COM and .NET](/office/client-developer/outlook/pia/introduction-to-interoperability-between-com-and-net)(COM과 .NET 간 상호 운용성 소개)
- [Visual Basic의 COM Interop 소개](../../../visual-basic/programming-guide/com-interop/introduction-to-com-interop.md)
- [관리 코드와 비관리 코드 간의 마샬링](../../../framework/interop/interop-marshaling.md)
- [비관리 코드와의 상호 운용](../../../framework/interop/index.md)
- [C# 프로그래밍 가이드](../index.md)
