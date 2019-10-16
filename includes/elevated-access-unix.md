---
ms.openlocfilehash: 85f50b221e7ecb1ebd6fa539894ab7aabed8d362
ms.sourcegitcommit: b5c59eaaf8bf48ef3ec259f228cb328d6d4c0ceb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67540114"
---
### <a name="install-the-global-tool"></a>글로벌 도구 설치

패키지 자산은 `--tool-path` 옵션을 사용하여 보호된 위치에 설치해야 합니다. 이러한 분리는 제한된 사용자 환경을 높은 환경과 공유하지 않도록 합니다.

```bash
sudo dotnet tool install PACKAGEID --tool-path /usr/local/share/dotnet-tools
```

`/usr/local/share/dotnet-tools`는 `drwxr-xr-x` 사용 권한으로 생성됩니다. 디렉터리가 이미 존재하는 경우 `ls -l` 명령을 사용하여 제한된 사용자에게 디렉터리 편집 권한이 없는지 확인합니다. 그렇다면 `sudo chmod o-w -R /usr/share/dotnet-tools` 명령을 사용하여 액세스를 제거합니다.

### <a name="run-the-global-tool"></a>글로벌 도구 실행

**옵션 1** sudo로 함께 전체 경로를 사용합니다.

```bash
sudo /usr/local/share/dotnet-tools/TOOLCOMMAND
```

**옵션 2** 도구당 한 번씩 도구의 기호 링크를 추가합니다.

```bash
sudo ln -s /usr/local/share/dotnet-tools/TOOLCOMMAND /usr/local/bin/TOOLCOMMAND
```

다음 항목으로 실행합니다.

```bash
sudo TOOLCOMMAND
```

### <a name="uninstall-the-global-tool"></a>글로벌 도구 제거

```bash
sudo dotnet tool uninstall PACKAGEID --tool-path /usr/local/share/dotnet-tools
```

기호 링크를 만든 경우 기호 링크도 제거해야 합니다.

```bash
sudo rm /usr/local/bin/TOOLCOMMAND
```
