---
title: .NET Framework 로깅 제어
ms.date: 03/30/2017
helpviewer_keywords:
- CLR ETW events, logging
ms.assetid: ce13088e-3095-4f0e-9f6b-fad30bbd3d41
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 45df41e10dc81bc6011e5329723bca55925825f9
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046680"
---
# <a name="controlling-net-framework-logging"></a>.NET Framework 로깅 제어

ETW(Windows용 이벤트 추적)를 사용하여 CLR(공용 언어 런타임) 이벤트를 기록할 수 있습니다. 다음과 같은 도구를 사용하여 추적을 만들고 볼 수 있습니다.

- Windows 운영 체제에 포함되어 있는 [Logman](/windows-server/administration/windows-commands/logman) 및 [Tracerpt](/windows-server/administration/windows-commands/tracerpt_1) 명령줄 도구

- [Windows 성능 도구 키트](/windows-hardware/test/wpt/)에 있는 [Xperf](/windows-hardware/test/wpt/xperf-command-line-reference) 도구 Xperf에 대한 자세한 내용은 [Windows Performance 블로그](https://go.microsoft.com/fwlink/?LinkId=179509)를 참조하세요.

CLR 이벤트 정보를 캡처하려면 컴퓨터에 CLR 공급자가 설치되어 있어야 합니다. 공급자가 설치되어 있는지 확인하려면 명령줄에 `logman query providers`를 입력합니다. 공급자 목록이 나타납니다. 이 목록에는 다음과 같이 CLR 공급자 항목이 포함되어 있어야 합니다.

```output
Provider                                 GUID
-------------------------------------------------------------------------------
.NET Common Language Runtime    {E13C0D23-CCBC-4E12-931B-D9CC2EEE27E4}.
```

CLR 공급자가 목록에 없는 경우 Windows [Wevtutil](/windows-server/administration/windows-commands/wevtutil) 명령줄 도구를 사용하여 Windows Vista 이상의 운영 체제에 설치할 수 있습니다. 관리자 권한으로 명령 프롬프트 창을 엽니다. 프롬프트 디렉터리를 .NET Framework 4 폴더 (%WINDIR%\Microsoft.NET\Framework [64] \v4.\<)로 변경 합니다. NET version > \). 이 폴더에는 CLR-ETW.man 파일이 들어 있습니다. 명령 프롬프트에서 다음 명령을 입력하여 CLR 공급자를 설치합니다.

`wevtutil im CLR-ETW.man`

## <a name="capturing-clr-etw-events"></a>CLR ETW 이벤트 캡처

[Logman](/windows-server/administration/windows-commands/logman) 및 [Xperf](/windows-hardware/test/wpt/xperf-command-line-reference) 명령줄 도구를 사용하여 ETW 이벤트를 캡처하고, [Tracerpt](/windows-server/administration/windows-commands/tracerpt_1) 및 [Xperf](/windows-hardware/test/wpt/xperf-command-line-reference) 도구를 사용하여 추적 이벤트를 디코딩할 수 있습니다.

로깅을 설정하려면 사용자가 다음 세 가지를 지정해야 합니다.

- 통신 대상 공급자

- 일련의 키워드를 나타내는 64비트 숫자. 각 키워드는 공급자가 설정할 수 있는 이벤트 집합을 나타내고, 숫자는 설정할 키워드가 결합된 집합을 나타냅니다.

- 로그 수준(자세한 정도)을 나타내는 작은 숫자. 수준 1은 가장 간결하고 수준 5는 가장 자세합니다. 기본값은 수준 0이고, 이 수준은 공급자별로 다릅니다.

### <a name="to-capture-clr-etw-events-using-logman"></a>Logman을 사용하여 CLR ETW 이벤트를 캡처하려면

