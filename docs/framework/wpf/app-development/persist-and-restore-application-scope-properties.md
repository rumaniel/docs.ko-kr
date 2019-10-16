---
title: '방법: 애플리케이션 세션 간의 애플리케이션 범위 속성 유지 및 복원'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application-scope properties [WPF], persisting
- persisting application-scope properties [WPF]
- properties [WPF], persisting
- restoring application-scope properties [WPF]
- properties [WPF], restoring
- application-scope properties [WPF], restoring
ms.assetid: 55d5904a-f444-4eb5-abd3-6bc74dd14226
ms.openlocfilehash: d9c2dda2745e7528902b6b1c4f46d17264d1a8d8
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666719"
---
# <a name="how-to-persist-and-restore-application-scope-properties-across-application-sessions"></a>방법: 애플리케이션 세션 간의 애플리케이션 범위 속성 유지 및 복원
이 예제에서는 응용 프로그램이 종료 될 때 응용 프로그램 범위 속성을 유지 하는 방법과 응용 프로그램이 다음에 시작 될 때 응용 프로그램 범위 속성을 복원 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 응용 프로그램은 응용 프로그램 범위 속성을에 유지 하 고 격리 된 저장소에서 복원 합니다. 격리 된 저장소는 파일 액세스 권한이 없는 응용 프로그램에서 안전 하 게 사용할 수 있는 보호 된 저장소 영역입니다.  *App.xaml* 파일은 첫 번째 예제의 강조 `App_Startup` 표시 된 줄에 표시 된 <xref:System.Windows.Application.Startup?displayProperty=nameWithType> 것 처럼 메서드를 `App_Exit` 이벤트 처리기로 정의 하 고 <xref:System.Windows.Application.Exit?displayProperty=nameWithType> 메서드를 이벤트 처리기로 정의 합니다. 두 번째 예제에서는 응용 프로그램 범위 속성 `App_Exit` 을 복원 하는 메서드와 응용 프로그램 범위를 저장 하는 메서드의 `App_Startup` 코드를 강조 표시 하는 *App.xaml.cs* 및 app.xaml 파일의 일부를 보여 줍니다. 정보의.

 [!code-xaml[HOWTOApplicationModelSnippets#PersistRestoreAppScopePropertiesXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml?highlight=1-7)]
  
 [!code-csharp[HOWTOApplicationModelSnippets#PersistRestoreAppScopePropertiesCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml.cs?highlight=17-55)]
 [!code-vb[HOWTOApplicationModelSnippets#PersistRestoreAppScopePropertiesCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/visualbasic/application.xaml.vb?highlight=14-45)]
