---
title: '방법: 클립보드에서 데이터 검색'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- pasting Clipboard data
- Clipboard [Windows Forms], retrieving data
ms.assetid: 99612537-2c8a-449f-aab5-2b3b28d656e7
ms.openlocfilehash: ca24615049abcc145698c033f31e6c98a38253bf
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040563"
---
# <a name="how-to-retrieve-data-from-the-clipboard"></a>방법: 클립보드에서 데이터 검색

클래스 <xref:System.Windows.Forms.Clipboard> 는 Windows 운영 체제 클립보드 기능과 상호 작용 하는 데 사용할 수 있는 메서드를 제공 합니다. 대부분의 응용 프로그램은 데이터에 대 한 임시 리포지토리로 클립보드를 사용 합니다. 예를 들어 워드 프로세서는 잘라내기 및 붙여넣기 작업 중에 클립보드를 사용 합니다. 또한 클립보드는 한 응용 프로그램에서 다른 응용 프로그램으로 정보를 전송 하는 데 유용 합니다.

일부 응용 프로그램은 데이터를 잠재적으로 사용할 수 있는 다른 응용 프로그램의 수를 늘리기 위해 클립보드의 데이터를 여러 형식으로 저장 합니다. 클립보드 형식은 형식을 식별 하는 문자열입니다. 식별 된 형식을 사용 하는 응용 프로그램은 클립보드에서 연결 된 데이터를 검색할 수 있습니다. 클래스 <xref:System.Windows.Forms.DataFormats> 는 사용 하기 위해 미리 정의 된 형식 이름을 제공 합니다. 사용자 고유의 형식 이름을 사용 하거나 개체의 형식을 형식으로 사용할 수도 있습니다. 클립보드에 데이터를 추가 하 [는 방법에 대 한 자세한 내용은 방법: 클립보드](how-to-add-data-to-the-clipboard.md)에 데이터를 추가 합니다.

클립보드에 특정 형식의 데이터가 포함 되어 있는지 여부를 확인 하려면 *format* 메서드 또는 <xref:System.Windows.Forms.Clipboard.GetData%2A> 메서드 `Contains`중 하나를 사용 합니다. 클립보드에서 데이터를 검색 하려면 *Format* 메서드 또는 <xref:System.Windows.Forms.Clipboard.GetData%2A> 메서드 중 하나 `Get`를 사용 합니다. 이러한 메서드는 .NET Framework 2.0의 새로운 방법입니다.

.NET Framework 2.0 이전 버전을 사용 하 여 클립보드의 데이터에 액세스 하려면 <xref:System.Windows.Forms.Clipboard.GetDataObject%2A?displayProperty=nameWithType> 메서드를 사용 하 고 반환 <xref:System.Windows.Forms.IDataObject>된의 메서드를 호출 합니다. 예를 들어 반환 된 개체에서 특정 형식을 사용할 수 있는지 여부를 확인 하려면 <xref:System.Windows.Forms.IDataObject.GetDataPresent%2A> 메서드를 호출 합니다.

> [!NOTE]
> 모든 Windows 기반 응용 프로그램은 시스템 클립보드를 공유 합니다. 따라서 다른 응용 프로그램으로 전환할 때 내용이 변경 될 수 있습니다.
>
> <xref:System.Windows.Forms.Clipboard> 단일 스레드 아파트 (STA) 모드를 설정 하는 스레드의 클래스 에서만 사용할 수 있습니다. 이 클래스를 사용 하려면 프로그램 `Main` 표시 된 메서드가 <xref:System.STAThreadAttribute> 특성입니다.

### <a name="to-retrieve-data-from-the-clipboard-in-a-single-common-format"></a>클립보드에서 데이터를 단일 공통 형식으로 검색 하려면

1. ,, 또는 메서드<xref:System.Windows.Forms.Clipboard.GetText%2A> 를 사용 합니다. <xref:System.Windows.Forms.Clipboard.GetFileDropList%2A> <xref:System.Windows.Forms.Clipboard.GetAudioStream%2A> <xref:System.Windows.Forms.Clipboard.GetImage%2A> 필요에 따라 해당 `Contains` *형식* 메서드를 먼저 사용 하 여 특정 형식으로 데이터를 사용할 수 있는지 여부를 확인 합니다. 이러한 메서드는 .NET Framework 2.0 에서만 사용할 수 있습니다.

    [!code-csharp[System.Windows.Forms.Clipboard#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#2)]
    [!code-vb[System.Windows.Forms.Clipboard#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#2)]

### <a name="to-retrieve-data-from-the-clipboard-in-a-custom-format"></a>클립보드의 데이터를 사용자 지정 형식으로 검색 하려면

1. 사용자 지정 <xref:System.Windows.Forms.Clipboard.GetData%2A> 형식 이름을 사용 하 여 메서드를 사용 합니다. 이 메서드는 .NET Framework 2.0 에서만 사용할 수 있습니다.

    미리 정의 된 형식 이름을 <xref:System.Windows.Forms.Clipboard.SetData%2A> 메서드와 함께 사용할 수도 있습니다. 자세한 내용은 <xref:System.Windows.Forms.DataFormats>을 참조하세요.

    [!code-csharp[System.Windows.Forms.Clipboard#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#3)]
    [!code-vb[System.Windows.Forms.Clipboard#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#3)]
    [!code-csharp[System.Windows.Forms.Clipboard#100](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]

### <a name="to-retrieve-data-from-the-clipboard-in-multiple-formats"></a>클립보드에서 여러 형식의 데이터를 검색 하려면

1. <xref:System.Windows.Forms.Clipboard.GetDataObject%2A> 메서드를 사용하세요. .NET Framework 2.0 이전 버전의 클립보드에서 데이터를 검색 하려면이 메서드를 사용 해야 합니다.

    [!code-csharp[System.Windows.Forms.Clipboard#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#4)]
    [!code-vb[System.Windows.Forms.Clipboard#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#4)]
    [!code-csharp[System.Windows.Forms.Clipboard#100](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]

## <a name="see-also"></a>참고자료

- [끌어서 놓기 작업 및 클립보드 지원](drag-and-drop-operations-and-clipboard-support.md)
- [방법: 클립보드에 데이터 추가](how-to-add-data-to-the-clipboard.md)
