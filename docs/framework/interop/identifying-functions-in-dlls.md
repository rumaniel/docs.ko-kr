---
title: DLL 함수 식별
ms.date: 03/30/2017
helpviewer_keywords:
- platform invoke, identifying functions
- COM interop, DLL functions
- unmanaged functions
- COM interop, platform invoke
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- identifying DLL functions
- DLL functions
ms.assetid: 3e3f6780-6d90-4413-bad7-ba641220364d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: deae99f5bdc7c187997d4bad4957b2fcdccdc166
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051722"
---
# <a name="identifying-functions-in-dlls"></a>DLL 함수 식별
DLL 함수 ID는 다음 요소로 구성됩니다.  
  
- 함수 이름 또는 서수  
  
- 구현을 찾을 수 있는 DLL 파일의 이름  
  
 예를 들어 User32.dll의 **MessageBox**함수는 함수(**MessageBox**) 및 해당 위치(User32.dll, User32 또는 user32)를 식별합니다. Microsoft Windows 애플리케이션 프로그래밍 인터페이스(Windows API)에는 문자와 문자열을 처리하는 각 함수의 두 가지 버전인 1바이트 문자 ANSI 버전 및 2바이트 문자 유니코드 버전이 포함될 수 있습니다. 지정하지 않을 경우 <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet> 필드로 표현되는 문자 집합은 기본적으로 ANSI로 설정됩니다. 일부 함수에는 버전이 세 개 이상 있을 수 있습니다.  
  
 **MessageBoxA**는 **MessageBox** 함수의 ANSI 진입점이고 **MessageBoxW**는 유니코드 버전입니다. 다양한 명령줄 도구를 실행하여 user32.dll과 같은 특정 DLL에 대한 함수 이름을 나열할 수 있습니다. 예를 들어 `dumpbin /exports user32.dll` 또는 `link /dump /exports user32.dll`을 사용하여 함수 이름을 얻을 수 있습니다.  
  
 DLL에서 새 이름을 원래 진입점에 매핑할 경우 코드 내에서 관리되지 않는 함수의 이름을 원하는 대로 바꿀 수 있습니다. 관리 소스 코드에서 관리되지 않는 DLL 함수의 이름을 바꾸는 방법에 대한 자세한 내용은 [진입점 지정](specifying-an-entry-point.md)을 참조하세요.  
  
 플랫폼 호출을 사용하면 Windows API 및 기타 DLL의 함수를 호출하여 운영 체제의 상당한 부분을 제어할 수 있습니다. Windows API 이외에 플랫폼 호출을 통해 사용할 수 있는 수많은 기타 API 및 DLL이 있습니다.  
  
 다음 표에서는 Windows API에서 일반적으로 사용되는 여러 DLL을 설명합니다.  
  
|DLL|콘텐츠 설명|  
|---------|-----------------------------|  
|GDI32.dll|디바이스 출력을 위한 GDI(그래픽 디바이스 인터페이스) 함수입니다(예: 그리기 및 글꼴 관리용 함수).|  
|Kernel32.dll|메모리 관리 및 리소스 처리를 위한 하위 수준 운영 체제 함수입니다.|  
|User32.dll|메시지 처리, 타이머, 메뉴 및 통신을 위한 Windows 관리 함수입니다.|  
  
 Windows API에 대한 전체 설명서는 플랫폼 SDK를 참조하세요. 플랫폼 호출에서 사용되는 .NET 기반 선언을 생성하는 방법을 보여 주는 예제는 [플랫폼 호출을 사용하여 데이터 마샬링](marshaling-data-with-platform-invoke.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [관리되지 않는 DLL 함수 사용](consuming-unmanaged-dll-functions.md)
- [진입점 지정](specifying-an-entry-point.md)
- [DLL 함수가 포함된 클래스 만들기](creating-a-class-to-hold-dll-functions.md)
- [관리 코드에서 프로토타입 만들기](creating-prototypes-in-managed-code.md)
- [DLL 함수 호출](calling-a-dll-function.md)
