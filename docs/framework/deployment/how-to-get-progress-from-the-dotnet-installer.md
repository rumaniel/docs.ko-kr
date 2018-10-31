---
title: '방법: .NET Framework 4.5 설치 관리자에서 진행률 가져오기'
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- progress information, .NET Framework installer
- .NET Framework, installing
ms.assetid: 0a1a3ba3-7e46-4df2-afd3-f3a8237e1c4f
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bec27165d1bfd6a501ba8b96a1eb133276fe7269
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50197953"
---
# <a name="how-to-get-progress-from-the-net-framework-45-installer"></a>방법: .NET Framework 4.5 설치 관리자에서 진행률 가져오기
[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]는 재배포 가능 런타임입니다. .NET Framework의 이 버전용 응용 프로그램을 개발하는 경우 응용 프로그램 설치 시 필수 구성 요소로 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 설치를 포함(연결)시킬 수 있습니다. 사용자 지정 설치 환경이나 통합 설치 환경을 제공하려면 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 설치 프로그램을 자동으로 시작하고 앱의 설치 진행률을 표시하는 동안 진행 상태를 추적하는 것이 좋습니다. 자동 추적을 사용하도록 설정하기 위해 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 설치 프로그램(감시할 수 있음)은 메모리 매핑된 I/O(MMIO) 세그먼트를 사용하여 설치 프로그램과 함께 통신할 프로토콜(감시자 또는 chainer)을 정의합니다. 이 프로토콜은 chainer가 진행률 정보를 가져오고, 자세한 결과를 확인하고. 메시지에 응답하고, [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 설치를 취소하는 방법을 정의합니다.  
  
-   **호출**.  [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 설치 프로그램을 호출하고 MMIO 섹션에서 진행률 정보를 받으려면 설치 프로그램에서 다음을 수행해야 합니다.  
  
    1.  [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 재배포 가능 프로그램을 호출합니다.  
  
        ```  
        dotNetFx45_Full_x86_x64.exe /q /norestart /pipe section-name  
        ```  
  
         여기서 *section name*은 응용 프로그램을 식별하는 데 사용할 이름입니다. .NET Framework 설치 프로그램은 MMIO 섹션을 읽고 비동기적으로 쓰므로 이 시간 동안 이벤트 및 메시지를 사용하는 것이 편리할 수도 있습니다. 예제에서는 MMIO 섹션(`TheSectionName`)을 할당하고 이벤트(`TheEventName`)를 정의하는 생성자가 .NET Framework 설치 프로세스를 만듭니다.  
  
        ```  
        Server():ChainerSample::MmioChainer(L"TheSectionName", L"TheEventName")  
        ```  
  
         이러한 이름을 설치 프로그램에 고유한 이름으로 바꾸세요.  
  
    2.  MMIO 섹션을 읽습니다. [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]에서 다운로드 및 설치 작업은 동시에 진행됩니다. 따라서 .NET Framework에서 하나의 구성 요소를 설치하면서 다른 구성 요소를 다운로드할 수 있습니다. 따라서 진행률이 0에서 255까지 증가하는 두 개의 숫자(`m_downloadSoFar` 및 `m_installSoFar`)로 MMIO 섹션에 다시 전송(기록)됩니다. 255가 기록되고 .NET Framework가 종료되면 설치가 완료된 것입니다.  
  
-   **종료 코드**. [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 재배포 가능 프로그램을 호출하는 명령의 다음 종료 코드는 설치에 성공했는지 아니면 실패했는지를 나타냅니다.  
  
    -   0 - 설치가 완료되었습니다.  
  
    -   3010 – 설치가 완료되었습니다. 시스템 다시 시작해야 합니다.  
  
    -   1602 – 설치가 취소되었습니다.  
  
    -   기타 모든 코드 - 설치 중 오류가 발생했습니다. 자세한 내용을 보려면 %temp%에 생성된 로그 파일을 검사하세요.  
  
-   **설치 취소**. 언제든지 `Abort` 메서드를 통해 MMIO 섹션에 `m_downloadAbort` 및 `m_ installAbort` 플래그를 설정하여 설치를 취소할 수 있습니다.  
  
## <a name="chainer-sample"></a>chainer 샘플  
 chainer 샘플은 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 설치 프로그램을 자동으로 시작하고 진행률을 표시하는 동안 설치를 추적합니다. 이 샘플은 .NET Framework 4에 대해 제공된 chainer 샘플과 비슷합니다. 그러나 또한 .NET Framework 4 앱을 닫기 위한 메시지 상자를 처리하여 시스템 다시 시작을 방지할 수 있습니다. 이 메시지 상자에 대한 자세한 내용은 [.NET Framework 4.5를 설치하는 동안 시스템 다시 시작 줄이기](../../../docs/framework/deployment/reducing-system-restarts.md)를 참조하세요. .NET Framework 4 설치 관리자와 함께 이 샘플을 사용할 수 있습니다. 해당 시나리오에서는 메시지가 전송되지 않습니다.  
  
> [!WARNING]
>  관리자 권한으로 예제를 실행해야 합니다.  
  
 MSDN 샘플 갤러리에서 [.NET Framework 4.5 chainer 샘플](https://go.microsoft.com/fwlink/?LinkId=231345)에 대한 전체 Visual Studio 솔루션을 다운로드할 수 있습니다.  
  
 다음 섹션에서는 이 샘플의 중요한 파일인 MMIOChainer.h, ChainingdotNet4.cpp 및 IProgressObserver.h에 대해 설명합니다.  
  
#### <a name="mmiochainerh"></a>MMIOChainer.h  
  
-   MMIOChainer.h 파일([전체 코드](https://go.microsoft.com/fwlink/?LinkId=231369) 참조)에는 chainer 클래스가 파생되어야 하는 데이터 구조 정의와 기본 클래스가 포함되어 있습니다. [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]는 MMIO 데이터 구조를 확장하여 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 설치 관리자에 필요한 데이터를 처리합니다. MMIO 구조에 대한 변경 내용은 이전 버전과 호환되므로 .NET Framework 4 chainer가 다시 컴파일하지 않고도 .NET Framework 4.5 설치 프로그램에서 작동할 수 있습니다. 그러나 이 시나리오에서는 시스템 다시 시작을 줄이는 기능이 지원되지 않습니다.  
  
     버전 필드를 통해 구조 및 메시지 형식에 대한 수정 버전을 식별할 수 있습니다.  .NET Framework 설치 프로그램은 `VirtualQuery` 함수 호출을 통해 파일 매핑의 크기를 확인하여 chainer 인터페이스 버전을 확인합니다.  크기가 버전 필드를 수용하기에 충분히 큰 경우 .NET Framework 설치 프로그램은 지정된 값을 사용합니다. .NET Framework 4의 경우처럼 파일 매핑이 너무 작아서 버전 필드를 포함할 수 없는 경우 설치 프로세스에서 버전 0(4)을 가정합니다. chainer가 .NET Framework 설치 프로그램에서 보내려고 하는 메시지 버전을 지원하지 않는 경우 .NET Framework 설치 프로그램은 무시 응답을 가정합니다.  
  
     MMIO 데이터 구조는 다음과 같이 정의됩니다.  
  
    ```cpp  
    // MMIO data structure for interprocess communication  
        struct MmioDataStructure  
        {  
            bool m_downloadFinished;               // Is download complete?  
            bool m_installFinished;                // Is installation complete?  
            bool m_downloadAbort;                  // Set to cause downloader to abort.  
            bool m_installAbort;                   // Set to cause installer to abort.  
            HRESULT m_hrDownloadFinished;          // Resulting HRESULT for download.  
            HRESULT m_hrInstallFinished;           // Resulting HRESULT for installation.  
            HRESULT m_hrInternalError;  
            WCHAR m_szCurrentItemStep[MAX_PATH];  
            unsigned char m_downloadSoFar;         // Download progress 0-255 (0-100% done).   
            unsigned char m_installSoFar;          // Installation progress 0-255 (0-100% done).  
            WCHAR m_szEventName[MAX_PATH];         // Event that chainer creates and chainee opens to sync communications.  
  
            BYTE m_version;                        // Version of the data structure, set by chainer:  
                                                   // 0x0: .NET Framework 4   
                                                   // 0x1: .NET Framework 4.5  
  
            DWORD m_messageCode;                   // Current message sent by the chainee; 0 if no message is active.  
            DWORD m_messageResponse;               // Chainer's response to current message; 0 if not yet handled.  
            DWORD m_messageDataLength;             // Length of the m_messageData field, in bytes.  
            BYTE m_messageData[1];                 // Variable-length buffer; content depends on m_messageCode.  
        };  
    ```  
  
-   `MmioDataStructure` 데이터 구조를 직접 사용하면 안 됩니다. `MmioChainer` 클래스를 대신 사용하여 chainer를 구현하세요. `MmioChainer` 클래스에서 파생하여 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 재배포 가능 패키지를 연결합니다.  
  
#### <a name="iprogressobserverh"></a>IProgressObserver.h  
  
-   IProgressObserver.h 파일은 진행률 관찰자([전체 코드 참조](https://go.microsoft.com/fwlink/?LinkId=231370))를 구현합니다. 이 관찰자는 다운로드 및 설치 진행률에 대한 알림을 받습니다(부호 없는 `char` 0-255로 지정됨, 1%-100% 완료를 나타냄). chainee가 메시지를 보낼 때도 관찰자에게 알림이 전달되며, 관찰자는 응답을 보내야 합니다.  
  
    ```cpp  
        class IProgressObserver  
        {  
        public:  
            virtual void OnProgress(unsigned char) = 0; // 0 - 255:  255 == 100%  
            virtual void Finished(HRESULT) = 0;         // Called when operation is complete    
            virtual DWORD Send(DWORD dwMessage, LPVOID pData, DWORD dwDataLength) = 0; // Called when a message is sent  
        };  
    ```  
  
#### <a name="chainingdotnet45cpp"></a>ChainingdotNet4.5.cpp  
  
-   [ChainingdotNet4.5.cpp](https://go.microsoft.com/fwlink/?LinkId=231368) 파일은 `MmioChainer` 클래스에서 파생되는 `Server` 클래스를 구현하고 진행률 정보를 표시하기 위해 적절한 메서드를 재정의합니다. MmioChainer는 지정된 섹션 이름으로 섹션을 만들고 지정된 이벤트 이름으로 chainer를 초기화합니다. 이벤트 이름은 매핑된 데이터 구조에 저장됩니다. 섹션 및 이벤트 이름을 고유하게 설정해야 합니다. 다음 코드의 `Server` 클래스는 지정된 설치 프로그램을 시작하고 해당 진행률을 모니터링하고 종료 코드를 반환합니다.  
  
    ```cpp  
    class Server : public ChainerSample::MmioChainer, public ChainerSample::IProgressObserver  
    {  
    public:  
        …………….  
        Server():ChainerSample::MmioChainer(L"TheSectionName", L"TheEventName") //customize for your event names  
        {}  
    ```  
  
     Main 메서드에서 설치가 시작됩니다.  
  
    ```cpp  
    // Main entry point for program  
    int __cdecl main(int argc, _In_count_(argc) char **_argv)  
    {  
        int result = 0;  
        CString args;  
        if (argc > 1)  
        {  
            args = CString(_argv[1]);  
        }  
  
        if (IsNetFx4Present(NETFX45_RC_REVISION))  
        {  
            printf(".NET Framework 4.5 is already installed");  
        }  
        else  
        {  
            result = Server().Launch(args);  
        }  
  
        return result;  
    }  
    ```  
  
-   설치를 시작하기 전에 chainer는 `IsNetFx4Present`를 호출하여 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]가 이미 설치되어 있는지 확인합니다.  
  
    ```cpp  
    ///  Checks for presence of the .NET Framework 4.  
    ///    A value of 0 for dwMinimumRelease indicates a check for the .NET Framework 4 full  
    ///    Any other value indicates a check for a specific compatible release of the .NET Framework 4.  
    #define NETFX40_FULL_REVISION 0  
    // TODO: Replace with released revision number  
    #define NETFX45_RC_REVISION MAKELONG(50309, 5)   // .NET Framework 4.5   
    bool IsNetFx4Present(DWORD dwMinimumRelease)  
    {  
        DWORD dwError = ERROR_SUCCESS;  
        HKEY hKey = NULL;  
        DWORD dwData = 0;  
        DWORD dwType = 0;  
        DWORD dwSize = sizeof(dwData);  
  
        dwError = ::RegOpenKeyExW(HKEY_LOCAL_MACHINE, L"SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full", 0, KEY_READ, &hKey);  
        if (ERROR_SUCCESS == dwError)  
        {  
            dwError = ::RegQueryValueExW(hKey, L"Release", 0, &dwType, (LPBYTE)&dwData, &dwSize);  
  
            if ((ERROR_SUCCESS == dwError) && (REG_DWORD != dwType))  
            {  
                dwError = ERROR_INVALID_DATA;  
            }  
            else if (ERROR_FILE_NOT_FOUND == dwError)  
            {  
                // Release value was not found, let's check for 4.0.  
                dwError = ::RegQueryValueExW(hKey, L"Install", 0, &dwType, (LPBYTE)&dwData, &dwSize);  
  
                // Install = (REG_DWORD)1;  
                if ((ERROR_SUCCESS == dwError) && (REG_DWORD == dwType) && (dwData == 1))  
                {  
                    // treat 4.0 as Release = 0  
                    dwData = 0;  
                }  
                else  
                {  
                    dwError = ERROR_INVALID_DATA;  
                }  
            }  
        }  
  
        if (hKey != NULL)  
        {  
            ::RegCloseKey(hKey);  
        }  
  
        return ((ERROR_SUCCESS == dwError) && (dwData >= dwMinimumRelease));  
    }  
    ```  
  
-   올바른 위치를 가리키도록 `Launch` 메서드의 실행 파일(예제에서는 Setup.exe) 경로를 변경하거나 코드를 사용자 지정하여 위치를 결정할 수 있습니다. `MmioChainer` 기본 클래스는 파생 클래스가 호출하는 차단 `Run()` 메서드를 제공합니다.  
  
    ```cpp  
    bool Launch(const CString& args)  
    {  
    CString cmdline = L"dotNetFx45_Full_x86_x64.exe -pipe TheSectionName " + args; // Customize with name and location of setup .exe that you want to run  
    STARTUPINFO si = {0};  
    si.cb = sizeof(si);  
    PROCESS_INFORMATION pi = {0};  
  
    // Launch the Setup.exe that installs the .NET Framework 4.5  
    BOOL bLaunchedSetup = ::CreateProcess(NULL,   
     cmdline.GetBuffer(),  
     NULL, NULL, FALSE, 0, NULL, NULL,   
     &si,  
     &pi);  
  
    // If successful   
    if (bLaunchedSetup != 0)  
    {  
    IProgressObserver& observer = dynamic_cast<IProgressObserver&>(*this);  
    Run(pi.hProcess, observer);  
  
    ……………………..   
    return (bLaunchedSetup != 0);  
    }  
    ```  
  
-   `Send` 메서드는 메시지를 가로채서 처리합니다.  이 버전의 .NET Framework에서 지원되는 메시지는 응용 프로그램 닫기 메시지뿐입니다.  
  
    ```cpp  
            // SendMessage  
            //  
            // Send a message and wait for the response.  
            // dwMessage: Message to send  
            // pData: The buffer to copy the data to  
            // dwDataLength: Initially a pointer to the size of pBuffer.  Upon successful call, the number of bytes copied to pBuffer.  
            //--------------------------------------------------------------  
        virtual DWORD Send(DWORD dwMessage, LPVOID pData, DWORD dwDataLength)  
        {  
            DWORD dwResult = 0;  
            printf("recieved message: %d\n", dwMessage);  
            // Handle message  
            switch (dwMessage)  
            {  
            case MMIO_CLOSE_APPS:  
                {  
                    printf("    applications are holding files in use:\n");  
                    IronMan::MmioCloseApplications* applications = reinterpret_cast<IronMan::MmioCloseApplications*>(pData);  
                    for(DWORD i = 0; i < applications->m_dwApplicationsSize; i++)  
                    {  
                        printf("      %ls (%d)\n", applications->m_applications[i].m_szName, applications->m_applications[i].m_dwPid);  
                    }  
  
                    printf("    should appliations be closed? (Y)es, (N)o, (R)efresh : ");  
                    while (dwResult == 0)  
                    {  
                        switch (toupper(getwchar()))  
                        {  
                        case 'Y':  
                            dwResult = IDYES;  // Close apps  
                            break;  
                        case 'N':  
                            dwResult = IDNO;  
                            break;  
                        case 'R':  
                            dwResult = IDRETRY;  
                            break;  
                        }  
                    }  
                    printf("\n");  
                    break;  
                }  
            default:  
                break;  
            }  
            printf("  response: %d\n  ", dwResult);  
            return dwResult;  
        }  
    };  
    ```  
  
-   진행률 데이터는 0(0%)에서 255(100%) 사이의 부호 없는 `char`입니다.  
  
    ```cpp  
    private: // IProgressObserver  
        virtual void OnProgress(unsigned char ubProgressSoFar)  
        {…………  
       }  
    ```  
  
-   HRESULT는 `Finished` 메서드에 전달됩니다.  
  
    ```cpp  
    virtual void Finished(HRESULT hr)  
    {  
    // This HRESULT is communicated over MMIO and may be different than process  
    // Exit code of the Chainee Setup.exe itself  
    printf("\r\nFinished HRESULT: 0x%08X\r\n", hr);  
    }  
    ```  
  
    > [!IMPORTANT]
    >  [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 재배포 가능 패키지는 일반적으로 많은 진행률 메시지와 완료를 나타내는 단일 메시지(chainer 쪽)를 씁니다. 또한 비동기적으로 읽으면서 `Abort` 레코드를 찾습니다. `Abort` 레코드를 받으면 설치를 취소하고, 설치가 중단되고 설치 작업이 롤백된 후 E_ABORT를 해당 데이터로 사용하여 완성된 레코드를 씁니다.  
  
 일반적인 서버는 임의의 MMIO 파일 이름을 만들고, 파일을 만든 다음(이전 코드 예제와 같이 `Server::CreateSection`에서) `CreateProcess` 메서드를 사용하고 `-pipe someFileSectionName` 옵션으로 파이프 이름을 전달하여 재배포 가능 패키지를 시작합니다. 서버는 응용 프로그램 UI 관련 코드를 사용하여 `OnProgress`, `Send` 및 `Finished` 메서드를 구현해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
- [개발자를 위한 배포 가이드](../../../docs/framework/deployment/deployment-guide-for-developers.md)  
- [배포](../../../docs/framework/deployment/index.md)
