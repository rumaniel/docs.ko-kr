---
title: -win32res(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /win32res
helpviewer_keywords:
- win32res compiler option
- /win32res compiler option [C#]
- -win32res compiler option [C#]
- win32res compiler option [C#]
ms.assetid: 3c33f750-6948-4c7e-a27e-bef98f77255b
ms.openlocfilehash: 39f02c4c2e060c4be40002a2f48b0da31004a9ae
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69606203"
---
# <a name="-win32res-c-compiler-options"></a>-win32res(C# 컴파일러 옵션)
**-win32res** 옵션은 출력 파일에 Win32 리소스를 삽입합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-win32res:filename  
```  
  
## <a name="arguments"></a>인수  
 `filename`  
 출력 파일에 추가하려는 리소스 파일입니다.  
  
## <a name="remarks"></a>설명  
 Win32 리소스 파일은 [리소스 컴파일러](../../language-reference/compiler-options/resource-compiler-option.md)로 만들 수 있습니다. 리소스 컴파일러는 Visual C++ 프로그램을 컴파일할 때 실행되며 .rc 파일에서 .res 파일이 만들어집니다.  
  
 Win32 리소스는 파일 탐색기에서 애플리케이션을 식별하는 데 도움이 되는 버전 정보나 비트맵 (아이콘) 정보를 포함할 수 있습니다. **-win32res**를 지정하지 않으면 컴파일러에서 어셈블리 버전을 기반으로 하여 버전 정보를 생성합니다.  
  
 .NET Framework 리소스 파일을 참조하려면 [-linkresource](./linkresource-compiler-option.md)를, 첨부하려면 [-resource](./resource-compiler-option.md)를 참조하세요.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1. 프로젝트 **속성** 페이지를 엽니다.  
  
2. **애플리케이션** 속성 페이지를 클릭합니다.  
  
3. **리소스 파일** 단추를 클릭한 다음 콤보 상자를 사용하여 파일을 선택합니다.  
  
## <a name="example"></a>예  
 `in.cs`를 컴파일하고 Win32 리소스 파일 `rf.res`를 첨부하여 `in.exe`를 생성합니다.  
  
```console  
csc -win32res:rf.res in.cs  
```  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
