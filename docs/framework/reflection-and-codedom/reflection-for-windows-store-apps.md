---
title: Windows 스토어 앱에 대한 .NET Framework의 리플렉션
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- reflection, Windows Store apps
- .NET for Windows Store apps, TypeInfo class
ms.assetid: 0d07090c-9b47-4ecc-81d1-29d539603c9b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c9edab859900bf2001956045a5285801bb61d310
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045936"
---
# <a name="reflection-in-the-net-framework-for-windows-store-apps"></a>Windows 스토어 앱에 대한 .NET Framework의 리플렉션
.NET Framework 4.5부터 .NET Framework에는 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱에서 사용하기 위한 리플렉션 형식 및 멤버 세트가 포함되어 있습니다. 이러한 형식과 멤버는 전체 .NET Framework 및 [Windows 스토어 앱용 .NET](https://go.microsoft.com/fwlink/?LinkID=225700)에서 사용할 수 있습니다. 이 문서에서는 이러한 항목과 .NET Framework 4 이전 버전에 있는 해당 항목 간의 주요 차이점을 설명합니다.  
  
 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱을 만드는 경우 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]에서 리플렉션 형식 및 멤버를 사용해야 합니다. 이러한 형식과 멤버를 데스크톱 앱에서 사용할 수도 있지만 필수는 아니므로 두 유형의 앱에 동일한 코드를 사용할 수 있습니다.  
  
## <a name="typeinfo-and-assembly-loading"></a>TypeInfo 및 어셈블리 로딩  
 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]에서 <xref:System.Reflection.TypeInfo> 클래스에는 .NET Framework 4 <xref:System.Type> 클래스의 일부 기능이 포함되어 있습니다. <xref:System.Type> 개체는 형식 정의에 대한 참조를 나타내는 반면 <xref:System.Reflection.TypeInfo> 개체는 형식 정의 자체를 나타냅니다. 이렇게 하면 런타임에서 참조하는 어셈블리를 로드하지 않고도 <xref:System.Type> 개체를 조작할 수 있습니다. 연결된 <xref:System.Reflection.TypeInfo> 개체를 가져오면 어셈블리가 로드됩니다.  
  
 <xref:System.Reflection.TypeInfo>에는 <xref:System.Type>에서 사용할 수 있는 대부분의 멤버가 포함되고, [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]의 리플렉션 속성은 대부분 <xref:System.Reflection.TypeInfo> 개체 컬렉션을 반환합니다. <xref:System.Type> 개체에서 <xref:System.Reflection.TypeInfo> 개체를 가져오려면 <xref:System.Reflection.IReflectableType.GetTypeInfo%2A> 메서드를 사용합니다.  
  
## <a name="query-methods"></a>쿼리 메서드  
 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]에서 배열을 반환하는 메서드 대신 <xref:System.Collections.Generic.IEnumerable%601> 컬렉션을 반환하는 리플렉션 속성을 사용합니다. 리플렉션 컨텍스트는 큰 어셈블리 또는 형식에 대해 이러한 컬렉션의 지연 순회를 구현할 수 있습니다.  
  
 리플렉션 속성은 상속 트리를 트래버스하는 대신 특정 개체에 선언된 메서드만 반환합니다. 또한 <xref:System.Reflection.BindingFlags> 매개 변수를 필터링에 사용하지 않습니다. 대신, 반환된 컬렉션에 대해 LINQ 쿼리를 사용하여 사용자 코드에서 필터링이 수행됩니다. 런타임에 발생하는 리플렉션 개체(예: `typeof(Object)`의 결과로)의 경우 <xref:System.Reflection.RuntimeReflectionExtensions> 클래스의 도우미 메서드를 사용하면 상속 트리 트래버스가 가장 효과적으로 수행됩니다. 사용자 지정 리플렉션 컨텍스트의 개체 소비자는 이러한 메서드를 사용할 수 없으며, 상속 트리 자체를 트래버스해야 합니다.  
  
## <a name="restrictions"></a>제한  
 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱에서 일부 .NET Framework 형식 및 멤버에 대한 액세스는 제한됩니다. 예를 들어 <xref:System.Reflection.MethodInfo> 개체를 사용하여 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]에 포함되지 않은 .NET Framework 메서드를 호출할 수 없습니다. 또한 <xref:System.Runtime.InteropServices.Marshal> 및 <xref:System.Runtime.InteropServices.WindowsRuntime.WindowsRuntimeMarshal> 멤버처럼 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱의 컨텍스트 내에서 안전하게 간주되지 않는 특정 형식 및 멤버는 차단됩니다. 이 제한은 .NET Framework 형식 및 멤버에만 영향을 줍니다. 일반적인 방법으로 사용자 코드나 타사 코드를 호출할 수 있습니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]의 리플렉션 형식 및 멤버를 사용하여 상속된 메서드 및 속성을 비롯한 <xref:System.Globalization.Calendar> 형식의 메서드 및 속성을 검색합니다. 이 코드를 실행하려면 리플렉션 프로젝트에서 `textblock1`이라는 <xref:Windows.UI.Xaml.Controls.TextBlock?displayProperty=nameWithType> 컨트롤을 포함하는 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 페이지에 대한 코드 파일에 코드를 붙여넣습니다. 다른 이름을 사용하여 프로젝트에 이 코드를 붙여넣는 경우 프로젝트와 일치하도록 네임스페이스 이름을 변경해야 합니다.  
  
 [!code-csharp[System.ReflectionWinStoreApp#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.reflectionwinstoreapp/cs/mainpage.xaml.cs#1)]
 [!code-vb[System.ReflectionWinStoreApp#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.reflectionwinstoreapp/vb/mainpage.xaml.vb#1)]  
  
## <a name="see-also"></a>참고 항목

- [리플렉션](reflection.md)
- [Windows 스토어 앱용 .NET – 지원되는 API](https://go.microsoft.com/fwlink/?LinkID=225700)
