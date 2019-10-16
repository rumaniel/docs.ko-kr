---
title: '완화: ZipArchiveEntry.FullName 경로 구분 기호'
ms.date: 03/30/2017
helpviewer_keywords:
- application compatibility
- ',NET Framework application compatibility'
- .NET Framework 4.6.1
- .NET Framework 4.6.1 retargeting changes
- retargeting changes
ms.assetid: 8d575722-4fb6-49a2-8a06-f72d62dc3766
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b97436ca2f81fea139689c7c2c2348718827b90f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70778857"
---
# <a name="mitigation-ziparchiveentryfullname-path-separator"></a>완화: ZipArchiveEntry.FullName 경로 구분 기호
.NET Framework 4.6.1을 대상으로 하는 앱부터 <xref:System.IO.Compression.ZipArchiveEntry.FullName%2A?displayProperty=nameWithType> 속성에 사용되는 경로 구분 기호가 이전 버전의 .NET Framework에서 사용된 백슬래시("\\")에서 슬래시("/")로 변경되었습니다.   <xref:System.IO.Compression.ZipFile.CreateFromDirectory%2A?displayProperty=nameWithType> 메서드의 오버로드 중 하나를 호출하여 <xref:System.IO.Compression.ZipArchiveEntry?displayProperty=nameWithType> 개체를 만듭니다.  
  
## <a name="impact"></a>영향  
 이 변경으로 인해 .NET 구현은 [.ZIP 파일 형식 사양](https://pkware.cachefly.net/webdocs/casestudies/APPNOTE.TXT)의 섹션 4.4.17.1과 일치하게 되고 비 Windows 시스템에서.ZIP 아카이브의 압축이 풀리게 됩니다.  
  
 Macintosh와 같은 비 Windows 운영 체제에서 이전 버전의 .NET Framework를 대상으로 하는 앱이 생성한 zip 파일의 압축을 풀면 디렉터리 구조가 유지되지 않습니다. 예를 들어 Macintosh에서는 해당 파일 이름이 디렉터리 경로, 백슬래시("\\") 문자 및 파일 이름으로 연결된 파일 집합이 만들어집니다. 결과적으로 압축을 푼 파일의 디렉터리 구조는 유지되지 않습니다.  
  
 .NET Framework <xref:System.IO> 네임스페이스의 API는 슬래시("/") 또는 백슬래시("\\")를 경로 구분 기호 문자로 원활하게 처리할 수 있으므로 이러한 API에 의해 Windows 운영 체제에서 압축 해제된 .ZIP 파일에 이러한 변경이 미치는 영향은 최소로 유지될 것입니다.  
  
## <a name="mitigation"></a>완화  
 이 동작을 원치 않을 경우 애플리케이션 구성 파일의 [\<runtime&gt;](../configure-apps/file-schema/runtime/runtime-element.md) 섹션에 구성 설정을 추가하여 옵트아웃(opt out)할 수 있습니다. 다음에서는 `<runtime>` 섹션 및 옵트아웃 스위치를 둘 다 보여 줍니다.  
  
```xml  
<runtime>  
   <AppContextSwitchOverrides value="Switch.System.IO.Compression.ZipFile.UseBackslash=true" />  
</runtime>  
```  
  
 또한 이전 버전의 .NET Framework를 대상으로 하지만 .NET Framework 4.6.1 이상 버전에서 실행되는 앱은 애플리케이션 구성 파일의 [\<runtime&gt;](../configure-apps/file-schema/runtime/runtime-element.md) 섹션에 구성 설정을 추가하여 이 동작을 옵트인할 수 있습니다. 다음에서는 `<runtime>` 섹션 및 옵트인 스위치를 둘 다 보여 줍니다.  
  
```xml  
<runtime>  
   <AppContextSwitchOverrides value="Switch.System.IO.Compression.ZipFile.UseBackslash=false" />  
</runtime>  
```  
  
## <a name="see-also"></a>참고 항목

- [대상 다시 지정 변경 내용](retargeting-changes-in-the-net-framework-4-6-1.md)
- [4.6.1의 애플리케이션 호환성](application-compatibility-in-the-net-framework-4-6-1.md)
