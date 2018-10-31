---
title: '방법: Windows 서비스 응용 프로그램 디버깅'
ms.date: 03/30/2017
helpviewer_keywords:
- debugging Windows Service applications
- debugging [Visual Studio], Windows services
- Windows NT services, debugging
- Windows Service applications, debugging
- services, debugging
ms.assetid: 63ab0800-0f05-4f1e-88e6-94c73fd920a2
author: ghogen
ms.openlocfilehash: 3f8dfff59acaa10fa99874dde2eb6eb6ed04e8fb
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48035950"
---
# <a name="how-to-debug-windows-service-applications"></a>방법: Windows 서비스 응용 프로그램 디버깅
서비스는 Visual Studio 내에서가 아니라 서비스 제어 관리자의 컨텍스트 내에서 실행해야 합니다. 따라서 서비스를 디버그하는 것은 다른 Visual Studio 응용 프로그램 형식을 디버그하는 것처럼 단순하지 않습니다. 서비스를 디버그하려면 서비스를 시작한 다음 서비스가 실행되는 프로세스에 디버거를 연결해야 합니다. 그리고 나면 Visual Studio의 모든 표준 디버깅 기능을 사용하여 응용 프로그램을 디버그할 수 있습니다.  
  
> [!CAUTION]
>  프로세스에 대해 알고 있으며 해당 프로세스에 디버거를 연결하는 경우 프로세스가 종료될 수도 있음을 이해한 상태에서 프로세스에 디버거를 연결해야 합니다. 예를 들어 WinLogon 프로세스에 연결한 후에 디버깅을 중지하면 시스템이 중단됩니다. 시스템은 WinLogon 없이는 작동할 수 없기 때문입니다.  
  
 실행 중인 서비스에만 디버거를 연결할 수 있습니다. 연결 프로세스에서는 현재 서비스 작동이 중단되지만 서비스 처리가 실제로 중지되거나 일시 중지되지는 않습니다. 즉, 디버깅을 시작할 때 실행 중인 서비스는 디버그할 때도 기술적으로 계속 시작됨 상태이지만 처리는 일시 중단됩니다.  
  
 프로세스에 연결한 후에는 중단점을 설정하여 코드를 디버그하는 데 사용할 수 있습니다. 프로세스에 연결하는 데 사용한 대화 상자를 종료하면 디버그 모드가 시작됩니다. 서비스 제어 관리자를 사용하여 서비스를 시작, 중지, 일시 중지 및 계속해 설정된 중단점을 적중할 수 있습니다. 나중에 디버깅이 정상적으로 완료되면 이 더미 서비스를 제거할 수 있습니다.  
  
 이 문서에서는 로컬 컴퓨터에서 실행되는 서비스를 디버그하는 방법에 대해 다루지만, 원격 컴퓨터에서 실행되는 Windows 서비스도 디버그할 수 있습니다. [원격 디버깅](/visualstudio/debugger/debug-installed-app-package)을 참조하세요.  
  
> [!NOTE]
>  서비스 제어 관리자는 모든 서비스 시작 시도에 대해 30초의 제한을 적용하므로 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드를 디버그하는 작업은 까다로울 수 있습니다. 자세한 내용은 [Troubleshooting: Debugging Windows Services](../../../docs/framework/windows-services/troubleshooting-debugging-windows-services.md)(문제 해결: Windows 서비스 디버그)를 참조하세요.  
  
