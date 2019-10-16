---
title: 애플리케이션 시작 시간
ms.date: 03/30/2017
helpviewer_keywords:
- splash screen [WPF], startup time
- WPF [WPF], startup time
- startup time [WPF]
- application startup [WPF]
- performance [WPF], startup time
ms.assetid: f0ec58d8-626f-4d8a-9873-c20f95e08b96
ms.openlocfilehash: 8bdd70a6eaea8aff196e2156d88460a6d24b5d3f
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487183"
---
# <a name="application-startup-time"></a>애플리케이션 시작 시간
WPF 애플리케이션을 시작하는 데 필요한 시간은 크게 다를 수 있습니다. 이 항목에서는 WPF(Windows Presentation Foundation) 애플리케이션의 체감 시작 시간과 실제 시작 시간을 줄일 수 있는 다양한 기술에 대해 설명합니다.  
  
## <a name="understanding-cold-startup-and-warm-startup"></a>콜드 시작과 웜 시작 이해  
 콜드 시작은 시스템을 다시 부팅한 후 애플리케이션을 처음 시작하거나 애플리케이션을 시작한 다음 닫았다가 오랜 시간이 지난 후에 다시 시작하는 경우에 발생합니다. 애플리케이션을 시작할 때 코드, 정적 데이터, 레지스트리 등 필요한 페이지가 Windows 메모리 관리자의 대기 목록에 없으면 페이지 오류가 발생합니다. 페이지를 메모리로 가져오려면 디스크에 액세스해야 합니다.  
  
 웜 시작은 주 CLR(공용 언어 런타임) 구성 요소의 페이지 대부분이 메모리에 이미 로드되어 있을 때 발생하며, 이 경우 비용이 많이 드는 디스크 액세스 시간을 줄일 수 있습니다. 이에 따라 관리되는 애플리케이션을 다시 실행할 때 더 빠르게 시작됩니다.  
  
## <a name="implement-a-splash-screen"></a>시작 화면 구현  
 애플리케이션을 시작한 후 첫 번째 UI가 표시될 때까지 어쩔 수 없이 상당히 지연될 경우 *시작 화면*을 사용하여 체감 시작 시간을 최적화합니다. 이 방법을 사용하면 사용자가 애플리케이션을 시작한 직후에 이미지가 표시됩니다. 애플리케이션에서 첫 번째 UI를 표시할 준비가 되면 시작 화면이 사라집니다. .NET Framework 3.5 SP1부터 사용할 수는 <xref:System.Windows.SplashScreen> 시작 화면을 구현 하는 클래스입니다. 자세한 내용은 [WPF 애플리케이션에 시작 화면 추가](../app-development/how-to-add-a-splash-screen-to-a-wpf-application.md)를 참조하세요.  
  
 네이티브 Win32 그래픽을 사용하여 사용자 고유의 시작 화면을 구현할 수도 있습니다. 구현 하기 전에 표시 된 <xref:System.Windows.Application.Run%2A> 메서드가 호출 됩니다.  
  
## <a name="analyze-the-startup-code"></a>시작 코드 분석  
 콜드 시작이 느린 이유를 확인합니다. 디스크 I/O 때문일 수 있지만 항상 그렇지는 않습니다. 일반적으로 네트워크, 웹 서비스 또는 디스크와 같은 외부 리소스의 사용을 최소화해야 합니다.  
  
 테스트하기 전에 실행 중인 다른 애플리케이션이나 서비스에서 관리 코드나 WPF 코드를 사용하고 있는지 확인합니다.  
  
 다시 부팅한 즉시 WPF 애플리케이션을 시작하고 표시하는 데 걸리는 시간을 확인합니다. 애플리케이션의 모든 후속 실행(웜 시작)이 훨씬 빠르면 콜드 시작 문제는 I/O로 인해 발생될 가능성이 큽니다.  
  
 애플리케이션의 콜드 시작 문제가 I/O와 관련이 없는 경우 애플리케이션에서 시간이 오래 소요되는 초기화 또는 계산을 수행하거나, 특정 이벤트가 완료될 때까지 기다리거나, 시작 시 많은 양의 JIT 컴파일이 필요한 것일 수 있습니다. 다음 섹션에서는 이러한 경우 중 일부에 대해 자세히 설명합니다.  
  
