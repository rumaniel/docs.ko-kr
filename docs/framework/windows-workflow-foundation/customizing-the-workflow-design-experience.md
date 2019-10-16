---
title: 워크플로 디자인 환경 사용자 지정
ms.date: 03/30/2017
helpviewer_keywords:
- extending [WF], Workflow Designer
ms.assetid: 98135077-0f5d-4d16-9337-01094e843537
ms.openlocfilehash: 926edb4478551affa03619f44ee886d5eb591e4d
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65637257"
---
# <a name="customizing-the-workflow-design-experience"></a>워크플로 디자인 환경 사용자 지정

[!INCLUDE[wfd1](../../../includes/wfd1-md.md)]에서는 사용자 지정 활동을 디자인하고 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]를 다시 호스트하기 위한 시나리오가 크게 단순화되었습니다. 따라서 개발과 배포를 더 쉽고 유연하게 수행할 수 있습니다. 핵심 인프라 변경 내용을 새로운 활동 디자이너 프로그래밍 모델이 Windows Presentation Foundation (WPF)으로 빌드되는 경우 따라서 다른 애플리케이션에서 비교적 쉽게 활동 디자이너를 선언적으로 정의하고 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)]를 다시 호스트할 수 있습니다. Workflow Designer를 다시 호스트하면 IntelliSense 또는 간소화된 식 도메인을 지원하는 사용자 지정 식 편집기를 개발할 수 있습니다. 통합 Windows Communication Foundation (WCF)를 사용 하 여 워크플로 서비스를 사용 하 여 더욱 원활 하 게 되었습니다. 사용자 지정 활동 디자이너와 모델 항목 트리를 사용하여 다시 호스트된 Workflow Designer의 디자인 타임 환경을 향상시킬 수 있습니다.

## <a name="in-this-section"></a>섹션 내용

 [사용자 지정 활동 디자이너 및 템플릿 사용](using-custom-activity-designers-and-templates.md)

 새로운 사용자 지정 활동 디자이너와 템플릿을 만드는 방법을 설명합니다.

 [워크플로 디자이너 재호스트](rehosting-the-workflow-designer.md)

 다시 호스트 하는 방법에 설명 합니다 [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] Visual Studio 업데이트 및 유효성 검사 오류를 표시 하는 방법입니다.

 [사용자 지정 식 편집기 사용](using-a-custom-expression-editor.md)

 Visual Studio 2010 외부에서 다시 호스트 된 워크플로 디자이너를 사용 하려면 사용자 지정 식 편집기를 구현 하는 방법에 설명 합니다.

## <a name="reference"></a>참조

<xref:System.Activities.Presentation.ActivityDesigner>

## <a name="see-also"></a>참고자료

- [Windows Workflow Foundation 확장](extend.md)
- [디자이너](./samples/designer.md)
- [사용자 지정 작업 디자이너](./samples/custom-activity-designers.md)
- [디자이너 재호스팅](./samples/designer-rehosting.md)
