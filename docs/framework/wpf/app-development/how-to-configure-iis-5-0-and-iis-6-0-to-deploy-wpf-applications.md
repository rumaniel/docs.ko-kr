---
title: '방법: IIS 5.0 및 IIS 6.0을 구성하여 WPF 애플리케이션 배포'
ms.date: 03/30/2017
helpviewer_keywords:
- MIME types [WPF], registering
- adjusting content expiration setting [WPF]
- registering file extensions [WPF]
- deploying applications [WPF]
- applications [WPF], deploying
- Web servers [WPF], configuring to deploy WPF applications
- configuring Web servers to deploy WPF applications [WPF]
- content expiration setting [WPF], adjusting
- file extensions [WPF], registering
- registering MIME types [WPF]
ms.assetid: c6e8c2cb-9ba2-4e75-a0d5-180ec9639433
ms.openlocfilehash: 3a9bf79a9d505fef53b62cb589920adcf95ae92a
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69611497"
---
# <a name="how-to-configure-iis-50-and-iis-60-to-deploy-wpf-applications"></a>방법: IIS 5.0 및 IIS 6.0을 구성하여 WPF 애플리케이션 배포

적절 한 mime ( [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 인터넷 메일 확장) 형식으로 구성 된 대부분의 웹 서버에서 응용 프로그램을 배포할 수 있습니다. 기본적으로 Microsoft 인터넷 정보 서비스 (IIS) 7.0는 이러한 MIME 형식으로 구성 되지만 Microsoft 인터넷 정보 서비스 (IIS) 5.0 및 Microsoft 인터넷 정보 서비스 (IIS) 6.0는 그렇지 않습니다.

이 항목에서는 응용 프로그램을 배포 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 하기 위해 microsoft 인터넷 정보 서비스 (iis) 5.0 및 microsoft 인터넷 정보 서비스 (iis) 6.0를 구성 하는 방법을 설명 합니다.

> [!NOTE]
> 레지스트리에서 *UserAgent* 문자열을 확인 하 여 시스템에 .NET Framework 설치 되어 있는지 여부를 확인할 수 있습니다. *UserAgent* 문자열을 검사 하 여 .NET Framework가 시스템에 설치 되어 있는지 여부를 확인 하는 스크립트 및 세부 정보는 [.NET Framework 3.0가 설치 되어 있는지 검색](how-to-detect-whether-the-net-framework-3-0-is-installed.md)을 참조 하세요.

<a name="content_expiration"></a>

## <a name="adjust-the-content-expiration-setting"></a>콘텐츠 만료 설정 조정

콘텐츠 만료 설정을 1분으로 조정할 수 있습니다. 다음 절차에서는 IIS를 사용 하 여이 작업을 수행 하는 방법을 간략하게 설명 합니다.

1. **시작** 메뉴를 클릭하고 **관리 도구**를 가리킨 후 **IIS(인터넷 정보 서비스) 관리자**를 클릭합니다. 명령줄에서도 “%SystemRoot%\system32\inetsrv\iis.msc”로 이 애플리케이션을 시작할 수 있습니다.

2. **기본 웹 사이트** 노드를 찾을 때까지 IIS 트리를 확장 합니다.

3. **기본 웹 사이트**를 마우스 오른쪽 단추로 클릭하고 컨텍스트 메뉴에서 **속성**을 선택합니다.

4. **HTTP 헤더** 탭을 선택하고 “콘텐츠 만료 사용”을 클릭합니다.

5. 1분 후에 만료하도록 콘텐츠를 설정합니다.

<a name="register_mime_types"></a>

## <a name="register-mime-types-and-file-extensions"></a>MIME 형식과 파일 확장명 등록

클라이언트 시스템의 브라우저에서 올바른 처리기를 로드할 수 있도록 여러 MIME 형식 및 파일 확장명을 등록 해야 합니다. 다음 형식을 추가해야 합니다.

|확장명|MIME 형식|
|---------------|---------------|
|.manifest|application/manifest|
|.xaml|application/xaml+xml|
|.application|application/x-ms-application|
|.xbap|application/x-ms-xbap|
|.deploy|application/octet-stream|
|.xps|application/vnd.ms-xpsdocument|

> [!NOTE]
> 클라이언트 시스템에는 MIME 형식 또는 파일 확장명을 등록할 필요가 없습니다. Microsoft .NET Framework를 설치할 때 자동으로 등록 됩니다.

다음 VBScript (Microsoft Visual Basic Scripting Edition) 샘플에서는 IIS에 필요한 MIME 형식을 자동으로 추가 합니다. 스크립트를 사용하려면 서버에서 .vbs 파일을 코드에 복사합니다. 그런 다음 명령줄에서 파일을 실행하거나 [!INCLUDE[TLA#tla_winexpl](../../../../includes/tlasharptla-winexpl-md.md)]에서 파일을 두 번 클릭하여 스크립트를 실행합니다.

```vb
' This script adds the necessary Windows Presentation Foundation MIME types
' to an IIS Server.
' To use this script, just double-click or execute it from a command line.
' Running this script multiple times results in multiple entries in the IIS MimeMap.

Dim MimeMapObj, MimeMapArray, MimeTypesToAddArray, WshShell, oExec
Const ADS_PROPERTY_UPDATE = 2

' Set the MIME types to be added
MimeTypesToAddArray = Array(".manifest", "application/manifest", ".xaml", _
    "application/xaml+xml", ".application", "application/x-ms-application", _
    ".deploy", "application/octet-stream", ".xbap", "application/x-ms-xbap", _
    ".xps", "application/vnd.ms-xpsdocument")

' Get the MimeMap object
Set MimeMapObj = GetObject("IIS://LocalHost/MimeMap")

' Call AddMimeType for every pair of extension/MIME type
For counter = 0 to UBound(MimeTypesToAddArray) Step 2
    AddMimeType MimeTypesToAddArray(counter), MimeTypesToAddArray(counter+1)
Next

' Create a Shell object
Set WshShell = CreateObject("WScript.Shell")

' Stop and Start the IIS Service
Set oExec = WshShell.Exec("net stop w3svc")
Do While oExec.Status = 0
    WScript.Sleep 100
Loop

Set oExec = WshShell.Exec("net start w3svc")
Do While oExec.Status = 0
    WScript.Sleep 100
Loop

Set oExec = Nothing

' Report status to user
WScript.Echo "Windows Presentation Foundation MIME types have been registered."

' AddMimeType Sub
Sub AddMimeType (Ext, MType)

    ' Get the mappings from the MimeMap property.
    MimeMapArray = MimeMapObj.GetEx("MimeMap")

    ' Add a new mapping.
    i = UBound(MimeMapArray) + 1
    ReDim Preserve MimeMapArray(i)
    Set MimeMapArray(i) = CreateObject("MimeMap")
    MimeMapArray(i).Extension = Ext
    MimeMapArray(i).MimeType = MType
    MimeMapObj.PutEx ADS_PROPERTY_UPDATE, "MimeMap", MimeMapArray
    MimeMapObj.SetInfo

End Sub
```

> [!NOTE]
> 이 스크립트를 여러 번 실행 하면 Microsoft 인터넷 정보 서비스 (IIS) 5.0 또는 Microsoft 인터넷 정보 서비스 (IIS) 6.0 메타 베이스에 여러 MIME 맵 항목이 생성 됩니다.

이 스크립트를 실행 한 후에는 Microsoft 인터넷 정보 서비스 (IIS) 5.0 또는 microsoft 인터넷 정보 서비스 (IIS) 6.0 MMC (microsoft Management Console)에서 추가 MIME 형식이 표시 되지 않을 수 있습니다. 그러나 이러한 MIME 형식은 Microsoft 인터넷 정보 서비스 (IIS) 5.0 또는 Microsoft 인터넷 정보 서비스 (IIS) 6.0 메타 베이스에 추가 되었습니다. 다음 스크립트는 Microsoft 인터넷 정보 서비스 (IIS) 5.0 또는 Microsoft 인터넷 정보 서비스 (IIS) 6.0 메타 베이스에 모든 MIME 형식을 표시 합니다.

```vb
' This script lists the MIME types for an IIS Server.
' To use this script, just double-click or execute it from a command line
' by calling cscript.exe

dim mimeMapEntry, allMimeMaps

' Get the MimeMap object.
Set mimeMapEntry = GetObject("IIS://localhost/MimeMap")
allMimeMaps = mimeMapEntry.GetEx("MimeMap")

' Display the mappings in the table.
For Each mimeMap In allMimeMaps
    WScript.Echo(mimeMap.MimeType & " (" & mimeMap.Extension + ")")
Next
```

스크립트를 `.vbs` 파일로 저장하고(예: `DiscoverIISMimeTypes.vbs`) 다음 명령을 사용하여 명령 프롬프트에서 실행합니다.

```console
cscript DiscoverIISMimeTypes.vbs
```
