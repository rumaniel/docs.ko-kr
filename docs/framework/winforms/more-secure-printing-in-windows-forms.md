---
title: Windows Forms의 인쇄 추가 보안
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, printing
- PrintingPermission class [Windows Forms], Windows Forms security
- printing [Windows Forms], security
- security [Windows Forms], printing
ms.assetid: 48fd36ac-872f-4de0-902a-e52969cd4367
ms.openlocfilehash: b0387a82f142fb32912dad1370d6ac0c784e8894
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592647"
---
# <a name="more-secure-printing-in-windows-forms"></a>Windows Forms의 인쇄 추가 보안
Windows Forms 응용 프로그램에 인쇄 기능이 포함 되는 경우가 많습니다. .NET Framework를 사용 합니다 <xref:System.Drawing.Printing.PrintingPermission> 인쇄 기능에 대 한 액세스 제어 및 관련 클래스 <xref:System.Drawing.Printing.PrintingPermissionLevel> 액세스 수준을 나타내는 열거형 값입니다. 기본적으로 인쇄 로컬 인트라넷 및 인터넷 영역;에 기본적으로 사용 하도록 설정 그러나 두 영역에 대 한 액세스 수준이 제한 됩니다. 사용자 상호 작용이 필요한 응용 프로그램 인쇄할 수 있는지 또는 수 없습니다. 응용 프로그램에 부여 된 사용 권한 값에 따라 달라 집니다 인쇄 합니다. 기본적으로 로컬 인트라넷 영역 받게 <xref:System.Drawing.Printing.PrintingPermissionLevel.DefaultPrinting> 권한과 인트라넷 영역 수신 <xref:System.Drawing.Printing.PrintingPermissionLevel.SafePrinting> 액세스 합니다.  
  
 다음 표에서 각 인쇄 권한 수준에서 사용할 수 있는 기능을 보여 줍니다.  
  
|PrintingPermissionLevel|설명|  
|-----------------------------|-----------------|  
|<xref:System.Drawing.Printing.PrintingPermissionLevel.AllPrinting>|설치 된 모든 프린터에 대 한 전체 액세스를 제공합니다.|  
|<xref:System.Drawing.Printing.PrintingPermissionLevel.DefaultPrinting>|기본 프린터를 프로그래밍 방식 인쇄 및 인쇄 제한적인 대화 상자를 통해 안전 하 게 인쇄할 수 있습니다. <xref:System.Drawing.Printing.PrintingPermissionLevel.DefaultPrinting>는 <xref:System.Drawing.Printing.PrintingPermissionLevel.AllPrinting>의 하위 집합입니다.|  
|<xref:System.Drawing.Printing.PrintingPermissionLevel.SafePrinting>|보다 제한 된 대화 상자 에서만에서 인쇄를 제공합니다. <xref:System.Drawing.Printing.PrintingPermissionLevel.SafePrinting>는 <xref:System.Drawing.Printing.PrintingPermissionLevel.DefaultPrinting>의 하위 집합입니다.|  
|<xref:System.Drawing.Printing.PrintingPermissionLevel.NoPrinting>|프린터에 대 한 액세스를 차단합니다. <xref:System.Drawing.Printing.PrintingPermissionLevel.NoPrinting>는 <xref:System.Drawing.Printing.PrintingPermissionLevel.SafePrinting>의 하위 집합입니다.|  
  
## <a name="see-also"></a>참고자료

- [Windows Forms의 파일 및 데이터 액세스 추가 보안](more-secure-file-and-data-access-in-windows-forms.md)
- [Windows Forms의 추가 보안 고려 사항](additional-security-considerations-in-windows-forms.md)
- [Windows Forms의 보안 개요](security-in-windows-forms-overview.md)
- [Windows Forms 보안](windows-forms-security.md)
