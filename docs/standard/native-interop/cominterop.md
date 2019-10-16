---
title: .NET의 COM Interop
description: .NET에서 COM 라이브러리와 상호 운용하는 방법을 알아봅니다.
author: jkoritzinsky
ms.author: jekoritz
ms.date: 07/11/2019
ms.openlocfilehash: 9355e2ae84da623ffa725f5b2ac1bdee25b966d8
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68971889"
---
# <a name="com-interop-in-net"></a>.NET의 COM Interop

COM(구성 요소 개체 모델)을 통해 개체는 기능을 다른 구성 요소에 노출하고 Windows 플랫폼에서 애플리케이션을 호스트할 수 있습니다. 사용자가 기존 코드 베이스와 상호 운용할 수 있도록 .NET Framework에서는 COM 라이브러리와 항상 상호 운용할 수 있도록 강력한 지원 기능을 제공합니다. .NET Core 3.0에서 이 지원 기능의 대부분은 Windows의 .NET Core에 추가되었습니다. 이 설명서에서는 일반적인 COM interop 기술의 작동 방식 및 이를 활용하여 기존 COM 라이브러리와 상호 운용하는 방법을 설명합니다.

- [COM 래퍼](./com-wrappers.md)
- [COM 호출 가능 래퍼](./com-callable-wrapper.md)
- [런타임 호출 가능 래퍼](./runtime-callable-wrapper.md)
- [COM 상호 운용성을 위한 .NET 형식 정규화](./qualify-net-types-for-interoperation.md)
