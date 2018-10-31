---
title: Regasm.exe(어셈블리 등록 도구)
ms.date: 03/30/2017
helpviewer_keywords:
- Assembly Registration tool
- assemblies [.NET Framework], registering
- Regasm.exe
- registering assemblies
ms.assetid: e190e342-36ef-4651-a0b4-0e8c2c0281cb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 30b13c75907ad0bc4d6dbce6a3ecd07f1fbede11
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48264436"
---
# <a name="regasmexe-assembly-registration-tool"></a>Regasm.exe(어셈블리 등록 도구)

어셈블리 등록 도구를 사용하면 어셈블리 내의 메타데이터를 읽고 필요한 엔트리를 레지스트리에 추가할 수 있습니다. 이렇게 하면 COM 클라이언트에서 .NET Framework 클래스를 투명하게 만들 수 있습니다. 클래스가 등록되고 나면 COM 클라이언트에서는 해당 클래스가 마치 COM 클래스인 것처럼 사용할 수 있습니다. 클래스는 어셈블리가 설치될 때 한 번만 등록됩니다. 클래스가 실제로 등록되어야만 COM에서 어셈블리 내의 클래스 인스턴스를 만들 수 있습니다.

도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트를 사용합니다. 자세한 내용은 [명령 프롬프트](../../../docs/framework/tools/developer-command-prompt-for-vs.md)를 참조하세요.

명령 프롬프트에 다음을 입력합니다.

## <a name="syntax"></a>구문

