---
title: WCF 배포 개체 모델을 Atom 및 RSS로 매핑하는 방법
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0365eb37-98cc-4b13-80fb-f1e78847a748
ms.openlocfilehash: 1a2723a445c71dd883492907587f8cbe7b89666a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64613213"
---
# <a name="how-the-wcf-syndication-object-model-maps-to-atom-and-rss"></a>WCF 배포 개체 모델을 Atom 및 RSS로 매핑하는 방법
Windows Communication Foundation (WCF) 배포 서비스를 개발할 때 피드 및 다음 클래스를 사용 하 여 항목을 만듭니다.  
  
- <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
- <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
- <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
- <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
- <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
- <xref:System.ServiceModel.Syndication.TextSyndicationContent>  
  
- <xref:System.ServiceModel.Syndication.UrlSyndicationContent>  
  
- <xref:System.ServiceModel.Syndication.XmlSyndicationContent>  
  
 <xref:System.ServiceModel.Syndication.SyndicationFeed>를 포맷터가 정의된 배포로 serialize할 수 있습니다. WCF 포맷터와 함께 제공 됩니다. <xref:System.ServiceModel.Syndication.Atom10FeedFormatter> 고 <xref:System.ServiceModel.Syndication.Rss20FeedFormatter>입니다.  
  
 <xref:System.ServiceModel.Syndication.SyndicationFeed> 및 <xref:System.ServiceModel.Syndication.SyndicationItem>에 대한 개체 모델은 RSS 2.0 사양보다는 Atom 1.0 사양에 더 가깝습니다. 이는 Atom 1.0이 RSS 2.0 사양에서 모호하거나 생략된 요소를 정의하는 실질적인 사양이기 때문입니다. 이 때문에 WCF 배포 개체 모델에서 여러 항목 직접적인 표현이 없습니다 RSS 2.0 사양에서입니다. 직렬화 할 때 <xref:System.ServiceModel.Syndication.SyndicationFeed> 고 <xref:System.ServiceModel.Syndication.SyndicationItem> 개체를 RSS 2.0으로 WCF를 사용 하면 Atom 특정 데이터 요소를 Atom 사양을 따르는 네임 스페이스로 한정 된 확장명 요소로 serialize 할 수 있습니다. <xref:System.ServiceModel.Syndication.Rss20FeedFormatter> 생성자에 전달된 매개 변수를 사용하여 이 작업을 제어할 수 있습니다.  
  
 이 항목의 코드 샘플에서는 여기에 정의된 두 개 메서드 중 하나를 사용하여 실제 serialization을 수행합니다.  
  
 `SerializeFeed`는 배포 피드를 serialize합니다.  
  
 [!code-csharp[SyndicationMapping#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#10)]
 [!code-vb[SyndicationMapping#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#10)]  
  
 `SerializeItem`은 배포 항목을 serialize합니다.  
  
 [!code-csharp[SyndicationMapping#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#11)]
 [!code-vb[SyndicationMapping#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#11)]  
  
## <a name="syndicationfeed"></a>SyndicationFeed  
 다음 코드 예제에서는 <xref:System.ServiceModel.Syndication.SyndicationFeed> 클래스를 Atom 1.0 및 RSS 2.0으로 serialize하는 방법을 보여 줍니다.  
  
 [!code-csharp[SyndicationMapping#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#0)]
 [!code-vb[SyndicationMapping#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#0)]  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.SyndicationFeed>가 Atom 1.0으로 serialize되는 방법을 보여 줍니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<feed xml:lang="EN-US" xmlns="http://www.w3.org/2005/Atom">  
  <title type="text">My Feed Title</title>  
  <subtitle type="text">My Feed Description</subtitle>  
  <id>FeedID</id>  
  <rights type="text">Copyright 2007</rights>  
  <updated>2007-08-29T13:57:17-07:00</updated>  
  <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
  <logo>http://server/image.jpg</logo>  
  <generator>Sample Code</generator>  
  <link rel="alternate" href="http://myfeeduri/" />  
  <entry>  
    <id>ItemID</id>  
    <title type="text">Item Title</title>  
    <summary type="text">Item Summary</summary>  
    <published>2007-08-29T00:00:00-07:00</published>  
    <updated>2007-08-29T13:57:17-07:00</updated>  
    <author>  
      <name>Jesper Aaberg</name>  
      <uri>http://Jesper/Aaberg</uri>  
      <email>Jesper@Aaberg.com</email>  
    </author>  
    <contributor>  
      <name>Lene Aaling</name>  
      <uri>http://Lene/Aaling</uri>  
      <email>Lene@Aaling.com</email>  
    </contributor>  
    <link rel="alternate" href="http://myitemuri/" />  
    <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
    <content type="text">Item Content</content>  
    <rights type="text">Copyright 2007</rights>  
    <source>  
      <title type="text">My Feed Title</title>  
      <subtitle type="text">My Feed Description</subtitle>  
      <id>FeedID</id>  
      <rights type="text">Copyright 2007</rights>  
      <updated>2007-08-29T13:57:17-07:00</updated>  
      <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
      <logo>http://server/image.jpg</logo>  
      <generator>Sample Code</generator>  
      <link rel="alternate" href="http://myfeeduri/" />  
    </source>  
  </entry>  
</feed>  
```  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.SyndicationFeed>가 RSS 2.0으로 serialize되는 방법을 보여 줍니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<rss xmlns:a10="http://www.w3.org/2005/Atom" version="2.0">  
  <channel>  
    <title>My Feed Title</title>  
    <link>http://myfeeduri/</link>  
    <description>My Feed Description</description>  
    <language>EN-US</language>  
    <copyright>Copyright 2007</copyright>  
    <lastBuildDate>Wed, 29 Aug 2007 13:57:17 -0700</lastBuildDate>  
    <category domain="categoryScheme">categoryName</category>  
    <generator>Sample Code</generator>  
    <image>  
      <url>http://server/image.jpg</url>  
      <title>My Feed Title</title>  
      <link>http://myfeeduri/</link>  
    </image>  
    <a10:id>FeedID</a10:id>  
    <item>  
      <guid isPermaLink="false">ItemID</guid>  
      <link>http://myitemuri/</link>  
      <author>Jesper@Aaberg.com</author>  
      <category domain="categoryScheme">categoryName</category>  
      <title>Item Title</title>  
      <description>Item Summary</description>  
      <source>My Feed Title</source>  
      <pubDate>Wed, 29 Aug 2007 00:00:00 -0700</pubDate>  
      <a10:updated>2007-08-29T13:57:17-07:00</a10:updated>  
      <a10:rights type="text">Copyright 2007</a10:rights>  
      <a10:content type="text">Item Content</a10:content>  
      <a10:contributor>  
        <a10:name>Lene Aaling</a10:name>  
        <a10:uri>http://Lene/Aaling</a10:uri>  
        <a10:email>Lene@Aaling.com</a10:email>  
      </a10:contributor>  
    </item>  
  </channel>  
</rss>  
```  
  
## <a name="syndicationitem"></a>SyndicationItem  
 다음 코드 예제에서는 <xref:System.ServiceModel.Syndication.SyndicationItem> 클래스를 Atom 1.0 및 RSS 2.0으로 serialize하는 방법을 보여 줍니다.  
  
 [!code-csharp[SyndicationMapping#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#1)]
 [!code-vb[SyndicationMapping#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#1)]  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.SyndicationItem>가 Atom 1.0으로 serialize되는 방법을 보여 줍니다.  
  
```xml  
<entry xmlns="http://www.w3.org/2005/Atom">  
  <id>ItemID</id>  
  <title type="text">Item Title</title>  
  <summary type="text">Item Summary</summary>  
  <published>2007-08-29T00:00:00-07:00</published>  
  <updated>2007-08-29T14:07:09-07:00</updated>  
  <author>  
    <name>Jesper Aaberg</name>  
    <uri>http://Contoso/Aaberg</uri>  
    <email>Jesper.Aaberg@contoso.com</email>  
  </author>  
  <author>  
    <name>Syed Abbas</name>  
    <uri>http://Contoso/Abbas</uri>  
    <email>Syed.Abbas@contoso.com</email>  
  </author>  
  <contributor>  
    <name>Lene Aaling</name>  
    <uri>http://Contoso/Aaling</uri>  
    <email>Lene.Aaling@contoso.com</email>  
  </contributor>  
  <contributor>  
    <name>Kim Abercrombie</name>  
    <uri>http://Contoso/Abercrombie</uri>  
    <email>Kim.Abercrombie@contoso.com</email>  
  </contributor>  
  <link rel="alternate" href="http://myitemuri/" />  
  <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
  <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
  <content type="text">Item Content</content>  
  <rights type="text">Copyright 2007</rights>  
  <source>  
    <title type="text">My Feed Title</title>  
    <subtitle type="text">My Feed Description</subtitle>  
    <link rel="alternate" href="http://myfeeduri/" />  
  </source>  
</entry>  
```  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.SyndicationItem>가 RSS 2.0으로 serialize되는 방법을 보여 줍니다.  
  
```xml  
<item>  
  <guid isPermaLink="false">ItemID</guid>  
  <link>http://myitemuri/</link>  
  <author xmlns="http://www.w3.org/2005/Atom">  
    <name>Jesper Aaberg</name>  
    <uri>http://Jesper/Aaberg</uri>  
    <email>Jesper@Aaberg.com</email>  
  </author>  
  <author xmlns="http://www.w3.org/2005/Atom">  
    <name>Syed Abbas</name>  
    <uri>http://Contoso/Abbas</uri>  
    <email>Syed.Abbas@contoso.com</email>  
  </author>  
  <category domain="categoryScheme">categoryName</category>  
  <category domain="categoryScheme">categoryName</category>  
  <title>Item Title</title>  
  <description>Item Summary</description>  
  <source>My Feed Title</source>  
  <pubDate>Wed, 29 Aug 2007 00:00:00 -0700</pubDate>  
  <updated xmlns="http://www.w3.org/2005/Atom">2007-08-29T14:07:09-07:00</updated>  
  <rights type="text" xmlns="http://www.w3.org/2005/Atom">Copyright 2007</rights>  
  <content type="text" xmlns="http://www.w3.org/2005/Atom">Item Content</content>  
  <contributor xmlns="http://www.w3.org/2005/Atom">  
    <name>Lene Aaling</name>  
    <uri>http://Contoso/Aaling</uri>  
    <email>Lene.Aaling@contoso.com</email>  
  </contributor>  
  <contributor xmlns="http://www.w3.org/2005/Atom">  
    <name>Kim Abercrombie</name>  
    <uri>http://Contoso/Abercrombie</uri>  
    <email>Kim.Abercrombie@contoso.com</email>  
  </contributor>  
</item>  
```  
  
## <a name="syndicationperson"></a>SyndicationPerson  
 다음 코드 예제에서는 <xref:System.ServiceModel.Syndication.SyndicationPerson> 클래스를 Atom 1.0 및 RSS 2.0으로 serialize하는 방법을 보여 줍니다.  
  
 [!code-csharp[SyndicationMapping#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#2)]
 [!code-vb[SyndicationMapping#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#2)]  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.SyndicationPerson>가 Atom 1.0으로 serialize되는 방법을 보여 줍니다.  
  
```xml  
  <author>  
    <name>Jesper Aaberg</name>  
    <uri>http://Contoso/Aaberg</uri>  
    <email>Jesper.Aaberg@contoso.com</email>  
  </author>  
<contributor>  
    <name>Lene Aaling</name>  
    <uri>http://Contoso/Aaling</uri>  
    <email>Lene.Aaling@contoso.com</email>  
  </contributor>  
```  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.SyndicationPerson>이 <xref:System.ServiceModel.Syndication.SyndicationPerson> 또는 `Authors` 컬렉션에 각각 하나만 있는 경우 `Contributors` 클래스가 RSS 2.0으로 serialize되는 방법을 보여 줍니다.  
  
```xml  
<author>Jesper.Aaberg@contoso.com</author>  
<a10:contributor>  
    <a10:name>Lene Aaling</a10:name>  
    <a10:uri>http://Contoso/Aaling</a10:uri>  
    <a10:email>Lene.Aaling@contoso.com</a10:email>  
</a10:contributor>  
```  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.SyndicationPerson>이 <xref:System.ServiceModel.Syndication.SyndicationPerson> 또는 `Authors` 컬렉션에 각각 두 개 이상 있는 경우 `Contributors` 클래스가 RSS 2.0으로 serialize되는 방법을 보여 줍니다.  
  
```xml  
<a10:author>  
    <a10:name>Jesper Aaberg</a10:name>  
    <a10:uri>http://Contoso/Aaberg</a10:uri>  
    <a10:email>Jesper.Aaberg@contoso.com</a10:email>  
</a10:author>  
<a10:author>  
    <a10:name>Syed Abbas</a10:name>  
    <a10:uri>http://Contoso/Abbas</a10:uri>  
    <a10:email>Syed.Abbas@contoso.com</a10:email>  
</a10:author>  
<a10:contributor>  
    <a10:name>Lene Aaling</a10:name>  
    <a10:uri>http://Contoso/Aaling</a10:uri>  
    <a10:email>Lene.Aaling@contoso.com</a10:email>  
</a10:contributor>  
<a10:contributor>  
    <a10:name>Kim Abercrombie</a10:name>  
    <a10:uri>http://Contoso/Abercrombie</a10:uri>  
    <a10:email>Kim.Abercrombie@contoso.com</a10:email>  
</a10:contributor>  
```  
  
## <a name="syndicationlink"></a>SyndicationLink  
 다음 코드 예제에서는 <xref:System.ServiceModel.Syndication.SyndicationLink> 클래스를 Atom 1.0 및 RSS 2.0으로 serialize하는 방법을 보여 줍니다.  
  
 [!code-csharp[SyndicationMapping#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#3)]
 [!code-vb[SyndicationMapping#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#3)]  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.SyndicationLink>가 Atom 1.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<link rel="alternate" type="text/html" title="My Link Title" length="2048" href="http://contoso/MyLink" />`  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.SyndicationLink>가 RSS 2.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<a10:link rel="alternate" type="text/html" title="My Link Title" length="2048" href="http://contoso/MyLink" />`  
  
## <a name="syndicationcategory"></a>SyndicationCategory  
 다음 코드 예제에서는 <xref:System.ServiceModel.Syndication.SyndicationCategory> 클래스를 Atom 1.0 및 RSS 2.0으로 serialize하는 방법을 보여 줍니다.  
  
 [!code-csharp[SyndicationMapping#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#4)]
 [!code-vb[SyndicationMapping#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#4)]  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.SyndicationCategory>가 Atom 1.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<category term="categoryName" label="categoryLabel" scheme="categoryScheme" />`  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.SyndicationCategory>가 RSS 2.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<category domain="categoryScheme">categoryName</category>`  
  
## <a name="textsyndicationcontent"></a>TextSyndicationContent  
 다음 코드 예제에서는 <xref:System.ServiceModel.Syndication.TextSyndicationContent>가 HTML 콘텐츠로 만들어진 경우 <xref:System.ServiceModel.Syndication.TextSyndicationContent> 클래스를 Atom 1.0 및 RSS 2.0으로 serialize하는 방법을 보여 줍니다.  
  
 [!code-csharp[SyndicationMapping#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#5)]
 [!code-vb[SyndicationMapping#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#5)]  
  
 다음 XML에서는 HTML 콘텐츠가 있는 <xref:System.ServiceModel.Syndication.TextSyndicationContent> 클래스가 Atom 1.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<content type="html"><html> some html </html></content>`  
  
 다음 XML에서는 HTML 콘텐츠가 있는 <xref:System.ServiceModel.Syndication.TextSyndicationContent> 클래스가 RSS 2.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<description><html> some html </html></description>`  
  
 다음 코드 예제에서는 <xref:System.ServiceModel.Syndication.TextSyndicationContent>가 일반 텍스트 콘텐츠로 만들어진 경우 <xref:System.ServiceModel.Syndication.TextSyndicationContent> 클래스를 Atom 1.0 및 RSS 2.0으로 serialize하는 방법을 보여 줍니다.  
  
 [!code-csharp[SyndicationMapping#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#6)]
 [!code-vb[SyndicationMapping#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#6)]  
  
 다음 XML에서는 일반 텍스트 콘텐츠가 있는 <xref:System.ServiceModel.Syndication.TextSyndicationContent> 클래스가 Atom 1.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<content type="text">Some Plain Text</content>`  
  
 다음 XML에서는 일반 텍스트 콘텐츠가 있는 <xref:System.ServiceModel.Syndication.TextSyndicationContent> 클래스가 RSS 2.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<description>Some Plain Text</description>`  
  
 다음 코드 예제에서는 <xref:System.ServiceModel.Syndication.TextSyndicationContent>가 XHTML 콘텐츠로 만들어진 경우 <xref:System.ServiceModel.Syndication.TextSyndicationContent> 클래스를 Atom 1.0 및 RSS 2.0으로 serialize하는 방법을 보여 줍니다.  
  
 [!code-csharp[SyndicationMapping#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#7)]
 [!code-vb[SyndicationMapping#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#7)]  
  
 다음 XML에서는 XHTML 콘텐츠가 있는 <xref:System.ServiceModel.Syndication.TextSyndicationContent> 클래스가 Atom 1.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<content type="xhtml">`  
  
 `<html> some xhtml </html>`  
  
 `</content>`  
  
 다음 XML에서는 XHTML 콘텐츠가 있는 <xref:System.ServiceModel.Syndication.TextSyndicationContent> 클래스가 RSS 2.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<description><html> some xhtml </html></description>`  
  
## <a name="urlsyndicationcontent"></a>UrlSyndicationContent  
 다음 코드 예제에서는 <xref:System.ServiceModel.Syndication.UrlSyndicationContent> 클래스를 Atom 1.0 및 RSS 2.0으로 serialize하는 방법을 보여 줍니다.  
  
 [!code-csharp[SyndicationMapping#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#8)]
 [!code-vb[SyndicationMapping#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#8)]  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.UrlSyndicationContent> 클래스가 Atom 1.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<content type="audio" src="http://someurl/" />`  
  
 다음 XML에서는 XHTML 콘텐츠가 있는 <xref:System.ServiceModel.Syndication.UrlSyndicationContent> 클래스가 RSS 2.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<description />`  
  
 `<content type="audio" src="http://Contoso/someurl/" xmlns="http://www.w3.org/2005/Atom" />`  
  
## <a name="xmlsyndicationcontent"></a>XmlSyndicationContent  
 다음 코드 예제에서는 <xref:System.ServiceModel.Syndication.XmlSyndicationContent> 클래스를 Atom 1.0 및 RSS 2.0으로 serialize하는 방법을 보여 줍니다.  
  
 [!code-csharp[SyndicationMapping#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#9)]
 [!code-vb[SyndicationMapping#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#9)]  
  
 다음 XML에서는 <xref:System.ServiceModel.Syndication.XmlSyndicationContent> 클래스가 Atom 1.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<content type="mytype">`  
  
 `<SomeData xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.datacontract.org/2004/07/FeedMapping" />`  
  
 `</content>`  
  
 다음 XML에서는 XHTML 콘텐츠가 있는 <xref:System.ServiceModel.Syndication.XmlSyndicationContent> 클래스가 RSS 2.0으로 serialize되는 방법을 보여 줍니다.  
  
 `<content type="mytype" xmlns="http://www.w3.org/2005/Atom">`  
  
 `<SomeData xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.datacontract.org/2004/07/FeedMapping" />`  
  
 `</content>`  
  
## <a name="see-also"></a>참고자료

- [WCF 배포 개요](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)
- [배포 아키텍처](../../../../docs/framework/wcf/feature-details/architecture-of-syndication.md)
- [방법: 기본 RSS 피드 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-rss-feed.md)
- [방법: 기본 Atom 피드 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-atom-feed.md)
- [방법: Atom로 피드 공개 및 RSS](../../../../docs/framework/wcf/feature-details/how-to-expose-a-feed-as-both-atom-and-rss.md)
