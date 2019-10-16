---
title: -keyfile
ms.date: 03/10/2018
helpviewer_keywords:
- /keyfile compiler option [Visual Basic]
- keyfile compiler option [Visual Basic]
- -keyfile compiler option [Visual Basic]
ms.assetid: ffa82a4b-517a-4c6c-9889-5bae7b534bb8
ms.openlocfilehash: b17df3cb803cfbef324b74a9dee4394fce70215b
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005545"
---
# <a name="-keyfile"></a>-keyfile
어셈블리에 강력한 이름을 지정하는 키 또는 키 쌍이 포함된 파일을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console 
-keyfile:file  
```  
  
## <a name="arguments"></a>인수  
 `file`  
 필수. 키를 포함 하는 파일입니다. 파일 이름에 공백이 포함 된 경우 이름을 큰따옴표 ("")로 묶습니다.  
  
## <a name="remarks"></a>설명  
 컴파일러는 공개 키를 어셈블리 매니페스트에 삽입 한 다음 개인 키를 사용 하 여 최종 어셈블리에 서명 합니다. 키 파일을 생성하려면 명령줄에 `sn -k file`을 입력합니다. 자세한 내용은 [sn.exe (강력한 이름 도구)](../../../framework/tools/sn-exe-strong-name-tool.md))를 참조 하세요.  
  
 @No__t-0으로 컴파일하는 경우 키 파일의 이름이 모듈에 저장 되 고 [/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)을 사용 하 여 어셈블리를 컴파일할 때 생성 되는 어셈블리에 통합 됩니다.  
  
 [-keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)를 사용하여 암호화 정보를 컴파일러에 전달할 수도 있습니다. 부분 서명된 어셈블리가 필요한 경우 [-delaysign](../../../visual-basic/reference/command-line-compiler/delaysign.md)을 사용합니다.  
  
 Microsoft 중간 언어 모듈의 소스 코드에서이 옵션을 사용자 지정 특성 (<xref:System.Reflection.AssemblyKeyFileAttribute>)으로 지정할 수도 있습니다.  
  
 동일한 컴파일에서 명령줄 옵션이 나 사용자 지정 특성을 통해 `-keyfile`과 [-keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md) 를 둘 다 지정 하는 경우 컴파일러는 먼저 키 컨테이너를 시도 합니다. 키 컨테이너를 찾으면 키 컨테이너의 정보를 사용하여 어셈블리가 서명됩니다. 컴파일러가 키 컨테이너를 찾지 못하면 `-keyfile`으로 지정 된 파일을 시도 합니다. 이 작업이 성공 하면 어셈블리는 키 파일의 정보를 사용 하 여 서명 되 고 키 정보는 키 컨테이너 (`sn -i`과 유사)에 설치 되므로 다음 컴파일에서 키 컨테이너가 유효 하 게 됩니다.  
  
 키 파일에는 공개 키만 포함될 수 있습니다.  
  
 어셈블리 서명에 대 한 자세한 내용은 [강력한 이름의 어셈블리 만들기 및 사용](../../../standard/assembly/create-use-strong-named.md) 을 참조 하세요.  
  
> [!NOTE]
> @No__t-0 옵션은 Visual Studio 개발 환경에서 사용할 수 없습니다. 명령줄에서 컴파일하는 경우에만 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 코드는-0 @no__t 소스 파일을 컴파일하고 키 파일을 지정 합니다.  
  
```console  
vbc -keyfile:myfile.sn input.vb  
```  
  
## <a name="see-also"></a>참조

- [.NET 어셈블리](../../../standard/assembly/index.md)
- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
