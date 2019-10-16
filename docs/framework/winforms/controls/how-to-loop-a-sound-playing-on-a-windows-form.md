---
title: '방법: Windows Form에서 재생되는 소리 반복'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sound loops
- SoundPlayer class [Windows Forms], play looping
- sounds [Windows Forms], looping
- playing sounds [Windows Forms], looping
ms.assetid: ea95dd46-10a3-46c0-8263-4b205f00df7f
ms.openlocfilehash: e14d9de2326234b86c1f24b227e86f822fbfdb71
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592365"
---
# <a name="how-to-loop-a-sound-playing-on-a-windows-form"></a>방법: Windows Form에서 재생되는 소리 반복
다음 코드 예제에서는 반복해서 소리를 재생합니다. `stopPlayingButton_Click` 이벤트 처리기의 코드가 실행되면 현재 재생되는 모든 소리가 중지됩니다. 소리가 재생되지 않으면 아무것도 발생하지 않습니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Media.SoundPlayer.PlayLooping#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Media.SoundPlayer.PlayLooping/CS/Form1.cs#1)]
 [!code-vb[System.Media.SoundPlayer.PlayLooping#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Media.SoundPlayer.PlayLooping/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System 및 System.Windows.Forms 어셈블리에 대한 참조  
  
- 파일 이름 `"c:\Windows\Media\chimes.wav"`를 유효한 파일 이름으로 바꿉니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 파일 작업을 적절한 예외 처리 블록 내에 묶어야 합니다.  
  
 다음 조건에서 예외가 발생합니다.  
  
- 경로 이름 형식이 잘못되었습니다. 예를 들어 잘못된 문자를 포함하거나 공백만 포함합니다(<xref:System.ArgumentException> 클래스).  
  
- 경로가 읽기 전용입니다(<xref:System.IO.IOException> 클래스).  
  
- 경로 이름이 `Nothing`입니다(<xref:System.ArgumentNullException> 클래스).  
  
- 경로 이름이 너무 깁니다(<xref:System.IO.PathTooLongException> 클래스).  
  
- 경로가 잘못되었습니다(<xref:System.IO.DirectoryNotFoundException> 클래스).  
  
- 경로가 콜론 “:”뿐입니다(<xref:System.NotSupportedException> 클래스).  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 파일 이름을 바탕으로 파일 내용을 판단하면 안 됩니다. 예를 들어 Form1.vb 파일이 Visual Basic 소스 파일이 아닐 수도 있습니다. 애플리케이션에서 데이터를 사용하기 전에 모든 입력을 확인해야 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Media.SoundPlayer.PlayLooping%2A>
- [방법: Windows Form에서 소리 재생](how-to-play-a-sound-from-a-windows-form.md)
- [SoundPlayer 클래스 개요](soundplayer-class-overview.md)
