---
title: 복사 및 고정
ms.date: 03/30/2017
helpviewer_keywords:
- pinning, interop marshaling
- copying, interop marshaling
- interop marshaling, copying
- interop marshaling, pinning
ms.assetid: 0059f576-e460-4e70-b257-668870e420b8
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 90ed12862c4cadc45777150deb1b9f91f111bf41
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64750505"
---
# <a name="copying-and-pinning"></a>복사 및 고정

데이터를 마샬링할 때 interop 마샬러는 마샬링되는 데이터를 복사 또는 고정할 수 있습니다. 데이터를 복사하면 한 메모리 위치의 데이터 복사본이 또 다른 메모리 위치에 배치됩니다. 다음 그림에서는 값 형식 복사와 관리되는 메모리에서 관리되지 않는 메모리로 참조를 통해 전달되는 형식 복사의 차이점을 보여 줍니다.

![값 및 참조 형식을 복사하는 방법을 보여 주는 다이어그램입니다.](./media/copying-and-pinning/interop-marshal-copy.gif)

값으로 전달되는 메서드 인수는 스택의 값으로 비관리 코드에 마샬링됩니다. 복사는 직접 프로세스입니다. 참조로 전달된 인수는 스택의 포인터로 전달됩니다. 참조 형식도 값 및 참조로 전달됩니다. 다음 그림과 같이 값으로 전달되는 참조 형식은 복사 또는 고정됩니다.

![값 및 참조로 전달되는 참조 형식을 보여 주는 다이어그램입니다.](./media/copying-and-pinning/interop-marshal-reference-pin.gif)

고정 작업은 현재 메모리 위치에서 데이터를 일시적으로 잠그므로 공용 언어 런타임의 가비지 수집기에 의해 데이터가 재배치되지 않습니다. 마샬러는 데이터를 고정하여 복사 오버헤드를 줄이고 성능을 개선합니다. 데이터 형식에 따라 마샬링 프로세스 중에 복사 또는 고정되는지 결정됩니다.  고정 작업은 <xref:System.String> 같은 개체의 마샬링 중에 수행되지만 <xref:System.Runtime.InteropServices.GCHandle> 클래스를 사용하여 메모리를 수동으로 고정할 수도 있습니다.

## <a name="formatted-blittable-classes"></a>서식 있는 Blittable 클래스

서식 있는 [blittable](blittable-and-non-blittable-types.md) 클래스의 경우 수정된 레이아웃(서식 있음)을 포함하고 관리되는 메모리와 관리되지 않는 메모리에서 모두 공통적인 데이터 표현을 사용합니다. 이러한 형식에 마샬링이 필요하면 힙의 개체 포인터가 호출 수신자에게 직접 전달됩니다. 호출 수신자는 포인터로 참조되는 메모리 위치의 콘텐츠를 변경할 수 있습니다.

> [!NOTE]
> 매개 변수가 Out 또는 In/Out으로 표시된 경우 호출 수신자는 메모리 콘텐츠를 변경할 수 있습니다. 반면 호출 수신자는 매개 변수가 In(서식 있는 blittable 형식의 기본값)으로 마샬링되도록 설정된 경우 콘텐츠 변경을 피해야 합니다. In 개체를 수정하면 같은 클래스를 형식 라이브러리로 내보내고 아파트 간 호출을 수행하는 데 사용할 경우 문제가 발생합니다.

## <a name="formatted-non-blittable-classes"></a>서식 있는 비 Blittable 클래스

서식 있는 비 [blittable](blittable-and-non-blittable-types.md) 클래스의 경우 수정된 레이아웃(서식 있음)을 포함하지만 관리되는 메모리와 관리되지 않는 메모리에서 서로 다른 데이터 표현을 사용합니다. 다음 조건에서는 데이터를 변환해야 할 수 있습니다.

- 비 blittable 클래스가 값으로 마샬링될 경우 호출 수신자는 데이터 구조의 복사본 포인터를 받습니다.

- 비 blittable 클래스가 참조로 마샬링될 경우 호출 수신자는 데이터 구조의 복사본 포인터에 대한 포인터를 받습니다.

- <xref:System.Runtime.InteropServices.InAttribute> 특성이 설정되면 이 복사본은 항상 인스턴스 상태로 초기화되고 필요에 따라 마샬링됩니다.

- <xref:System.Runtime.InteropServices.OutAttribute> 특성이 설정되면 반환 시 항상 상태가 인스턴스로 다시 복사되고 필요에 따라 마샬링됩니다.

