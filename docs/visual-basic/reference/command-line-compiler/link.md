---
title: -link (Visual Basic)
ms.date: 03/10/2018
helpviewer_keywords:
- l compiler option [Visual Basic]
- EmbedInteropTypes
- embed interop types [COM Interop]
- -link compiler option [Visual Basic]
- /link compiler option [Visual Basic]
- link compiler option [Visual Basic]
- -l compiler option [Visual Basic]
- /l compiler option [Visual Basic]
ms.assetid: 1885f24a-86f5-486c-a064-9fb7e455ccec
ms.openlocfilehash: e131b39e05badf0bb90fbbb14761571003156f85
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005517"
---
# <a name="-link-visual-basic"></a>-link (Visual Basic)
컴파일러에서 지정된 어셈블리의 COM 형식 정보를 현재 컴파일하고 있는 프로젝트에 사용할 수 있도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-link:fileList  
```

로 구분하거나 여러  

```console
-l:fileList  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`fileList`|필수. 쉼표로 구분된 어셈블리 파일 이름 목록입니다. 파일 이름에 공백이 있으면 이름을 따옴표로 묶습니다.|  
  
## <a name="remarks"></a>설명  
 `-link` 옵션을 사용하면 포함된 형식 정보가 있는 애플리케이션을 배포할 수 있습니다. 그러면 애플리케이션은 런타임 어셈블리에 대한 참조를 요구하지 않고 포함된 형식 정보를 구현하는 형식을 런타임 어셈블리에서 사용할 수 있습니다. 다양한 버전의 런타임 어셈블리가 게시된 경우 포함된 형식 정보를 포함하는 애플리케이션은 다시 컴파일하지 않아도 다양한 버전에서 사용할 수 있습니다. 예제를 보려면 [연습: 관리되는 어셈블리의 형식 포함](../../../standard/assembly/embed-types-visual-studio.md)을 참조하세요.  
  
 `-link` 옵션을 사용하면 COM interop를 사용하여 작업할 때 특히 유용합니다. 애플리케이션에 대상 컴퓨터의 PIA(주 interop 어셈블리)가 더 이상 필요하지 않도록 COM 형식을 포함할 수 있습니다. `-link` 옵션은 참조된 interop 어셈블리의 COM 형식 정보를 컴파일된 결과 코드에 포함하도록 컴파일러에 지시합니다. COM 형식은 CLSID(GUID) 값으로 식별됩니다. 따라서 동일한 CLSID 값을 갖는 동일한 COM 형식이 설치된 대상 컴퓨터에서 애플리케이션을 실행할 수 있습니다. Microsoft Office를 자동화하는 애플리케이션이 좋은 예입니다. Office와 같은 애플리케이션은 일반적으로 여러 버전에서 동일한 CLSID 값을 유지하지 때문에 .NET Framework 4 이상이 대상 컴퓨터에 설치되어 있고 애플리케이션이 참조된 COM 형식에 포함된 메서드, 속성 또는 이벤트를 사용하는 한 애플리케이션에서 참조된 COM 형식을 사용할 수 있습니다.  
  
 `-link` 옵션은 인터페이스, 구조체 및 대리자만 포함합니다. COM 클래스는 포함할 수 없습니다.  
  
> [!NOTE]
> 코드에서 포함된 COM 형식의 인스턴스를 만드는 경우 적절한 인터페이스를 사용하여 인스턴스를 만들어야 합니다. CoClass를 사용하여 포함된 COM 형식의 인스턴스를 만들려고 하면 오류가 발생합니다.  
  
 Visual Studio에서 `-link` 옵션을 설정하려면 어셈블리 참조를 추가하고 `Embed Interop Types` 속성을 **true**로 설정합니다. `Embed Interop Types` 속성의 기본값은 **false**입니다.  
  
 COM 어셈블리 자체가 또 다른 COM 어셈블리(어셈블리 B)를 참조하는 COM 어셈블리(어셈블리 A)에 연결하는 경우 다음 중 하나에 해당되면 어셈블리 B에도 연결해야 합니다.  
  
