---
title: Version Tolerant Serialization 기술 샘플
ms.date: 03/30/2017
ms.assetid: 2a183664-bfbf-4ff0-96f6-c836284ea916
ms.openlocfilehash: 317a47d46b839417e01eed9deca2459a96aaa201
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960775"
---
# <a name="version-tolerant-serialization-technology-sample"></a>Version Tolerant Serialization 기술 샘플
[샘플 다운로드](https://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Runtime%20Serialization/VTS.zip.exe)  
  
 이 샘플에서는 .NET Serialization의 버전 내결함성 기능을 보여 줍니다. 이 샘플에서는 서로 다른 버전의 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>를 사용하여 데이터를 serialize하거나 deserialize하는 두 개의 응용 프로그램을 만듭니다. 서로 다른 형식 버전이 사용되지만 응용 프로그램은 서로 원활하게 통신합니다. 자세한 내용은 [버전 독립적 Serialization](../../../docs/standard/serialization/version-tolerant-serialization.md)을 참조하세요.  
  
### <a name="to-build-the-sample-using-the-command-prompt"></a>명령 프롬프트를 사용하여 샘플을 빌드하려면  
  
1. 명령 프롬프트 창을 열고 V1 응용 프로그램 또는 V2 응용 프로그램 아래에 있는 샘플에 대한 언어별 하위 디렉터리 중 하나로 이동합니다.  
  
2. 명령줄에 **msbuild.exe \<ver> application.sln**을 입력합니다. 여기서 \<ver>은 v1 또는 v2입니다.  
  
### <a name="to-build-the-sample-using-visual-studio"></a>Visual Studio를 사용하여 샘플을 빌드하려면  
  
1. 파일 탐색기를 열고 샘플에 대 한 언어별 하위 디렉터리 중 하나로 이동 합니다.  
  
2. 이전 단계에서 선택한 디렉터리의 V1 Application 하위 디렉터리로 이동합니다.  
  
3. V1 Application.sln의 아이콘을 두 번 클릭하여 Visual Studio에서 파일을 엽니다.  
  
4. **빌드** 메뉴에서 **솔루션 빌드**를 클릭합니다.  
  
5. V2 Application 하위 디렉터리로 이동하고 이전의 두 단계를 반복하여 V2 Application을 빌드합니다.  
  
 응용 프로그램은 각각의 프로젝트 디렉터리에 있는 기본 \bin 또는 \bin\Debug 하위 디렉터리에 빌드됩니다.  
  
### <a name="to-run-the-sample"></a>이 샘플을 실행하려면  
  
1. 명령 프롬프트 창에서 샘플 응용 프로그램을 빌드할 때 선택한 언어별 하위 디렉터리로 이동합니다.  
  
2. 명령줄에 **runme.cmd**를 입력하여 두 애플리케이션을 한 번에 실행합니다.  
  
 새 실행 파일이 있는 디렉터리로 이동한 다음 하나씩 순서대로 실행할 수도 있습니다.  
  
> [!NOTE]
> 이 샘플에서는 콘솔 응용 프로그램을 빌드합니다. 출력을 보려면 응용 프로그램을 명령 프롬프트 창에서 시작하고 실행해야 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>
- <xref:System.IO.FileStream>
