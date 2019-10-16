---
title: .NET Framework에 COM 구성 요소 노출
ms.date: 03/30/2017
helpviewer_keywords:
- exposing COM components to .NET Framework
- interoperation with unmanaged code, exposing COM components
- COM interop, exposing COM components
ms.assetid: e78b14f1-e487-43cd-9c6d-1a07483f1730
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a5059f629a341bb4689428855807fb3c66b0949b
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70969077"
---
# <a name="exposing-com-components-to-the-net-framework"></a>.NET Framework에 COM 구성 요소 노출
이 섹션에서는 프로세스를 기존 COM 구성 요소를 관리 코드에 노출하는 데 필요한 간략하게 설명합니다. .NET Framework와 강력하게 통합되는 COM 서버를 작성하는 방법에 대한 자세한 내용은 [상호 운용을 위한 디자인 고려 사항](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/61aax4kh(v=vs.100))을 참조하세요.
  
 기존 COM 구성요소는 중간 계층 비즈니스 애플리케이션 또는 격리된 기능으로서 관리 코드의 중요한 리소스입니다. 이상적인 구성 요소는 주 interop 어셈블리를 포함하고 COM을 통해 적용되는 프로그래밍 표준을 엄격하게 준수합니다.  
  
#### <a name="to-expose-com-components-to-the-net-framework"></a>.NET Framework에 COM 구성 요소를 노출하려면  
  
1. [형식 라이브러리를 어셈블리로 가져옵니다](importing-a-type-library-as-an-assembly.md).  
  
     공용 언어 런타임에는 COM 형식을 비롯한 모든 형식에 대한 메타데이터가 필요합니다. 메타데이터로 가져온 COM 형식이 포함된 어셈블리를 가져오는 다양한 방법이 있습니다.  
  
2. [관리 코드에서 COM 형식을 사용합니다](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3y76b69k(v=vs.100)).  
  
     관리되는 형식의 경우와 같은 방식으로 COM 형식을 검사하고, 인스턴스를 활성화하고, COM 개체에서 메서드를 호출할 수 있습니다.  
  
3. [Interop 프로젝트를 컴파일합니다](compiling-an-interop-project.md).  
  
     Windows SDK에서는 Visual Basic, C# 및 C++를 포함하여 CLS(공용 언어 사양)와 호환되는 여러 언어용 컴파일러를 제공합니다.  
  
4. [Interop 애플리케이션을 배포합니다](deploying-an-interop-application.md).  
  
     Interop 애플리케이션은 전역 어셈블리 캐시에 [강력한 이름의](../../standard/assembly/strong-named.md) 서명된 어셈블리로서 가장 잘 배포됩니다.  
  
## <a name="see-also"></a>참고 항목

- [비관리 코드와의 상호 운용](index.md)
- [상호 운용을 위한 디자인 고려 사항](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/61aax4kh(v=vs.100))
- [COM Interop 샘플: .NET 클라이언트 및 COM 서버](com-interop-sample-net-client-and-com-server.md)
- [언어 독립성 및 언어 독립적 구성 요소](../../standard/language-independence-and-language-independent-components.md)
- [Gacutil.exe(전역 어셈블리 캐시 도구)](../tools/gacutil-exe-gac-tool.md)