- 어셈블리 A의 형식은 형식에서 상속되거나 어셈블리 B의 인터페이스를 구현합니다.  
  
- 어셈블리 B의 반환 형식이나 매개 변수 형식을 사용하는 필드, 속성, 이벤트 또는 메서드가 호출됩니다.  
  
 하나 이상의 어셈블리 참조가 있는 디렉터리를 지정 하려면 [-libpath](libpath.md) 을 사용 합니다.  
  
 [/Reference](reference.md) 컴파일러 옵션과 마찬가지로 @no__t 컴파일러 옵션은 일반적으로 사용 되는 .NET Framework 어셈블리를 참조 하는 vbc.exe 지시 파일을 사용 합니다. 컴파일러가 Vbc.rsp 파일을 사용 하지 않도록 하려면 [-noconfig](noconfig.md) 컴파일러 옵션을 사용 합니다.  
  
 `-link`의 약식은 `-l`입니다.  
  
## <a name="generics-and-embedded-types"></a>제네릭 및 포함된 형식  
 다음 섹션에서는 interop 형식을 포함하는 애플리케이션에서 제네릭 형식을 사용할 경우의 제한 사항에 대해 설명합니다.  
  
### <a name="generic-interfaces"></a>제네릭 인터페이스  
 interop 어셈블리에서 포함되는 제네릭 인터페이스는 사용할 수 없습니다. 이는 다음 예에서 확인할 수 있습니다.  
  
 [!code-vb[VbLinkCompiler#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vblinkcompiler/vb/module1.vb#1)]  
  
### <a name="types-that-have-generic-parameters"></a>제네릭 매개 변수가 있는 형식  
 형식이 interop 어셈블리에서 포함된 제네릭 매개 변수가 있는 형식은 해당 형식이 외부 어셈블리에서 제공된 경우 사용할 수 없습니다. 인터페이스에는 이 제한이 적용되지 않습니다. 예를 들어 <xref:Microsoft.Office.Interop.Excel> 어셈블리에 정의된 <xref:Microsoft.Office.Interop.Excel.Range> 인터페이스를 살펴보세요. 다음 코드 예제와 같이 라이브러리가 <xref:Microsoft.Office.Interop.Excel> 어셈블리의 interop 형식을 포함하고 형식이 <xref:Microsoft.Office.Interop.Excel.Range> 인터페이스인 매개 변수가 있는 제네릭 형식을 반환하는 메서드를 노출하는 경우 해당 메서드는 제네릭 인터페이스를 반환해야 합니다.  
  
 [!code-vb[VbLinkCompiler#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vblinkcompiler/vb/utility.vb#2)]  
[!code-vb[VbLinkCompiler#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vblinkcompiler/vb/utility.vb#3)]  
[!code-vb[VbLinkCompiler#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vblinkcompiler/vb/utility.vb#4)]  
  
 다음 예제에서 클라이언트 코드는 <xref:System.Collections.IList> 제네릭 인터페이스를 반환하는 메서드를 오류 없이 호출할 수 있습니다.  
  
 [!code-vb[VbLinkCompiler#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vblinkcompiler/vb/module1.vb#5)]  
  
## <a name="example"></a>예제  
 다음 명령줄은 `COMData1.dll` 및 `COMData2.dll`의 소스 파일 `OfficeApp.vb` 및 참조 어셈블리를 컴파일하여-3 @no__t을 생성 합니다.  
  
```console  
vbc -link:COMData1.dll,COMData2.dll /out:OfficeApp.exe OfficeApp.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](index.md)
- [연습: 관리되는 어셈블리의 형식 포함](../../../standard/assembly/embed-types-visual-studio.md)
- [-reference (Visual Basic)](reference.md)
- [-noconfig](noconfig.md)
- [-libpath](libpath.md)
- [샘플 컴파일 명령줄](sample-compilation-command-lines.md)
- [COM Interop 소개](../../../visual-basic/programming-guide/com-interop/introduction-to-com-interop.md)
