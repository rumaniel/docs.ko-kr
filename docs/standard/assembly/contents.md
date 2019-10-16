---
title: 어셈블리 콘텐츠
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET Framework], multifile
- assemblies [.NET Framework], single-file
- assemblies [.NET Core]
- single-file assemblies
- multifile assemblies [.NET Framework]
ms.assetid: 28116714-da77-45f7-826d-fa035d121948
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6d9268b0ec1ea919730a2ebcd209507692284cc6
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972824"
---
# <a name="assembly-contents"></a>어셈블리 콘텐츠
일반적으로 정적 어셈블리는 네 가지 요소로 구성됩니다.

- 어셈블리 메타데이터를 포함하는 [어셈블리 매니페스트](manifest.md)

- 형식 메타데이터  

- 형식을 구현하는 MSIL(Microsoft Intermediate Language) 코드 하나 이상의 소스 코드 파일에서 컴파일러에 의해 생성됩니다.

- 리소스 집합  

어셈블리 매니페스트만 있으면 되지만, 어셈블리에 의미 있는 기능을 부여하려면 형식 또는 리소스가 필요합니다.

다음 그림은 단일 물리적 파일에 그룹화된 이러한 요소를 보여 줍니다.

![MyAssembly.dll이라는 단일 파일 어셈블리를 보여주는 다이어그램.](./media/contents/single-file-assembly.gif)

이 그림에서는 MyAssembly.dll에 포함된 어셈블리 매니페스트에 설명된 대로, 세 개 파일 모두 어셈블리에 속하지만 파일 시스템에서는 이들 파일을 세 개의 별도 파일로 인식합니다. Util.netmodule 파일은 아무런 어셈블리 정보를 포함하지 않기 때문에 모듈로 컴파일되었습니다. 어셈블리가 만들어질 때 MyAssembly.dll과 Util.netmodule 및 Graphic.bmp와의 관계를 나타내도록 어셈블리 매니페스트가 MyAssembly.dll에 추가되었습니다.

소스 코드를 디자인하는 경우 애플리케이션의 기능을 하나 이상의 파일로 분리하는 방법에 대해 명시적으로 결정해야 합니다. 또한 .NET Framework 코드를 디자인하는 경우에도 해당 기능을 하나 이상의 어셈블리로 분리하는 방법에 대해 결정해야 합니다.

## <a name="see-also"></a>참고 항목

- [.NET 어셈블리](index.md)
- [어셈블리 매니페스트](manifest.md)
- [어셈블리 보안 고려 사항](security-considerations.md)
