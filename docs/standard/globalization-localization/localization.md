---
title: 지역화
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- culture, localization
- application development [.NET Framework], localization
- globalization [.NET Framework], localization
- code blocks
- international applications [.NET Framework], localization
- global applications, localization
- world-ready applications, localization
- user interface blocks
- localization [.NET Framework], about localization
- localizing resources
ms.assetid: 49d520d7-92d7-44ee-bb24-8b615db1d41b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ee7de15130644e63b17a6d067c5cce9088d199a0
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48840417"
---
# <a name="localization"></a>지역화
지역화는 응용 프로그램에서 지원할 각 문화권에 맞는 지역화된 버전으로 응용 프로그램 리소스를 변환하는 프로세스입니다. [지역화 가능성 검토](../../../docs/standard/globalization-localization/localizability-review.md) 단계를 완료한 후에만 지역화 단계를 진행하여 전역화된 응용 프로그램이 지역화 준비가 되었는지 확인해야 합니다.  
  
 지역화 준비가 된 응용 프로그램은 두 가지 개념 블록 즉, 모든 사용자 인터페이스 요소가 포함된 블록 및 실행 코드가 포함된 블록으로 구분됩니다. 사용자 인터페이스 블록에는 중립적인 문화권에 적용할 수 있는 문자열, 오류 메시지, 대화 상자, 메뉴, 포함 개체 리소스 등과 같은 지역화 가능한 사용자 인터페이스 요소만 포함됩니다. 코드 블록에는 지원되는 모든 문화권에서 사용할 응용 프로그램 코드만 포함됩니다. 공용 언어 런타임은 해당 리소스에서 응용 프로그램의 실행 코드를 분리하는 위성 어셈블리 리소스 모델을 지원합니다. 이 모델을 구현하는 방법에 대한 자세한 내용은 [데스크톱 앱의 리소스](../../../docs/framework/resources/index.md)를 참조하세요.  
  
 응용 프로그램의 지역화된 버전 각각에 대해 대상 문화권의 적절한 언어로 번역된 지역화된 사용자 인터페이스 블록을 포함한 새 위성 어셈블리를 추가합니다. 모든 문화권의 코드 블록은 동일하게 유지해야 합니다. 지역화된 버전의 사용자 인터페이스 블록과 코드 블록을 조합하면 응용 프로그램의 지역화된 버전이 생성됩니다.  
  
 [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)]에서는 대상 문화권에 대한 Windows Forms를 빠르게 지역화할 수 있게 하는 Windows Forms 리소스 편집기(Winres.exe)를 제공합니다. 이 도구 사용에 대한 자세한 내용은 [Winres.exe(Windows Forms 리소스 편집기)](../../../docs/framework/tools/winres-exe-windows-forms-resource-editor.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [전역화 및 지역화](../../../docs/standard/globalization-localization/index.md)  
- [지역화 가능성 검토](../../../docs/standard/globalization-localization/localizability-review.md)  
- [전역화](../../../docs/standard/globalization-localization/globalization.md)  
- [데스크톱 앱의 리소스](../../../docs/framework/resources/index.md)