## <a name="optimize-module-loading"></a>모듈 로드 최적화  
 Process Explorer(Procexp.exe) 및 Tlist.exe와 같은 도구를 사용하여 애플리케이션에서 로드하는 모듈을 확인합니다. `Tlist <pid>` 명령은 프로세스에서 로드하는 모든 모듈을 표시합니다.  
  
 예를 들어 웹에 연결하지 않았지만 System.Web.dll이 로드되었다면 애플리케이션에 이 어셈블리를 참조하는 모듈이 있는 것입니다. 이 경우 해당 참조가 필요한지 확인합니다.  
  
 애플리케이션에 여러 모듈이 있는 경우 단일 모듈로 병합합니다. 이렇게 하면 CLR 어셈블리 로드 오버헤드를 줄일 수 있습니다. 어셈블리 수가 적을수록 CLR에서 상태를 더 적게 유지 관리하게 됩니다.  
  
## <a name="defer-initialization-operations"></a>초기화 작업 지연  
 주 애플리케이션 창이 렌더링될 때까지 초기화 코드를 연기하는 것이 좋습니다.  
  
 초기화는 클래스 생성자 내에서 수행 될 수 있으며, 초기화 코드에서 다른 클래스들을 참조하면 계단식 효과(cascading effect)로 인해 많은 클래스 생성자가 실행될 수 있음에 주의해야 합니다.  
  
## <a name="avoid-application-configuration"></a>애플리케이션 구성 금지  
 애플리케이션을 구성하지 않는 것이 좋습니다. 예를 들어 애플리케이션에 대한 구성 요구 사항이 간단하고, 시작 시간 목표가 명확한 경우 레지스트리 항목이나 간단한 INI 파일을 사용하여 시작하는 것이 더 빠를 수 있습니다.  
  
## <a name="utilize-the-gac"></a>GAC 사용  
 어셈블리가 GAC(전역 어셈블리 캐시)에 설치되어 있지 않으면 강력한 이름의 어셈블리에 대한 해시 확인 및 컴퓨터에서 해당 어셈블리의 네이티브 이미지를 사용할 수 있는 경우의 Ngen 이미지 유효성 검사로 인해 지연이 발생할 수 있습니다. GAC에 설치된 모든 어셈블리에서는 강력한 이름 확인을 건너뜁니다. 자세한 내용은 [Gacutil.exe(전역 어셈블리 캐시 도구)](../../tools/gacutil-exe-gac-tool.md)를 참조하세요.  
  
## <a name="use-ngenexe"></a>Ngen.exe 사용  
 애플리케이션에서 네이티브 이미지 생성기(Ngen.exe)를 사용하는 것이 좋습니다. Ngen.exe에서 생성하는 네이티브 이미지가 일반적으로 MSIL 이미지보다 클 수 있기 때문에 Ngen.exe를 사용하면 CPU 사용량이 줄어드는 대신 디스크 액세스가 많아질 수 있습니다.  
  
 웜 시작 시간을 줄이려면 Ngen.exe에서 애플리케이션 코드의 JIT 컴파일로 인한 CPU 비용 발생을 방지하므로 애플리케이션에서 항상 Ngen.exe를 사용해야 합니다.  
  
 일부 콜드 시작 시나리오에서도 Ngen.exe를 사용하면 도움이 될 수 있습니다. 이는 JIT 컴파일러(mscorjit.dll)를 로드할 필요가 없기 때문입니다.  
  
 Ngen과 JIT 모듈을 모두 사용하면 최악의 효과가 발생할 수 있습니다. 이는 mscorjit.dll을 로드해야 하고, JIT 컴파일러가 코드에서 작동하여 어셈블리의 메타데이터를 읽을 때 Ngen 이미지의 많은 페이지에 액세스해야 하기 때문입니다.  
  
