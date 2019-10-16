---
title: Aximp.exe (Windows Forms ActiveX 컨트롤 가져오기)
ms.date: 03/30/2017
helpviewer_keywords:
- ActiveX controls, hosting in Windows Forms
- ActiveX Control Importer
- type definitions, converting
- Aximp.exe
- Windows Forms ActiveX Control Importer
ms.assetid: 482c0d83-7144-4497-b626-87d2351b78d0
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c879375a4b0622311c8731acc276ec79fe0217d5
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044883"
---
# <a name="aximpexe-windows-forms-activex-control-importer"></a>Aximp.exe (Windows Forms ActiveX 컨트롤 가져오기)
ActiveX 컨트롤 가져오기를 사용하면 ActiveX 컨트롤에 대한 COM 형식 라이브러리의 형식 정의를 Windows Forms 컨트롤로 변환할 수 있습니다.  
  
 Windows Forms는 Windows Forms 컨트롤, 즉 <xref:System.Windows.Forms.Control>에서 파생된 클래스만 호스팅할 수 있습니다. Aximp.exe를 사용하여 Windows Form에서 ActiveX 컨트롤을 호스팅할 수 있도록 ActiveX 컨트롤에 대한 래퍼 클래스를 생성합니다. 이렇게 하면 다른 Windows Forms 컨트롤에 사용할 수 있는 것과 동일한 디자인 타임 지원 및 프로그래밍 방법을 사용할 수 있습니다.  
  
 ActiveX 컨트롤을 호스팅하려면 <xref:System.Windows.Forms.AxHost>에서 파생된 래퍼 컨트롤을 생성해야 합니다. 이 래퍼 컨트롤에는 내부 ActiveX 컨트롤의 인스턴스가 들어 있으며, ActiveX 컨트롤과 통신할 수는 있지만 Windows Forms 컨트롤로 나타납니다. 이렇게 생성된 컨트롤은 ActiveX 컨트롤을 호스팅하며, 해당 속성, 메서드 및 이벤트를 생성된 컨트롤의 속성, 메서드 및 이벤트로 표시합니다.  
  
 이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.  
  
 명령 프롬프트에 다음을 입력합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
