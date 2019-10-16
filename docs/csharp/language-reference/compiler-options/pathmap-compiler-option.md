---
title: -pathmap(C# 컴파일러 옵션)
ms.date: 05/16/2018
f1_keywords:
- /pathmap
helpviewer_keywords:
- -pathmap compiler option [C#]
- pathmap compiler option [C#]
- /pathmap compiler option [C#]
ms.openlocfilehash: 48e96d2ec2ccbea83d573c0eb3630b1591c407a9
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69606633"
---
# <a name="-pathmap-c-compiler-options"></a>-pathmap(C# 컴파일러 옵션)

**-pathmap** 컴파일러 옵션은 실제 경로를 컴파일러에서 출력되는 소스 경로 이름에 매핑하는 방법을 지정합니다.

## <a name="syntax"></a>구문

```console
-pathmap:path1=sourcePath1,path2=sourcePath2
```

## <a name="arguments"></a>인수

 `path1` 현재 환경에서 소스 파일의 전체 경로입니다.

 `sourcePath1` 출력 파일에서 `path1`을 대체하는 소스 경로입니다.

매핑되는 소스 경로를 여럿 지정하려면 각각을 쉼표로 구분합니다.

## <a name="remarks"></a>설명

컴파일러가 출력에 소스 경로를 쓰는 이유는 다음과 같습니다.

1. 선택적 매개 변수에 <xref:System.Runtime.CompilerServices.CallerFilePathAttribute>를 적용할 때 소스 경로가 인수 대신 사용되는 경우
1. 소스 경로가 PDB 파일에 포함된 경우
1. PDB 파일의 경로가 PE(이식 가능한 실행 파일) 파일에 포함된 경우

이 옵션은 컴파일러가 실행되는 컴퓨터의 실제 경로 각각을 출력 파일에 써야 하는 해당 경로에 매핑합니다.

## <a name="example"></a>예

**C:\\work\\tests** 디렉터리에 `t.cs`를 컴파일하고 출력에서 디렉터리를 **\publish**에 매핑합니다.

```console
csc -pathmap:C:\work\tests=\publish t.cs
```

## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
