---
title: Web Services Generics Serialization 기술 샘플
ms.date: 03/30/2017
ms.assetid: cdc15ea4-f678-4729-8ebe-188ae720bef7
ms.openlocfilehash: 467bfe1fd9eb8a0222385c34cb29a90df00dc937
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960758"
---
# <a name="web-services-generics-serialization-technology-sample"></a>Web Services Generics Serialization 기술 샘플
[샘플 다운로드](https://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Xml%20Serialization/GenericsSerialization.zip.exe)  
  
 이 샘플에서는 ASP.NET 웹 서비스에서 제네릭의 serialization을 사용하고 제어하는 방법을 보여 줍니다.  
  
### <a name="to-build-the-sample-using-visual-studio"></a>Visual Studio를 사용하여 샘플을 빌드하려면  
  
1. Visual Studio를 열고 **파일** 메뉴에서 **새 웹 사이트**를 선택합니다.  
  
2. **새 웹 사이트** 대화 상자의 왼쪽 창에서 원하는 프로그래밍 언어를 선택한 다음 오른쪽 창에서 **ASP.NET 웹 서비스**를 선택합니다.  
  
3. **찾아보기**를 클릭하고 \CS\GenericsService 하위 디렉터리로 이동합니다.  
  
4. Service.asmx를 선택하여 Visual Studio에서 파일을 엽니다.  
  
5. **빌드** 메뉴에서 **솔루션 빌드**를 클릭합니다.  
  
> [!NOTE]
> 이 목록의 처음 5개 단계는 선택 사항입니다. .NET Framework 런타임에서는 웹 서비스가 처음 요청될 때 웹 서비스를 자동으로 생성합니다.  
  
> [!NOTE]
> 다음 단계는 샘플을 빌드하는 데 필요합니다.  
  
1. 파일 탐색기를 열고 \CS 하위 디렉터리로 이동 합니다.  
  
2. GenericsService 하위 디렉터리의 아이콘을 마우스 오른쪽 단추로 클릭하고 **공유 및 보안**을 선택합니다.  
  
3. **웹 공유** 탭에서 **이 폴더를 공유함**을 선택합니다.  
  
> [!IMPORTANT]
> 샘플을 실행하는 데 필요하므로 **별칭** 창에 표시된 가상 디렉터리 이름을 기록해 놓습니다.  
  
### <a name="to-build-the-sample-using-internet-information-services"></a>인터넷 정보 서비스를 사용하여 샘플을 빌드하려면  
  
1. **인터넷 정보 서비스** 관리 스냅인을 열고 **웹 사이트**를 확장합니다.  
  
2. **기본 웹 사이트**를 마우스 왼쪽 단추로 클릭하고 **새로 만들기**, **가상 디렉터리?** 를 차례로 선택하여 **가상 디렉터리 만들기 마법사**를 만듭니다.  
  
3. **다음**을 클릭하고 가상 디렉터리의 공용 별칭을 입력한 후 **다음**을 클릭합니다.  
  
4. 샘플을 저장한 디렉터리의 경로(일반적으로 \CS\GenericsService 하위 디렉터리)를 입력하고 **다음**을 클릭합니다. **다음**을 클릭하여 마법사를 마칩니다.  
  
> [!IMPORTANT]
> 샘플을 실행하는 데 필요하므로 **별칭** 창에 표시된 가상 디렉터리 이름을 기록해 놓습니다.  
  
### <a name="to-run-the-sample"></a>이 샘플을 실행하려면  
  
1. 브라우저 창을 열고 주소 표시줄을 선택합니다.  
  
2. 을 `http://localhost/[virtual directory]/Service.asmx`입력 합니다 `[virtual directory]` . 여기서는 샘플을 빌드할 때 만든 가상 디렉터리를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 이 샘플에서는 웹 서비스의 정의에 대한 링크가 포함된 기본 ASP.NET 페이지를 표시합니다. 웹 서비스의 소스 코드를 수정할 수 있을 뿐 아니라 화면 표시를 사용자 지정할 수도 있습니다. 자세한 내용은 [XML Web Service 클라이언트 빌드](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w3h45ebk(v=vs.100))를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Collections.Generic>
- <xref:System.Web.Services>
- <xref:System.Xml.Serialization>
- [serialization](../../../docs/standard/serialization/index.md)
- [ASP.NET 및 XML Web Service 클라이언트를 사용하여 만든 XML Web Services](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7bkzywba(v=vs.100))
