---
title: XamlName 문법
ms.date: 03/30/2017
helpviewer_keywords:
- DottedXamlName grammar [XAML Services]
- grammar [XAML Services], DottedXamlName
- grammar [XAML Services], XamlName
- names in XAML [XAML Services]
- XamlName grammar [XAML Services]
ms.assetid: 11e4cada-41d2-494d-9531-0d3df4dfcbe3
ms.openlocfilehash: 837a18ca18d0c634dfa5cc133aa013919cfb9d96
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053894"
---
# <a name="xamlname-grammar"></a>XamlName 문법
XamlName Grammar은 편의를 위해 여기에서 재현 되는 XAML 언어 사양 [MS XAML]에 정의 된 특정 문법입니다.  
  
## <a name="from-the-xaml-specification"></a>XAML 사양에서  
 [XamlName] 사양은 문법 검사를 정의 하 여 형식 및 속성에 사용 되는 유효한 기호화 된 식별자 집합을 식별 합니다.  
  
 XamlName 형식의 문자열 값은 다음 문법을 준수 해야 합니다.  
  
```xaml  
XamlName ::= NameStartChar ( NameChar )*   
NameStartChar ::= LetterCharacter | '_'   
NameChar ::= NameStartChar | DecimalDigit | CombiningCharacter   
LetterCharacter ::= UnicodeLu | UnicodeLl | UnicodeLo | UnicodeLt | UnicodeNl   
DecimalDigit ::= UnicodeNd   
CombiningCharacter ::= UnicodeMn | UnicodeMc  
```  
  
 유니코드 문자 데이터베이스에 정의 된 다음과 같은 일반 범주 값을 가정 합니다.  

| 유니코드 범주   | Description                   |
|--------------------|-------------------------------|
| Lu                 | 문자, 대문자             |
| Ll                 | 문자, 소문자             |
| Lt                 | 문자, 제목 스타일             |
| Lm                 | 문자, 한정자              |
| Lo                 | 문자, 기타                 |
| Mn                 | 표시, 공백 없음             |
| Mc                 | 표시, 공백 조합       |
| Nd                 | 숫자, 10 진수               |
| Nl                 | 숫자, 문자                |
 
 XAML은 속성 및 이벤트 정규화 된 참조와 연결 된 멤버에 사용 되는 두 번째 문법 인 DottedXamlName를 정의 합니다. 자세한 내용은 및 <xref:System.Windows.DependencyProperty> [XAML 개요 (WPF)](../wpf/advanced/xaml-overview-wpf.md)를 참조 하세요.  
  
 DottedXamlName 형식의 문자열 값은 다음 문법을 준수 해야 합니다.  
  
```xaml  
DottedXamlName ::= XamlName '.' XamlName  
```  
  
## <a name="remarks"></a>설명  
 전체 사양은 [ \[MS-XAML\]](https://go.microsoft.com/fwlink/?LinkId=114525)을 참조 하세요.