### <a name="ngen-and-clickonce"></a>Ngen 및 ClickOnce  
 애플리케이션 배포 계획에 따라서도 로드 시간이 달라질 수 있습니다. ClickOnce 응용 프로그램 배포는 Ngen을 지원 하지 않습니다. 애플리케이션에 Ngen.exe를 사용하려면 Windows Installer와 같은 다른 배포 메커니즘을 사용해야 합니다.  
  
 자세한 내용은 [Ngen.exe(네이티브 이미지 생성기)](../../tools/ngen-exe-native-image-generator.md)를 참조하세요.  
  
### <a name="rebasing-and-dll-address-collisions"></a>기준 주소 다시 지정 및 DLL 주소 충돌  
 Ngen.exe를 사용하는 경우 네이티브 이미지가 메모리에 로드될 때 기준 주소 다시 지정이 발생할 수 있습니다. 해당 주소 범위가 이미 할당되어 있어 기본 설정된 기준 주소에 DLL을 로드할 수 없으면, Windows 로더에서 다른 주소에 DLL을 로드하지만 이 작업에는 시간이 오래 걸릴 수 있습니다.  
  
 가상 주소 덤프 도구(Vadump.exe)를 사용하여 모든 페이지가 전용(private)으로 된 모듈이 있는지 확인할 수 있습니다. 이러한 모듈이 있는 경우 해당 모듈은 다른 주소로 다시 지정되며, 이로 인해 해당 페이지를 공유할 수 없습니다.  
  
 기준 주소 설정 방법에 대한 자세한 내용은 [Ngen.exe(네이티브 이미지 생성기)](../../tools/ngen-exe-native-image-generator.md)를 참조하세요.  
  
## <a name="optimize-authenticode"></a>Authenticode 최적화  
 Authenticode 확인으로 인해 시작 시간이 길어질 수 있습니다. Authenticode로 서명된 어셈블리는 CA(인증 기관)에서 확인해야 합니다. 이 확인 작업을 수행하는 경우 현재 인증서 해지 목록을 다운로드하기 위해 네트워크에 여러 번 연결해야 하므로 시간이 오래 걸릴 수 있습니다. 또한 신뢰할 수 있는 루트에 대한 경로에 유효한 인증서의 전체 체인이 있는지도 확인합니다. 이로 인해 어셈블리가 로드되는 동안 몇 초 정도 지연될 수 있습니다.  
  
 클라이언트 컴퓨터에 CA 인증서를 설치하거나, 가능한 경우 Authenticode를 사용하지 않는 것이 좋습니다. 애플리케이션에 게시자 증명 정보가 필요하지 않은 경우 서명 확인에 비용을 들일 필요가 없습니다.  
  
 Authenticode 확인을 무시할 수 있도록 구성 옵션은.NET Framework 3.5부터. 이렇게 하려면 app.exe.config 파일에 다음 설정을 추가합니다.  
  
```xml  
<configuration>  
    <runtime>  
        <generatePublisherEvidence enabled="false"/>   
    </runtime>  
</configuration>  
```  
  
 자세한 내용은 [\<generatePublisherEvidence> 요소](../../configure-apps/file-schema/runtime/generatepublisherevidence-element.md)를 참조하세요.  
  
## <a name="compare-performance-on-windows-vista"></a>Windows Vista에서 성능 비교  
 Windows Vista의 메모리 관리자에는 SuperFetch라는 기술이 있습니다. SuperFetch는 시간의 경과에 따른 메모리 사용 패턴을 분석하여 특정 사용자에 맞는 최적의 메모리 콘텐츠를 결정하며, 해당 콘텐츠를 항상 유지하기 위해 지속적으로 작동합니다.  
  
 이 방법은 Windows XP에서 사용 패턴을 분석하지 않고 메모리에 데이터를 미리 로드하는 Windows XP에서 사용되는 프리페치 기술과 다릅니다. 시간이 지남에 따라 사용자가 Windows Vista에서 WPF 애플리케이션을 자주 사용하면 애플리케이션의 콜드 시작 시간이 줄어들 수 있습니다.  
  
