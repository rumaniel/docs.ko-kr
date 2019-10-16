---
title: '방법: .NET Framework 3.5 설치 여부 확인'
ms.date: 03/30/2017
helpviewer_keywords:
- verifying whether.NET Framework 3.5 is installed [WPF]
- detecting .NET Framework 3.5 installation [WPF]
- detecting whether.NET Framework 3.5 is installed [WPF]
- determining whether.NET Framework 3.5 is installed [WPF]
ms.assetid: 8556a9d2-1eb8-48ef-919c-5baf22a2a9a2
ms.openlocfilehash: 18e5c819eb4deb62208280816d11dce0940d134d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053422"
---
# <a name="how-to-detect-whether-the-net-framework-35-is-installed"></a>방법: .NET Framework 3.5 설치 여부 확인
관리자가 3.5 .NET Framework를 대상으로 하는 시스템에 Windows Presentation Foundation (WPF) 응용 프로그램을 배포 하려면 먼저 .NET Framework 3.5 런타임이 있는지 확인 해야 합니다. 이 항목에서는 관리자가 .NET Framework 3.5가 시스템에 있는지 여부를 확인 하는 데 사용할 수 있는 HTML/JavaScript로 작성 된 스크립트를 제공 합니다.  
  
> [!NOTE]
> .NET Framework 설치, 배포 및 검색에 대 한 자세한 내용은 [개발자 용 .NET Framework 설치](../../install/guide-for-developers.md)를 참조 하세요.  
  
## <a name="example"></a>예제  
 .NET Framework 3.5가 설치 되 면 MSI는 ".NET CLR" 및 버전 번호를 UserAgent 문자열에 추가 합니다. 다음 예에서는 간단한 HTML 페이지에 포함 된 스크립트를 보여 줍니다. 이 스크립트는 UserAgent 문자열을 검색 하 여 .NET Framework 3.5가 설치 되어 있는지 확인 하 고 검색 결과에 상태 메시지를 표시 합니다.  
  
> [!NOTE]
> 이 스크립트는 Internet Explorer 용으로 설계 되었습니다. 다른 브라우저에는 UserAgent 문자열에 .NET CLR 정보가 포함 되지 않을 수 있습니다.  
  
```html  
<HTML>  
  <HEAD>  
    <TITLE>Test for the .NET Framework 3.5</TITLE>  
    <META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=utf-8" />  
    <SCRIPT LANGUAGE="JavaScript">  
    <!--  
    var dotNETRuntimeVersion = "3.5.0.0";  
  
    function window::onload()  
    {  
      if (HasRuntimeVersion(dotNETRuntimeVersion))  
      {  
        result.innerText =   
          "This machine has the correct version of the .NET Framework 3.5."  
      }   
      else  
      {  
        result.innerText =   
          "This machine does not have the correct version of the .NET Framework 3.5." +  
          " The required version is v" + dotNETRuntimeVersion + ".";  
      }  
      result.innerText += "\n\nThis machine's userAgent string is: " +   
        navigator.userAgent + ".";  
    }  
  
    //  
    // Retrieve the version from the user agent string and   
    // compare with the specified version.  
    //  
    function HasRuntimeVersion(versionToCheck)  
    {  
      var userAgentString =   
        navigator.userAgent.match(/.NET CLR [0-9.]+/g);  
  
      if (userAgentString != null)  
      {  
        var i;  
  
        for (i = 0; i < userAgentString.length; ++i)  
        {  
          if (CompareVersions(GetVersion(versionToCheck),   
            GetVersion(userAgentString[i])) <= 0)  
            return true;  
        }  
      }  
  
      return false;  
    }  
  
    //  
    // Extract the numeric part of the version string.  
    //  
    function GetVersion(versionString)  
    {  
      var numericString =   
        versionString.match(/([0-9]+)\.([0-9]+)\.([0-9]+)/i);  
      return numericString.slice(1);  
    }  
  
    //  
    // Compare the 2 version strings by converting them to numeric format.  
    //  
    function CompareVersions(version1, version2)  
    {  
      for (i = 0; i < version1.length; ++i)  
      {  
        var number1 = new Number(version1[i]);  
        var number2 = new Number(version2[i]);  
  
        if (number1 < number2)  
          return -1;  
  
        if (number1 > number2)  
          return 1;  
      }  
  
      return 0;  
    }  
  
    -->  
    </SCRIPT>  
  </HEAD>  
  
  <BODY>  
    <div id="result" />  
  </BODY>  
</HTML>  
```  
  
 ".NET CLR" 버전 검색에 성공 하면 다음과 같은 유형의 상태 메시지가 표시 됩니다.  
  
 `This machine has the correct version of the .NET Framework 3.5.`  
  
 `This machine's userAgent string is: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; SLCC1; .NET CLR 2.0.50727; .NET CLR 1.1.4322; InfoPath.2; .NET CLR 3.0.590; .NET CLR 3.5.20726; MS-RTC LM 8).`  
  
 그렇지 않으면 다음과 같은 유형의 상태 메시지가 표시 됩니다.  
  
 `This machine does not have the correct version of the .NET Framework 3.5. The required version is v3.5.0.0.`  
  
 `This machine's userAgent string is: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; SLCC1; .NET CLR 2.0.50727; .NET CLR 1.1.4322; InfoPath.2; .NET CLR 3.0.590; MS-RTC LM 8).`  
  
## <a name="see-also"></a>참고자료

- [.NET Framework 3.0 설치 여부 확인](how-to-detect-whether-the-net-framework-3-0-is-installed.md)
