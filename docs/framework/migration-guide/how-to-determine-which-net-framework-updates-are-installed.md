---
title: '방법: 설치된 .NET Framework 보안 업데이트 및 핫픽스 확인'
description: 컴퓨터에 설치된 .NET Framework 보안 업데이트 및 핫픽스를 확인하는 방법을 알아봅니다.
ms.date: 11/27/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- updates, determining for .NET Framework
- .NET Framework, determining updates
ms.assetid: 53c7b5f7-d47a-402a-b194-7244a696a88b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c4c505c679c46494f7dc2534c2bbe9f50243a7dd
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790072"
---
# <a name="how-to-determine-which-net-framework-security-updates-and-hotfixes-are-installed"></a>방법: 설치된 .NET Framework 보안 업데이트 및 핫픽스 확인

이 문서에서는 컴퓨터에 설치된 .NET Framework 보안 업데이트 및 핫픽스를 확인하는 방법을 보여 줍니다.

> [!NOTE]
> 이 문서에 표시된 모든 방법을 사용하려면 관리자 권한이 있는 계정이 필요합니다.

## <a name="to-find-installed-updates-using-the-registry"></a>레지스트리를 사용하여 설치된 업데이트를 찾으려면

컴퓨터에 설치된 각 .NET Framework 버전에 대해 설치된 보안 업데이트 및 핫픽스는 Windows 레지스트리에 나열됩니다. 레지스트리 편집기(*regedit.exe*)를 사용하여 이 정보를 볼 수 있습니다.

1. **regedit.exe** 프로그램을 엽니다. Windows 8 및 이후 버전에서는 **시작** ![Windows 로고](../get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo")을 마우스 오른쪽 단추로 클릭한 다음 **실행**을 선택합니다. **열기** 상자에 **regedit**를 입력하고 **확인**을 선택합니다.

2. 레지스트리 편집기에서 다음 하위 키를 엽니다.

     `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Updates`

     설치된 업데이트가 적용되는 .NET Framework 버전을 식별하는 하위 키 아래에 나열됩니다. 각 업데이트는 KB(기술 자료) 번호로 식별됩니다.

레지스트리 편집기에서 .NET Framework 버전과 각 버전에 대해 설치된 업데이트는 서로 다른 하위 키에 저장되어 있습니다. 설치된 버전 번호를 검색하는 방법에 대한 내용은 [방법: 설치된 .NET Framework 버전 확인](how-to-determine-which-versions-are-installed.md)을 참조하세요.

## <a name="to-find-installed-updates-by-querying-the-registry-in-code"></a>코드에서 레지스트리를 쿼리하여 설치된 업데이트를 찾으려면

다음 예제에서는 컴퓨터에 설치된 .NET Framework 보안 업데이트 및 핫픽스를 프로그래밍 방식으로 확인합니다.

[!code-csharp[ListUpdates](../../../samples/snippets/csharp/VS_Snippets_CLR/listupdates/cs/program.cs)]
[!code-vb[ListUpdates](../../../samples/snippets/visualbasic/VS_Snippets_CLR/listupdates/vb/program.vb)]

이 예제는 다음과 유사한 출력을 생성합니다.

```console
Microsoft .NET Framework 4 Client Profile
  KB2468871
  KB2468871v2
  KB2478063
  KB2533523
  KB2544514
  KB2600211
  KB2600217
Microsoft .NET Framework 4 Extended
  KB2468871
  KB2468871v2
  KB2478063
  KB2533523
  KB2544514
  KB2600211
  KB2600217
```

## <a name="to-find-installed-updates-by-querying-the-registry-in-powershell"></a>PowerShell에서 레지스트리를 쿼리하여 설치된 업데이트를 찾으려면

다음 예제에서는 PowerShell을 사용하여 컴퓨터에 설치된 .NET Framework 보안 업데이트 및 핫픽스를 확인하는 방법을 보여 줍니다.

```powershell
$DotNetVersions = Get-ChildItem HKLM:\SOFTWARE\WOW6432Node\Microsoft\Updates | Where-Object {$_.name -like
 "*.NET Framework*"}

ForEach($Version in $DotNetVersions){
    
   $Updates = Get-ChildItem $Version.PSPath
    $Version.PSChildName
    ForEach ($Update in $Updates){
       $Update.PSChildName
       }
}
```

이 예제는 다음과 유사한 출력을 생성합니다.

```console
Microsoft .NET Framework 4 Client Profile
KB2468871
KB2468871v2
KB2478063
KB2533523
KB2544514
KB2600211
KB2600217
Microsoft .NET Framework 4 Extended
KB2468871
KB2468871v2
KB2478063
KB2533523
KB2544514
KB2600211
KB2600217
```

## <a name="see-also"></a>참고 항목

- [방법: 설치된 .NET Framework 버전 확인](how-to-determine-which-versions-are-installed.md)
- [개발자용 .NET Framework 설치](../install/guide-for-developers.md)
- [버전 및 종속성](versions-and-dependencies.md)
