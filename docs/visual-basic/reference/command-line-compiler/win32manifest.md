---
title: -win32manifest (Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- /win32manifest compiler option [Visual Basic]
- win32manifest compiler option [Visual Basic]
- -win32manifest compiler option [Visual Basic]
ms.assetid: 9e3191b4-90db-41c8-966a-28036fd20005
ms.openlocfilehash: cae6b34aadf6698a337e52aa1ea1ce44206836ac
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004630"
---
# <a name="-win32manifest-visual-basic"></a>-win32manifest (Visual Basic)
프로젝트의 PE(포팅 가능한 실행 파일) 파일에 포함할 사용자 정의 Win32 애플리케이션 매니페스트 파일을 식별합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-win32manifest: fileName  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`fileName`|사용자 지정 매니페스트 파일의 경로입니다.|  
  
## <a name="remarks"></a>설명  
 기본적으로 Visual Basic 컴파일러는 asInvoker의 요청 된 실행 수준을 지정 하는 응용 프로그램 매니페스트를 포함 합니다. 실행 파일이 빌드되는 폴더 (일반적으로 Visual Studio를 사용 하는 경우 bin\Debug 또는 bin\Release 폴더)에 매니페스트를 만듭니다. 예를 들어 highestAvailable 또는 requireAdministrator의 요청 된 실행 수준을 지정 하기 위해 사용자 지정 매니페스트를 제공 하려면이 옵션을 사용 하 여 파일 이름을 지정 합니다.  
  
> [!NOTE]
> 이 옵션과 [-win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md) 옵션은 함께 사용할 수 없습니다. 동일한 명령줄에서 두 옵션을 모두 사용 하려고 하면 빌드 오류가 발생 합니다.  
  
 요청된 실행 수준을 지정하는 애플리케이션 매니페스트가 없는 애플리케이션은 Windows Vista의 사용자 계정 컨트롤 기능 아래에서 파일/레지스트리 가상화의 적용을 받습니다. 가상화에 대한 자세한 내용은 [ClickOnce Deployment on Windows Vista](/visualstudio/deployment/clickonce-deployment-on-windows-vista)(Windows Vista의 ClickOnce 배포)를 참조하세요.  
  
 다음 조건 중 하나에 해당 하는 경우 응용 프로그램에 가상화가 적용 됩니다.  
  
1. @No__t-0 옵션을 사용 하며, `-win32resource` 옵션을 사용 하 여 이후 빌드 단계 또는 Windows 리소스 (.res) 파일의 일부로 매니페스트를 제공 하지 않습니다.  
  
2. 요청한 실행 수준을 지정하지 않는 사용자 지정 매니페스트를 제공합니다.  
  
 Visual Studio는 기본 .manifest 파일을 만들고 이를 실행 파일과 함께 debug 및 release 디렉터리에 저장합니다. 프로젝트 디자이너의 **응용 프로그램** 탭에서 **UAC 설정 보기** 를 클릭 하 여 기본 응용 프로그램 매니페스트 파일을 보거나 편집할 수 있습니다. 자세한 내용은 [프로젝트 디자이너, 응용 프로그램 페이지(Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)를 참조하세요.  
  
 @No__t-0 옵션을 사용 하 여 응용 프로그램 매니페스트를 사용자 지정 빌드 후 단계 또는 Win32 리소스 파일의 일부로 제공할 수 있습니다. 애플리케이션이 Windows Vista에서 파일 또는 레지스트리 가상화의 적용을 받도록 하려면 동일한 옵션을 사용합니다. 이렇게 하면 컴파일러가 PE 파일에 기본 매니페스트를 만들고 포함 하지 않습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 Visual Basic 컴파일러가 PE에 삽입 하는 기본 매니페스트를 보여 줍니다.  
  
> [!NOTE]
> 컴파일러는 표준 응용 프로그램 이름 MyApplication. app을 매니페스트 XML에 삽입 합니다. 이는 Windows Server 2003 서비스 팩 3에서 애플리케이션을 실행하기 위한 해결 방법입니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
  <assemblyIdentity version="1.0.0.0" name="MyApplication.app"/>  
  <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">  
    <security>  
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">  
        <requestedExecutionLevel level="asInvoker"/>  
      </requestedPrivileges>  
    </security>  
  </trustInfo>  
</assembly>  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-nowin32manifest (Visual Basic)](../../../visual-basic/reference/command-line-compiler/nowin32manifest.md)
