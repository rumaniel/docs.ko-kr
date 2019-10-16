---
title: Windows Forms 컨트롤의 다중 스레딩
ms.date: 03/30/2017
helpviewer_keywords:
- BackgroundWorker component
- threading [Windows Forms], controls
ms.assetid: c311d652-0f26-45fa-bdcc-b1615d73ce4e
ms.openlocfilehash: cf6790172b7445ad154eead5d17f8efddd78ffee
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69952675"
---
# <a name="multithreading-in-windows-forms-controls"></a>Windows Forms 컨트롤의 다중 스레딩
많은 응용 프로그램에서 다른 스레드에서 시간이 많이 걸리는 작업을 수행 하 여 UI (사용자 인터페이스)의 응답성을 향상 시킬 수 있습니다. <xref:System.Threading> 네임 스페이스 `BackgroundWorker` , 메서드 및 구성 요소를 포함 하 여 Windows Forms 컨트롤에 여러 가지 도구를 사용할 수 있습니다. <xref:System.Windows.Forms.Control.BeginInvoke%2A?displayProperty=nameWithType>  
  
> [!NOTE]
> 구성 `BackgroundWorker` 요소는 기능을 대체 하 고 <xref:System.Threading> 네임 스페이스 및 <xref:System.Windows.Forms.Control.BeginInvoke%2A?displayProperty=nameWithType> 메서드에 기능을 추가 합니다. 그러나 선택 하는 경우 이전 버전과의 호환성 및 향후 사용을 위해 유지 됩니다. 자세한 내용은 [BackgroundWorker 구성 요소 개요](backgroundworker-component-overview.md)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [방법: Windows Forms 컨트롤을 스레드로부터 안전 하 게 호출 합니다.](how-to-make-thread-safe-calls-to-windows-forms-controls.md)  
 Windows Forms 컨트롤을 스레드로부터 안전 하 게 호출 하는 방법을 보여 줍니다.  
  
 [방법: 백그라운드 스레드를 사용 하 여 파일 검색](how-to-use-a-background-thread-to-search-for-files.md)  
 <xref:System.Threading> 네임 스페이스<xref:System.Windows.Forms.Control.BeginInvoke%2A> 및 메서드를 사용 하 여 파일을 비동기적으로 검색 하는 방법을 보여 줍니다.  
  
## <a name="reference"></a>참조  
 <xref:System.ComponentModel.BackgroundWorker>  
 비동기 작업에 대 한 작업자 스레드를 캡슐화 하는 구성 요소를 문서화 합니다.  
  
 <xref:System.Media.SoundPlayer.LoadAsync%2A>  
 소리를 비동기적으로 로드 하는 방법을 설명 합니다.  
  
 <xref:System.Windows.Forms.PictureBox.LoadAsync%2A>  
 이미지를 비동기적으로 로드 하는 방법을 설명 합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [방법: 백그라운드에서 작업 실행](how-to-run-an-operation-in-the-background.md)  
 <xref:System.ComponentModel.BackgroundWorker> 구성 요소를 사용 하 여 시간이 오래 걸리는 작업을 수행 하는 방법을 보여 줍니다.  
  
 [BackgroundWorker 구성 요소 개요](backgroundworker-component-overview.md)  
 비동기 작업에 <xref:System.ComponentModel.BackgroundWorker> 구성 요소를 사용 하는 방법을 설명 하는 항목을 제공 합니다.