> [!WARNING]
>  디버깅을 위한 의미 있는 정보를 가져오려면 Visual Studio 디버거가 디버그 중인 이진 파일에 대한 기호 파일을 찾아야 합니다. Visual Studio에서 빌드한 서비스를 디버그하는 경우 기호 파일(.pdb 파일)은 실행 파일이나 라이브러리와 같은 폴더에 있으며 디버거는 이러한 파일을 자동으로 로드합니다. 직접 빌드하지 않은 서비스를 디버그할 때는 먼저 서비스의 기호를 찾아 디버거가 해당 기호를 검색할 수 있는지 확인해야 합니다. [기호 파일(.pdb) 및 원본 파일 지정](https://msdn.microsoft.com/library/1105e169-5272-4e7c-b3e7-cda1b7798a6b)을 참조하세요. 시스템 프로세스를 디버그하거나 서비스에 시스템 호출을 위한 기호를 포함하려는 경우에는 Microsoft 기호 서버를 추가해야 합니다. [디버깅 기호](/windows/desktop/DxTechArts/debugging-with-symbols)를 참조하세요.  
  
### <a name="to-debug-a-service"></a>서비스를 디버깅하려면  
  
1.  디버그 구성에서 서비스를 빌드합니다.  
  
2.  서비스를 설치합니다. 자세한 내용은 [How to: Install and Uninstall Services](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)을 참조하세요.  
  
3.  **서비스 제어 관리자**, **서버 탐색기** 또는 코드에서 서비스를 시작합니다. 자세한 내용은 [How to: Start Services](../../../docs/framework/windows-services/how-to-start-services.md)(방법: 서비스 시작)를 참조하세요.  
  
4.  시스템 프로세스에 연결할 수 있도록 관리 자격 증명을 사용하여 Visual Studio를 시작합니다.  
  
5.  (선택 사항) Visual Studio 메뉴 모음에서 **도구**, **옵션**을 선택합니다. **옵션** 대화 상자에서 **디버깅**, **기호**를 차례로 선택하고 **Microsoft 기호 서버** 확인란을 선택한 다음, **확인** 단추를 선택합니다.  
  
6.  메뉴 모음의 **디버그** 또는 **도구** 메뉴에서 **프로세스에 연결**을 선택합니다(키보드: Ctrl+Alt+P).  
  
     **프로세스** 대화 상자가 표시됩니다.  
  
7.  **모든 사용자의 프로세스 표시** 확인란을 선택합니다.  
  
8.  **사용 가능한 프로세스** 섹션에서 서비스의 프로세스를 선택한 다음, **연결**을 선택합니다.  
  
    > [!TIP]
    >  프로세스의 이름은 서비스의 실행 파일 이름과 같습니다.  
  
     **프로세스에 연결** 대화 상자가 나타납니다.  
  
9. 적절한 옵션을 선택하고 **확인** 단추를 선택하여 대화 상자를 닫습니다.  
  
    > [!NOTE]
    >  이제 디버그 모드가 설정되었습니다.  
  
10. 코드에서 사용할 중단점을 설정합니다.  
  
11. 서비스 제어 관리자에 액세스하고 서비스를 조작하여 중단점을 적중하는 중지, 일시 중지 및 계속 명령을 보냅니다. 서비스 제어 관리자 실행에 대한 자세한 내용은 [How to: Start Services](../../../docs/framework/windows-services/how-to-start-services.md)(방법: 서비스 시작)를 참조하세요. 또한 [Troubleshooting: Debugging Windows Services](../../../docs/framework/windows-services/troubleshooting-debugging-windows-services.md)(문제 해결: Windows 서비스 디버그)를 참조하세요.  
  
## <a name="debugging-tips-for-windows-services"></a>Windows 서비스 디버깅 팁  
 서비스의 프로세스에 연결하면 해당 서비스의 코드를 대부분 디버그할 수 있지만 모든 코드를 디버그할 수 있는 것은 아닙니다. 예를 들어 서비스가 이미 시작되었기 때문에 이러한 방식으로 서비스를 로드하는 데 사용되는 서비스의 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드 내 코드나 `Main` 메서드 내의 코드는 디버그할 수 없습니다. 이 제한을 해결하는 한 가지 방법은 디버그에만 사용되는 두 번째 임시 서비스를 서비스 응용 프로그램에 만드는 것입니다. 두 서비스를 모두 설치하고서 이 더미 서비스를 시작하여 서비스 프로세스를 로드할 수는 없습니다. 임시 서비스에서 프로세스를 시작하고 나면 Visual Studio에서 **디버그** 메뉴를 사용하여 서비스 프로세스에 연결할 수 있습니다.  
  
 프로세스에 연결할 수 있을 때까지 <xref:System.Threading.Thread.Sleep%2A> 메서드에 대한 호출을 추가하여 작업을 지연시켜 봅니다.  
  
 프로그램을 일반 콘솔 응용 프로그램으로 변경해 봅니다. 이렇게 하려면 `Main` 메서드를 시작하는 방법에 따라 Windows 서비스와 콘솔 응용 프로그램 둘 다로 실행할 수 있도록 다음과 같이 다시 작성합니다.  
  
#### <a name="how-to-run-a-windows-service-as-a-console-application"></a>방법: 콘솔 응용 프로그램으로 Windows 서비스 실행  
  
1.  <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 및 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 메서드를 실행하는 서비스에 메서드를 추가합니다.  
  
    ```csharp  
    internal void TestStartupAndStop(string[] args)  
    {  
        this.OnStart(args);  
        Console.ReadLine();  
        this.OnStop();  
    }  
    ```  
  
2.  `Main` 메서드를 다음과 같이 다시 작성합니다.  
  
    ```csharp  
    static void Main(string[] args)  
    {  
        if (Environment.UserInteractive)  
        {  
            MyNewService service1 = new MyNewService(args);  
            service1.TestStartupAndStop(args);  
        }  
        else  
        {  
            // Put the body of your old Main method here.  
        }  
    }
    ```  
  
3.  프로젝트 속성의 **응용 프로그램** 탭에서 **출력 형식**을 **콘솔 응용 프로그램**으로 설정합니다.  
  
4.  **디버깅 시작**(F5)을 선택합니다.  
  
5.  프로그램을 Windows 서비스로 다시 실행하려면 해당 프로그램을 설치하고 Windows 서비스를 시작하는 일반적인 방법으로 시작합니다. 이러한 변경 내용을 되돌릴 필요는 없습니다.  
  
 시스템 시작 시에만 발생하는 문제를 디버그하려는 등의 일부 경우에는 Windows 디버거를 사용해야 합니다. [Windows용 디버깅 도구](https://msdn.microsoft.com/windows/hardware/hh852365)를 설치하고 [How to debug Windows Services](https://support.microsoft.com/kb/824344)(Windows 서비스를 디버깅하는 방법)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Windows 서비스 응용 프로그램 소개](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)  
 [방법: 서비스 설치 및 제거](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)  
 [방법: 서비스 시작](../../../docs/framework/windows-services/how-to-start-services.md)  
 [서비스 디버그](/windows/desktop/Services/debugging-a-service)
