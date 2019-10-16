---
title: COM에 어셈블리 등록
ms.date: 03/30/2017
helpviewer_keywords:
- COM interop, registering assemblies
- unregistering assemblies
- interoperation with unmanaged code, registering assemblies
- registering assemblies
ms.assetid: 87925795-a3ae-4833-b138-125413478551
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6482d5fa046409d15913ea26300d298238750326
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648548"
---
# <a name="registering-assemblies-with-com"></a>COM에 어셈블리 등록
[어셈블리 등록 도구(Regasm.exe)](../tools/regasm-exe-assembly-registration-tool.md)라는 명령줄 도구를 실행하여 COM과 사용할 어셈블리를 등록하거나 등록 취소할 수 있습니다. COM 클라이언트에서 .NET Framework 클래스를 투명하게 사용할 수 있도록 Regasm.exe에서는 클래스에 대한 정보를 시스템 레지스트리에 추가합니다. <xref:System.Runtime.InteropServices.RegistrationServices> 클래스는 이와 동등한 기능을 제공합니다.  
  
 관리되는 구성 요소를 Windows 레지스트리에 등록해야 COM 클라이언트에서 활성화할 수 있습니다. 다음 표에서는 Regasm.exe를 통해 일반적으로 Windows 레지스트리에 추가하는 키를 보여 줍니다. (000000은 실제 GUID 값을 표시합니다.)  
  
|GUID|설명|레지스트리 키|  
|----------|-----------------|------------------|  
|CLSID|클래스 식별자|HKEY_CLASSES_ROOT\CLSID\\{000…000}|  
|IID|인터페이스 식별자|HKEY_CLASSES_ROOT\Interface\\{000…000}|  
|LIBID|라이브러리 식별자|HKEY_CLASSES_ROOT\TypeLib\\{000…000}|  
|ProgID|프로그래밍 ID|HKEY_CLASSES_ROOT\000…000|  
  
 HKCR\CLSID\\{0000…0000} 키에서 기본값은 클래스의 ProgID로 설정되며 새로 이름이 지정된 두 개의 값(Class 및 Assembly)이 추가됩니다. 런타임 시 레지스트리에서 Assembly 값을 읽어 런타임 어셈블리 확인자에 전달합니다. 어셈블리 확인자는 이름 및 버전 번호와 같은 어셈블리 정보를 기반으로 어셈블리를 찾으려 합니다. 어셈블리 확인자에서 어셈블리를 찾으려면 어셈블리가 다음 위치 중 하나에 있어야 합니다.  
  
- 전역 어셈블리 캐시(강력한 이름의 어셈블리여야 함).  
  
- 애플리케이션 디렉터리. 애플리케이션 경로에서 로드된 어셈블리는 해당 애플리케이션에서만 액세스할 수 있습니다.  
  
- **/codebase** 옵션을 사용하여 지정된 Regasm.exe의 파일 경로.  
  
 Regasm.exe는 HKCR\CLSID\\{0000…0000} 키 아래에 InProcServer32 키도 만듭니다. 키의 기본값은 공용 언어 런타임(Mscoree.dll)을 초기화하는 DLL의 이름으로 설정됩니다.  
  
## <a name="examining-registry-entries"></a>레지스트리 항목 검사  
 COM interop에서는 모든 .NET Framework 클래스의 인스턴스를 만드는 표준 클래스 팩터리 구현을 제공합니다. 클라이언트는 관리되는 DLL에서 **DllGetClassObject**를 호출하여 다른 COM 구성 요소에서와 마찬가지로 클래스 팩터리를 가져오고 개체를 만들 수 있습니다.  
  
 `InprocServer32` 하위 키의 경우, 기존 COM 형식 라이브러리의 위치에 Mscoree.dll의 참조가 표시되어 공용 언어 런타임을 통해 관리 개체가 생성되었음을 나타냅니다.  
  
## <a name="see-also"></a>참고 항목

- [.NET Framework 구성 요소를 COM에 노출](exposing-dotnet-components-to-com.md)
- [방법: COM에서 .NET 형식 참조](how-to-reference-net-types-from-com.md)
- [.NET 개체 호출](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8hw8h46b(v=vs.100))
- [COM 액세스를 위해 애플리케이션 배포](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/c2850st8(v=vs.100))
