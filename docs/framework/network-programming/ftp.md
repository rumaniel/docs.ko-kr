---
title: FTP - .NET
ms.date: 03/30/2017
helpviewer_keywords:
- FTP
ms.assetid: 9b43f8b4-89d7-46a7-89fc-71aca916dd32
ms.openlocfilehash: d945f03077a863d9e1baa6b59fe8a908566aba5a
ms.sourcegitcommit: 90775b20343b6ad831af6f5380f8ab7553abb16b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/10/2019
ms.locfileid: "54186152"
---
# <a name="ftp"></a>FTP

.NET Framework에서는 <xref:System.Net.FtpWebRequest> 및 <xref:System.Net.FtpWebResponse> 클래스를 사용한 FTP 프로토콜을 포괄적으로 지원합니다. 이러한 클래스는 <xref:System.Net.WebRequest> 및 <xref:System.Net.WebResponse>에서 파생됩니다. 대부분의 경우 <xref:System.Net.WebRequest> 및 <xref:System.Net.WebResponse> 클래스는 요청을 만드는 데 필요한 모든 것을 제공하지만, 속성으로 노출되는 FTP별 기능에 액세스해야 할 경우 이러한 클래스를 <xref:System.Net.FtpWebRequest> 또는 <xref:System.Net.FtpWebResponse>로 형식 캐스팅해야 합니다.

## <a name="examples"></a>예제

자세한 내용은 다음 항목을 참조하세요. [방법: FTP를 사용하여 파일 다운로드](how-to-download-files-with-ftp.md), [방법: FTP를 사용하여 파일 업로드](how-to-upload-files-with-ftp.md), [방법: FTP를 사용하여 디렉터리 내용 나열](how-to-list-directory-contents-with-ftp.md).

## <a name="ftp-and-proxies"></a>FTP 및 프록시

<xref:System.Net.FtpWebRequest.Proxy%2A> 속성으로 지정되는 프록시가 HTTP 프로시인 경우 <xref:System.Net.WebRequestMethods.Ftp.DownloadFile>, <xref:System.Net.WebRequestMethods.Ftp.ListDirectory> 및 <xref:System.Net.WebRequestMethods.Ftp.ListDirectoryDetails> 명령만 지원됩니다.

## <a name="see-also"></a>참고 항목

- [프록시를 통해 인터넷 액세스](accessing-the-internet-through-a-proxy.md)
- [네트워크 프로그래밍 샘플](network-programming-samples.md)
- [애플리케이션 프로토콜 사용](using-application-protocols.md)
