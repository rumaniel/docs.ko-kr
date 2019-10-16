---
title: 대/소문자 표기법
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- camel-case names [.NET Framework]
- class library design guidelines [.NET Framework], capitalization
- Pascal-case names [.NET Framework]
- case sensitivity, capitalization conventions
- names [.NET Framework], capitalization
ms.assetid: 4c4ea526-9203-486f-b72d-29d61c5b3c6d
author: KrzysztofCwalina
ms.openlocfilehash: e0da4cd747846921d170d9c07d6f1fb91dbd4ed7
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615260"
---
# <a name="capitalization-conventions"></a>대/소문자 표기법
형식, 멤버 및 매개 변수를 읽기 쉽게 확인 식별자를 일관 되 게 적용 하는 경우의 지침에는 간단한 방법 사용 하 여이 장 레이아웃을 만드는 경우는입니다.  
  
## <a name="capitalization-rules-for-identifiers"></a>식별자에 대 한 대/소문자 규칙  
 식별자에서 단어를 구별 하 식별자에서 각 단어의 첫 번째 글자를 대문자로 바꿉니다. 단어를 구분 하기 위해 밑줄을 사용 하지 않는 또는 식별자 어디에서 나 해당 문제에 대 한 합니다. 두 가지 적절 한 식별자의 사용에 따라 식별자를 활용 하려면:  
  
- PascalCasing  
  
- camelCasing  
  
 매개 변수 이름 제외한 모든 식별자에 사용 되는 PascalCasing 규칙을 다음 예와에서 같이 (머리 글자어 길이가 두 문자를 통해) 각 단어의 첫 번째 문자를 대문자로 표시:  
  
 `PropertyDescriptor`  
 `HtmlTag`  
  
 다음 식별자에 표시 된 대로 특수 한 경우는 두 문자를 대문자로 표시, 2 자 약어에 대 한 구성 됩니다.  
  
 `IOStream`  
  
 다음 예제와 같이 camelCasing 규칙, 매개 변수 이름에 대해서만 사용 되는 첫 번째 단어를 제외 하 고 각 단어의 첫 번째 문자를 대문자로 바꿉니다. 또한이 예제에서는, 카멜식 대 / 소문자 식별자를 시작 하는 2 자 약어는 모두 소문자입니다.  
  
 `propertyDescriptor`  
 `ioStream`  
 `htmlTag`  
  
 **✓ DO** PascalCasing 여러 단어로 구성 된 모든 public 멤버, 형식 및 네임 스페이스 이름을 사용 합니다.  
  
 **✓ DO** camelCasing 매개 변수 이름에 사용 합니다.  
  
 다음 표에서 다양 한 유형의 식별자에 대 한 대/소문자 규칙을 설명합니다.  
  
|식별자|대/소문자 구분|예제|  
|----------------|------------|-------------|  
|네임스페이스|Pascal|`namespace System.Security { ... }`|  
|형식|Pascal|`public class StreamReader { ... }`|  
|인터페이스|Pascal|`public interface IEnumerable { ... }`|  
|메서드|Pascal|`public class Object {` <br />  `public virtual string ToString();` <br /> `}`|  
|속성|Pascal|`public class String {` <br />  `public int Length { get; }` <br /> `}`|  
|이벤트(event)|Pascal|`public class Process {` <br />  `public event EventHandler Exited;` <br /> `}`|  
|필드|Pascal|`public class MessageQueue {` <br />  `public static readonly TimeSpan` <br /> `InfiniteTimeout;` <br /> `}` <br /> `public struct UInt32 {` <br />  `public const Min = 0;` <br /> `}`|  
|열거형 값|Pascal|`public enum FileMode {` <br />  `Append,` <br />  `...` <br /> `}`|  
|매개 변수|카멜식 대 /|`public class Convert {` <br />  `public static int ToInt32(string value);` <br /> `}`|  
  
## <a name="capitalizing-compound-words-and-common-terms"></a>복합 단어 및 일반적인 용어를 활용 하세요.  
 대부분의 복합 용어는 대/소문자의 목적을 위해 단일 단어로 취급 됩니다.  
  
 **X DO NOT** 소위 닫힌 형식의 복합 단어 각 글자를 대문자로 표시 합니다.  
  
 이들은 끝점 등 한 단어로 작성 하는 복합 단어입니다. 대/소문자 구분 지침을 위해 단일 단어 닫힌 형식의 복합 단어를 처리 합니다. 현재 사전을 사용 하 여 복합 단어 닫힌 형태로 기록 됩니다 결정 합니다.  
  
|Pascal|카멜식 대 /|not|  
|------------|-----------|---------|  
|`BitFlag`|`bitFlag`|`Bitflag`|  
|`Callback`|`callback`|`CallBack`|  
|`Canceled`|`canceled`|`Cancelled`|  
|`DoNot`|`doNot`|`Don't`|  
|`Email`|`email`|`EMail`|  
|`Endpoint`|`endpoint`|`EndPoint`|  
|`FileName`|`fileName`|`Filename`|  
|`Gridline`|`gridline`|`GridLine`|  
|`Hashtable`|`hashtable`|`HashTable`|  
|`Id`|`id`|`ID`|  
|`Indexes`|`indexes`|`Indices`|  
|`LogOff`|`logOff`|`LogOut`|  
|`LogOn`|`logOn`|`LogIn`|  
|`Metadata`|`metadata`|`MetaData, metaData`|  
|`Multipanel`|`multipanel`|`MultiPanel`|  
|`Multiview`|`multiview`|`MultiView`|  
|`Namespace`|`namespace`|`NameSpace`|  
|`Ok`|`ok`|`OK`|  
|`Pi`|`pi`|`PI`|  
|`Placeholder`|`placeholder`|`PlaceHolder`|  
|`SignIn`|`signIn`|`SignOn`|  
|`SignOut`|`signOut`|`SignOff`|  
|`UserName`|`userName`|`Username`|  
|`WhiteSpace`|`whiteSpace`|`Whitespace`|  
|`Writable`|`writable`|`Writeable`|  
  
## <a name="case-sensitivity"></a>대/소문자 구분  
 일부 있지만 CLR에서 실행할 수 있는 언어 대/소문자 구분을 지원할 필요가 없습니다. 언어를 지 원하는 경우에 프레임 워크에 액세스할 수 있는 다른 언어는 그렇지 않습니다. 따라서 외부에서 액세스할 수 있는 모든 Api는 동일한 컨텍스트에서 두 이름을 구별할 하려면 사례에 사용할 수 없습니다.  
  
 **X DO NOT** 모든 프로그래밍 언어는 대/소문자 구분 하는 것으로 가정 합니다. 그러나 동일하지 않습니다. 대/소문자만 다른 이름 수 없습니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
- [명명 지침](../../../docs/standard/design-guidelines/naming-guidelines.md)
