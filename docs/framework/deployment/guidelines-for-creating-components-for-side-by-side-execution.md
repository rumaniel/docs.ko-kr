---
title: Side-by-Side 실행용 구성 요소를 만들기 위한 지침
ms.date: 03/30/2017
helpviewer_keywords:
- side-by-side execution, multiple application versions
- side-by-side execution, multiple component versions
ms.assetid: 5c540161-6e40-42e9-be92-6175aee2c46a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2cedcb20ba12e7c362c60d33dfedfa1882eaa7e7
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198499"
---
# <a name="guidelines-for-creating-components-for-side-by-side-execution"></a>Side-by-Side 실행용 구성 요소를 만들기 위한 지침
다음 일반 지침에 따라 Side-by-Side 실행용으로 디자인된 관리되는 응용 프로그램 또는 구성 요소를 만듭니다.  
  
-   파일의 특정 버전에 형식 ID를 바인딩합니다.  
  
     공용 언어 런타임은 강력한 이름의 어셈블리를 사용하여 특정 파일 버전에 형식 ID를 바인딩합니다. Side-by-side 실행용 응용 프로그램 또는 구성 요소를 만들려면 모든 어셈블리에 강력한 이름을 제공해야 합니다. 이를 통해 정확한 형식 ID를 만들고 형식 확인이 올바른 파일로 전달되는지 확인합니다. 강력한 이름의 어셈블리에는 런타임이 바인딩 요청을 충족하는 올바른 파일을 찾는 데 사용하는 버전, 문화권 및 게시자 정보가 포함됩니다.  
  
-   버전 인식 저장소를 사용합니다.  
  
     런타임은 전역 어셈블리 캐시를 사용하여 버전 인식 저장소를 제공합니다. 전역 어셈블리 캐시는 .NET Framework를 사용하는 모든 컴퓨터에 설치된 버전 인식 디렉터리 구조입니다. 전역 어셈블리 캐시에 설치된 어셈블리는 해당 어셈블리의 새 버전을 설치할 경우 덮어쓰지 않습니다.  
  
-   격리 상태로 실행되는 응용 프로그램 또는 구성 요소를 만듭니다.  
  
     격리 상태로 실행되는 응용 프로그램 또는 구성 요소는 응용 프로그램이나 구성 요소의 두 인스턴스가 동시에 실행될 때 충돌을 방지하려면 리소스를 관리해야 합니다. 또한 응용 프로그램 또는 구성 요소는 버전별 파일 구조를 사용해야 합니다.  
  
## <a name="application-and-component-isolation"></a>응용 프로그램 및 구성 요소 격리  
 Side-by-side 실행용 응용 프로그램 또는 구성 요소를 성공적으로 디자인하는 한 가지 핵심 요소는 격리입니다. 응용 프로그램 또는 구성 요소는 특히 파일 I/O를 비롯하여 모든 리소스를 격리된 방식으로 관리해야 합니다. 다음 지침에 따라 응용 프로그램 또는 구성 요소가 격리 상태로 실행되는지 확인합니다.  
  
-   버전별 방식으로 레지스트리에 씁니다. 버전을 나타내는 값을 Hive 또는 키에 저장하고 구성 요소 버전 간에 정보나 상태를 공유하지 않습니다. 이렇게 하면 동시에 실행되는 응용 프로그램 또는 구성 요소 두 개가 정보를 덮어쓰지 않습니다.  
  
-   경합 상태가 발생하지 않도록 명명된 커널 개체를 버전별로 만듭니다. 예를 들어 경합 상태는 같은 응용 프로그램의 두 가지 버전의 두 세마포가 서로 대기하는 경우 발생합니다.  
  
-   파일 및 디렉터리 이름을 버전 인식으로 만듭니다. 이는 파일 구조에서 버전 정보를 사용해야 함을 의미합니다.  
  
-   사용자 계정 및 그룹을 버전별 방식으로 만듭니다. 응용 프로그램에서 만들어진 사용자 계정 및 그룹은 버전으로 식별되어야 합니다. 응용 프로그램 버전 간에 사용자 계정 및 그룹을 공유하지 마세요.  
  
## <a name="installing-and-uninstalling-versions"></a>버전 설치 및 제거  
 Side-by-Side 실행용 응용 프로그램을 디자인할 때 버전 설치 및 제거와 관련된 다음 지침을 따릅니다.  
  
-   다른 버전의.NET Framework에서 실행 중인 다른 응용 프로그램에서 필요할 수 있는 레지스트리에서 정보를 삭제하지 마세요.  
  
-   다른 버전의.NET Framework에서 실행 중인 다른 응용 프로그램에서 필요할 수 있는 레지스트리에서 정보를 바꾸지 마세요.  
  
-   다른 버전의.NET Framework에서 실행 중인 다른 응용 프로그램에서 필요할 수 있는 COM 구성 요소를 등록 해제하지 마세요.  
  
-   이미 등록된 COM 서버에 대한 **InprocServer32** 또는 기타 레지스트리 항목을 변경하지 마세요.  
  
-   다른 버전의.NET Framework에서 실행 중인 다른 응용 프로그램에서 필요할 수 있는 사용자 계정 또는 그룹을 삭제하지 마세요.  
  
-   버전이 지정되지 않은 경로를 포함하는 아무것도 레지스트리에 추가하지 마세요.  
  
## <a name="file-version-number-and-assembly-version-number"></a>파일 버전 번호 및 어셈블리 버전 번호  
 파일 버전은 런타임에서 사용되지 않는 Win32 버전 리소스입니다. 일반적으로, 내부 업데이트에 대해서도 파일 버전을 업데이트합니다. 두 동일한 파일에 서로 다른 파일 버전 정보를 포함될 수 있고 서로 다른 두 파일에 같은 파일 버전 정보를 포함될 수 있습니다.  
  
 어셈블리 버전은 런타임에서 어셈블리 바인딩에 사용됩니다. 버전 번호가 다른 두 동일한 어셈블리는 런타임에서 서로 다른 두 어셈블리로 처리됩니다.  
  
 [전역 어셈블리 캐시 도구(Gacutil.exe)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)를 사용하여 파일 버전 번호만 최신일 경우 어셈블리를 바꿀 수 있습니다. 일반적으로 설치 관리자는 어셈블리 버전 번호가 더 클 경우가 아니면 어셈블리를 통해 설치되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
- [Side-by-Side 실행](../../../docs/framework/deployment/side-by-side-execution.md)  
- [방법: 자동 바인딩 리디렉션 사용 설정 및 해제](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)
