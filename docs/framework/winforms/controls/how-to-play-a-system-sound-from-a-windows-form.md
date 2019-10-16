---
title: '방법: Windows Form에서 시스템 소리 재생'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sounds [Windows Forms], playing for system events
- playing sounds [Windows Forms], Windows Forms
- system sounds [Windows Forms], playing from Windows Forms
- playing sounds [Windows Forms], system
- SoundPlayer class [Windows Forms], system sounds
- sounds [Windows Forms], playing
- examples [Windows Forms], sounds
ms.assetid: afb206ff-4824-4804-a8d4-185bf5ad8e7c
ms.openlocfilehash: 765021875767a754e62e3ec11e56487e4de91e93
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64602773"
---
# <a name="how-to-play-a-system-sound-from-a-windows-form"></a>방법: Windows Form에서 시스템 소리 재생
다음 코드 예제에서는 런타임에 `Exclamation` 시스템 소리를 재생합니다. 시스템 소리에 대 한 자세한 내용은 참조 하세요. <xref:System.Media.SystemSounds>합니다.  
  
## <a name="example"></a>예제  
  
```vb  
Public Sub PlayExclamation()  
    SystemSounds.Exclamation.Play()  
End Sub  
```  
  
```csharp  
public void playExclamation()  
{  
    SystemSounds.Exclamation.Play();  
}  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- <xref:System.Media?displayProperty=nameWithType> 네임스페이스에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Media.SoundPlayer>
- <xref:System.Media.SystemSounds>
- [방법: Windows Form에서 경고음 재생](how-to-play-a-beep-from-a-windows-form.md)
- [방법: Windows Form에서 소리 재생](how-to-play-a-sound-from-a-windows-form.md)
