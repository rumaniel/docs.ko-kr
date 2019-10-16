---
title: 격리 유형
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- storing data using isolated storage, accessing isolated storage
- storing data using isolated storage, isolation types
- authentication [.NET Framework], isolated storage
- assemblies [.NET Framework], identity
- isolated storage, accessing
- data storage using isolated storage, isolation types
- data storage using isolated storage, accessing isolated storage
- domain identity
- isolated storage, types
- user authentication, isolated storage
ms.assetid: 14812988-473f-44ae-b75f-fd5c2f21fb7b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c6c5337fedd13cb18b8e5eeadec48a2e4695a543
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70969349"
---
# <a name="types-of-isolation"></a>격리 유형
격리된 스토리지에 대한 액세스는 항상 스토리지를 만든 사용자로 제한됩니다. 이 유형의 격리를 구현하기 위해 공용 언어 런타임은 운영 체제에서 인식하고 저장소가 열릴 때 코드가 실행 중인 프로세스에 연결된 ID인 사용자 ID의 동일한 표기법을 사용합니다. 이 ID는 인증된 사용자 ID이지만 가장으로 인해 현재 사용자의 ID가 동적으로 변경될 수 있습니다.  
  
 격리된 스토리지에 대한 액세스는 애플리케이션의 도메인 및 어셈블리에 연결되거나 어셈블리에만 연결된 ID에 따라 제한됩니다. 런타임은 다음과 같은 방법으로 이러한 ID를 얻습니다.  
  
- 도메인 ID는 애플리케이션의 증거를 나타내며 웹 애플리케이션의 경우 전체 URL일 수 있습니다. 셸에 호스트된 코드의 경우 도메인 ID는 애플리케이션 디렉터리 경로를 기반으로 할 수 있습니다. 예를 들어 실행 파일이 C:\Office\MyApp.exe 경로에서 실행되는 경우 도메인 ID는 C:\Office\MyApp.exe입니다.  
  
- 어셈블리 ID는 어셈블리의 증거입니다. 이 ID는 암호화 디지털 서명에서 가져올 수 있고 어셈블리의 [강력한 이름](../assembly/strong-named.md), 어셈블리의 소프트웨어 게시자 또는 해당 URL ID가 사용될 수 있습니다. 어셈블리에 강력한 이름과 소프트웨어 게시자 ID가 모두 있는 경우 소프트웨어 게시자 ID가 사용됩니다. 어셈블리를 인터넷에서 가져오고 서명이 없는 경우 URL ID가 사용됩니다. 어셈블리 및 강력한 이름에 대한 자세한 내용은 [어셈블리를 사용한 프로그래밍](../assembly/program.md)을 참조하세요.  
  
- 로밍 저장소는 로밍 사용자 프로필이 있는 사용자와 함께 이동됩니다. 파일은 네트워크 디렉터리에 기록되고 사용자가 로그인한 컴퓨터로 다운로드됩니다. 로밍 사용자 프로필에 대한 자세한 내용은 <xref:System.IO.IsolatedStorage.IsolatedStorageScope.Roaming?displayProperty=nameWithType>을 참조하세요.  
  
 사용자, 도메인 및 어셈블리 ID의 개념을 결합하면 격리된 스토리지가 다음 방법으로 데이터를 격리할 수 있으며 각 방법에는 고유한 사용 시나리오가 있습니다.  
  
