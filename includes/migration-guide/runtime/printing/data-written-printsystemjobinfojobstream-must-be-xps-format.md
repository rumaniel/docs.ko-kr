---
ms.openlocfilehash: 74f00821f2304664729faa8de2f0163c6611f513
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "66379536"
---
### <a name="data-written-to-printsystemjobinfojobstream-must-be-in-xps-format"></a>PrintSystemJobInfo.JobStream에 기록된 데이터는 XPS 형식이어야 합니다.

|   |   |
|---|---|
|세부 정보|<xref:System.Printing.PrintSystemJobInfo.JobStream> 속성은 인쇄 작업 스트림을 공개합니다. 사용자는 이 스트림을 작성하여 기본 운영 체제 인쇄 구성 요소로 원시 데이터를 보낼 수 있습니다. Windows 8 이후 버전 Windows 운영 체제의 .NET Framework 4.5부터 이 스트림에 작성되는 데이터는 패키지 스트림과 같은 XPS 형식이어야 합니다.|
|제안 해결 방법|인쇄 내용을 출력하려면 다음 중 하나를 수행할 수 있습니다.<ul><li><xref:System.Windows.Xps.XpsDocumentWriter> 클래스를 사용하여 인쇄 내용을 출력합니다. 이는 권장되는 대안입니다.</li><li><xref:System.Printing.PrintSystemJobInfo.JobStream> 속성에서 반환된 스트림으로 전송된 데이터가 패키지 스트림과 같은 XPS 형식인지 확인합니다.</li></ul>|
|범위|부|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Printing.PrintSystemJobInfo.JobStream?displayProperty=nameWithType></li></ul>|
