---
title: 모델링 및 매핑
ms.date: 03/30/2017
ms.assetid: ec8a9515-3708-4cde-a688-4d8e6975f150
ms.openlocfilehash: 133539ab1b6d6f2f0ab3f8deed5b22240c2bb07e
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854398"
---
# <a name="modeling-and-mapping"></a>모델링 및 매핑
Entity Framework에서 개념적 모델, 저장소 모델 및 응용 프로그램에 가장 적합 한 방식으로 두 모델 간의 매핑을 정의할 수 있습니다. Visual Studio의 엔터티 데이터 모델 도구를 사용 하 여를 만들 수 있습니다. 데이터베이스나 모델이 변경 될 때 데이터베이스 또는 그래픽 모델의 [edmx 파일](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100)) 을 업데이트 한 다음 해당 파일을 업데이트 합니다.  
  
 Entity Framework 4.1부터는 Code First 개발을 통해 모델을 프로그램 방식으로 만들 수도 있습니다. Code First 개발에는 두 가지 다른 시나리오가 있습니다. 두 경우 모두 개발자는 .NET Framewor 클래스 정의를 코딩하여 모델을 정의한 후 데이터 주석 또는 fluent API를 사용하여 추가 매핑 또는 구성을 선택적으로 지정합니다.  
  
 자세한 내용은 [개념적 모델 만들기 및 매핑](https://go.microsoft.com/fwlink/?LinkId=235016)을 참조 하세요.  
  
 .NET Framework에 포함 된 EDM 생성기를 사용할 수도 있습니다. EdmGen.exe 생성기는 기존 데이터 소스에서 .csdl, .ssdl 및 .msl 파일을 생성합니다. 또한 모델 및 매핑 콘텐츠를 수동으로 만들 수 있습니다. 자세한 내용은 [EDM 생성기 (edmgen.exe)](edm-generator-edmgen-exe.md)를 참조 하세요.