aximp [options]{file.dll | file.ocx}  
```  
  
## <a name="remarks"></a>설명  
  
|인수|설명|  
|--------------|-----------------|  
|*file*|변환할 ActiveX 컨트롤이 들어 있는 소스 파일의 이름입니다. file 인수의 확장명은 .dll 또는 .ocx이어야 합니다.|  
  
|옵션|설명|  
|------------|-----------------|  
|`/delaysign`|Aximp.exe에서 지연 서명을 사용하여 결과 컨트롤에 서명하도록 지정합니다. 이 옵션은 `/keycontainer:`, `/keyfile:` 또는 `/publickey:` 옵션과 함께 지정해야 합니다. 지연 서명 프로세스에 대한 자세한 내용은 [어셈블리 서명 연기](../../standard/assembly/delay-sign.md)를 참조하세요.|  
|`/help`|이 도구의 명령 구문 및 옵션을 표시합니다.|  
|`/keycontainer:` *containerName*|*containerName*에서 지정된 키 컨테이너에 있는 퍼블릭/프라이빗 키 쌍을 사용하여 강력한 이름으로 결과 컨트롤에 서명합니다.|  
|`/keyfile:` *filename*|*filename*에 있는 게시자의 공식 퍼블릭/프라이빗 키 쌍을 사용하여 강력한 이름으로 결과 컨트롤에 서명합니다.|  
|`/nologo`|Microsoft 시작 배너를 표시하지 않습니다.|  
|`/out:` *filename*|만들 어셈블리의 이름을 지정합니다.|  
|`/publickey:` *filename*|*filename*에서 지정한 파일에 있는 공개 키를 사용하여 강력한 이름으로 결과 컨트롤에 서명합니다.|  
|`/rcw:` *filename*|새로 생성하는 대신 지정된 런타임 호출 가능 래퍼를 사용합니다. 여러 인스턴스를 지정할 수 있습니다. 현재 디렉터리는 상대 경로에서 사용합니다. 자세한 내용은 [런타임 호출 가능 래퍼](../../standard/native-interop/runtime-callable-wrapper.md)를 참조하세요.|  
|`/silent`|성공 메시지를 표시하지 않습니다.|  
|`/source`|Windows Forms 래퍼에 대한 C# 소스 코드를 생성합니다.|  
|`/verbose`|세부 정보 표시 모드를 지정합니다. 즉, 추가 진행 정보를 표시합니다.|  
|`/?`|이 도구의 명령 구문 및 옵션을 표시합니다.|  
  
 Aximp.exe를 사용하면 전체 ActiveX 컨트롤 형식 라이브러리를 한꺼번에 변환하고, 공용 언어 런타임 메타데이터가 들어 있으며 원본 형식 라이브러리에 정의된 형식의 구현을 제어하는 어셈블리를 생성할 수 있습니다. 이렇게 생성된 파일의 이름은 다음 패턴에 따라 지정됩니다.  
  
 COM 형식을 위한 공용 언어 런타임 프록시: *progid*.dll  
  
 ActiveX 컨트롤을 위한 Windows Forms 프록시(여기서 Ax는 ActiveX를 의미함): Ax*progid*.dll  
  
> [!NOTE]
> ActiveX 컨트롤의 멤버 이름이 .NET Framework에 정의된 이름과 일치하는 경우 Aximp.exe에서 AxHost 파생 클래스를 만들 때 해당 멤버 이름 앞에 "Ctl"이 붙습니다. 예를 들어, ActiveX 컨트롤에 이름이 "Layout"인 멤버가 있을 경우 .NET Framework에 Layout이라는 이벤트가 이미 정의되어 있으므로 AxHost 파생 클래스에서 이 멤버의 이름이 "CtlLayout"으로 변경됩니다.  
  
 생성된 파일은 [Ildasm.exe(IL 디스어셈블러)](ildasm-exe-il-disassembler.md)와 같은 도구를 사용하여 검사할 수 있습니다.  
  
 Aximp.exe를 사용하여 ActiveX WebBrowser 컨트롤에 대한 .NET 어셈블리(shdocvw.dll)를 생성할 수는 없습니다.  
  
 shdocvw.dll을 대상으로 Aximp.exe를 실행하면 도구가 실행되는 디렉터리에 shdocvw.dll이라는 다른 파일이 만들어집니다. 이렇게 생성된 파일이 Documents 및 Settings 디렉터리에 있으면 Microsoft Internet Explorer 및 Windows 탐색기에 문제가 발생합니다. 컴퓨터가 다시 부팅되면 Windows는 system32 디렉터리보다 Documents and Settings 디렉터리에서 먼저 shdocvw.dll 복사본을 찾습니다. 그러면 Documents and Settings의 복사본을 사용하여 관리되는 래퍼를 로드하려고 시도합니다. Internet Explorer 및 Windows 탐색기는 system32 디렉터리에 있는 shdocvw.dll 버전의 렌더링 엔진에 따라 작동하므로 이 경우 제대로 작동하지 않게 됩니다. 이러한 문제가 발생하면 Documents and Settings 디렉터리에 있는 shdocvw.dll 복사본을 삭제한 다음 컴퓨터를 다시 부팅합니다.  
  
 shdocvw.dll과 함께 Aximp.exe를 사용하여 애플리케이션 개발에 사용할 .NET 어셈블리를 만드는 경우에도 문제가 발생할 수 있습니다. 이러한 경우 애플리케이션에서 shdocvw.dll의 시스템 버전과 생성된 버전을 모두 로드하고 시스템 버전을 우선 적용하게 됩니다. 이때 WebBrowser ActiveX 컬렉션 내에서 웹 페이지를 로드하려고 하면 사용자에게 열기/저장 대화 상자가 표시될 수 있습니다. 사용자가 **열기**를 클릭하면 웹 페이지가 Internet Explorer에서 열립니다. 이 문제는 Internet Explorer 버전 6 또는 이전 버전을 실행하는 컴퓨터에서만 발생합니다. 이 문제를 방지하려면 관리되는 <xref:System.Windows.Forms.WebBrowser> 컨트롤을 사용하거나 다음의 설명에 따라 Visual Studio를 사용하여 관리되는 shdocvw.dll을 생성합니다. [방법: 형식 라이브러리에 참조 추가](../interop/how-to-add-references-to-type-libraries.md).  
  
## <a name="example"></a>예  
 다음 명령을 사용하여 Media Player 컨트롤 `msdxm.ocx`를 위한 MediaPlayer.dll 및 AxMediaPlayer.dll을 생성합니다.  
  
```console 
aximp c:\systemroot\system32\msdxm.ocx  
```  
  
## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [Ildasm.exe(IL 디스어셈블러)](ildasm-exe-il-disassembler.md)
