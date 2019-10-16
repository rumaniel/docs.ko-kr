---
title: Graphics 컨테이너 사용
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [Windows Forms], using containers
- graphics containers
- examples [Windows Forms], graphics containers
ms.assetid: 74632f91-cefa-4f51-ab7c-f9ac91942caf
ms.openlocfilehash: cfad7254057a31ea8268784cd4b6849850f3e2aa
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61766157"
---
# <a name="using-graphics-containers"></a>Graphics 컨테이너 사용
A <xref:System.Drawing.Graphics> 개체와 같은 메서드를 제공 합니다 <xref:System.Drawing.Graphics.DrawLine%2A>를 <xref:System.Drawing.Graphics.DrawImage%2A>, 및 <xref:System.Drawing.Graphics.DrawString%2A> 벡터 이미지, 래스터 이미지 및 텍스트를 표시 합니다. <xref:System.Drawing.Graphics> 개체에 나타나는 항목의 방향을 확인 하 고 품질에 영향을 주는 몇 가지 속성에 있습니다. 예를 들어, 다듬기 모드 속성을 여부를 확인 앤티 앨리어싱 선 및 곡선을 적용할 위치 및 회전에 나타나는 항목의 세계 변환 속성에 영향을 줍니다.  
  
 <xref:System.Drawing.Graphics> 개체는 특정 디스플레이 장치에 연결 합니다. 사용 하는 경우는 <xref:System.Drawing.Graphics> 창에서 그릴 개체는 <xref:System.Drawing.Graphics> 개체는 특정 창에 연결 됩니다.  
  
 <xref:System.Drawing.Graphics> 개체 생각할 수 있습니다 컨테이너로 그리기에 영향을 주는 속성 집합을 보유 하 고 있으므로 및 장치 관련 정보에 연결 됩니다. 기존 내에서 보조 컨테이너를 만들 수 있습니다 <xref:System.Drawing.Graphics> 를 호출 하 여 개체를 <xref:System.Drawing.Graphics.BeginContainer%2A> 는 메서드의 <xref:System.Drawing.Graphics> 개체입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [Graphics 개체의 상태 관리](managing-the-state-of-a-graphics-object.md)  
 설명 품질 설정, 클리핑 영역 및 변환 하는 방법을 관리는 <xref:System.Drawing.Graphics> 개체입니다.  
  
 [중첩된 Graphics 컨테이너 사용](using-nested-graphics-containers.md)  
 컨테이너의 상태를 제어를 사용 하는 방법을 보여 줍니다는 <xref:System.Drawing.Graphics> 개체입니다.
