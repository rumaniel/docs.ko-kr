---
title: -errorreport
ms.date: 08/14/2018
helpviewer_keywords:
- -errorreport compiler option [Visual Basic]
- /errorreport compiler option [Visual Basic]
- errorreport compiler option [Visual Basic]
ms.assetid: a7fe83a2-a6d8-460c-8dad-79a8f433f501
ms.openlocfilehash: c8e193a8cb4d4dbc7515c32139bad9dce8b48ed7
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005622"
---
# <a name="-errorreport"></a>-errorreport

Visual Basic 컴파일러에서 내부 컴파일러 오류를 보고 하는 방법을 지정 합니다.

## <a name="syntax"></a>구문

```console
-errorreport:{ prompt | queue | send | none }
```

## <a name="remarks"></a>설명

이 옵션은 Microsoft의 Visual Basic 팀에 Visual Basic ICE (내부 컴파일러 오류)를 보고 하는 편리한 방법을 제공 합니다. 기본적으로 컴파일러는 Microsoft에 정보를 보내지 않습니다. 그러나 내부 컴파일러 오류가 발생 하는 경우이 옵션을 사용 하면 오류를 Microsoft에 보고할 수 있습니다. 이 정보는 Microsoft 엔지니어가 원인을 파악 하는 데 도움이 되며 Visual Basic의 다음 릴리스를 개선 하는 데 도움이 될 수 있습니다.

사용자는 컴퓨터 및 사용자 정책 권한에 따라 보고서를 보낼 수 있습니다.

다음 표에서는 `-errorreport` 옵션의 효과를 요약 하 여 보여 줍니다.

|옵션|동작|
|---|---|
|`prompt`|내부 컴파일러 오류가 발생 하는 경우 컴파일러에서 수집한 정확한 데이터를 볼 수 있는 대화 상자가 나타납니다. 오류 보고서에 중요 한 정보가 있는지 확인 하 고 Microsoft로 보낼지 여부를 결정할 수 있습니다. 이를 전송 하기로 결정 하 고 컴퓨터 및 사용자 정책 설정에서 허용 하는 경우 컴파일러는 데이터를 Microsoft로 보냅니다.|
|`queue`|오류 보고서를 큐에 넣습니다. 관리자 권한으로 로그인 하는 경우 마지막으로 로그인 한 이후에 발생 한 모든 오류를 보고할 수 있습니다 (오류에 대 한 보고서를 3 일 마다 한 번만 보낼지 묻는 메시지는 표시 되지 않음). @No__t-0 옵션이 지정 되지 않은 경우의 기본 동작입니다.|
|`send`|내부 컴파일러 오류가 발생 하 고 컴퓨터 및 사용자 정책 설정에서 허용 하는 경우 컴파일러는 데이터를 Microsoft로 보냅니다.<br /><br /> [Windows 오류 보고](/windows/desktop/wer/windows-error-reporting) 시스템 설정에서 보고를 사용 하도록 설정한 경우 `-errorreport:send` 옵션은 오류 정보를 자동으로 Microsoft에 보내도록 시도 합니다. |
|`none`|내부 컴파일러 오류가 발생 하면 수집 되거나 Microsoft로 전송 되지 않습니다.|

컴파일러는 일반적으로 일부 소스 코드를 포함 하는 오류가 발생 했을 때 스택을 포함 하는 데이터를 보냅니다. @No__t-0이-에 해당 하는 [보고서](../../../visual-basic/reference/command-line-compiler/bugreport.md) 옵션을 사용 하는 경우 전체 원본 파일이 전송 됩니다.

이 옵션은 Microsoft 엔지니어가 오류를 보다 쉽게 재현할 수 있도록 하기 때문에 [/prohreport](../../../visual-basic/reference/command-line-compiler/bugreport.md) 옵션과 함께 사용 하는 것이 가장 좋습니다.

> [!NOTE]
> @No__t-0 옵션은 Visual Studio 개발 환경에서 사용할 수 없습니다. 명령줄에서 컴파일하는 경우에만 사용할 수 있습니다.

## <a name="example"></a>예제

다음 코드는 `T2.vb`을 컴파일하도록 시도 하 고, 컴파일러에서 내부 컴파일러 오류가 발생 하는 경우 오류 보고서를 Microsoft로 보낼지 묻는 메시지를 표시 합니다.

```console
vbc -errorreport:prompt t2.vb
```

## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [-bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)