- [사용자 및 어셈블리별 격리](#UserAssembly)  
  
- [사용자, 도메인 및 어셈블리별 격리](#UserDomainAssembly)  
  
 이러한 경리 중 하나가 로밍 사용자 프로필과 결합될 수 있습니다. 자세한 내용은 [격리된 스토리지 및 로밍](#Roaming) 섹션을 참조하세요.  
  
 다음 그림은 저장소를 여러 범위로 격리하는 방법을 보여줍니다.  
  
 ![사용자 및 어셈블리별 격리를 보여주는 다이어그램](./media/types-of-isolation/isolated-storage-types.gif)  
  
 로밍 저장소를 제외하고 격리된 스토리지는 지정된 컴퓨터에 로컬인 스토리지 시설을 사용하므로 항상 컴퓨터에서 암시적으로 격리됩니다.  
  
> [!IMPORTANT]
> [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱에는 격리된 스토리지를 사용할 수 없습니다. 대신에 Windows Runtime API에 포함된 `Windows.Storage` 네임스페이스의 애플리케이션 데이터 클래스를 사용하여 로컬 데이터 및 파일을 저장합니다. 자세한 내용은 Windows 개발자 센터에서 [애플리케이션 데이터](https://docs.microsoft.com/previous-versions/windows/apps/hh464917(v=win.10)) 를 참조하세요.  
  
<a name="UserAssembly"></a>   
## <a name="isolation-by-user-and-assembly"></a>사용자 및 어셈블리별 격리  
 데이터 저장소를 사용하는 어셈블리를 애플리케이션 도메인에서 액세스할 수 있어야 하는 경우 사용자 및 어셈블리별로 격리하는 것이 적절합니다. 일반적으로 이 상황에서 격리된 스토리지는 여러 애플리케이션에 적용되는 데이터를 저장하는 데 사용되며 사용자 이름 또는 라이선스 정보와 같은 특정 애플리케이션에 연결되지 않습니다. 사용자 및 어셈블리별로 격리된 스토리지에 액세스하려면 애플리케이션 간에 정보를 전송하기 위해 코드를 신뢰할 수 있어야 합니다. 일반적으로 사용자 및 어셈블리별 격리는 인트라넷에서 허용되지만 인터넷에는 허용되지 않습니다. 정적 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A?displayProperty=nameWithType> 메서드를 호출하고 사용자 및 어셈블리로 전달하면 <xref:System.IO.IsolatedStorage.IsolatedStorageScope>는 이 유형의 격리를 통해 스토리지를 반환합니다.  
  
 다음 코드 예제에서는 사용자 및 어셈블리별로 격리되는 저장소를 검색합니다. `isoFile` 개체를 통해 저장소에 액세스할 수 있습니다.  
  
 [!code-cpp[Conceptual.IsolatedStorage#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source11.cpp#17)]
 [!code-csharp[Conceptual.IsolatedStorage#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source11.cs#17)]
 [!code-vb[Conceptual.IsolatedStorage#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source11.vb#17)]  
  
 증거 매개 변수를 사용하는 예제는 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%28System.IO.IsolatedStorage.IsolatedStorageScope%2CSystem.Security.Policy.Evidence%2CSystem.Type%2CSystem.Security.Policy.Evidence%2CSystem.Type%29>을 참조하세요.  
  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A> 메서드는 다음 코드 예제와 같이 바로 가기로 사용할 수 있습니다. 이 바로 가기는 로밍할 수 있는 저장소를 여는 데 사용할 수 없습니다. 이 경우에는 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>를 사용합니다.  
  
 [!code-cpp[Conceptual.IsolatedStorage#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source11.cpp#18)]
 [!code-csharp[Conceptual.IsolatedStorage#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source11.cs#18)]
 [!code-vb[Conceptual.IsolatedStorage#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source11.vb#18)]  
  
<a name="UserDomainAssembly"></a>   
## <a name="isolation-by-user-domain-and-assembly"></a>사용자, 도메인 및 어셈블리별 격리  
 애플리케이션에서 개인 데이터 스토리지가 필요한 타사 어셈블리를 사용하는 경우 격리된 스토리지를 사용하여 개인 데이터를 저장할 수 있습니다. 사용자, 도메인 및 어셈블리별 격리를 사용하면 어셈블리가 저장소를 만들 때 실행 중이던 애플리케이션에서 어셈블리가 사용될 경우 및 저장소를 만든 사용자가 애플리케이션을 실행하는 경우에만 지정된 어셈블리의 코드만 해당 데이터에 액세스할 수 있습니다. 사용자, 도메인 및 어셈블리별 격리를 사용하면 타사 어셈블리에 의해 데이터가 다른 애플리케이션으로 누출되지 않습니다. 격리된 스토리지를 사용하려고 하지만 어떤 격리 유형을 사용할지 확신할 수 없는 경우에는 기본적으로 이 격리 유형을 선택해야 합니다. <xref:System.IO.IsolatedStorage.IsolatedStorageFile>의 정적 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> 메서드를 호출하고 사용자, 도메인 및 어셈블리로 전달하면 <xref:System.IO.IsolatedStorage.IsolatedStorageScope>는 이 유형의 격리를 통해 스토리지를 반환합니다.  
  
 다음 코드 예제에서는 사용자, 도메인 및 어셈블리별로 격리되는 저장소를 검색합니다. `isoFile` 개체를 통해 저장소에 액세스할 수 있습니다.  
  
 [!code-cpp[Conceptual.IsolatedStorage#14](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source10.cpp#14)]
 [!code-csharp[Conceptual.IsolatedStorage#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source10.cs#14)]
 [!code-vb[Conceptual.IsolatedStorage#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source10.vb#14)]  
  
 또 다른 메서드는 다음 코드 예제와 같이 바로 가기로 사용할 수 있습니다. 이 바로 가기는 로밍할 수 있는 저장소를 여는 데 사용할 수 없습니다. 이 경우에는 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>를 사용합니다.  
  
 [!code-cpp[Conceptual.IsolatedStorage#15](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source10.cpp#15)]
 [!code-csharp[Conceptual.IsolatedStorage#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source10.cs#15)]
 [!code-vb[Conceptual.IsolatedStorage#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source10.vb#15)]  
  
<a name="Roaming"></a>   
## <a name="isolated-storage-and-roaming"></a>격리된 스토리지 및 로밍  
 로밍 사용자 프로필은 사용자가 네트워크에서 ID를 설정하고 해당 ID를 사용하여 모든 개인 설정을 적용하여 네트워크 컴퓨터에 로그인하도록 하는 Windows 기능입니다. 격리된 스토리지를 사용하는 어셈블리는 사용자의 격리된 스토리지가 로밍 사용자 프로필과 함께 이동되도록 지정할 수 있습니다. 로밍은 사용자 및 어셈블리별 격리 및 사용자, 도메인 및 어셈블리별 격리와 함께 사용할 수 있습니다. 로밍 범위를 사용하지 않으면 로밍 사용자 프로필이 사용되는 경우에도 저장소가 로밍되지 않습니다.  
  
 다음 코드 예제에서는 사용자 및 어셈블리별로 격리된 로밍 저장소를 검색합니다. `isoFile` 개체를 통해 저장소에 액세스할 수 있습니다.  
  
 [!code-cpp[Conceptual.IsolatedStorage#11](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source9.cpp#11)]
 [!code-csharp[Conceptual.IsolatedStorage#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source9.cs#11)]
 [!code-vb[Conceptual.IsolatedStorage#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source9.vb#11)]  
  
 사용자, 도메인 및 애플리케이션별로 격리된 로밍 저장소를 만들 위해 도메인 범위를 추가할 수 있습니다. 다음 코드 예제에서는 이 작업을 보여줍니다.  
  
 [!code-cpp[Conceptual.IsolatedStorage#12](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source9.cpp#12)]
 [!code-csharp[Conceptual.IsolatedStorage#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source9.cs#12)]
 [!code-vb[Conceptual.IsolatedStorage#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source9.vb#12)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO.IsolatedStorage.IsolatedStorageScope>
- [격리된 스토리지](../../../docs/standard/io/isolated-storage.md)
