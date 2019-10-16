---
title: .NET Framework 버전 및 종속성
ms.custom: updateeachrelease
ms.date: 04/18/2019
helpviewer_keywords:
- versions, .NET Framework
ms.assetid: f75a72de-e2f2-4a7a-9574-3f278684ea90
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c9f7a0bc3a7a41a77db3c90c2f88fb5ddfd7bfa0
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70971084"
---
# <a name="net-framework-versions-and-dependencies"></a>.NET Framework 버전 및 종속성
.NET Framework의 각 버전에는 CLR(공용 언어 런타임), 기본 클래스 라이브러리 및 기타 관리되는 라이브러리가 포함되어 있습니다. 이 항목에서는 버전별 .NET Framework의 주요 기능에 대해 설명하고 기본 CLR 버전 및 관련 개발 환경에 대한 정보를 제공하며 Windows 운영 체제별로 설치된 버전을 확인합니다.  
  
> [!NOTE]
> .NET Framework 다운로드 및 설치에 대한 자세한 내용은 [개발자용 .NET Framework 설치](../install/guide-for-developers.md)를 참조하세요.  
  
 다음 테이블에는 .NET Framework 버전 기록이 요약되어 있으며 Visual Studio, Windows 및 Windows Server와의 상관 관계가 나와 있습니다. Visual Studio에서는 나열된 .NET Framework 버전으로 사용이 제한되지 않도록 멀티 타기팅 기능을 제공합니다.  
  
 새 .NET Framework 버전에서는 각각 이전 버전의 기능을 유지하며 새 기능을 추가합니다. CLR은 고유한 버전 번호로 식별됩니다. CLR 버전은 매번 증가하지 않지만, .NET Framework 버전 번호는 각 릴리스마다 증가합니다. 예를 들어 .NET Framework 4, 4.5 및 이후 릴리스에는 CLR 4가 포함되지만 .NET Framework 2.0, 3.0 및 3.5에는 CLR 2.0이 포함됩니다. CLR 버전 3이 포함된 .NET Framework 버전은 없습니다.  
  
 지원되는 운영 체제의 전체 목록은 [시스템 요구 사항](../get-started/system-requirements.md)을 참조하십시오. 다운로드에 대해서는 [개발자용 .NET Framework 설치](../install/guide-for-developers.md)를 참조하세요. 컴퓨터에 설치되어 있는 .NET Framework의 버전을 확인하려면 [방법: 설치된 .NET Framework 버전 확인](how-to-determine-which-versions-are-installed.md)을 참조하세요.  
  
 표의 **Windows에 포함됨/설치 가능** 및 **Windows Server에 포함됨/설치 가능** 열에 ✓ 표시된 운영 체제 버전에 설치된 .NET Framework 버전은 [제어판에서 활성화](../install/dotnet-35-windows-10.md)되거나(Windows의 경우) 서버 관리자를 통해 활성화되어야(Windows Server의 경우) 합니다.  

[!INCLUDE[Release key values note](~/includes/version-keys-note.md)]
 
