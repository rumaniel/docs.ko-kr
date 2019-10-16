---
title: '방법: .NET Framework와 Windows 런타임 스트림 간의 변환(Windows에만 해당)'
ms.date: 01/14/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 23a763ea-8348-4244-9f8c-a4280b870b47
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 22cf168c660349bda16c59aec4824e3283430807
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65877935"
---
# <a name="how-to-convert-between-net-framework-and-windows-runtime-streams-windows-only"></a>방법: .NET Framework와 Windows 런타임 스트림 간의 변환(Windows에만 해당)

UWP 앱용 .NET Framework는 전체 .NET Framework의 하위 집합입니다. UWP 앱에 대한 보안과 기타 요구 사항 때문에, 전체 .NET Framework API 세트를 사용하여 파일을 열고 읽을 수는 없습니다. 자세한 내용은 [UWP 앱용 .NET 개요](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140))를 참조하세요. 그러나 다른 스트림 조작 작업에 대한 .NET Framework API를 사용하고 싶을 수 있습니다. 이러한 스트림을 조작하려면 <xref:System.IO.MemoryStream> 또는 <xref:System.IO.FileStream>과 같은 .NET Framework 스트림 형식과 <xref:Windows.Storage.Streams.IInputStream>,<xref:Windows.Storage.Streams.IOutputStream> 또는 <xref:Windows.Storage.Streams.IRandomAccessStream>과 같은 Windows 런타임 스트림 간에 변환하면 됩니다.

<xref:System.IO.WindowsRuntimeStreamExtensions?displayProperty=nameWithType> 클래스는 이러한 변환을 쉽게 하는 메서드를 포함합니다. 하지만 .NET Framework와 Windows 런타임 스트림의 근본적인 차이점은 이러한 메서드를 사용한 결과에 영향을 미치며, 다음 섹션에 설명되어 있습니다.

## <a name="convert-from-a-windows-runtime-to-a-net-framework-stream"></a>Windows 런타임에서 .NET Framework 스트림으로 변환
Windows 런타임 스트림에서 .NET Framework 스트림으로 변환하려면 다음 <xref:System.IO.WindowsRuntimeStreamExtensions?displayProperty=nameWithType> 메서드 중 하나를 사용하세요.

- <xref:System.IO.WindowsRuntimeStreamExtensions.AsStream%2A?displayProperty=nameWithType>은 Windows 런타임의 임의 액세스 스트림을 UWP용 .NET 앱의 관리형 스트림으로 변환합니다.
  
- <xref:System.IO.WindowsRuntimeStreamExtensions.AsStreamForWrite%2A?displayProperty=nameWithType>은 Windows 런타임의 출력 스트림을 UWP용 .NET 앱의 관리형 스트림으로 변환합니다.
  
- <xref:System.IO.WindowsRuntimeStreamExtensions.AsStreamForRead%2A?displayProperty=nameWithType>은 Windows 런타임의 입력 스트림을 UWP용 .NET 앱의 관리형 스트림으로 변환합니다.

Windows 런타임은 읽기 전용, 쓰기 전용 또는 읽기 및 쓰기를 지원하는 스트림 형식을 제공합니다. 이러한 기능은 Windows 런타임 스트림을 .NET Framework 스트림으로 변환할 때 유지됩니다. 더구나 Windows 런타임 스트림을 .NET Framework 스트림으로 변환하고 그 반대로 변환하는 경우 원래 Windows 런타임 인스턴스를 다시 얻습니다. 

변환하려는 Windows 런타임 스트림의 기능과 일치하는 변환 메서드를 사용하는 것이 가장 좋습니다. 하지만 <xref:Windows.Storage.Streams.IRandomAccessStream>을 읽고 쓸 수 있으므로(<xref:Windows.Storage.Streams.IOutputStream>과 <xref:Windows.Storage.Streams.IInputStream> 둘 다 구현함) 변환 메서드는 원본 스트림의 기능을 유지합니다. 예를 들어 <xref:System.IO.WindowsRuntimeStreamExtensions.AsStreamForRead%2A?displayProperty=nameWithType>을 사용하여 <xref:Windows.Storage.Streams.IRandomAccessStream>을 변환하면 변환된 .NET Framework 스트림을 읽을 수 있도록 제한하지 않습니다. 쓰기도 가능합니다.

## <a name="example-convert-windows-runtime-random-access-to-net-framework-stream"></a>예제: Windows 런타임 임의 액세스를 .NET Framework 스트림으로 변환
Windows 런타임 임의 액세스 스트림에서 .NET Framework 스트림으로 변환하려면 <xref:System.IO.WindowsRuntimeStreamExtensions.AsStream%2A?displayProperty=nameWithType> 메서드를 사용하세요.

