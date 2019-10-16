---
title: XSLT 컴파일러(xsltc.exe)
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 672a5ac8-8305-4d28-ba10-11089c2c0924
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 729e6caa36ed8c2f6e77153f8d8ae356513b0603
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71956988"
---
# <a name="xslt-compiler-xsltcexe"></a>XSLT 컴파일러(xsltc.exe)
XSLT 컴파일러(xsltc.exe)에서는 XSLT 스타일시트를 컴파일하여 어셈블리를 생성합니다. 컴파일된 스타일시트는 <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Type%29?displayProperty=nameWithType> 메서드로 직접 전달될 수 있습니다. 서명된 어셈블리는 xsltc.exe를 사용하여 생성할 수 없습니다.  
  
 xsltc.exe 도구는 Visual Studio에 포함됩니다. 자세한 내용은 [Visual Studio 다운로드](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)를 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```console  
xsltc [options] [/class:<name>] <sourceFile> [[/class:<name>] <sourceFile>...]  
```  
  
## <a name="argument"></a>인수  
  
|인수|설명|  
|--------------|-----------------|  
|`sourceFile`|스타일시트 이름을 지정합니다. 스타일시트는 로컬 파일이거나 인트라넷에 있어야 합니다.|  
  
## <a name="options"></a>변수  
  
|옵션|설명|  
|------------|-----------------|  
|`/c[lass]:` `name`|다음 스타일시트의 클래스 이름을 지정합니다. 클래스 이름은 정규화된 이름일 수 있습니다.<br /><br /> 클래스 이름은 기본적으로 스타일시트 이름입니다. 예를 들어 customers.xsl 스타일시트가 컴파일되면 기본 클래스 이름은 customers입니다.|  
|`/debug[`+&#124;-`]`|디버깅 정보를 생성할지 여부를 지정합니다.<br /><br /> `+` 또는 `/debug`를 지정하면 컴파일러에서 디버깅 정보를 생성하여 PDB(프로그램 데이터베이스) 파일에 넣습니다. 생성된 PDB 파일 이름은 `assemblyName`.pdb입니다.<br /><br /> `-`를 지정하면 `/debug`를 지정하지 않은 것으로 적용되어 디버그 정보가 생성되지 않습니다. 정식 버전의 어셈블리가 생성됩니다. **참고:**  디버그 모드에서 컴파일하면 XSLT 성능에 크게 영향을 미칠 수 있습니다.|  
|`/help`|이 도구의 명령 구문 및 옵션을 표시합니다.|  
|`/nologo`|컴파일러 저작권 메시지가 표시되지 않도록 합니다.|  
|`/platform:` `string`|어셈블리가 실행되는 플랫폼을 지정합니다. 유효한 플랫폼 값은 다음과 같습니다.<br /><br /> `x86`을 지정하면 32비트 x86 호환 공용 언어 런타임에 의해 실행되도록 어셈블리를 컴파일합니다.<br /><br /> `x64`를 지정하면 AMD64 또는 EM64T 명령 집합을 지원하는 컴퓨터에서 64비트 공용 언어 런타임에 의해 실행되도록 어셈블리를 컴파일합니다.<br /><br /> Itanium은 Itanium 프로세서가 있는 컴퓨터에서 64비트 공용 언어 런타임에 의해 실행되도록 어셈블리를 컴파일합니다.<br /><br /> `anycpu`를 지정하면 임의의 플랫폼에서 실행되도록 어셈블리를 컴파일합니다. 이 값이 기본값입니다.|  
|`/out:` `assemblyName`|출력되는 어셈블리 이름을 지정합니다. 어셈블리 이름은 기본적으로 기본 스타일시트 이름 또는 첫 번째 스타일시트 이름(스타일시트가 여러 개 있는 경우)입니다.<br /><br /> 스타일시트에 스크립트가 포함된 경우 스크립트는 별도 어셈블리로 저장됩니다. 스크립트 어셈블리 이름은 기본 어셈블리 이름에서 생성됩니다. 예를 들어 어셈블리 이름으로 CustOrders.dll을 지정한 경우 첫 번째 스크립트 어셈블리 이름은 CustOrders_Script1.dll입니다.|  
|`/settings:` `document+-, script+-, DTD+-,`|스타일시트에 `document()` 함수, XSLT 스크립트 또는 DTD(문서 종류 정의)를 허용할지 여부를 지정합니다.<br /><br /> 기본 동작에서는 DTD, `document()` 함수 및 스크립트를 지원하지 않습니다.|  
|`@` `file`|컴파일러 옵션이 포함된 파일을 지정할 수 있습니다.|  
|`?`|이 도구의 명령 구문 및 옵션을 표시합니다.|  
  
## <a name="remarks"></a>설명  
 XSLT 솔루션은 여러 스타일시트 모듈로 구성됩니다. xsltc.exe 도구는 스타일시트에서 어셈블리를 생성합니다. 그런 다음 어셈블리가 <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Type%29?displayProperty=nameWithType> 메서드에 전달될 수 있습니다. 따라서 일부 XSLT 배포 시나리오에서 성능을 유지하는 데 드는 비용을 감소하는 데 도움이 될 수 있습니다.  
  
> [!NOTE]
> 애플리케이션에서 컴파일된 어셈블리를 참조로 포함해야 합니다.  
  
 xsltc.exe 도구에서는 클래스(`/class:`*이름*) 또는 어셈블리(`/out:`*assemblyName*) 이름의 유효성을 검사하지 않습니다. 이름의 유효성을 확인할 수 없으면 공용 언어 런타임에서 오류가 throw됩니다.  
  
## <a name="examples"></a>예  
 다음 명령에서는 스타일시트를 컴파일하여 이름이 booksort.dll인 어셈블리를 만듭니다.  
  
```console  
xsltc booksort.xsl  
```  
  
 다음 명령에서는 스타일시트를 컴파일하여 이름이 각각 booksort.dll 및 booksort.pdb인 어셈블리와 PDB 파일을 만듭니다.  
  
```console  
xsltc booksort.xsl /debug  
```  
  
 다음 명령에서는 msxsl:script 요소가 포함된 스타일시트를 컴파일하여 이름이 calc.dll 및 calc_Script1.dll인 두 개의 어셈블리를 만듭니다.  
  
```console  
xsltc /settings:script+ calc.xsl  
```  
  
 다음 명령에서는 DTD 처리 및 스크립트 지원을 활성화하여 이름이 myTest.dll 및 myTest_Script1.dll인 두 개의 어셈블리를 만듭니다.  
  
```console  
xsltc /settings:DTD+,script+ /out:myTest calc.xsl  
```  
  
 다음 명령에서는 두 개의 스타일시트 모듈을 컴파일하여 이름이 booksort.dll인 단일 어셈블리를 만듭니다.  
  
```console  
xsltc booksort.xsl output.xsl  
```  
  
## <a name="see-also"></a>참조

- <xref:System.Xml.Xsl.XslCompiledTransform>
- [방법: 어셈블리를 사용하여 XSLT 변형 수행](../../../../docs/standard/data/xml/how-to-perform-an-xslt-transformation-by-using-an-assembly.md)
- [XSLT 변환](../../../../docs/standard/data/xml/xslt-transformations.md)
