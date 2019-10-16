---
ms.openlocfilehash: e613f0c52c77efebf250f5935d5cbfc29bc09a6b
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67802522"
---
### <a name="wpf-printing-stack-update"></a>WPF 인쇄 스택 업데이트

|   |   |
|---|---|
|세부 정보|이제 <xref:System.Printing.PrintQueue?displayProperty=name>을 사용하는 WPF 인쇄 API는 사용되지 않는 XPS 인쇄 API 대신 Windows의 인쇄 문서 패키지 API를 호출합니다. 서비스 효율성이 변경됩니다. 사용자와 개발자 모두 동작이나 API 사용에서 달라진 내용을 알 수 없습니다. Windows 10 크리에이터스 업데이트에서 실행될 때 기본적으로 새로운 인쇄 스택을 사용합니다. 이전 인쇄 스택은 이전 Windows 버전에서처럼 계속 작동합니다.|
|제안|Windows 10 크리에이터스 업데이트에서 이전 스택을 사용하려면 <code>HKEY_CURRENT_USER\Software\Microsoft\.NETFramework\Windows Presentation Foundation\Printing</code> 레지스트리 키의 <code>UseXpsOMPrinting</code> REG_DWORD 값을 <code>1</code>로 설정합니다.|
|범위|Microsoft Edge|
|버전|4.7|
|Type|런타임|