```
regasm assemblyFile [options]
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------------|-----------------|
|*assemblyFile*|COM을 사용하여 등록할 어셈블리를 나타냅니다.|

|옵션|설명|
|------------|-----------------|
|**/codebase**|레지스트리에 있는 코드베이스 엔트리를 만듭니다. 코드베이스 엔트리는 전역 어셈블리 캐시에 설치되지 않은 어셈블리에 대한 파일 경로를 지정합니다. 전역 어셈블리 캐시에 등록 중인 어셈블리를 다음에 설치하려면 이 옵션을 지정해야 합니다. **/codebase** 옵션을 사용하여 지정한 *assemblyFile* 인수는 [강력한 이름의 어셈블리](../../../docs/framework/app-domains/strong-named-assemblies.md)여야 합니다.|
|**/registered**|이 도구가 이미 등록된 형식 라이브러리만 참조하도록 지정합니다.|
|**/asmpath:directory**|어셈블리 참조가 들어 있는 디렉터리를 지정합니다. **/regfile** 옵션과 함께 사용해야 합니다.|
|**/nologo**|Microsoft 시작 배너를 표시하지 않습니다.|
|**/regfile** [**:** *regFile*]|어셈블리에 대해 필요한 레지스트리 항목이 들어 있는 지정된 .reg 파일을 생성합니다. 이 옵션을 지정할 경우 레지스트리는 변경되지 않습니다. 이 옵션은 **/u** 또는 **/tlb** 옵션과 함께 사용할 수 없습니다.|
|**/silent** 또는 **/s**|성공 메시지를 표시하지 않습니다.|
|**/tlb** [**:** *typeLibFile*]|어셈블리 내에 정의된 액세스 가능 형식에 대한 정의가 들어 있는 지정된 어셈블리에서 형식 라이브러리를 생성합니다.|
|**/unregister** 또는 **/u**|*assemblyFile*에 있는 생성 가능한 클래스를 등록 취소합니다. 이 옵션을 지정하지 않으면 Regasm.exe를 통해 해당 어셈블리의 생성 가능한 클래스가 등록됩니다.|
|**/verbose**|세부 정보 표시 모드를 지정합니다. 즉, **/tlb** 옵션과 함께 지정할 경우 형식 라이브러리가 생성되어야 하는 참조된 어셈블리의 목록을 표시합니다.|
|**/?** 또는 **/help**|이 도구의 명령 구문 및 옵션을 표시합니다.|

> [!NOTE]
> Regasm.exe의 명령줄 옵션은 대/소문자가 구분되지 않습니다. 따라서 옵션을 고유하게 식별할 수 있을 정도로만 옵션을 지정하면 됩니다. 예를 들어, **/n**은 **/nologo**와 같고, **/t:** *outfile.tlb*는 **/tlb:** *outfile.tlb*와 같습니다.

## <a name="remarks"></a>설명

**/regfile** 옵션을 사용하면 레지스트리를 직접 변경하는 대신 레지스트리 항목이 들어 있는 .ref 파일을 생성할 수 있습니다. 레지스트리 편집기 도구(Regedit.exe)를 사용하여 .reg 파일을 가져오면 시스템의 레지스트리를 업데이트할 수도 있습니다. 사용자 정의 등록 함수에서 수행되는 레지스트리 업데이트 내용은 .reg 파일에 포함되지 않습니다.  **/regfile** 옵션은 관리되는 클래스에 대한 레지스트리 항목만 내보냅니다.  이 옵션은 `TypeLibID` 또는 `InterfaceID`에 대한 항목은 내보내지 않습니다.

**/tlb** 옵션을 지정하면 Regasm.exe를 사용하여 해당 어셈블리에 있는 형식을 설명하는 형식 라이브러리를 생성 및 등록할 수 있습니다. 이렇게 생성된 형식 라이브러리는 현재 작업 디렉터리 또는 출력 파일에 대해 지정된 디렉터리에 포함됩니다. 다른 어셈블리를 참조하는 어셈블리에 대해 형식 라이브러리를 생성하면 한 번에 여러 개의 형식 라이브러리를 생성할 수 있습니다. 형식 라이브러리를 사용하여 Visual Studio와 같은 개발 도구에 형식 정보를 제공할 수 있습니다. 등록할 어셈블리가 형식 라이브러리 가져오기([Tlbimp.exe](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md))를 통해 만들어진 경우에는 **/tlb** 옵션을 사용하면 안 됩니다. 왜냐하면 형식 라이브러리에서 가져온 어셈블리에서는 형식 라이브러리를 내보낼 수 없기 때문입니다. **/tlb** 옵션을 사용하면 형식 라이브러리 내보내기([Tlbexp.exe](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md)) 및 Regasm.exe를 사용할 때와 같은 결과가 발생합니다. 그러나 Tlbexp.exe를 사용하여 생성한 형식 라이브러리는 등록할 수 없습니다.  **/tlb** 옵션을 사용하여 형식 라이브러리를 등록한 경우 **/tlb** 옵션을 **/unregister** 옵션과 함께 사용하여 해당 형식 라이브러리의 등록을 취소할 수 있습니다. 이 두 옵션을 함께 사용하면 형식 라이브러리 및 인터페이스 항목의 등록이 취소되며 이로 인해 레지스트리가 상당히 정리될 수 있습니다.

COM에서 사용할 수 있게 어셈블리를 등록하면 Regasm.exe는 로컬 컴퓨터의 레지스트리에 항목을 추가합니다. 좀 더 구체적으로 말하면 한 대의 컴퓨터에서 동일한 어셈블리의 여러 버전을 side by side 방식으로 실행할 수 있도록 하는 버전별 레지스트리 키를 만듭니다. 처음 어셈블리가 등록되면 어셈블리에 대해 하나의 최상위 수준 키가 만들어지고 특정 버전에 대해 고유한 하위 키가 만들어집니다. 새 버전의 어셈블리를 등록할 때마다 Regasm.exe는 새 버전에 대한 하위 키를 만듭니다.

예를 들어, COM에서 사용하기 위해 관리되는 구성 요소 myComp.dll 버전 1.0.0.0을 등록한다고 가정해 봅시다. 나중에 myComp.dll, 버전 2.0.0.0을 등록할 수 있습니다. 컴퓨터의 모든 COM 클라이언트 응용 프로그램이 myComp.dll 버전 2.0.0.0을 사용하기로 하고 myComponent.dll 버전 1.0.0.0은 등록 해제하기로 했습니다. 이 레지스트리 스키마를 사용하면 버전 1.0.0.0 하위 키만 제거되므로 myComp.dll 버전 1.0.0.0을 등록 해제할 수 있습니다.

Regasm.exe를 사용하여 어셈블리를 등록한 다음에는 COM 클라이언트에서 해당 어셈블리를 활성화할 수 있도록 [전역 어셈블리 캐시](../../../docs/framework/app-domains/gac.md)에 설치할 수 있습니다. 어셈블리가 한 응용 프로그램에서만 활성화되도록 하려면 해당 응용 프로그램의 디렉터리에 어셈블리를 포함하면 됩니다.

## <a name="examples"></a>예제

다음 명령을 사용하여 `myTest.dll`에 들어 있는 모든 공용 클래스를 등록합니다.

```
regasm myTest.dll
```

다음 명령을 사용하여 필요한 모든 레지스트리 항목이 들어 있는 `myTest.reg` 파일을 생성합니다. 그러나 레지스트리는 업데이트되지 않습니다.

```
regasm myTest.dll /regfile:myTest.reg
```

다음 명령을 사용하여 `myTest.dll`에 들어 있는 모든 공용 클래스를 등록하고, `myTest.tlb`에 정의된 모든 공용 형식에 대한 정의가 들어 있는 형식 라이브러리 `myTest.dll`를 생성 및 등록합니다.

```
regasm myTest.dll /tlb:myTest.tlb
```

## <a name="see-also"></a>참고 항목

- [도구](../../../docs/framework/tools/index.md)
- [Tlbexp.exe(형식 라이브러리 내보내기)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md)
- [Tlbimp.exe(형식 라이브러리 가져오기)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)
- [COM에 어셈블리 등록](../../../docs/framework/interop/registering-assemblies-with-com.md)
- [명령 프롬프트](../../../docs/framework/tools/developer-command-prompt-for-vs.md)
