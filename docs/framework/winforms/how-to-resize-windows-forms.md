---
title: '방법: Windows Forms 크기 조정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- resizing Windows Forms
- Windows Forms, resizing
ms.assetid: 5d9dd47e-e68c-48c9-a0a3-a9ff34ba009d
ms.openlocfilehash: aa7ee2bbbf6983a371ea71edc0dfd0cc12cd0c9d
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211662"
---
# <a name="how-to-resize-windows-forms"></a>방법: Windows Forms 크기 조정

여러가지 방법으로 Windows Form의 크기를 지정할 수 있습니다. <xref:System.Windows.Forms.Form.Size%2A> 속성에 대해 새 값을 설정하거나 <xref:System.Windows.Forms.Control.Height%2A> 또는 <xref:System.Windows.Forms.Control.Width%2A> 속성을 개별적으로 조정하여 프로그래밍 방식으로 폼의 높이와 너비를 모두 변경할 수 있습니다. Visual Studio를 사용 하는 경우에 Windows Forms 디자이너를 사용 하 여 크기를 변경할 수 있습니다. 또한 참조 [방법: 디자이너를 사용 하 여 Windows Forms 크기 조정](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/37k2zkwx(v=vs.100))합니다.

## <a name="resize-a-form-programmatically"></a>프로그래밍 방식으로 폼의 크기를 조정합니다

폼의 <xref:System.Windows.Forms.Form.Size%2A> 속성을 설정하여 런타임에 폼의 크기를 정의합니다.

다음 코드 예제에서는 100 × 100 픽셀로 설정된 폼 크기를 보여 줍니다.

```vb
Form1.Size = New System.Drawing.Size(100, 100)
```

```csharp
Form1.Size = new System.Drawing.Size(100, 100);
```

```cpp
Form1->Size = System::Drawing::Size(100, 100);
```

## <a name="change-form-width-and-height-programmatically"></a>프로그래밍 방식으로 폼 너비와 높이 변경

<xref:System.Windows.Forms.Form.Size%2A>가 정의된 후 <xref:System.Windows.Forms.Control.Width%2A> 또는 <xref:System.Windows.Forms.Control.Height%2A> 속성을 사용하여 폼 높이나 너비를 변경합니다.

다음 코드 예제에서는 높이가 일정하게 유지되고 폼의 왼쪽 가장자리에서 300픽셀로 설정된 폼의 너비를 보여 줍니다.

```vb
Form1.Width = 300
```

```csharp
Form1.Width = 300;
```

```cpp
Form1->Width = 300;
```

또는

<xref:System.Windows.Forms.Form.Size%2A> 속성을 설정하여 <xref:System.Drawing.Size.Width%2A> 또는 <xref:System.Drawing.Size.Height%2A>를 변경합니다.

그러나 다음 코드 예제와 같이 이 접근 방식은 단순히 <xref:System.Windows.Forms.Control.Width%2A> 또는 <xref:System.Windows.Forms.Control.Height%2A> 속성을 설정하는 것보다 성가십니다.

```vb
Form1.Size = New Size(300, Form1.Size.Height)
```

```csharp
Form1.Size = new Size(300, Form1.Size.Height);
```

```cpp
Form1->Size = System::Drawing::Size(300, Form1->Size.Height);
```

## <a name="change-form-size-by-increments-programmatically"></a>프로그래밍 방식으로 증가 하 여 폼의 크기 변경

폼의 크기를 증가시키려면 <xref:System.Drawing.Size.Width%2A> 및 <xref:System.Drawing.Size.Height%2A> 속성을 설정합니다.

다음 코드 예제에서는 현재 설정보다 200픽셀 넓게 설정된 폼의 너비를 보여 줍니다.

```vb
Form1.Width += 200
```

```csharp
Form1.Width += 200;
```

```cpp
Form1->Width += 200;
```

> [!CAUTION]
> <xref:System.Windows.Forms.Form.Size%2A> 속성을 새로운 <xref:System.Drawing.Size> 구조체로 설정하여 동시에 높이 및 너비 크기를 설정하지 않는 한 항상 <xref:System.Drawing.Size.Height%2A> 또는 <xref:System.Drawing.Size.Width%2A> 속성을 사용하여 폼의 크기를 변경합니다. <xref:System.Windows.Forms.Form.Size%2A> 속성은 값 형식인 <xref:System.Drawing.Size> 구조체를 반환합니다. 값 형식의 속성에 새 값을 할당할 수 없습니다. 따라서 다음 코드 예제는 컴파일되지 않습니다.

```vb
' NOTE: CODE WILL NOT COMPILE
Dim f As New Form()
f.Size.Width += 100
```

```csharp
// NOTE: CODE WILL NOT COMPILE
Form f = new Form();
f.Size.Width += 100;
```

```cpp
// NOTE: CODE WILL NOT COMPILE
Form^ f = gcnew Form();
f->Size->X += 100;
```

## <a name="see-also"></a>참고자료

- [Windows Forms 시작](getting-started-with-windows-forms.md)
- [Windows Forms 응용 프로그램 강화](./advanced/index.md)
