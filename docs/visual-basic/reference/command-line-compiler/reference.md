---
title: -reference (Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- /reference compiler option [Visual Basic]
- r compiler option [Visual Basic]
- -reference compiler option [Visual Basic]
- /r compiler option [Visual Basic]
- reference compiler option [Visual Basic]
- -r compiler option [Visual Basic]
ms.assetid: 66bdfced-bbf6-43d1-a554-bc0990315737
ms.openlocfilehash: 552fbcf920be609de83708a995a87761f6080220
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005263"
---
# <a name="-reference-visual-basic"></a>-reference (Visual Basic)
컴파일러가 지정 된 어셈블리의 형식 정보를 현재 컴파일하고 있는 프로젝트에 사용할 수 있도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-reference:fileList  
```

로 구분하거나 여러

```console
-r:fileList  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`fileList`|필수. 쉼표로 구분된 어셈블리 파일 이름 목록입니다. 파일 이름에 공백이 있으면 이름을 따옴표로 묶습니다.|  
  
## <a name="remarks"></a>설명  
 가져오는 파일에는 어셈블리 메타 데이터가 포함 되어야 합니다. Public 형식만 어셈블리 외부에서 볼 수 있습니다. [/Addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) 옵션은 모듈에서 메타 데이터를 가져옵니다.  
  
 다른 어셈블리 (어셈블리 B)를 참조 하는 어셈블리 (어셈블리 A)를 참조 하는 경우에는 어셈블리 B를 참조 해야 합니다.  
  
- 어셈블리 A의 형식은 형식에서 상속되거나 어셈블리 B의 인터페이스를 구현합니다.  
  
- 어셈블리 B의 반환 형식이나 매개 변수 형식을 사용하는 필드, 속성, 이벤트 또는 메서드가 호출됩니다.  
  
 하나 이상의 어셈블리 참조가 있는 디렉터리를 지정 하려면 [-libpath](../../../visual-basic/reference/command-line-compiler/libpath.md) 을 사용 합니다.  
  
 컴파일러가 모듈이 아니라 어셈블리의 형식을 인식할 수 있도록 하려면 강제로 형식을 확인 해야 합니다. 이 작업을 수행 하는 방법에 대 한 한 가지 예는 형식의 인스턴스를 정의 하는 것입니다. 컴파일러에 대 한 어셈블리의 형식 이름을 확인 하는 데 사용할 수 있는 다른 방법이 있습니다. 예를 들어, 어셈블리의 형식에서 상속 하는 경우 형식 이름이 컴파일러에 인식 됩니다.  
  
 일반적으로 사용 되는 .NET Framework 어셈블리를 참조 하는 Vbc.exe 지시 파일은 기본적으로 사용 됩니다. 컴파일러가 Vbc.rsp를 사용 하지 않도록 하려면 `-noconfig`을 사용 합니다.  
  
 `-reference`의 약식은 `/r`입니다.  
  
## <a name="example"></a>예제  
 다음 명령은 `Metad1.dll` 및 `Metad2.dll`의 소스 파일 `Input.vb` 및 참조 어셈블리를 컴파일하여-3 @no__t을 생성 합니다.  
  
```console
vbc -reference:metad1.dll,metad2.dll -out:out.exe input.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)
- [-target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
- [공개](../../../visual-basic/language-reference/modifiers/public.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
