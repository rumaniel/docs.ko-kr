---
title: 애플리케이션 구성
ms.date: 03/30/2017
ms.assetid: a2f995b0-669d-4721-b00f-4561ec7eb6a4
ms.openlocfilehash: 4e19e4d0ecb6bc90402f99dddd280ee1dbcf7ea0
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798154"
---
# <a name="configuring-your-application"></a>애플리케이션 구성
WCF (Windows Communication Foundation)는 .NET 구성 시스템을 사용 하 여 컴퓨터 및 응용 프로그램 범위에서 서비스를 구성할 수 있도록 합니다.  
  
 WCF에서 정의한 구성 설정은 `<system.serviceModel>` 섹션 그룹에 있습니다. WCF 서비스를 구성 하는 방법에 대 한 자세한 내용은 다음 항목을 참조 하십시오.  
  
- [서비스 구성](../configuring-services.md)  
  
- [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md)  
  
 애플리케이션에서 정의한 구성 설정은 `<appSettings>` 섹션 그룹에 정의되어 있습니다. .Net 구성 파일의 응용 프로그램 설정에 대 한 자세한 내용은 [ \<appSettings >](https://go.microsoft.com/fwlink/?LinkId=95159)를 참조 하세요.  
  
## <a name="using-the-configuration-editor"></a>Configuration Editor 사용  
 WCF [구성 편집기 도구 (SvcConfigEditor)](../configuration-editor-tool-svcconfigeditor-exe.md) 를 사용 하면 관리자와 개발자가 그래픽 사용자 인터페이스를 사용 하 여 wcf 서비스의 구성 설정을 만들고 수정할 수 있습니다. 이 도구를 사용 하면 XML 구성 파일을 직접 편집 하지 않고도 WCF 바인딩, 동작, 서비스 및 진단에 대 한 설정을 관리할 수 있습니다.  
  
## <a name="editing-configuration-files-in-visual-studio"></a>Visual Studio에서 구성 파일 편집  
 Visual Studio에서 WCF 서비스 프로젝트의 구성 파일을 편집 하려면 **솔루션 탐색기** 에서 해당 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **wcf 구성 편집** 상황에 맞는 메뉴 항목을 선택 합니다. [구성 편집기 도구 (SvcConfigEditor)](../configuration-editor-tool-svcconfigeditor-exe.md)가 시작 됩니다.  
  
> [!NOTE]
> **솔루션 탐색기**에서 Visual Studio를 마우스 오른쪽 단추로 클릭 하 여 Wcf 웹 서비스 프로젝트의 구성 파일을 편집 하는 경우 **wcf 구성 편집** 상황에 맞는 메뉴 항목이 누락 되었는지 확인 합니다. 이 문제를 해결 하려면 **도구** 메뉴를 클릭 하 고 **WCF 서비스 구성 편집기**를 선택 합니다. 그런 다음 구성 파일을 마우스 오른쪽 단추로 클릭 하 고 **WCF 구성 편집** 상황에 맞는 메뉴 항목을 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [Configuration Editor 도구(SvcConfigEditor.exe)](../configuration-editor-tool-svcconfigeditor-exe.md)
- [서비스 구성](../configuring-services.md)
- [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md)
