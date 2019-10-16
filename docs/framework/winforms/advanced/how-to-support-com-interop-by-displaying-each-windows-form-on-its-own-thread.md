---
title: '방법: 각 Windows Form을 별개의 스레드에서 표시하여 COM Interop 지원'
ms.date: 03/30/2017
dev_langs:
- vb
helpviewer_keywords:
- COM interop [Windows Forms], Windows Forms
- COM [Windows Forms]
- Windows Forms, unmanaged
- ActiveX controls [Windows Forms], COM interop
- Windows Forms, interop
ms.assetid: a9e04765-d2de-4389-a494-a9a6d07aa6ee
ms.openlocfilehash: 41af4d81995a0a4eac912ecce7dc70cf04f012cd
ms.sourcegitcommit: 1e72e2990220b3635cebc39586828af9deb72d8c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71306385"
---
# <a name="how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread"></a>방법: 각 Windows Form을 자체 스레드에서 표시 하 여 COM interop 지원

<xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType> 메서드를 사용 하 여 만들 수 있는 .NET Framework 메시지 루프에 폼을 표시 하 여 COM 상호 운용성 문제를 해결할 수 있습니다.

Windows Form이 COM 클라이언트 애플리케이션에서 제대로 작동하게 하려면 Windows Forms 메시지 루프에서 폼을 실행해야 합니다. 이렇게 하려면 다음 접근 방식 중 하나를 사용합니다.

- <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> 메서드를 사용하여 Windows Form을 표시합니다. 자세한 내용은 [방법: ShowDialog 메서드로](com-interop-by-displaying-a-windows-form-shadow.md)Windows Form을 표시 하 여 COM Interop를 지원 합니다.

- 각 Windows Form을 별도 스레드에 표시합니다.

Visual Studio에서이 기능에 대해 폭넓게 지원이 됩니다.

[또한 연습: 각 Windows Form을 자체 스레드에서](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233639(v=vs.100))표시 하 여 COM Interop를 지원 합니다.

## <a name="example"></a>예제

다음 코드 예제에서는 별도 스레드에서 폼을 표시하고 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType> 메서드를 호출하여 해당 스레드에서 Windows Forms 메시지 펌프를 시작하는 방법을 보여 줍니다. 이 접근 방식을 사용하려면 <xref:System.Windows.Forms.Control.Invoke%2A> 메서드를 사용하여 관리되지 않는 애플리케이션의 폼 호출을 모두 마샬링해야 합니다.

이 접근 방법을 사용하려면 폼의 각 인스턴스가 고유한 메시지 루프를 통해 고유한 스레드에서 실행되어야 합니다. 스레드당 둘 이상의 메시지 루프 실행을 가질 수 없습니다. 따라서 클라이언트 애플리케이션의 메시지 루프를 변경할 수 없습니다. 그러나 .NET Framework 구성 요소를 수정 하 여 자체 메시지 루프를 사용 하는 새 스레드를 시작할 수 있습니다.

[!code-vb[System.Windows.Forms.ComInterop#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ComInterop/VB/COMForm.vb#1)]

[!code-vb[System.Windows.Forms.ComInterop#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ComInterop/VB/FormManager.vb#10)]

[!code-vb[System.Windows.Forms.ComInterop#100](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ComInterop/VB/Form1.vb#100)]

## <a name="compile-the-code"></a>코드 컴파일

`COMForm`, `Form1`및 `FormManager` 형식을 `COMWinform.dll`이라는 어셈블리로 컴파일합니다. [Packaging an Assembly for COM](../../interop/packaging-an-assembly-for-com.md)에 설명된 방법 중 하나를 사용하여 COM interop에 대한 어셈블리를 등록합니다. 이제 관리되지 않는 애플리케이션에서 어셈블리 및 해당 형식 라이브러리(.tlb) 파일을 사용할 수 있습니다. 예를 들어 Visual Basic 6.0 실행 프로젝트에서 형식 라이브러리를 참조로 사용할 수 있습니다.

## <a name="see-also"></a>참조

- [.NET Framework 구성 요소를 COM에 노출](../../interop/exposing-dotnet-components-to-com.md)
- [COM에서 사용할 어셈블리의 패키징](../../interop/packaging-an-assembly-for-com.md)
- [COM에 어셈블리 등록](../../interop/registering-assemblies-with-com.md)
- [방법: ShowDialog 메서드로 Windows Form을 표시 하 여 COM Interop 지원](com-interop-by-displaying-a-windows-form-shadow.md)
- [Windows Forms 및 관리되지 않는 애플리케이션 개요](windows-forms-and-unmanaged-applications-overview.md)