|.NET Framework 버전|CLR 버전|포함된 운영 체제<br /> Visual Studio<br/>버전|✓ 다음에서 포함된 버전:<br />+ 다음에서 설치 가능한 버전:<br />Windows|✓ 다음에서 포함된 버전:<br />+ 다음에서 설치 가능한 버전:<br />Windows Server|설치된 .NET 버전 확인 방법|  
|----------------------------|-----------------|--------------|---------------------------------------|----------------------------------------------------|-----------------------------------------------------------|-----------------------------------------| 
|4.8<br/><br/>[새로운 기능](../whats-new/index.md#whats-new-in-net-framework-48)<br/><br/>[내게 필요한 옵션의 새로운 기능](../whats-new/whats-new-in-accessibility.md#whats-new-in-accessibility-in-net-framework-48)<br /><br >[릴리스 정보](https://github.com/Microsoft/dotnet/tree/master/releases/net48/README.md)|4| | ✓ 2019년 5월 10일 업데이트<br/><br/> + 2018년 10월 10일 업데이트(버전 1809) <br/> + 2018년 4월 10일 업데이트(버전 1803) <br/> + 10 Fall Creators Update(버전 1709) <br/> + 10 Creators Update(버전 1703) <br/> + 10 1주년 업데이트(버전 1607) <br/> + 8.1 <br/> +7 | + Windows Server 2019<br/> + Windows Server, 버전 1809 <br/> + Windows Server, 버전 1803 <br/> + 2016 <br/> + 2012 R2 <br/> + 2012 <br/> + 2008 R2 SP1 |`Release` DWORD 사용:<br/><br/> - 528040(Windows 10 2019년 5월 업데이트) <br/> - 528049(다른 모든 OS 버전) <br/><br/> ([지침](how-to-determine-which-versions-are-installed.md) 참조)|
|4.7.2<br/><br/>[새로운 기능](../whats-new/index.md#whats-new-in-net-framework-472)<br/><br/>[내게 필요한 옵션의 새로운 기능](../whats-new/whats-new-in-accessibility.md#whats-new-in-accessibility-in-net-framework-472)<br /><br >[릴리스 정보](https://github.com/Microsoft/dotnet/tree/master/releases/net472/README.md)|4| | ✓ 10 2018년 10월 업데이트(버전 1809) <br/> ✓ 10 2018년 4월 업데이트(버전 1803) <br/><br/> + 10 Fall Creators Update(버전 1709) <br/> + 10 Creators Update(버전 1703) <br/> + 10 1주년 업데이트(버전 1607) <br/> + 8.1 <br/> +7 | ✓ Windows Server 2019<br/> ✓ Windows Server, 버전 1809 <br/> ✓ Windows Server, 버전 1803 <br/><br/> + Windows Server, 버전 1709 <br/> + 2016 <br/> + 2012 R2 <br/> + 2012 <br/> + 2008 R2 SP1 |`Release` DWORD 사용:<br/><br/> - 461814(Windows 10 2018년 10월 업데이트) <br/> - 461808(Windows 10 2018년 4월 업데이트 및 Windows Server, 버전 1803) <br/> - 461814(다른 모든 OS 버전) <br/><br/> ([지침](how-to-determine-which-versions-are-installed.md) 참조)|
|4.7.1<br/><br/>[새로운 기능](../whats-new/index.md#whats-new-in-net-framework-471)<br/><br/>[내게 필요한 옵션의 새로운 기능](../whats-new/whats-new-in-accessibility.md#whats-new-in-accessibility-in-net-framework-471)<br /><br >[릴리스 정보](https://github.com/Microsoft/dotnet/tree/master/releases/net471/README.md)|4| | ✓ 10 Fall Creators Update(버전 1709) <br/> <br/> + 10 Creators Update(버전 1703) <br/> + 10 1주년 업데이트(버전 1607) <br/> + 8.1 <br/> +7| + Windows Server, 버전 1803 <br/><br/> ✓ Windows Server, 버전 1709 <br/><br/> + 2016 <br/> + 2012 R2 <br/> + 2012 <br/> + 2008 R2 SP1 |`Release` DWORD 사용:<br/><br/> - 461308(Windows 10 Creators Update 및 Windows Server, 버전 1709) <br/> - 461310(다른 모든 OS 버전) <br/><br/> ([지침](how-to-determine-which-versions-are-installed.md) 참조)| 
|4.7<br/><br/>[새로운 기능](../whats-new/index.md#whats-new-in-net-framework-47)<br /><br >[릴리스 정보](https://github.com/Microsoft/dotnet/tree/master/releases/net47/README.md)|4| | ✓ 10 크리에이터 업데이트(버전 1703) <br/> <br/> + 10 1주년 업데이트(버전 1607) <br/> + 8.1 <br/> +7| + 2016 <br/> + 2012 R2 <br/> + 2012 <br/> + 2008 R2 SP1 |`Release` DWORD 사용:<br/><br/> - 460798(Windows 10 크리에이터 업데이트) <br/> - 460805(다른 모든 OS 버전) <br/><br/> ([지침](how-to-determine-which-versions-are-installed.md) 참조) |  
|4.6.2<br/><br/>[새로운 기능](../whats-new/index.md#whats-new-in-net-framework-462)<br /><br >[릴리스 정보](https://github.com/Microsoft/dotnet/tree/master/releases/net462/README.md)|4||✓ 10 1주년 업데이트(버전 1607) <br /><br /> + 10 11월 업데이트(버전 1511) <br/> + 10 <br/> + 8.1<br />+ 7|✓ 2016<br /><br /> + 2012 R2<br />+ 2012<br />+ 2008 R2 SP1|`Release` DWORD 사용:<br /><br /> - 394802(Windows 10 1주년 업데이트 및 Windows Server 2016) <br />- 394806(다른 모든 OS 버전)<br /><br /> ([지침](how-to-determine-which-versions-are-installed.md) 참조)|  
|4.6.1<br/><br/>[새로운 기능](../whats-new/index.md#whats-new-in-net-framework-461)<br /><br >[릴리스 정보](https://github.com/Microsoft/dotnet/tree/master/releases/net461/README.md)|4||✓ 10 11월 업데이트(버전 1511) <br /><br /> + 10<br />+ 8.1<br />+ 8<br />+ 7|+ 2012 R2<br />+ 2012<br />+ 2008 R2 SP1|`Release` DWORD 사용:<br /><br /> - 394254(Windows 10 11월 업데이트)<br />- 394271(다른 모든 OS 버전)<br /><br /> ([지침](how-to-determine-which-versions-are-installed.md) 참조)|  
|4.6<br/><br/>[새로운 기능](../whats-new/index.md#whats-new-in-net-2015)<br /><br >[릴리스 정보](https://github.com/Microsoft/dotnet/tree/master/releases/net46/README.md)|4|2015|✓ 10<br /><br />+ 8.1<br />+ 8<br />+ 7<br />+ Vista|+ 2012 R2<br />+ 2012<br />+ 2008 R2 SP1<br />+ 2008 SP2|`Release` DWORD 사용:<br /><br /> - 393295(Windows 10)<br />- 393297(다른 모든 OS 버전)<br /><br /> ([지침](how-to-determine-which-versions-are-installed.md) 참조)|  
|4.5.2<br/><br/>[새로운 기능](../whats-new/index.md#whats-new-in-net-framework-452)<br /><br >[릴리스 정보](https://github.com/Microsoft/dotnet/tree/master/releases/net452/README.md)|4|-|+ 8.1<br />+ 8<br />+ 7<br />+ Vista|+ 2012 R2<br />+ 2012<br />+ 2008 R2 SP1<br />+ 2008 SP2|`Release` DWORD 사용:<br /><br /> 379893<br /><br />([지침](how-to-determine-which-versions-are-installed.md) 참조)|  
|4.5.1<br/><br/>[새로운 기능](../whats-new/index.md#whats-new-in-net-framework-451)<br /><br >[릴리스 정보](https://github.com/Microsoft/dotnet/tree/master/releases/net451/README.md)|4|2013|✓ 8.1<br /><br />+ 8<br />+ 7<br />+ Vista|✓ 2012 R2<br /><br />+ 2012<br />+ 2008 R2 SP1<br />+ 2008 SP2|`Release` DWORD 사용:<br /><br /> - 378675(Windows 8.1)<br />- 378758(다른 모든 버전)<br /><br /> ([지침](how-to-determine-which-versions-are-installed.md) 참조)|  
|4.5<br/><br/>[새로운 기능](../whats-new/index.md#whats-new-in-net-framework-45)<br /><br >[릴리스 정보](https://github.com/Microsoft/dotnet/tree/master/releases/net45/README.md)|4|2012|✓ 8<br />+ 7<br />+ Vista|✓ 2012<br />+ 2008 R2 SP1<br />+ 2008 SP2|`Release` DWORD 사용:<br /><br /> 378389<br /><br />([지침](how-to-determine-which-versions-are-installed.md) 참조)|  
|4<br/><br/>[새로운 기능](../whats-new/index.md)|4|2010|+ 7<br />+ Vista|+ 2008 R2 SP1<br />+ 2008 SP2<br />+ 2003|[지침](how-to-determine-which-versions-are-installed.md) 참조|  
|3.5<br/><br/>[새로운 기능](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ms171868\(v=vs.90\))|2.0|2008|✓ 10\*<br/>✓ 8.1\*<br />✓ 8\*<br />✓ 7<br /><br />+ Vista|  + Windows Server, 버전 1803\* <br/> + Windows Server, 버전 1709\* <br/> + 2016\* <br/>+ 2012 R2\*<br />+ 2012\*<br /><br />✓2008 R2 SP1\*<br /><br/>+ 2008 SP2<br />+ 2003|[지침](how-to-determine-which-versions-are-installed.md) 참조|  
|3.0<br/><br/>새 항목:<br/>WPF, WCF, WF, CardSpace|2.0|-|✓ Vista|✓ 2008 R2 SP1*<br />✓ 2008 SP2\*<br /><br />+ 2003|[지침](how-to-determine-which-versions-are-installed.md) 참조|  
|2.0<br/><br/>[새로운 기능](https://docs.microsoft.com/previous-versions/dotnet/netframework-2.0/ms229284\(v%3dvs.80\))|2.0|2005|-|✓ 2008 R2 SP1<br />✓ 2008 SP2<br />✓ 2003|[지침](how-to-determine-which-versions-are-installed.md) 참조|  
|1.1<br/><br/>[새로운 기능](https://docs.microsoft.com/previous-versions/dotnet/netframework-1.1/9wtde3k4\(v%3dvs.71\))|1.1|2003|-|✓ 2003|[지침](how-to-determine-which-versions-are-installed.md) 참조|  
|1.0|1.0|Visual Studio .NET|-|-|[지침](how-to-determine-which-versions-are-installed.md) 참조|  

**참고**

<sup>\*</sup>&nbsp;&nbsp;[제어판(Windows) 또는 서버 관리자 (Windows Server)를 통해 이 운영 체제에서 .NET Framework를 사용하도록 설정해야 합니다](../install/dotnet-35-windows-10.md#enable-the-net-framework-35-in-control-panel).

 사용 중인 애플리케이션이 특정 버전에 종속적일 수 있고 해당 버전을 제거하면 애플리케이션이 중단될 수 있으므로 컴퓨터에 설치된 .NET Framework의 모든 버전은 일반적으로 제거하면 안 됩니다. 여러 버전의 .NET Framework를 동시에 단일 컴퓨터에서 로드할 수 있습니다. 즉, 이전 버전을 제거하지 않고도 .NET Framework를 설치할 수 있습니다. 자세한 내용은 [시작](../get-started/index.md)을 참조하십시오.

## <a name="targeting-and-running-net-framework-apps-for-version-45-and-later"></a>버전 4.5 이상의 .NET Framework 앱 대상 지정 및 실행  
 .NET Framework 4.5는 컴퓨터에서 .NET Framework 4를 대체하는 내부 업데이트이고, 마찬가지로 .NET Framework 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2 및 4.8은 .NET Framework 4.5에 대한 내부 업데이트입니다. 즉, 동일한 런타임 버전을 사용하지만, 어셈블리 버전이 업데이트되어 새로운 형식과 멤버를 포함합니다. 이러한 업데이트 중 하나를 설치한 후 .NET Framework 4, .NET Framework 4.5, .NET Framework 4.6 또는 .NET Framework 4.7용 앱은 다시 컴파일하지 않고도 계속 실행되어야 합니다. 하지만 그 반대의 경우는 성립되지 않습니다. 이전 버전의 .NET Framework에서 이후 버전의 .NET Framework를 대상으로 하는 앱을 실행하지 않는 것이 좋습니다. 예를 들어 .NET Framework 4.5에서 .NET Framework 4.6을 대상으로 하는 앱을 실행하지 않는 것이 좋습니다. 다음과 같은 지침이 적용됩니다.  
  
- Visual Studio에서는 프로젝트에 대한 대상 프레임워크로 .NET Framework 4.5를 선택(<xref:Microsoft.Build.Tasks.GetReferenceAssemblyPaths.TargetFrameworkMoniker%2A?displayProperty=nameWithType> 속성을 설정)하여 .NET Framework 4.5 어셈블리 또는 실행 파일로 프로젝트를 컴파일할 수 있습니다. 이 어셈블리 또는 실행 파일은 .NET Framework 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2 또는 4.8이 설치된 모든 컴퓨터에서 사용할 수 있습니다.  
  
- Visual Studio에서는 프로젝트에 대한 대상 프레임워크로 .NET Framework 4.5.1을 선택(<xref:Microsoft.Build.Tasks.GetReferenceAssemblyPaths.TargetFrameworkMoniker%2A?displayProperty=nameWithType> 속성을 설정)하여 .NET Framework 4.5.1 어셈블리 또는 실행 파일로 프로젝트를 컴파일할 수 있습니다. 이 어셈블리 또는 실행 파일은 .NET Framework 4.5.1 이상의 버전이 설치된 컴퓨터에서만 실행됩니다. .NET Framework 4.5.1을 대상으로 하는 실행 파일은 .NET Framework 4.5와 같은 이전 버전의 .NET Framework만 설치된 컴퓨터에서 실행되는 것이 차단되며 사용자에게 .NET Framework 4.5.1을 설치하라는 메시지가 표시됩니다. 또한 .NET Framework 4.5 같은 이전 버전의 .NET Framework를 대상으로 하는 앱에서 .NET Framework 4.5.1 어셈블리를 호출하지 않아야 합니다.  
  
     여기서의 .NET framework 4.5.1 및.NET Framework 4.5는 예제로만 사용되었습니다. 이 원칙은 실행 중인 시스템에 설치된 것보다 이후 버전의 .NET Framework를 대상으로 하는 모든 앱에 적용됩니다.  
  
 .NET Framework의 일부 변경 내용으로 인해 앱 코드를 변경해야 할 수 있습니다. .NET Framework 4.5 이상 버전에서 기존 앱을 실행하기 전에 [애플리케이션 호환성](application-compatibility.md)을 참조하십시오. 현재 버전 설치에 대한 자세한 내용은 [개발자용 .NET Framework 설치](../install/guide-for-developers.md)를 참조하세요. .NET Framework 지원에 대한 자세한 내용은 Microsoft 지원 웹 사이트의 [Microsoft .NET Framework 지원 기간 정책](https://go.microsoft.com/fwlink/?LinkId=196607)을 참조하십시오.  
  
## <a name="targeting-and-running-apps-for-older-versions"></a>이전 버전에 대한 대상 지정 및 앱 실행  

.NET Framework 버전 2.0, 3.0 및 3.5는 동일한 버전의 CLR(CLR 2.0)로 빌드됩니다. 이러한 버전은 단일 설치의 후속 레이어를 나타냅니다. 각 버전은 이전 버전 위에 증분 방식으로 빌드됩니다. 컴퓨터에서 버전 2.0, 3.0 및 3.5를 side-by-side 실행할 수는 없습니다. 버전 3.5를 설치하면 2.0 및 3.0 레이어가 자동으로 설치되며 버전 2.0, 3.0 및 3.5용으로 빌드된 앱 모두를 3.5 버전에서 실행할 수 있습니다. 그러나 .NET Framework 4에서는 이 계층적 접근 방법을 종료하고 이후 릴리스(.NET Framework 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2 및 4.8)에서도 단일 설치의 후속 레이어를 나타냅니다.  .NET Framework 4부터는 프로세스 내 병렬 호스팅을 사용하여 단일 프로세스에서 여러 버전의 CLR을 실행할 수 있습니다. 자세한 내용은 [어셈블리 및 Side-by-Side 실행](../../standard/assembly/side-by-side-execution.md)을 참조하십시오.  
  
 또한 앱이 버전 2.0, 3.0 또는 3.5를 대상으로 하는 경우 사용자가 앱을 실행하기 전에 Windows 8, Windows 8.1 또는 Windows 10 컴퓨터에서 .NET Framework 3.5를 사용하도록 설정해야 합니다. 자세한 내용은 [Windows 10, Windows 8.1 및 Windows 8에 .NET Framework 3.5 설치](../install/dotnet-35-windows-10.md)를 참조하세요.  
  
## <a name="next-steps"></a>다음 단계  
  
- .NET Framework를 처음 사용하는 경우 [개요](../get-started/overview.md)에서 주요 개념 및 기능에 대한 소개를 참조하십시오.  
  
- .NET Framework 4.5 및 해당 포인트 릴리스의 새로운 기능과 개선 사항을 확인하려면 [ .NET Framework의 새로운 기능](../whats-new/index.md)을 참조하세요.  
  
- 앱을 .NET Framework 4에서 .NET Framework 4.5 및 해당 포인트 릴리스로 마이그레이션하는 방법에 대한 자세한 내용은 [마이그레이션 가이드](index.md)를 참조하세요.  
  
- 컴퓨터에 설치된 버전이나 업데이트를 확인하는 방법에 대한 자세한 내용은 [방법: 설치된 .NET Framework 버전 확인](how-to-determine-which-versions-are-installed.md) 및 [방법: 설치된 .NET Framework 업데이트 확인](how-to-determine-which-net-framework-updates-are-installed.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [버전 호환성](version-compatibility.md)
- [Microsoft .NET Framework 지원 수명 주기 정책](https://go.microsoft.com/fwlink/?LinkId=196607)
- [차단된 .NET Framework 설치 및 제거 문제 해결](../install/troubleshoot-blocked-installations-and-uninstallations.md)
