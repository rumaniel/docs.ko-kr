---
title: '방법: 분석 힌트를 사용하여 잉크 분석'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ink [WPF], analyzing
- analyzing ink [WPF]
- ink [WPF], AnalysisHintNode objects [WPF]
- AnalysisHintNode objects [WPF]
ms.assetid: d4421ed4-77f5-4640-829e-9f1de50b2ff2
ms.openlocfilehash: a4c38ddf52e9054fe9126df4b7e172548617b90d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61777002"
---
# <a name="how-to-analyze-ink-with-analysis-hints"></a>방법: 분석 힌트를 사용하여 잉크 분석
[System.Windows.Ink.AnalysisHintNode](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms610344(v=vs.90)) 에 대 한 힌트를 제공 합니다 [System.Windows.Ink.InkAnalyzer](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms616754(v=vs.90)) 연결 됩니다.  힌트에서 지정한 영역에 적용 됩니다는 [System.Windows.Ink.ContextNode.Location%2A](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms594508(v=vs.90)) 의 속성을 [System.Windows.Ink.AnalysisHintNode](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms610344(v=vs.90)) 잉크 분석기를 추가 컨텍스트를 제공 하 고 인식 정확도 향상 합니다. 합니다 [System.Windows.Ink.InkAnalyzer](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms616754(v=vs.90)) 힌트 영역 내에서 가져온 잉크를 분석 하는 경우이 컨텍스트 정보에 적용 됩니다.  
  
## <a name="example"></a>예제  
 다음 예제는 여러를 사용 하는 응용 프로그램 [System.Windows.Ink.AnalysisHintNode](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms610344(v=vs.90)) 양식에서 잉크 입력을 허용 하는 개체입니다. 응용 프로그램을 사용 합니다 [System.Windows.Ink.AnalysisHintNode.Factoid%2A](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms594341(v=vs.90)) 양식의 각 항목에 대 한 컨텍스트 정보를 제공 하는 속성입니다.  응용 프로그램 백그라운드 분석을 사용 하 여 잉크를 분석 하 고 형식의 모든 잉크 사용자 잉크 추가 중지 한 후에 5 초를 지웁니다.  
  
 [!code-xaml[HowToAnalyzeInk#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAnalyzeInk/CSharp/FormAnalyzer.xaml#1)]  
  
 [!code-csharp[HowToAnalyzeInk#2](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAnalyzeInk/CSharp/FormAnalyzer.xaml.cs#2)]
 [!code-vb[HowToAnalyzeInk#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToAnalyzeInk/VisualBasic/FormAnalyzer.xaml.vb#2)]
