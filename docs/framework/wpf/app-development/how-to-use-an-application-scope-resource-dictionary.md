---
title: '방법: 애플리케이션 범위 리소스 사전 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dictionaries [WPF], resource
- resource dictionaries [WPF], application-scope
- application-scope resource dictionaries
ms.assetid: 53857682-bd2c-4f2c-8f25-1307d0b451a2
ms.openlocfilehash: 589e28b3c05496e3fc17055b98240e389faed068
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62007489"
---
# <a name="how-to-use-an-application-scope-resource-dictionary"></a>방법: 애플리케이션 범위 리소스 사전 사용
이 예제에서는 애플리케이션 범위 사용자 지정 리소스 사전을 정의하고 사용하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 <xref:System.Windows.Application> 공유 리소스인 <xref:System.Windows.Application.Resources%2A>에 대한 응용 프로그램 범위 저장소를 노출 합니다. 기본적으로 <xref:System.Windows.Application.Resources%2A> 속성은 <xref:System.Windows.ResourceDictionary> 형식의 인스턴스로 초기화 됩니다. 이 인스턴스를 <xref:System.Windows.Application.Resources%2A>를 사용하는 응용 프로그램 범위 속성을 가져오기 및 설정시에 사용 합니다. 자세한 내용은 [방법: Get 및 Set 응용 프로그램 범위 리소스를](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aa348547(v=vs.100))입니다.
  
 <xref:System.Windows.Application.Resources%2A>를 사용하여 설정할 다수의 리소스가 있는 경우, 해당 리소스를 저장하고 그것을 대신하여 <xref:System.Windows.Application.Resources%2A>에 설정하도록 사용자 지정 리소스 사전을 대신 사용할 수 있습니다. 다음은 XAML을 사용하여 사용자 지정 리소스 사전을 선언하는 방법을 보여 줍니다.
  
 [!code-xaml[HOWTOResourceDictionaries#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToResourceDictionaries/CSharp/MyResourceDictionary.xaml#1)]  
  
 <xref:System.Windows.Application.Resources%2A>를 사용하여 전체 리소스를 바꾸면 각 테마가 단일 리소스 사전으로 캡슐화된 응용 프로그램 범위 테마를 지원할 수 있습니다. 다음 예제에서는 <xref:System.Windows.ResourceDictionary>를 설정하는 방법을 보여 줍니다.  
  
 [!code-xaml[HOWTOResourceDictionaries#2](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToResourceDictionaries/CSharp/App.xaml#2)]  
  
 다음은 XAML에서 <xref:System.Windows.Application.Resources%2A>에 의해 노출된 리소스 사전에서 응용 프로그램 범위 리소스를 가져오는 방법을 보여 줍니다.  
  
 [!code-xaml[HOWTOResourceDictionaries#4](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToResourceDictionaries/CSharp/MainWindow.xaml#4)]  
  
 다음 예제에서는 코드에서 리소스를 가져오는 방법을 보여 줍니다.  
  
 [!code-csharp[HOWTOResourceDictionaries#3](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToResourceDictionaries/CSharp/MainWindow.xaml.cs#3)]
 [!code-vb[HOWTOResourceDictionaries#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToResourceDictionaries/VB/MainWindow.xaml.vb#3)]  
  
 <xref:System.Windows.Application.Resources%2A>를 사용 시에는 두 가지 고려할 사항이 있습니다. 첫 번째는, 사전 *키*가 개체(object)이므로 속성 값 설정 및 가져오기 시에 모두 정확히 동일한 개체 인스턴스를 사용해야 합니다. (문자열을 사용할 경우 키는 대/소문자를 구분해야 합니다.) 두 번째, 사전 *값* 개체 이므로 속성 값을 가져올 때 값을 원하는 형식으로 변환 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.ResourceDictionary>
- <xref:System.Windows.Application.Resources%2A>
- [XAML 리소스](../advanced/xaml-resources.md)
- [병합된 리소스 사전](../advanced/merged-resource-dictionaries.md)
