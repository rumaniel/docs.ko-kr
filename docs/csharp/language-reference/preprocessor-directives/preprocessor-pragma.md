---
title: '#pragma - C# 참조'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- '#pragma'
helpviewer_keywords:
- '#pragma directive [C#]'
ms.assetid: 5b7944cd-d402-46a1-ad8f-feffb2d83673
ms.openlocfilehash: 65ca38ff6993117b6ed9f716d4ac93ba2d4a9ddf
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69605663"
---
# <a name="pragma-c-reference"></a>#pragma(C# 참조)
`#pragma`는 이 코드가 표시되는 파일의 컴파일에 대한 특수 명령을 컴파일러에 제공합니다. 컴파일러에서 명령을 지원해야 합니다. 즉, `#pragma`를 사용하여 사용자 지정 전처리 명령을 만들 수 없습니다. Microsoft C# 컴파일러는 다음 두 가지 `#pragma` 명령을 지원합니다.  
  
 [#pragma warning](./preprocessor-pragma-warning.md)  
  
 [#pragma checksum](./preprocessor-pragma-checksum.md)  
  
## <a name="syntax"></a>구문  
  
```csharp
#pragma pragma-name pragma-arguments  
```  
  
## <a name="parameters"></a>매개 변수  
 `pragma-name`  
 인식된 pragma의 이름입니다.  
  
 `pragma-arguments`  
 pragma 관련 인수입니다.  
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 전처리기 지시문](./index.md)
- [#pragma warning](./preprocessor-pragma-warning.md)
- [#pragma checksum](./preprocessor-pragma-checksum.md)
