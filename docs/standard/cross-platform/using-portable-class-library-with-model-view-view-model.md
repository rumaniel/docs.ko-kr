---
title: Model-View-View Model과 함께 이식 가능한 클래스 라이브러리 사용
ms.date: 07/18/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Portable Class Library [.NET Framework], and MVVM
- MVVM, and Portable Class Library
ms.assetid: 41a0b9f8-15a2-431a-bc35-e310b2953b03
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b53be90764c6537fb27cb1b5ed781a68e69effa0
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67504669"
---
# <a name="using-portable-class-library-with-model-view-view-model"></a>Model-View-View Model과 함께 이식 가능한 클래스 라이브러리 사용
.NET Framework를 사용 하 여 [이식 가능한 클래스 라이브러리](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md) 모델-뷰 모델 (MVVM) 패턴을 구현 하 여 여러 플랫폼 간에 어셈블리를 공유 합니다.

[!INCLUDE[standard](../../../includes/pcl-to-standard.md)]

 MVVM은 내부 비즈니스 논리에서 사용자 인터페이스를 분리하는 애플리케이션 패턴입니다. Visual Studio 2012의 이식 가능한 클래스 라이브러리 프로젝트에서 모델 및 보기 모델 클래스를 구현 하 고 다양 한 플랫폼에 대 한 사용자 지정 된 뷰를 만들 수 있습니다. 이 접근 방식을 사용하면 한 번만 데이터 모델과 비즈니스 논리를 작성하고, 다음 설명에서와 같이 .NET Framework, Silverlight, Windows Phone 및 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램의 해당 코드를 사용할 수 있습니다.

 ![플랫폼에서 MVVM 공유 어셈블리를 사용 하 여 이식 가능한 클래스 라이브러리를 보여 줍니다.](./media/using-portable-class-library-with-model-view-view-model/mvvm-share-assemblies-across-platforms.png)

 이 항목에서는 MVVM 패턴에 대 한 일반 정보를 제공 하지 않습니다. 만 이식 가능한 클래스 라이브러리를 사용 하 여 MVVM을 구현 하는 방법에 대 한 정보를 제공 합니다. MVVM에 대 한 자세한 내용은 참조는 [MVVM 퀵 스타트를 사용 하 여 Prism 라이브러리 5.0 WPF 용](https://docs.microsoft.com/previous-versions/msp-n-p/gg430857(v=pandp.40))합니다.

## <a name="classes-that-support-mvvm"></a>MVVM을 지 원하는 클래스
 .NET Framework 4.5를 대상 지정 하면 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)], Silverlight 또는 Windows Phone 7.5 이식 가능한 클래스 라이브러리 프로젝트에 대해 다음 클래스는 MVVM 패턴을 구현 하기 위한 사용할 수 있습니다:

- <xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=nameWithType> 클래스

- <xref:System.Collections.ObjectModel.ReadOnlyObservableCollection%601?displayProperty=nameWithType> 클래스

- <xref:System.Collections.Specialized.INotifyCollectionChanged?displayProperty=nameWithType> 클래스

- <xref:System.Collections.Specialized.NotifyCollectionChangedAction?displayProperty=nameWithType> 클래스

- <xref:System.Collections.Specialized.NotifyCollectionChangedEventArgs?displayProperty=nameWithType> 클래스

- <xref:System.Collections.Specialized.NotifyCollectionChangedEventHandler?displayProperty=nameWithType> 클래스

- <xref:System.ComponentModel.DataErrorsChangedEventArgs?displayProperty=nameWithType> 클래스

- <xref:System.ComponentModel.INotifyDataErrorInfo?displayProperty=nameWithType> 클래스

- <xref:System.ComponentModel.INotifyPropertyChanged?displayProperty=nameWithType> 클래스

- <xref:System.Windows.Input.ICommand?displayProperty=nameWithType> 클래스

- 모든 클래스는 <xref:System.ComponentModel.DataAnnotations?displayProperty=nameWithType> 네임 스페이스

