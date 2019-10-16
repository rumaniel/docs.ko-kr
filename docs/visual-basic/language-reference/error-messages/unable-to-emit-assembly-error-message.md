---
title: 어셈블리를 생성할 수 없습니다. <error message>
ms.date: 08/14/2018
f1_keywords:
- vbc30145
- bc30145
helpviewer_keywords:
- BC30145
ms.assetid: 2e7eb2b9-eda6-4bdb-95cc-72c7f0be7528
ms.openlocfilehash: 530aaee40be92bf72ee4b83b4141108e9b81c8a1
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70968862"
---
# <a name="unable-to-emit-assembly-error-message"></a>어셈블리를 내보낼 수 없습니다 \<. 오류 메시지 >

Visual Basic 컴파일러는 어셈블리 링커 (*al.exe*, Alink 라고도 함)를 호출 하 여 매니페스트를 사용 하 여 어셈블리를 생성 하 고, 링커가 어셈블리 만들기의 내보내기 단계에서 오류를 보고 합니다.

**오류 ID:** BC30145

## <a name="to-correct-this-error"></a>이 오류를 해결하려면

1. 따옴표 붙은 오류 메시지를 확인 하 고 [al.exe](../../../framework/tools/al-exe-assembly-linker.md) 항목을 참조 하 여 추가 설명 및 조언을 확인 합니다.

2. [Al.exe](../../../framework/tools/al-exe-assembly-linker.md) 또는 [Sn.exe (강력한 이름 도구)](../../../framework/tools/sn-exe-strong-name-tool.md)를 사용 하 여 어셈블리에 수동으로 서명 하세요.

3. 오류가 계속 발생하면 해당 상황에 대한 정보를 수집하여 Microsoft 기술 지원 서비스에 알립니다.

### <a name="to-sign-the-assembly-manually"></a>어셈블리에 수동으로 서명하려면

1. [Sn.exe (강력한 이름 도구)](../../../framework/tools/sn-exe-strong-name-tool.md))를 사용 하 여 공개/개인 키 쌍 파일을 만듭니다.

   이 파일의 확장명은 *.snk* 입니다.

2. 프로젝트에서 오류를 생성하는 COM 참조를 삭제합니다.

3. [Visual Studio에 대 한 개발자 명령 프롬프트](../../../framework/tools/developer-command-prompt-for-vs.md)를 엽니다.

   Windows 10에서 작업 표시줄의 검색 상자에 **개발자 명령 프롬프트** 를 입력 합니다. 그런 다음 결과 목록에서 **VS 2017에 대 한 개발자 명령 프롬프트** 를 선택 합니다.

4. 어셈블리 래퍼를 저장 하려는 디렉터리로 디렉터리를 변경 합니다.

5. 다음 명령을 입력합니다.

    ```cmd
    tlbimp <path to COM reference file> /out:<output assembly name> /keyfile:<path to .snk file>
    ```

   입력할 수 있는 실제 명령의 예는 다음과 같습니다.

    ```cmd
    tlbimp c:\windows\system32\msi.dll /out:Interop.WindowsInstaller.dll /keyfile:"c:\documents and settings\mykey.snk"
    ```

   > [!TIP]
   > 경로 또는 파일에 공백이 있는 경우 큰따옴표를 사용 합니다.

6. Visual Studio에서 방금 만든 파일에 .NET 어셈블리 참조를 추가 합니다.

## <a name="see-also"></a>참고자료

- [Al.exe](../../../framework/tools/al-exe-assembly-linker.md)
- [Sn.exe(강력한 이름 도구)](../../../framework/tools/sn-exe-strong-name-tool.md)
- [방법: 퍼블릭/프라이빗 키 쌍 만들기](../../../standard/assembly/create-public-private-key-pair.md)
- [의견 보내기](/visualstudio/ide/talk-to-us)
