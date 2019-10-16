---
title: '방법: 클립보드에 데이터 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Clipboard [Windows Forms], copying data to
- data [Windows Forms], copying to Clipboard
ms.assetid: 25152454-0e78-40a9-8a9e-a2a5a274e517
ms.openlocfilehash: 0d9b82f01080d18353ecb91578a8005260bbe739
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044216"
---
# <a name="how-to-add-data-to-the-clipboard"></a>방법: 클립보드에 데이터 추가

클래스 <xref:System.Windows.Forms.Clipboard> 는 Windows 운영 체제 클립보드 기능과 상호 작용 하는 데 사용할 수 있는 메서드를 제공 합니다. 대부분의 응용 프로그램은 데이터에 대 한 임시 리포지토리로 클립보드를 사용 합니다. 예를 들어 워드 프로세서는 잘라내기 및 붙여넣기 작업 중에 클립보드를 사용 합니다. 또한 클립보드는 한 응용 프로그램에서 다른 응용 프로그램으로 데이터를 전송 하는 데 유용 합니다.

클립보드에 데이터를 추가 하는 경우 해당 형식을 사용할 수 있는 경우 다른 응용 프로그램이 데이터를 인식할 수 있도록 데이터 형식을 지정할 수 있습니다. 여러 다른 형식으로 클립보드에 데이터를 추가 하 여 잠재적으로 데이터를 사용할 수 있는 다른 응용 프로그램의 수를 늘릴 수도 있습니다.

클립보드 형식은 해당 형식을 사용 하는 응용 프로그램에서 연결 된 데이터를 검색할 수 있도록 형식을 식별 하는 문자열입니다. 클래스 <xref:System.Windows.Forms.DataFormats> 는 사용 하기 위해 미리 정의 된 형식 이름을 제공 합니다. 사용자 고유의 형식 이름을 사용 하거나 개체 형식을 형식으로 사용할 수도 있습니다.

하나 또는 여러 형식으로 클립보드에 데이터를 추가 하려면 <xref:System.Windows.Forms.Clipboard.SetDataObject%2A> 메서드를 사용 합니다. 이 메서드에 개체를 전달할 수 있지만 여러 형식으로 데이터를 추가 하려면 먼저 여러 형식으로 작업 하도록 설계 된 별도의 개체에 데이터를 추가 해야 합니다. 일반적으로에 데이터 <xref:System.Windows.Forms.DataObject>를 추가 하지만 인터페이스를 <xref:System.Windows.Forms.IDataObject> 구현 하는 모든 형식을 사용할 수 있습니다.

.NET Framework 2.0에서는 기본 클립보드 작업을 보다 쉽게 수행할 수 있도록 설계 된 새로운 메서드를 사용 하 여 클립보드에 데이터를 직접 추가할 수 있습니다. 텍스트와 같은 단일 공통 형식의 데이터로 작업 하는 경우 이러한 메서드를 사용 합니다.

> [!NOTE]
> 모든 Windows 기반 응용 프로그램은 클립보드를 공유 합니다. 따라서 다른 응용 프로그램으로 전환할 때 내용이 변경 될 수 있습니다.
>
> <xref:System.Windows.Forms.Clipboard> 단일 스레드 아파트 (STA) 모드를 설정 하는 스레드의 클래스 에서만 사용할 수 있습니다. 이 클래스를 사용 하려면 프로그램 `Main` 표시 된 메서드가 <xref:System.STAThreadAttribute> 특성입니다.
>
> 개체를 클립보드에 배치할 수 있도록 serializable 이어야 합니다. 형식을 serialize 할 수 있도록 하려면 <xref:System.SerializableAttribute> 특성으로 표시 합니다. 클립보드 메서드에 순차 불가능 한 개체를 전달 하는 경우 메서드가 예외를 throw 하지 않고 실패 합니다. serialization에 대한 자세한 내용은 <xref:System.Runtime.Serialization>을 참조하세요.

### <a name="to-add-data-to-the-clipboard-in-a-single-common-format"></a>단일 공통 형식으로 클립보드에 데이터를 추가 하려면

1. ,, 또는 메서드<xref:System.Windows.Forms.Clipboard.SetText%2A> 를 사용 합니다. <xref:System.Windows.Forms.Clipboard.SetFileDropList%2A> <xref:System.Windows.Forms.Clipboard.SetAudio%2A> <xref:System.Windows.Forms.Clipboard.SetImage%2A> 이러한 메서드는 .NET Framework 2.0 에서만 사용할 수 있습니다.

    [!code-csharp[System.Windows.Forms.Clipboard#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#2)]
    [!code-vb[System.Windows.Forms.Clipboard#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#2)]

### <a name="to-add-data-to-the-clipboard-in-a-custom-format"></a>클립보드에 데이터를 사용자 지정 형식으로 추가 하려면

1. 사용자 지정 <xref:System.Windows.Forms.Clipboard.SetData%2A> 형식 이름을 사용 하 여 메서드를 사용 합니다. 이 메서드는 .NET Framework 2.0 에서만 사용할 수 있습니다.

    미리 정의 된 형식 이름을 <xref:System.Windows.Forms.Clipboard.SetData%2A> 메서드와 함께 사용할 수도 있습니다. 자세한 내용은 <xref:System.Windows.Forms.DataFormats>을 참조하세요.

    [!code-csharp[System.Windows.Forms.Clipboard#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#3)]
    [!code-vb[System.Windows.Forms.Clipboard#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#3)]
    [!code-csharp[System.Windows.Forms.Clipboard#100](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]

### <a name="to-add-data-to-the-clipboard-in-multiple-formats"></a>여러 형식으로 클립보드에 데이터를 추가 하려면

1. 메서드를 <xref:System.Windows.Forms.Clipboard.SetDataObject%2A?displayProperty=nameWithType> 사용 하 고 데이터를 <xref:System.Windows.Forms.DataObject> 포함 하는를 전달 합니다. .NET Framework 2.0 이전 버전에서 클립보드에 데이터를 추가 하려면이 메서드를 사용 해야 합니다.

    [!code-csharp[System.Windows.Forms.Clipboard#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#4)]
    [!code-vb[System.Windows.Forms.Clipboard#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#4)]
    [!code-csharp[System.Windows.Forms.Clipboard#100](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]

## <a name="see-also"></a>참고자료

- [끌어서 놓기 작업 및 클립보드 지원](drag-and-drop-operations-and-clipboard-support.md)
- [방법: 클립보드에서 데이터를 검색 합니다.](how-to-retrieve-data-from-the-clipboard.md)
