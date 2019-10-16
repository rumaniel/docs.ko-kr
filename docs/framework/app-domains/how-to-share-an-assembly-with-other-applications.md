---
title: '방법: 다른 애플리케이션과 어셈블리 공유'
ms.date: 08/19/2019
ms.assetid: c30e972b-1693-4e05-b115-c31831fdf9f2
ms.openlocfilehash: b1ef195458dd2de95eeb5e25089339e55d9e3fbb
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972884"
---
# <a name="how-to-share-an-assembly-with-other-applications"></a>방법: 다른 애플리케이션과 어셈블리 공유
어셈블리는 전용이거나 공유될 수 있습니다. 기본적으로 대부분의 간단한 프로그램은 다른 애플리케이션에서 사용되지 않으므로 프라이빗 어셈블리로 구성됩니다.  

다른 애플리케이션과 어셈블리를 공유하려면 [전역 어셈블리 캐시(GAC)](gac.md)에 배치해야 합니다.  
  
어셈블리를 공유하려면:
  
1. 어셈블리를 만듭니다. 자세한 내용은 [어셈블리 만들기](../../standard/assembly/create.md)를 참조하세요.  
  
2. 어셈블리에 강력한 이름을 할당합니다. 자세한 내용은 [방법: 강력한 이름으로 어셈블리 서명](../../standard/assembly/sign-strong-name.md)을 참조하세요.  
  
3. 어셈블리에 버전 정보를 할당합니다. 자세한 내용은 [어셈블리 버전 관리](../../standard/assembly/versioning.md)를 참조하세요.  
  
4. 전역 어셈블리 캐시에 어셈블리를 추가합니다. 자세한 내용은 [방법: 전역 어셈블리 캐시에 어셈블리 설치](install-assembly-into-gac.md)를 참조하세요.  
  
5. 다른 애플리케이션에서 어셈블리에 포함된 형식에 액세스합니다. 자세한 내용은 [방법: 강력한 이름의 어셈블리 참조](../../standard/assembly/reference-strong-named.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../../../api/index.md)
- [프로그래밍 개념(Visual Basic)](../../../api/index.md)
- [어셈블리를 사용한 프로그램](../../standard/assembly/program.md)
