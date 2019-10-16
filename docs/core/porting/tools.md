---
title: .NET Core로 이식하는 작업을 위한 도구
description: .NET Core로 이식하는 데 사용할 수 있는 도구 중 일부에 대해 알아보기
author: cartermp
ms.author: mairaw
ms.date: 12/07/2018
ms.openlocfilehash: d0b74b5708f31922b72fa0e236c8bbe69ae06217
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65632249"
---
# <a name="tools-to-help-with-porting-to-net-core"></a>.NET Core로 이식하는 작업에 도움이 되는 도구

이 문서에 나와 있는 도구가 이식할 때 유용할 수 있습니다.

* [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md)는 .NET Framework와 .NET Core 사이에 코드를 얼마나 이식 가능한지에 대한 보고서를 생성할 수 있는 도구 체인입니다.  [명령줄 도구](https://github.com/Microsoft/dotnet-apiport/releases)로 사용하는 경우 [Visual Studio 확장](https://visualstudiogallery.msdn.microsoft.com/1177943e-cfb7-4822-a8a6-e56c7905292b)으로 사용하는 경우
* [.NET API 분석기](../../standard/analyzers/api-analyzer.md) - 여러 플랫폼에서 C# API에 대한 잠재적 호환성 위험을 검색하고 사용되지 않는 API 호출을 탐지하는 Roslyn 분석기입니다.

또한 [CsprojToVs2017](https://github.com/hvanbakel/CsprojToVs2017) 도구를 사용하여 작은 솔루션 또는 개별 프로젝트를 .NET Core 프로젝트 파일 형식으로 포팅할 수 있습니다.

> [!WARNING] 
> CsprojToVs2017은 타사 도구입니다. 모든 프로젝트에서 작동한다는 보장은 없으며, 사용하는 동작이 미묘하게 변경될 수도 있습니다. CsprojToVs2017은 자동화할 수 있는 기본 사항을 자동화하는 _시작점_으로 사용해야 합니다. 프로젝트 파일 형식을 마이그레이션하는 보장된 솔루션은 아닙니다.
