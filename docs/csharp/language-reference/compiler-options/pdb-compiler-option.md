---
title: -pdb(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /pdb
helpviewer_keywords:
- -pdb compiler option [C#]
- pdb compiler option [C#]
- /pdb compiler option [C#]
ms.assetid: e9d0f96a-5b75-45d6-9765-92538dd5f823
ms.openlocfilehash: 3081f4716e8cd858d789db6050e635af941aa05c
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69602571"
---
# <a name="-pdb-c-compiler-options"></a>-pdb(C# 컴파일러 옵션)
**-pdb** 컴파일러 옵션은 디버그 기호 파일의 이름 및 위치를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-pdb:filename  
```  
  
## <a name="arguments"></a>인수  
 `filename`  
 디버그 기호 파일의 이름 및 위치입니다.  
  
## <a name="remarks"></a>설명  
 [-debug(C# 컴파일러 옵션)](./debug-compiler-option.md)를 지정하는 경우 컴파일러는 출력 파일(.exe 또는 .dll)을 만들 디렉터리에 출력 파일의 이름과 동일한 파일 이름으로 .pdb 파일을 만듭니다.  
  
 **-pdb**를 사용하면 .pdb 파일에 대해 기본값이 아닌 파일 이름과 위치를 지정할 수 있습니다.  
  
 Visual Studio 개발 환경에서는 이 컴파일러 옵션을 설정할 수 없으며 프로그래밍 방식으로 변경할 수도 없습니다.  
  
## <a name="example"></a>예  
 `t.cs`를 컴파일하고 tt.pdb라는 .pdb 파일을 만듭니다.  
  
```console  
csc -debug -pdb:tt t.cs  
```  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