1. 명령 프롬프트에서 다음을 입력합니다.

     `logman start clrevents -p {e13c0d23-ccbc-4e12-931b-d9cc2eee27e4} 0x1CCBD 0x5 -ets -ct perf`

     각 항목이 나타내는 의미는 다음과 같습니다.

    - `-p` 매개 변수는 공급자 GUID를 식별합니다.

    - `0x1CCBD`는 발생할 이벤트의 범주를 지정합니다.

    - `0x5`는 로깅 수준을 설정합니다(이 경우, verbose(5)).

    - `-ets` 매개 변수는 이벤트 추적 세션에 명령을 보내도록 Logman에 지시합니다.

    - `-ct perf` 매개 변수는 `QueryPerformanceCounter` 함수를 사용하여 각 이벤트의 타임 스탬프를 로깅할 것임을 지정합니다.

2. 이벤트 로깅을 중지하려면 다음을 입력하십시오.

     `logman stop clrevents -ets`

     이 명령은 clrevents.etl이라는 이진 추적 파일을 만듭니다.

### <a name="to-capture-clr-etw-events-using-xperf"></a>Xperf를 사용하여 CLR ETW 이벤트를 캡처하려면

1. 명령 프롬프트에서 다음을 입력합니다.

     `xperf -start clr -on e13c0d23-ccbc-4e12-931b-d9cc2eee27e4:0x1CCBD:5 -f clrevents.etl`

     여기서 GUID는 CLR ETW 공급자 GUID이고, `0x1CCBD:5`는 수준 5(verbose) 이하의 모든 내용을 추적합니다.

2. 추적을 중지하려면 다음을 입력하십시오.

     `Xperf -stop clr`

     이 명령은 clrevents.etl이라는 추적 파일을 만듭니다.

## <a name="viewing-clr-etw-events"></a>CLR ETW 이벤트 보기

아래의 명령을 사용하여 CLR ETW 이벤트를 볼 수 있습니다. 이벤트에 대한 설명은 [CLR ETW 이벤트](clr-etw-events.md)를 참조하세요.

### <a name="to-view-clr-etw-events-using-tracerpt"></a>Tracerpt를 사용하여 CLR ETW 이벤트를 보려면

- 명령 프롬프트에서 다음을 입력합니다.

     `tracerpt clrevents.etl`

     이 명령은 dumpfile.xml 및 summary.txt라는 두 개의 파일을 만듭니다. dumpfile.xml 파일은 모든 이벤트를 나열하고, summary.txt는 이벤트 요약을 제공합니다.

### <a name="to-view-clr-etw-events-using-xperf"></a>Xperf를 사용하여 CLR ETW 이벤트를 보려면

- 명령 프롬프트에서 다음을 입력합니다.

     `xperf clrevents.etl`

     이 명령은 Xperf ETL 파일 뷰어를 엽니다. 이 뷰어에서 CLR 이벤트는 **제네릭 이벤트** 뷰에 나타납니다. 유형별로 범주화된 이벤트의 데이터 표를 표시하려면 이 뷰에서 시간 영역을 선택한 다음 마우스 오른쪽 단추를 클릭하고 **요약**을 선택합니다.

### <a name="to-convert-the-etl-file-to-a-comma-separated-value-file"></a>.etl 파일을 쉼표로 구분된 값 파일로 변환하려면

- 명령 프롬프트에서 다음을 입력합니다.

     `xperf -i clrevents.etl -f clrevents.csv`

     이 명령에 의해 XPerf는 사용자가 볼 수 있는 쉼표로 분리된 값 파일(CSV)로 이벤트를 덤프하게 됩니다. 이벤트별로 서로 다른 필드가 있기 때문에 이 CSV 파일에서는 데이터 앞에 헤더 줄이 둘 이상 있습니다. 모든 줄의 첫 번째 필드는 이벤트 유형이고, 이 유형은 나머지 필드 확인에 사용되어야 하는 헤더를 나타냅니다.

## <a name="see-also"></a>참고자료

- [Windows 성능 도구 키트](/windows-hardware/test/wpt/)
- [공용 언어 런타임의 ETW 이벤트](etw-events-in-the-common-language-runtime.md)
