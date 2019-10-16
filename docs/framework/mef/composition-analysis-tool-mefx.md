---
title: 컴퍼지션 분석 도구(Mefx)
ms.date: 03/30/2017
helpviewer_keywords:
- Composition Analysis Tool [MEF]
- MEF, Composition Analysis Tool
- Mefx [MEF], Composition Analysis Tool
ms.assetid: c48a7f93-83bb-4a06-aea0-d8e7bd1502ad
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f3777627caec7fc0d383804f71d9b7d3f09756fd
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894126"
---
# <a name="composition-analysis-tool-mefx"></a>컴퍼지션 분석 도구(Mefx)
컴퍼지션 분석 도구(Mefx)는 MEF(Managed Extensibility Framework) 파트를 포함하는 라이브러리(.dll) 및 애플리케이션(.exe) 파일을 분석하는 명령줄 애플리케이션입니다. Mefx는 주로 번거로운 추적 코드를 애플리케이션 자체에 추가할 필요 없이 MEF 애플리케이션에서 컴퍼지션 실패를 진단하는 방법을 개발자에게 제공하는 데 사용됩니다. 타사에서 제공된 라이브러리의 파트를 이해할 때 유용할 수 있습니다. 이 항목에서는 Mefx를 사용하는 방법을 설명하고 해당 구문에 대한 참조를 제공합니다.  
  
<a name="getting_mefx"></a>   
## <a name="getting-mefx"></a>Mefx 가져오기  
 Mefx는 GitHub의 [Managed Extensibility Framework](https://github.com/MicrosoftArchive/mef/releases/tag/4.0)에 있습니다. 도구를 다운로드하고 압축을 풀면 됩니다.  
  
<a name="basic_syntax"></a>   
## <a name="basic-syntax"></a>기본 구문  
 Mefx는 명령줄에서 다음 형식으로 호출됩니다.  
  
```console
mefx [files and directories] [action] [options]  
```  
  
 첫 번째 인수 집합은 분석할 파트를 로드할 소스 파일 및 디렉터리를 지정합니다. `/file:` 스위치를 사용하여 파일을 지정하고 `/directory:` 스위치를 사용하여 디렉터리를 지정합니다. 다음 예제와 같이 여러 파일 또는 디렉터리를 지정할 수 있습니다.  
  
```console  
mefx /file:MyAddIn.dll /directory:Program\AddIns [action...]  
```  
  
> [!NOTE]
> 각 .dll 또는 .exe는 한 번만 로드되어야 합니다. 파일이 여러 번 로드되면 도구가 잘못된 정보를 반환할 수 있습니다.  
  
 파일 및 디렉터리 목록 다음에 명령 및 해당 명령의 옵션을 지정해야 합니다.  
  
<a name="listing_available_parts"></a>   
## <a name="listing-available-parts"></a>사용 가능한 파트 나열  
 `/parts` 작업을 사용하여 로드된 파일에서 선언된 모든 파트를 나열합니다. 결과는 단순한 파트 이름 목록입니다.  
  
```console
mefx /file:MyAddIn.dll /parts  
MyAddIn.AddIn  
MyAddIn.MemberPart  
```  
  
 파트에 대한 자세한 내용은 `/verbose` 옵션을 사용하세요. 이를 통해 모든 사용 가능한 파트에 대한 자세한 정보가 출력됩니다. 단일 파트에 대한 자세한 정보를 가져오려면 `/type` 대신 `/parts`작업을 사용합니다.  
  
```console  
mefx /file:MyAddIn.dll /type:MyAddIn.AddIn /verbose  
[Part] MyAddIn.MemberPart from: AssemblyCatalog (Assembly=" MyAddIn, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
  [Export] MyAddIn.MemberPart (ContractName=" MyAddIn.MemberPart")  
```  
  
<a name="listing_imports_and_exports"></a>   
## <a name="listing-imports-and-exports"></a>가져오기 및 내보내기 나열  
 `/imports` 및 `/exports` 작업은 각각 모든 가져온 파트 및 모든 내보낸 파트를 나열합니다. `/importers` 또는 `/exporters` 작업을 사용하여 특정 형식을 가져오거나 내보내는 파트를 나열할 수도 있습니다.  
  
```console  
mefx /file:MyAddIn.dll /importers:MyAddin.MemberPart  
MyAddin.AddIn  
```  
  
 이들 작업에 `/verbose` 옵션을 적용할 수 있습니다.  
  
<a name="finding_rejected_parts"></a>   
## <a name="finding-rejected-parts"></a>거부된 파트 찾기  
 사용 가능한 파트를 로드한 후 Mefx는 MEF 컴퍼지션 엔진을 사용하여 파트를 구성합니다. 성공적으로 구성할 수 없는 파트를 *거부됨*이라고 합니다. 거부된 파트를 모두 나열하려면 `/rejected` 작업을 사용합니다.  
  
 `/verbose` 옵션을 `/rejected` 작업과 함께 사용하여 거부된 파트에 대한 자세한 정보를 인쇄할 수 있습니다. 다음 예제에서 `ClassLibrary1` DLL은 `AddIn` 및 `MemberPart` 파트를 가져오는 `ChainOne` 파트를 포함합니다. `ChainOne` 은 `ChainTwo`를 가져오지만 `ChainTwo` 가 없습니다. 즉, `ChainOne` 이 거부되어 `AddIn` 도 거부됩니다.  
  
```console  
mefx /file:ClassLibrary1.dll /rejected /verbose  
```  
  
 다음은 이전 명령의 전체 출력을 보여 줍니다.  
  
```output
[Part] ClassLibrary1.AddIn from: AssemblyCatalog (Assembly="ClassLibrary1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
  [Export] ClassLibrary1.AddIn (ContractName="ClassLibrary1.AddIn")  
  [Import] ClassLibrary1.AddIn.memberPart (ContractName="ClassLibrary1.MemberPart")  
    [SatisfiedBy] ClassLibrary1.MemberPart (ContractName="ClassLibrary1.MemberPart") from: ClassLibrary1.MemberPart from: AssemblyCatalog (Assembly="ClassLibrar  
y1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
  [Import] ClassLibrary1.AddIn.chain (ContractName="ClassLibrary1.ChainOne")  
    [Exception] System.ComponentModel.Composition.ImportCardinalityMismatchException: No valid exports were found that match the constraint '((exportDefinition.ContractName == "ClassLibrary1.ChainOne") AndAlso (exportDefinition.Metadata.ContainsKey("ExportTypeIdentity") AndAlso "ClassLibrary1.ChainOne".Equals(exportDefinition.Metadata.get_Item("ExportTypeIdentity"))))', invalid exports may have been rejected.  
   at System.ComponentModel.Composition.Hosting.ExportProvider.GetExports(ImportDefinition definition, AtomicComposition atomicComposition)  
   at Microsoft.ComponentModel.Composition.Diagnostics.CompositionInfo.AnalyzeImportDefinition(ExportProvider host, IEnumerable`1 availableParts, ImportDefinition id)  
    [Unsuitable] ClassLibrary1.ChainOne (ContractName="ClassLibrary1.ChainOne")  
