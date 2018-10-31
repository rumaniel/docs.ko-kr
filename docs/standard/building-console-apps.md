---
title: .NET Framework에서 콘솔 응용 프로그램 만들기
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- .NET Framework, building console applications
- application development [.NET Framework], console
- console applications
ms.assetid: c21fb997-9f0e-40a5-8741-f73bba376bd8
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 979989c3e1f90f3de47473aa1bd8bc5268520e57
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48840156"
---
# <a name="building-console-applications-in-the-net-framework"></a>.NET Framework에서 콘솔 응용 프로그램 만들기
.NET Framework의 응용 프로그램에서는 <xref:System.Console?displayProperty=nameWithType> 클래스를 사용하여 콘솔로부터 문자를 읽거나 콘솔에 문자를 쓸 수 있습니다. 콘솔의 데이터는 표준 입력 스트림에서 읽혀지고 표준 출력 스트림으로 쓰여지며, 콘솔의 오류 데이터는 표준 오류 출력 스트림으로 쓰여집니다. 이러한 스트림은 응용 프로그램이 시작될 때 콘솔과 자동으로 연결되며 <xref:System.Console.In%2A>, <xref:System.Console.Out%2A> 및 <xref:System.Console.Error%2A> 속성으로 나타납니다.  
  
 <xref:System.Console.In%2A?displayProperty=nameWithType> 속성의 값은 <xref:System.IO.TextReader?displayProperty=nameWithType> 개체인 반면 <xref:System.Console.Out%2A?displayProperty=nameWithType> 및 <xref:System.Console.Error%2A?displayProperty=nameWithType> 속성의 값은 <xref:System.IO.TextWriter?displayProperty=nameWithType> 개체입니다. 콘솔을 나타내지 않는 스트림과 이들 속성을 연결하여 스트림이 서로 다른 입력 또는 출력 위치를 향하도록 할 수 있습니다. 예를 들어 <xref:System.Console.Out%2A?displayProperty=nameWithType> 속성을 <xref:System.IO.StreamWriter?displayProperty=nameWithType>로 설정하여 출력을 파일로 리디렉션할 수 있습니다. 이 속성 값은 <xref:System.IO.FileStream?displayProperty=nameWithType>을 <xref:System.Console.SetOut%2A?displayProperty=nameWithType> 메서드로 캡슐화합니다. <xref:System.Console.In%2A?displayProperty=nameWithType> 및 <xref:System.Console.Out%2A?displayProperty=nameWithType> 속성은 동일한 스트림을 참조할 필요가 없습니다.  
  
> [!NOTE]
>  C#, Visual Basic 및 C++의 예제를 비롯하여 콘솔 응용 프로그램을 빌드하는 방법에 대한 자세한 내용은 <xref:System.Console> 클래스 설명서를 참조하세요.  
  
 Windows 기반 응용 프로그램 내에 콘솔이 존재하지 않을 경우 정보를 쓸 콘솔이 없으므로 표준 출력 스트림에 쓰여지는 출력은 보이지 않습니다. 액세스할 수 없는 콘솔에 정보를 쓸 경우 예외가 발생하지 않습니다.  
  
 또는 Visual Studio를 사용하여 개발된 Windows 기반 응용 프로그램 내에서 콘솔의 읽기 및 쓰기를 설정하려면 프로젝트의 **속성** 대화 상자를 열고, **응용 프로그램** 탭을 클릭하고, **응용 프로그램 종류**를 **콘솔 응용 프로그램**으로 설정합니다.  
  
 콘솔 응용 프로그램에는 기본적으로 시작되는 메시지 펌프가 없습니다. 따라서 Microsoft Win32 타이머에 대한 콘솔 호출이 실패할 수도 있습니다.  
  
 **System.Console** 클래스에는 콘솔에서 개별 문자나 전체 줄을 읽을 수 있는 메서드가 있습니다. 다른 메서드는 데이터 및 형식 문자열을 변환한 다음 형식 지정된 문자열을 콘솔에 씁니다. 문자열 형식 지정에 대한 자세한 내용은 [형식 서식 지정](../../docs/standard/base-types/formatting-types.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Console?displayProperty=nameWithType>  
- [형식 서식 지정](../../docs/standard/base-types/formatting-types.md)
