---
title: COM Interop 소개(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- interop assemblies
- COM interop [Visual Basic], about COM interop
ms.assetid: 8bd62e68-383d-407f-998b-29aa0ce0fd67
ms.openlocfilehash: 5eb862d75f8870da40af4cd817fa32a3d2781f38
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592725"
---
# <a name="introduction-to-com-interop-visual-basic"></a>COM Interop 소개(Visual Basic)
구성 요소 개체 모델 (COM) 응용 프로그램을 호스트 하는 다른 구성 요소에 해당 기능을 노출 하는 개체 수 있습니다. COM 개체 수년간 프로그래밍 Windows 기초 였을 동안 응용 프로그램은 CLR (공용 언어 런타임)을 위한 많은 이점을 제공 합니다.  
  
 .NET framework 응용 프로그램은 결국 대체 com 개발 그때 까지는 Visual Studio를 사용 하 여 COM 개체를 만들거나 사용 해야 합니다. COM 상호 운용성 이나 *COM interop*, 자신의 진도에.NET Framework로 전환 하는 동안 기존 COM 개체를 사용할 수 있습니다.  
  
 COM 구성 요소를 만드는.NET Framework를 사용 하 여 등록이 필요 없는 COM interop을 사용할 수 있습니다. 이 기능을 사용 하면 둘 이상의 버전이 컴퓨터에 설치 되어 있고 사용할 수 있도록 최종 XCOPY 또는 FTP 복사 컴퓨터에 적절 한 디렉터리를 응용 프로그램을 실행할 수 있는 경우에 DLL 버전을 사용할 수를 제어할 수 있습니다. 자세한 내용은 [등록이 필요 없는 COM Interop](../../../framework/interop/registration-free-com-interop.md)합니다.  
  
## <a name="managed-code-and-data"></a>관리 코드 및 데이터  
 .NET Framework 라고 코드 개발 *관리 코드*, CLR에서 사용 되는 메타 데이터를 포함 합니다. .NET Framework 응용 프로그램에서 사용 되는 데이터 라고 *관리 되는 데이터* 런타임에 할당 및 메모리를 회수 하 고 수행 형식 검사와 같은 데이터 관련 작업을 관리 하기 때문입니다. 기본적으로 Visual Basic.NET 관리 코드와 데이터를 사용 하지만 관리 되지 않는 코드 및 interop 어셈블리 (이 페이지 뒷부분 설명 됨)를 사용 하 여 COM 개체의 데이터에 액세스할 수 있습니다.  
  
## <a name="assemblies"></a>어셈블리  
 어셈블리는.NET Framework 응용 프로그램의 기본 빌딩 블록. 작성, 버전 지정 및 하나 이상의 파일이 포함 된 단일 구현 단위로 배포 되는 기능 컬렉션입니다. 각 어셈블리는 어셈블리 매니페스트를 포함합니다.  
  
## <a name="type-libraries-and-assembly-manifests"></a>형식 라이브러리와 어셈블리 매니페스트  
 형식 라이브러리 멤버 이름 및 데이터 형식과 같은 COM 개체의 특성을 설명 합니다. 어셈블리 매니페스트는.NET Framework 응용 프로그램에 대 한 동일한 기능을 수행 합니다. 이들은 다음에 대 한 정보:  
  
- 어셈블리 id, 버전, 문화권 및 디지털 서명 합니다.  
  
- 어셈블리 구현을 구성 하는 파일입니다.  
  
- 형식 및 어셈블리를 구성 하는 리소스입니다. 여기에서 내보내는 것입니다.  
  
- 다른 어셈블리의 컴파일 시간 종속성입니다.  
  
- 올바르게 실행 하는 어셈블리에 필요한 사용 권한입니다.  
  
 어셈블리 및 어셈블리 매니페스트에 대 한 자세한 내용은 참조 하세요. [.net에서 어셈블리](../../../standard/assembly/index.md)합니다.  
  
### <a name="importing-and-exporting-type-libraries"></a>가져오기 및 형식 라이브러리 내보내기  
 Visual Studio에는 형식 라이브러리에서.NET Framework 응용 프로그램에 정보를 가져올 수 있도록 Tlbimp 유틸리티를 포함 합니다. Tlbexp 유틸리티를 사용 하 여 어셈블리에서 형식 라이브러리를 생성할 수 있습니다.  
  
 Tlbimp와 Tlbexp에 대 한 정보를 참조 하세요 [Tlbimp.exe (형식 라이브러리 가져오기)](../../../framework/tools/tlbimp-exe-type-library-importer.md) 하 고 [Tlbexp.exe (형식 라이브러리 내보내기)](../../../framework/tools/tlbexp-exe-type-library-exporter.md)합니다.  
  
## <a name="interop-assemblies"></a>Interop 어셈블리  
 Interop 어셈블리는.NET Framework 어셈블리 간의 브리지 관리 및 비관리 코드에 해당 하는.NET Framework에 COM 개체의 멤버 매핑 멤버를 관리 합니다. Interop 어셈블리를 Visual Basic.NET에서 만든 다양 한 상호 운용성 마샬링 같은 COM 개체를 사용 하 여 작업의 세부 정보를 처리 합니다.  
  
## <a name="interoperability-marshaling"></a>상호 운용성 마샬링  
 모든.NET Framework 응용 프로그램에 사용 되는 프로그래밍 언어에 관계 없이 개체의 상호 운용성을 사용 하도록 설정 하는 공통 형식 집합을 공유 합니다. 매개 변수 및 COM 개체의 반환 값의 경우 관리 코드에서 사용 되는 데이터 형식을 사용 하는 경우가 종종 합니다. *상호 운용성 마샬링* COM 개체에서 이동 하는 프로세스 패키징 매개 변수와 동일한 데이터 형식으로 반환 값입니다. 자세한 내용은 [Interop 마샬링](../../../framework/interop/interop-marshaling.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)
- [연습: COM 개체를 사용한 상속 구현](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)
- [비관리 코드와의 상호 운용](../../../framework/interop/index.md)
- [상호 운용성 문제 해결](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)
- [.NET 어셈블리](../../../standard/assembly/index.md)
- [Tlbimp.exe(형식 라이브러리 가져오기)](../../../framework/tools/tlbimp-exe-type-library-importer.md)
- [Tlbexp.exe(형식 라이브러리 내보내기)](../../../framework/tools/tlbexp-exe-type-library-exporter.md)
- [interop 마샬링](../../../framework/interop/interop-marshaling.md)
- [등록이 필요 없는 COM interop](../../../framework/interop/registration-free-com-interop.md)
