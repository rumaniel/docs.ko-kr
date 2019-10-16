---
title: '방법: C#에서 애플리케이션에 여러 설정 집합 추가'
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], multiple sets
- application settings [Windows Forms], C#
ms.assetid: 45007ac6-cf07-4be7-bc38-3f0ef962faf9
ms.openlocfilehash: c6842d11c04e905d42734af939f2c3f0cfeacd47
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040121"
---
# <a name="how-to-add-multiple-sets-of-settings-to-your-application-in-c"></a>방법: C의 응용 프로그램에 여러 설정 집합 추가\#

응용 프로그램에서 여러 설정 집합을 사용할 수 있는 경우도 있습니다. 예를 들어 특정 설정 그룹이 자주 변경 될 것으로 예상 되는 응용 프로그램을 개발 하는 경우 해당 파일을 단일 파일로 분리 하 여 다른 설정을 영향을 받지 않는 상태로 유지 하는 것이 좋을 수 있습니다. Visual Studio에서는 여러 설정 집합을 프로젝트에 추가할 수 있습니다. 개체를 `Properties.Settings` 통해 추가 설정 집합에 액세스할 수 있습니다.

## <a name="add-an-additional-set-of-settings"></a>추가 설정 집합 추가

1. Visual Studio의 **프로젝트** 메뉴에서 **새 항목 추가**를 선택 합니다.

   **새 항목 추가** 대화 상자가 열립니다.

2. **새 항목 추가** 대화 상자에서 **설정 파일**을 선택 하 고 파일 이름을 입력 한 다음 **추가** 를 클릭 하 여 새 설정 파일을 솔루션에 추가 합니다.

3. **솔루션 탐색기**에서 새 설정 파일을 **속성** 폴더로 끌어 옵니다. 이렇게 하면 코드에서 새 설정을 사용할 수 있습니다.

4. 다른 설정 파일과 마찬가지로이 파일에서 설정을 추가 하 고 사용 합니다. 개체를 `Properties.Settings` 통해이 설정 그룹에 액세스할 수 있습니다.

## <a name="see-also"></a>참고자료

- [응용 프로그램 설정 및 사용자 설정 사용](using-application-settings-and-user-settings.md)
- [응용 프로그램 설정 개요](application-settings-overview.md)
