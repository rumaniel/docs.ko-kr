---
title: '방법: 리플렉션을 사용하지 않고 인쇄 시스템 개체 속성 가져오기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PrintSystemObject [WPF], getting properties
ms.assetid: 43560f28-183d-41c1-b9d1-de7c2552273e
ms.openlocfilehash: bb906dafd98e75708764b5f0f009900719f6a475
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59335201"
---
# <a name="how-to-get-print-system-object-properties-without-reflection"></a>방법: 리플렉션을 사용하지 않고 인쇄 시스템 개체 속성 가져오기
개체의 속성 (및 해당 속성의 형식)를 항목별로 정리 하는 데 리플렉션을 사용 하면 응용 프로그램 성능이 느려질 수 있습니다. <xref:System.Printing.IndexedProperties> 네임 스페이스는 리플렉션을 사용 하 여이 정보를 가져올 수 있는 방법을 제공 합니다.  
  
## <a name="example"></a>예제  
 이 작업을 수행 하는 단계는 다음과 같습니다.  
  
1. 형식의 인스턴스를 만듭니다. 형식은 아래 예에는 <xref:System.Printing.PrintQueue> Microsoft.NET Framework 하지만 거의 동일한 코드와 함께 제공 되는 형식에서 파생 된 형식에 대해 작동 합니다 <xref:System.Printing.PrintSystemObject>합니다.  
  
2. 만들기는 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary> 형식에서 <xref:System.Printing.PrintSystemObject.PropertiesCollection%2A>합니다. 합니다 <xref:System.Collections.DictionaryEntry.Value%2A> 이 사전의 각 항목의 속성에서 파생 된 형식의 개체인 <xref:System.Printing.IndexedProperties.PrintProperty>합니다.  
  
3. 사전 멤버를 열거 합니다. 각각에 대해 다음을 수행 합니다.  
  
4. 위로 캐스팅 하려면 각 항목의 값이 <xref:System.Printing.IndexedProperties.PrintProperty> 만드는 데 사용 하 고는 <xref:System.Printing.IndexedProperties.PrintProperty> 개체입니다.  
  
5. 형식을 가져오는 합니다 <xref:System.Printing.IndexedProperties.PrintProperty.Value%2A> 각를 <xref:System.Printing.IndexedProperties.PrintProperty> 개체입니다.  
  
 [!code-csharp[GetPrintObjectPropertyTypesWithoutReflection#ShowPropertyTypesWithoutReflection](~/samples/snippets/csharp/VS_Snippets_Wpf/GetPrintObjectPropertyTypesWithoutReflection/CSharp/Program.cs#showpropertytypeswithoutreflection)]
 [!code-vb[GetPrintObjectPropertyTypesWithoutReflection#ShowPropertyTypesWithoutReflection](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GetPrintObjectPropertyTypesWithoutReflection/visualbasic/program.vb#showpropertytypeswithoutreflection)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Printing.IndexedProperties.PrintProperty>
- <xref:System.Printing.PrintSystemObject>
- <xref:System.Printing.IndexedProperties>
- <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>
- <xref:System.Printing.LocalPrintServer>
- <xref:System.Printing.PrintQueue>
- <xref:System.Collections.DictionaryEntry>
- [WPF의 문서](documents-in-wpf.md)
- [인쇄 개요](printing-overview.md)