## <a name="implementing-mvvm"></a>MVVM을 구현
 MVVM을 구현 하려면 일반적으로 만든 모델과 뷰 모델 이식 가능한 클래스 라이브러리 프로젝트에서 이식 가능한 클래스 라이브러리 프로젝트를 이식 가능 프로젝트를 참조할 수 없습니다 때문입니다. 동일한 프로젝트에서 또는 별도 프로젝트에서 모델 및 뷰 모델을 수 있습니다. 별도 프로젝트를 사용 하는 경우 모델 프로젝트에 뷰 모델 프로젝트에서 참조를 추가 합니다.

 모델을 컴파일하여 모델 프로젝트를 확인 한 후 뷰가 포함 된 앱에서 해당 어셈블리를 참조 합니다. 뷰는 뷰 모델만 상호 작용을 하는 경우 뷰 모델이 포함 된 어셈블리를 참조 해야 합니다.

### <a name="model"></a>모델
 다음 예제에서는 이식 가능한 클래스 라이브러리 프로젝트에 있을 수 있습니다 하는 간단한 모델 클래스를 보여 줍니다.

 [!code-csharp[PortableClassLibraryMVVM#1](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/customer.cs#1)]
 [!code-vb[PortableClassLibraryMVVM#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/customer.vb#1)]

 다음 예에서는 채우기, 검색 및 이식 가능한 클래스 라이브러리 프로젝트에서 데이터를 업데이트 하는 간단한 방법을 보여 줍니다. 실제 앱에서는 Windows Communication Foundation (WCF) 서비스와 같은 원본에서 데이터를 검색할 됩니다.

 [!code-csharp[PortableClassLibraryMVVM#2](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/customerrepository.cs#2)]
 [!code-vb[PortableClassLibraryMVVM#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/customerrepository.vb#2)]

### <a name="view-model"></a>뷰 모델
 보기 모델에 대 한 기본 클래스는 MVVM 패턴을 구현 하는 경우에 자주 추가 됩니다. 다음 예제에서는 기본 클래스를 보여 줍니다.

 [!code-csharp[PortableClassLibraryMVVM#3](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/viewmodelbase.cs#3)]
 [!code-vb[PortableClassLibraryMVVM#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/viewmodelbase.vb#3)]

 구현 된 <xref:System.Windows.Input.ICommand> 인터페이스 MVVM 패턴을 사용 하 여 자주 사용 됩니다. 다음 예제에서는 <xref:System.Windows.Input.ICommand> 인터페이스의 구현을 보여 줍니다.

 [!code-csharp[PortableClassLibraryMVVM#4](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/relaycommand.cs#4)]
 [!code-vb[PortableClassLibraryMVVM#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/relaycommand.vb#4)]

 다음 예제에서는 단순화 된 보기 모델을 보여 줍니다.

 [!code-csharp[PortableClassLibraryMVVM#5](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/mainpageviewmodel.cs#5)]
 [!code-vb[PortableClassLibraryMVVM#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/customerviewmodel.vb#5)]  
  
### <a name="view"></a>보기  
 .NET Framework 4.5 앱에서 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱, Silverlight 기반 앱 또는 Windows Phone 7.5 앱, 모델과 뷰 모델 프로젝트를 포함 하는 어셈블리를 참조할 수 있습니다.  그런 다음 뷰 모델을 사용 하 여 상호 작용 하는 뷰를 만듭니다. 다음 예제에서는 검색 및 보기 모델의 데이터를에서 업데이트 하는 간단한 Windows Presentation Foundation (WPF) 앱을 보여 줍니다. Windows Phone Silverlight에서 유사한 뷰를 만들 수 있습니다 또는 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱.  
  
 [!code-xaml[PortableClassLibraryMVVM#6](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/mainwindow.xaml#6)]  
  
## <a name="see-also"></a>참고자료

- [이식 가능한 클래스 라이브러리](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md)