from: ClassLibrary1.ChainOne from: AssemblyCatalog (Assembly="ClassLibrary1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
      [Because] PartDefinitionIsRejected, The part providing the export is rejected because of other issues.  
  
[Part] ClassLibrary1.ChainOne from: AssemblyCatalog (Assembly="ClassLibrary1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
  [Primary Rejection]  
  [Export] ClassLibrary1.ChainOne (ContractName="ClassLibrary1.ChainOne")  
  [Import] ClassLibrary1.ChainOne.chain (ContractName="ClassLibrary1.ChainTwo")  
    [Exception] System.ComponentModel.Composition.ImportCardinalityMismatchException: No valid exports were found that match the constraint '((exportDefinition.ContractName == "ClassLibrary1.ChainTwo") AndAlso (exportDefinition.Metadata.ContainsKey("ExportTypeIdentity") AndAlso "ClassLibrary1.ChainTwo".Equals(exportDefinition.Metadata.get_Item("ExportTypeIdentity"))))', invalid exports may have been rejected.  
   at System.ComponentModel.Composition.Hosting.ExportProvider.GetExports(ImportDefinition definition, AtomicComposition atomicComposition)  
   at Microsoft.ComponentModel.Composition.Diagnostics.CompositionInfo.AnalyzeImportDefinition(ExportProvider host, IEnumerable`1 availableParts, ImportDefinition id)  
```  
  
 관심 있는 정보는 `[Exception]` 및 `[Unsuitable]` 결과에 포함됩니다. `[Exception]` 결과는 파트가 거부된 이유에 대한 정보를 제공합니다. `[Unsuitable]` 결과는 이외의 경우 일치하는 파트가 가져오기를 채우는 데 사용될 수 없는 이유를 나타냅니다. 이 경우 누락된 가져오기로 인해 해당 파트가 거부되었기 때문입니다.  
  
<a name="analyzing_primary_causes"></a>   
## <a name="analyzing-primary-causes"></a>주 원인 분석  
 여러 파트가 긴 종속성 체인으로 연결된 경우 아래쪽에 가까운 파트 관련 문제로 인해 전체 체인이 거부될 수 있습니다. 실패의 근본 원인이 항상 분명한 것은 아니므로 이들 문제를 진단하기 어려울 수 있습니다. 문제에 도움이 되도록 연속 거부의 근본 원인을 찾으려고 시도하는 `/causes` 작업을 사용할 수 있습니다.  
  
 이전 예제에서 `/causes` 작업을 사용하면 채워지지 않은 가져오기가 `ChainOne`거부의 근본 원인인 `AddIn`에 대한 정보만 나열됩니다. `/causes` 작업은 일반 및 `/verbose` 옵션에서 둘 다 사용할 수 있습니다.  
  
> [!NOTE]
> 대부분 경우에 Mefx는 연속 실패의 근본 원인을 진단할 수 있습니다. 그러나 파트가 컨테이너에 프로그래밍 방식으로 추가된 경우, 계층적 컨테이너가 관련된 경우 또는 사용자 지정 `ExportProvider` 구현이 관련된 경우 Mefx는 원인을 진단할 수 없습니다. 일반적으로 실패를 진단하기 어려우므로 가능하면 앞에서 설명된 경우를 피해야 합니다.  
  
<a name="white_lists"></a>   
## <a name="white-lists"></a>허용 목록  
 `/whitelist` 옵션을 사용하여 거부될 것으로 예상되는 파트를 나열하는 텍스트 파일을 지정할 수 있습니다. 이에 따라 예기치 않은 거부에 플래그가 지정됩니다. 불완전한 라이브러리 또는 일부 종속성이 누락된 하위 라이브러리를 분석할 때 이 방법이 유용할 수 있습니다. `/whitelist` 옵션을 `/rejected` 또는 `/causes` 작업에 적용할 수 있습니다.  
  
 "ClassLibrary1.ChainOne" 텍스트를 포함하는 test.txt 파일을 고려하세요. 이전 예제에서 `/rejected` 작업을 `/whitelist` 옵션과 함께 실행하면 다음 출력이 생성됩니다.  
  
```console
mefx /file:ClassLibrary1.dll /rejected /whitelist:test.txt  
[Unexpected] ClassLibrary1.AddIn  
ClassLibrary1.ChainOne  
```