## <a name="use-appdomains-efficiently"></a>효율적인 AppDomain 사용  
 가능한 경우 어셈블리를 도메인 중립 코드 영역에 로드하여 네이티브 이미지(있는 경우)가 애플리케이션에서 만든 모든 AppDomain에서 사용되는지 확인합니다.  
  
 최상의 성능을 위해 도메인 간 호출을 줄여 도메인 간 통신의 효율성을 높입니다. 가능한 경우 인수를 사용하지 않거나 기본 형식 인수를 사용하여 호출합니다.  
  
## <a name="use-the-neutralresourceslanguage-attribute"></a>NeutralResourcesLanguage 특성 사용  
 사용 합니다 <xref:System.Resources.NeutralResourcesLanguageAttribute> 에 대 한 중립 문화권을 지정 하는 <xref:System.Resources.ResourceManager>합니다. 이렇게 하면 실패한 어셈블리 조회를 방지합니다.  
  
## <a name="use-the-binaryformatter-class-for-serialization"></a>serialization에 BinaryFormatter 클래스 사용  
 Serialization을 사용 해야 하는 경우 사용 합니다 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 클래스 대신는 <xref:System.Xml.Serialization.XmlSerializer> 클래스입니다. <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 클래스에서 클래스 라이브러리 BCL (기본) mscorlib.dll 어셈블리에서 구현 됩니다. <xref:System.Xml.Serialization.XmlSerializer> 로드할 추가 DLL 일 수 있는 System.Xml.dll 어셈블리에서 구현 됩니다.  
  
 사용 해야 하는 경우는 <xref:System.Xml.Serialization.XmlSerializer> 클래스 serialization 어셈블리를 미리 생성 하는 경우 성능의 높일 수 있습니다.  
  
## <a name="configure-clickonce-to-check-for-updates-after-startup"></a>시작 후 업데이트를 확인하도록 ClickOnce 구성  
 응용 프로그램이 ClickOnce를 사용 하는 경우 응용 프로그램이 시작 된 후 배포 사이트에서 업데이트를 확인 하도록 ClickOnce 구성 하 여 시작에 대 한 네트워크 액세스를 방지 합니다.  
  
 XAML 브라우저 응용 프로그램 (XBAP) 모델을 사용 하면 XBAP는 ClickOnce 캐시에 이미 있는 경우에 ClickOnce 배포 사이트에서 업데이트를 검사 하도록 염두에서에 둡니다. 자세한 내용은 [ClickOnce Security and Deployment](/visualstudio/deployment/clickonce-security-and-deployment)을 참조하세요.  
  
## <a name="configure-the-presentationfontcache-service-to-start-automatically"></a>자동으로 시작되도록 PresentationFontCache 서비스 구성  
 다시 부팅한 후에 실행할 첫 번째 WPF 애플리케이션은 PresentationFontCache 서비스입니다. 이 서비스는 시스템 글꼴을 캐시하고, 글꼴 액세스를 향상시키며 전반적인 성능을 높입니다. 이 서비스를 시작하는 데 있어 오버헤드가 발생하며, 제어된 일부 환경에서는 시스템을 다시 부팅할 때 이 서비스가 자동으로 시작되도록 구성하는 것이 좋습니다.  
  
## <a name="set-data-binding-programmatically"></a>프로그래밍 방식으로 데이터 바인딩 설정  
 XAML을 사용 하 여 설정 하는 대신 합니다 <xref:System.Windows.FrameworkElement.DataContext%2A> 선언적으로 주 창에 대 한 프로그래밍 방식으로 설정 고려해 야는 <xref:System.Windows.Application.OnActivated%2A> 메서드.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.SplashScreen>
- <xref:System.AppDomain>
- <xref:System.Resources.NeutralResourcesLanguageAttribute>
- <xref:System.Resources.ResourceManager>
- [WPF 응용 프로그램에 시작 화면 추가](../app-development/how-to-add-a-splash-screen-to-a-wpf-application.md)
- [Ngen.exe(네이티브 이미지 생성기)](../../tools/ngen-exe-native-image-generator.md)
- [\<generatePublisherEvidence> 요소](../../configure-apps/file-schema/runtime/generatepublisherevidence-element.md)