다음 코드 예제는 파일을 선택하라는 메시지를 표시하고 Windows 런타임 API로 파일을 연 다음, .NET Framework 스트림으로 변환합니다. 스트림을 읽어서 텍스트 블록으로 출력합니다. 일반적으로 결과를 출력하기 전에 .NET Framework API로 스트림을 조작합니다.

이 예제를 실행하려면, `TextBlock1`이라는 텍스트 블록과 `Button1`이라는 단추가 포함된 UWP XAML 앱을 만듭니다. 단추 클릭 이벤트를 이 예제에 표시된 `button1_Click` 메서드와 연결합니다.

  [!code-csharp[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](~/samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/cs/mainpage1.xaml.cs)]
  [!code-vb[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](~/samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/vb/mainpage1.xaml.vb)]

## <a name="convert-from-a-net-framework-to-a-windows-runtime-stream"></a>.NET Framework를 Windows 런타임 스트림으로 변환
.NET Framework 스트림에서 Windows 런타임 스트림으로 변환하려면 다음 <xref:System.IO.WindowsRuntimeStreamExtensions?displayProperty=nameWithType> 메서드 중 하나를 사용하세요.

- <xref:System.IO.WindowsRuntimeStreamExtensions.AsInputStream%2A?displayProperty=nameWithType>은 UWP용 .NET 앱의 관리형 스트림을 Windows 런타임의 입력 스트림으로 변환합니다.
  
- <xref:System.IO.WindowsRuntimeStreamExtensions.AsOutputStream%2A?displayProperty=nameWithType>은 UWP용 .NET 앱의 관리형 스트림을 Windows 런타임의 출력 스트림으로 변환합니다.
  
- <xref:System.IO.WindowsRuntimeStreamExtensions.AsRandomAccessStream%2A?displayProperty=nameWithType>은 UWP 앱용 .NET의 관리형 스트림을 Windows 런타임에서 읽거나 쓰는 데 사용할 수 있는 임의 액세스 스트림으로 변환합니다.

.NET Framework 스트림을 Windows 런타임 스트림으로 변환할 때 변환된 스트림의 기능은 원본 스트림에 따라 다릅니다. 예를 들어 원본 스트림이 읽기와 쓰기를 모두 지원하는 경우 <xref:System.IO.WindowsRuntimeStreamExtensions.AsInputStream%2A?displayProperty=nameWithType>을 호출하여 스트림을 변환하면, 반환되는 형식은 `IRandomAccessStream`입니다. `IRandomAccessStream`은 `IInputStream`과 `IOutputStream`을 구현하고 읽기와 쓰기를 지원합니다.

.NET Framework 스트림은 변환 후에도 복제를 지원하지 않습니다. .NET Framework 스트림을 Windows 런타임 스트림으로 변환하고 <xref:Windows.Storage.Streams.RandomAccessStreamOverStream.CloneStream%2A>을 호출하는 <xref:Windows.Storage.Streams.InMemoryRandomAccessStream.GetInputStreamAt%2A> 또는 <xref:Windows.Storage.Streams.IRandomAccessStream.GetOutputStreamAt%2A>을 호출하거나 <xref:Windows.Storage.Streams.RandomAccessStreamOverStream.CloneStream%2A>을 직접 호출하면 예외가 발생합니다.

## <a name="example-convert-net-framework-to-windows-runtime-random-access-stream"></a>예제: .NET Framework를 Windows 런타임 임의 액세스 스트림으로 변환

.NET Framework 스트림을 Windows 런타임 임의 액세스 스트림으로 변환하려면 다음 예제와 같이 <xref:System.IO.WindowsRuntimeStreamExtensions.AsRandomAccessStream%2A> 메서드를 사용합니다.

> [!IMPORTANT]
> 사용 중인 .NET Framework 스트림이 검색을 지원하는지 확인하고 그렇지 않으면 지원하는 스트림에 복사합니다. <xref:System.IO.Stream.CanSeek%2A?displayProperty=nameWithType> 속성을 사용하여 이를 확인할 수 있습니다.

이 예제를 실행하려면 .NET Framework 4.5.1을 대상으로 하고 `TextBlock2`라는 텍스트 블록과 `Button2`라는 단추를 포함하는 UWP XAML 앱을 만듭니다. 단추 클릭 이벤트를 이 예제에 표시된 `button2_Click` 메서드와 연결합니다.

  [!code-csharp[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](~/samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/cs/mainpage2.xaml.cs)]
  [!code-vb[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](~/samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/vb/mainpage2.xaml.vb)]

## <a name="see-also"></a>참고 항목

- [빠른 시작: 파일 읽기 및 쓰기(Windows)](https://docs.microsoft.com/previous-versions/windows/apps/hh464978(v=win.10))  
- [Windows 스토어 앱용 .NET 개요](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140))  
- [Windows 스토어용 .NET 앱 API](https://docs.microsoft.com/previous-versions/br230232(v=vs.120))  
