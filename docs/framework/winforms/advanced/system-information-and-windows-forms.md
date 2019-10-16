---
title: 시스템 정보 및 Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- domain names [Windows Forms], retrieving
- SystemInformation class [Windows Forms]
- user names [Windows Forms], retrieving
- system information [Windows Forms]
ms.assetid: 30cf43a3-8cb2-4ff3-862b-6c34576616a8
ms.openlocfilehash: 2edc2e867259f8884467c3d5b0ae3d22ba391a77
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66380111"
---
# <a name="system-information-and-windows-forms"></a>시스템 정보 및 Windows Forms
경우에 따라 코드에서 결정 하기 위해 응용 프로그램에서 실행 되는 컴퓨터에 대 한 정보를 수집 해야 합니다. 예를 들어만 특정 네트워크 도메인;에 연결 하는 경우에 적용할 수 있는 함수를 해야 할 수 있습니다. 이 경우 도메인을 확인 하 고 도메인에 없는 경우 함수를 사용 하지 않도록 설정 하는 방법을 해야 합니다.  
  
 Windows Forms 응용 프로그램에서 사용할 수는 <xref:System.Windows.Forms.SystemInformation> 실행된 시간에 다양 한 컴퓨터에 대 한 작업을 결정 하는 클래스입니다. 다음 예제는 <xref:System.Windows.Forms.SystemInformation> 검색할 클래스를 <xref:System.Windows.Forms.SystemInformation.UserName%2A> 및 <xref:System.Windows.Forms.SystemInformation.UserDomainName%2A>:  
  
```vb  
Dim User As String = Windows.Forms.SystemInformation.UserName  
Dim Domain As String = Windows.Forms.SystemInformation.UserDomainName  
  
MessageBox.Show("Good morning " & User & ". You are connected to " _  
& Domain)  
```  
  
```csharp  
string User = SystemInformation.UserName;  
string Domain = SystemInformation.UserDomainName;  
  
MessageBox.Show("Good morning " + User + ". You are connected to "
+ Domain);
```  
  
 모든 멤버는 <xref:System.Windows.Forms.SystemInformation> 클래스는 읽기 전용 이며 사용자의 설정을 수정할 수 없습니다. 컴퓨터에 연결 하는 모니터의 수는 모든 정보를 반환 하는 클래스의 100 개 이상의 멤버가 (<xref:System.Windows.Forms.SystemInformation.MonitorCount%2A>)의 Windows 탐색기 아이콘 간격으로 (<xref:System.Windows.Forms.SystemInformation.IconHorizontalSpacing%2A> 및 <xref:System.Windows.Forms.SystemInformation.IconVerticalSpacing%2A>).  
  
 유용한 구성원 중 일부는 <xref:System.Windows.Forms.SystemInformation> 클래스에 포함 <xref:System.Windows.Forms.SystemInformation.ComputerName%2A>를 <xref:System.Windows.Forms.SystemInformation.DbcsEnabled%2A>, <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A>, 및 <xref:System.Windows.Forms.SystemInformation.TerminalServerSession%2A>합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.SystemInformation>
- [Windows Forms의 전원 관리](power-management-in-windows-forms.md)
