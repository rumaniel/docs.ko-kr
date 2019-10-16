---
title: '방법: Windows Form에서 경고음 재생'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sounds [Windows Forms], beep
- Windows Forms, sounds
- sounds [Windows Forms], playing
- forms [Windows Forms], sounds
- examples [Windows Forms], sounds
ms.assetid: 7ea5cded-4888-4f35-8f28-5cab1a55c973
ms.openlocfilehash: 7fecc5d5b7259b743926713f87d9303596803582
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015819"
---
# <a name="how-to-play-a-beep-from-a-windows-form"></a>방법: Windows Form에서 경고음 재생
이 예제에서는 런타임에 경고음을 재생합니다.

## <a name="example"></a>예제

```vb
Public Sub OnePing()
    Beep()
End Sub
```

```csharp
public void onePing()
{
    SystemSounds.Beep.Play();
}
```

> [!NOTE]
> C# 코드 샘플에서 재생 되는 소리는 <xref:System.Media.SystemSounds.Beep%2A> 시스템 소리 설정에 따라 결정 됩니다. 자세한 내용은 <xref:System.Media.SystemSounds>을 참조하세요.

## <a name="compiling-the-code"></a>코드 컴파일
 의 C#경우이 예제에는 <xref:System.Media?displayProperty=nameWithType> 네임 스페이스에 대 한 참조가 필요 합니다.

## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Interaction.Beep%2A>
- <xref:System.Media.SoundPlayer>
- [방법: Windows Form에서 시스템 소리 재생](how-to-play-a-system-sound-from-a-windows-form.md)
- [방법: Windows Form에서 소리 재생](how-to-play-a-sound-from-a-windows-form.md)
