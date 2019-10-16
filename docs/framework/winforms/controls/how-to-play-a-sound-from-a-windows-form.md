---
title: '방법: Windows Form에서 소리 재생'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- playing sounds [Windows Forms], Windows Forms
- sounds [Windows Forms], playing
- sounds
- My.Computer.Audio object [Windows Forms], playing sounds
- examples [Windows Forms], sounds
ms.assetid: 3d3350b7-1ebd-4e05-a738-48ca1160a19d
ms.openlocfilehash: 68a68f05b847877641132e540995f6b14bb6e065
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015795"
---
# <a name="how-to-play-a-sound-from-a-windows-form"></a>방법: Windows Form에서 소리 재생
이 예제에서는 런타임에 지정된 경로에서 소리를 재생합니다.

## <a name="example"></a>예제

```vb
Sub PlaySimpleSound()
    My.Computer.Audio.Play("c:\Windows\Media\chimes.wav")
End Sub
```

```csharp
private void playSimpleSound()
{
    SoundPlayer simpleSound = new SoundPlayer(@"c:\Windows\Media\chimes.wav");
    simpleSound.Play();
}
```

## <a name="compiling-the-code"></a>코드 컴파일
 이 예제에는 다음 사항이 필요합니다.

- 파일 이름 `"c:\Windows\Media\chimes.wav"`를 유효한 파일 이름으로 바꿉니다.

- (C#) <xref:System.Media?displayProperty=nameWithType> 네임 스페이스에 대 한 참조입니다.

## <a name="robust-programming"></a>강력한 프로그래밍
 파일 작업은 적절한 구조적 예외 처리 블록 내에 묶어야 합니다.

 다음 조건에서 예외가 발생합니다.

- 경로 이름 형식이 잘못되었습니다. 예를 들어 잘못된 문자를 포함하거나 공백만으로 이루어져 있습니다(<xref:System.ArgumentException> 클래스).

- 경로가 읽기 전용입니다(<xref:System.IO.IOException> 클래스).

- 경로 이름이 `null`입니다(<xref:System.ArgumentNullException> 클래스).

- 경로 이름이 너무 깁니다(<xref:System.IO.PathTooLongException> 클래스).

- 경로가 잘못되었습니다(<xref:System.IO.DirectoryNotFoundException> 클래스).

- 경로는 콜론, ":" (<xref:System.NotSupportedException> 클래스)입니다.

## <a name="net-framework-security"></a>.NET Framework 보안
 파일 이름을 바탕으로 파일 내용을 판단하면 안 됩니다. 예를 들어 `Form1.vb` 파일이 Visual Basic 소스 파일이 아닐 수도 있습니다. 애플리케이션에서 데이터를 사용하기 전에 모든 입력을 확인해야 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Media.SoundPlayer>
- [방법: Windows Form에서 비동기적으로 소리 로드](how-to-load-a-sound-asynchronously-within-a-windows-form.md)