- **InAttribute** 및 **OutAttribute**가 둘 다 설정되면 두 복사본이 모두 필요합니다. 한쪽 특성이 생략되면 마샬러는 한쪽 복사본을 제거하여 최적화할 수 있습니다.

## <a name="reference-types"></a>참조 형식

참조 형식은 값 또는 참조로 전달될 수 있습니다. 참조 형식이 값으로 전달되면 형식 포인터가 스택에 전달됩니다. 참조로 전달될 경우 형식 포인터에 대한 포인터가 스택에 전달됩니다.

참조 형식에는 다음과 같은 조건부 동작이 있습니다.

- 참조 형식이 값으로 전달되고 비 blittable 형식의 멤버를 포함할 경우 형식은 두 번 변환됩니다.

  - 인수가 관리되지 않는 쪽에 전달될 경우.

  - 호출에서 반환 시.

  불필요한 복사와 변환을 피하기 위해 이러한 형식은 In 매개 변수로 마샬링됩니다. 호출자가 호출 수신자에 의한 변경 내용을 보려면 **InAttribute** 및 **OutAttribute** 특성을 인수에 명시적으로 적용해야 합니다.

- 참조 형식이 값으로 전달되고 blittable 형식의 멤버만 포함할 경우 형식이 마샬링 중에 고정될 수 있고 호출자는 호출 수신자에 의한 형식 멤버의 변경 내용을 볼 수 있습니다. 이 동작이 필요한 경우 **InAttribute** 및 **OutAttribute**를 명시적으로 적용합니다. 방향 특성을 사용하지 않으면 interop 마샬러가 방향 정보를 형식 라이브러리에 내보내지 않고(기본값인 In으로 내보냄), 이로 인해 COM 아파트 간 마샬링에 관련된 문제가 발생할 수 있습니다.

- 참조 형식이 참조로 전달되면 형식은 기본적으로 In/Out으로 마샬링됩니다.

## <a name="systemstring-and-systemtextstringbuilder"></a>System.String 및 System.Text.StringBuilder

데이터가 비관리 코드에 값 또는 참조로 마샬링되면 일반적으로 마샬러는 데이터를 보조 버퍼에 복사하고(복사 중에 문자 집합을 변환할 수 있음) 버퍼 참조를 호출 수신자에게 전달합니다. 참조가 **SysAllocString**을 사용하여 할당된 **BSTR**이 아니면 참조는 항상 **CoTaskMemAlloc**를 사용하여 할당됩니다.

한쪽 문자열 형식이 값(예: 유니코드 문자 문자열)으로 마샬링될 경우의 최적화처럼 마샬러는 새 버퍼에 복사하는 대신 내부 유니코드 버퍼의 관리되는 문자열에 대한 직접 포인터를 호출 수신자에게 전달합니다.

> [!CAUTION]
> 문자열이 값으로 전달되면 호출 수신자는 마샬러가 전달한 참조를 변경할 수 없습니다. 변경하면 관리되는 힙이 손상될 수 있습니다.

<xref:System.String?displayProperty=nameWithType>이 참조로 전달되면 마샬러는 호출을 수행하기 전에 문자열 콘텐츠를 보조 버퍼에 복사합니다. 그런 다음 호출에서 반환 시 버퍼 콘텐츠를 새 문자열에 복사합니다. 이 방법을 사용하면 변경할 수 없는 관리되는 문자열이 변경되지 않습니다.

<xref:System.Text.StringBuilder?displayProperty=nameWithType>가 값으로 전달되면 마샬러는 **StringBuilder**의 내부 버퍼에 대한 참조를 호출자에게 직접 전달합니다. 호출자와 호출 수신자가 버퍼 크기가 동의해야 합니다. 호출자는 적절한 길이의 **StringBuilder**를 만들어야 합니다. 호출 수신자는 버퍼가 오버런되지 않도록 필요한 예방 조치를 수행해야 합니다. **StringBuilder**는 값으로 전달되는 참조 형식이 기본적으로 In 매개 변수로 전달되는 규칙의 예외입니다. 항상 In/Out으로 전달됩니다.

## <a name="see-also"></a>참고 항목

- [기본 마샬링 동작](default-marshaling-behavior.md)
- [방향 특성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/77e6taeh(v=vs.100))
- [interop 마샬링](interop-marshaling.md)
