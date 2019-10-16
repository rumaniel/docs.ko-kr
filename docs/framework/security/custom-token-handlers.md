---
title: 사용자 지정 토큰 처리기
ms.date: 03/30/2017
ms.assetid: 5062669f-8bfc-420a-a25d-d8ab992ab10e
author: BrucePerlerMS
ms.openlocfilehash: f7d611bf396f028ff23a39cd529825f99fec300a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64650430"
---
# <a name="custom-token-handlers"></a>사용자 지정 토큰 처리기
이 항목에서는 WIF의 토큰 처리기 및 토큰 처리기를 사용하여 토큰을 처리하는 방법을 설명합니다. WIF에서 기본적으로 지원되지 않는 토큰 형식에 대한 사용자 지정 토큰 처리기를 만드는 데 필요한 항목에 대해서도 설명합니다.  
  
## <a name="introduction-to-token-handlers-in-wif"></a>WIF의 토큰 처리기 소개  
 WIF는 보안 토큰 처리기를 사용하여 RP(신뢰 당사자) 애플리케이션이나 STS(보안 토큰 서비스)에 대한 토큰을 만들고, 읽고, 쓰고, 유효성을 검사합니다. 토큰 처리기는 WIF 파이프라인에서 사용자 지정 토큰 처리기를 추가하거나 기존 토큰 처리기가 토큰을 관리하는 방법을 사용자 지정할 수 있는 확장성 지점입니다. WIF는 필요에 따라 기능을 변경하도록 수정하거나 전체적으로 재정의할 수 있는 9개의 기본 제공 보안 토큰 처리기를 제공합니다.  
  
## <a name="built-in-security-token-handlers-in-wif"></a>WIF의 기본 제공 보안 토큰 처리기  
 WIF 4.5에는 추상 기본 클래스 <xref:System.IdentityModel.Tokens.SecurityTokenHandler>에서 파생되는 9개의 보안 토큰 처리기 클래스가 포함됩니다.  
  
- <xref:System.IdentityModel.Tokens.EncryptedSecurityTokenHandler>  
  
- <xref:System.IdentityModel.Tokens.KerberosSecurityTokenHandler>  
  
- <xref:System.IdentityModel.Tokens.RsaSecurityTokenHandler>  
  
- <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>  
  
- <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>  
  
- <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>  
  
- <xref:System.IdentityModel.Tokens.UserNameSecurityTokenHandler>  
  
- <xref:System.IdentityModel.Tokens.WindowsUserNameSecurityTokenHandler>  
  
- <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler>  
  
## <a name="adding-a-custom-token-handler"></a>사용자 지정 토큰 처리기 추가  
 SWT(단순 웹 토큰) 및 JWT(JSON Web Token)와 같은 일부 토큰 형식에는 WIF에서 제공하는 기본 제공 토큰 처리기가 없습니다. 이러한 토큰 형식 및 기본 제공 처리기가 없는 다른 토큰 형식의 경우 사용자 지정 토큰 처리기를 만들려면 다음 단계를 수행해야 합니다.  
  
#### <a name="adding-a-custom-token-handler"></a>사용자 지정 토큰 처리기 추가  
  
1. <xref:System.IdentityModel.Tokens.SecurityTokenHandler>에서 파생되는 새 클래스를 만듭니다.  
  
2. 다음 메서드를 재정의하고 고유한 구현을 제공합니다.  
  
    - <xref:System.IdentityModel.Tokens.SecurityTokenHandler.CanReadToken%2A>  
  
    - <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ReadToken%2A>  
  
    - <xref:System.IdentityModel.Tokens.SecurityTokenHandler.CanWriteToken%2A>  
  
    - <xref:System.IdentityModel.Tokens.SecurityTokenHandler.WriteToken%2A>  
  
    - <xref:System.IdentityModel.Tokens.SecurityTokenHandler.CanValidateToken%2A>  
  
    - <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ValidateToken%2A>  
  
3. *Web.config* 또는 *App.config* 파일에서 WIF에 적용되는 **\<system.identityModel>** 섹션 내에 새 사용자 지정 토큰 처리기에 대한 참조를 추가합니다. 예를 들어 다음 구성 태그는 **CustomToken** 네임스페이스에 있는 **MyCustomTokenHandler**라는 새 토큰 처리기를 지정합니다.  
  
    ```xml  
    <system.identityModel>  
        <identityConfiguration saveBootstrapContext="true">  
            <securityTokenHandlers>  
                <add type="CustomToken.MyCustomTokenHandler, CustomToken" />  
            </securityTokenHandlers>  
        </identityConfiguration>  
    </system.identityModel>  
    ```  
  
     이미 기본 제공 토큰 처리기가 있는 토큰 형식을 처리하기 위해 고유한 토큰 처리기를 제공할 경우 기본 처리기를 삭제하고 사용자 지정 처리기를 대신 사용하려면 **\<remove>** 요소를 추가해야 합니다. 예를 들어 다음 구성은 기본 <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>를 사용자 지정 토큰 처리기로 바꿉니다.  
  
    ```xml  
    <system.identityModel>  
        <identityConfiguration saveBootstrapContext="true">  
            <securityTokenHandlers>  
                <remove type="System.IdentityModel.Tokens.SamlSecurityTokenHandler, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=abcdefg123456789">  
                <add type="CustomToken.MyCustomTokenHandler, CustomToken" />  
            </securityTokenHandlers>  
        </identityConfiguration>  
    </system.identityModel>  
    ```
