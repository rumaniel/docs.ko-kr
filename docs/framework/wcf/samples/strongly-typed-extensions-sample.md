---
title: 강력한 형식 확장 샘플
ms.date: 03/30/2017
ms.assetid: 02220f11-1a83-441c-9e5a-85f9a9367572
ms.openlocfilehash: 1fd873e02dcc1fc824c8b17c52231c80c61e7c60
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045479"
---
# <a name="strongly-typed-extensions-sample"></a>강력한 형식 확장 샘플
이 샘플에서는 예를 들기 위해 <xref:System.ServiceModel.Syndication.SyndicationFeed> 클래스를 사용하지만 이 샘플에 나온 패턴은 확장 데이터를 지원하는 모든 배포 클래스에서 사용할 수 있습니다.  
  
 배포 개체 모델(<xref:System.ServiceModel.Syndication.SyndicationFeed>, <xref:System.ServiceModel.Syndication.SyndicationItem> 및 관련 클래스)은 <xref:System.ServiceModel.Syndication.SyndicationFeed.AttributeExtensions%2A> 및 <xref:System.ServiceModel.Syndication.SyndicationFeed.ElementExtensions%2A> 속성을 사용하여 확장명 데이터에 대한 자유로운 형식의 액세스를 지원합니다. 이 샘플에서는 특정 애플리케이션 관련 확장을 강력한 형식의 속성으로 사용할 수 있게 하는 <xref:System.ServiceModel.Syndication.SyndicationFeed> 및 <xref:System.ServiceModel.Syndication.SyndicationItem>의 사용자 지정 파생 클래스를 구현하여 확장명 데이터에 대해 강력한 형식의 액세스를 제공하는 방법을 보여 줍니다.  
  
 한 예로 이 샘플에서는 제안된 Atom Threading Extensions RFC에 정의된 확장명 요소를 구현하는 방법을 보여 줍니다. 이 샘플은 데모용으로만 사용되며 제안된 사양을 전체 구현할 용도는 아닙니다.  
  
## <a name="sample-xml"></a>샘플 XML  
 다음 XML 예제에서는 추가 `<in-reply-to>` 확장명 요소가 포함된 Atom 1.0 항목을 보여 줍니다.  
  
```xml  
<entry>  
    <id>tag:example.org,2005:1,2</id>  
    <title type="text">Another response to the original</title>  
    <summary type="text">  
         This is a response to the original entry</summary>  
    <updated>2006-03-01T12:12:13Z</updated>  
    <link href="http://www.example.org/entries/1/2" />  
    <in-reply-to p3:ref="tag:example.org,2005:1"   
                 p3:href="http://www.example.org/entries/1"   
                 p3:type="application/xhtml+xml"   
                 xmlns:p3="http://contoso.org/syndication/thread/1.0"   
                 xmlns="http://contoso.org/syndication/thread/1.0">  
      <anotherElement xmlns="http://www.w3.org/2005/Atom">  
                     Some more data</anotherElement>  
      <aDifferentElement xmlns="http://www.w3.org/2005/Atom">  
                     Even more data</aDifferentElement>  
    </in-reply-to>  
</entry>  
```  
  
 요소 `<in-reply-to>` 는 세 가지 필수 특성 (`ref`, `type` 및 `href`)을 지정 하 고 추가 확장 특성 및 확장 요소도 허용 합니다.  
  
## <a name="modeling-the-in-reply-to-element"></a>In-Reply-To 요소 모델링  
 이 샘플에서는 `<in-reply-to>`와 함께 사용할 수 있도록 <xref:System.Xml.Serialization.IXmlSerializable> 요소가 <xref:System.Runtime.Serialization.DataContractSerializer>을 구현하는 CLR로 모델링됩니다. 또한 다음 샘플 코드에서와 같이 요소의 데이터에 액세스하기 위한 몇몇 메서드와 속성을 구현합니다.  
  
```  
[XmlRoot(ElementName = "in-reply-to", Namespace = "http://contoso.org/syndication/thread/1.0")]  
public class InReplyToElement : IXmlSerializable  
{  
    internal const string ElementName = "in-reply-to";  
    internal const string NsUri =   
                  "http://contoso.org/syndication/thread/1.0";  
    private Dictionary<XmlQualifiedName, string> extensionAttributes;  
    private Collection<XElement> extensionElements;  
  
    public InReplyToElement()  
    {  
        this.extensionElements = new Collection<XElement>();  
        this.extensionAttributes = new Dictionary<XmlQualifiedName,   
                                                          string>();  
    }  
  
    public Dictionary<XmlQualifiedName, string> AttributeExtensions  
    {  
        get { return this.extensionAttributes; }  
    }  
  
    public Collection<XElement> ElementExtensions  
    {  
        get { return this.extensionElements; }  
    }  
  
    public Uri Href  
    { get; set; }  
  
    public string MediaType  
    { get; set; }  
  
    public string Ref  
    { get; set; }  
  
    public Uri Source  
    { get; set; }  
}  
```  
  
 `InReplyToElement` 클래스는 필수 특성의 속성(`HRef`, `MediaType` 및 `Source`)뿐 아니라 <xref:System.ServiceModel.Syndication.SyndicationFeed.AttributeExtensions%2A> 및 <xref:System.ServiceModel.Syndication.SyndicationFeed.ElementExtensions%2A>를 보유하는 컬렉션을 구현합니다.  
  
 `InReplyToElement` 클래스는 XML에서 개체 인스턴스를 읽고 쓰는 방법을 직접 제어하는 <xref:System.Xml.Serialization.IXmlSerializable> 인터페이스를 구현합니다. `ReadXml` 메서드는 먼저 자신에게 전달된 `Ref`에서 `HRef`, `Source`, `MediaType` 및 <xref:System.Xml.XmlReader> 속성의 값을 읽습니다. 알 수 없는 특성은 모두 <xref:System.ServiceModel.Syndication.SyndicationFeed.AttributeExtensions%2A> 컬렉션에 저장됩니다. 모든 특성을 읽으면 <xref:System.Xml.XmlReader.ReadStartElement>가 호출되어 판독기가 다음 요소로 진행합니다. 이 클래스에서 모델링된 요소에는 필수 자식이 없으므로 다음 코드에 나온 것처럼 자식 요소는 `XElement` 인스턴스로 버퍼링되고 <xref:System.ServiceModel.Syndication.SyndicationFeed.ElementExtensions%2A> 컬렉션에 저장됩니다.  
  
```  
public void ReadXml(System.Xml.XmlReader reader)  
{  
    bool isEmpty = reader.IsEmptyElement;  
  
    if (reader.HasAttributes)  
    {  
        for (int i = 0; i < reader.AttributeCount; i++)  
        {  
            reader.MoveToNextAttribute();  
  
            if (reader.NamespaceURI == "")  
            {  
                if (reader.LocalName == "ref")  
                {  
                    this.Ref = reader.Value;  
                }  
                else if (reader.LocalName == "href")  
                {  
                    this.Href = new Uri(reader.Value);  
                }  
                else if (reader.LocalName == "source")  
                {  
                    this.Source = new Uri(reader.Value);  
                }  
                else if (reader.LocalName == "type")  
                {  
                    this.MediaType = reader.Value;  
                }  
                else  
                {  
                    this.AttributeExtensions.Add(new   
                                 XmlQualifiedName(reader.LocalName,   
                                 reader.NamespaceURI),   
                                 reader.Value);  
                }  
            }  
        }  
    }  
  
    reader.ReadStartElement();  
  
    if (!isEmpty)  
    {  
        while (reader.IsStartElement())  
        {  
            ElementExtensions.Add(  
                  (XElement) XElement.ReadFrom(reader));  
        }  
        reader.ReadEndElement();  
    }  
}  
```  
  
 `WriteXml`에서 `InReplyToElement` 메서드는 먼저 `Ref`, `HRef`, `Source` 및 `MediaType` 속성의 값을 XML 특성으로 씁니다. `WriteXml`은 `WriteXml`의 호출자가 수행한 실제 외부 요소는 쓰지 않습니다. 다음 코드에 나온 것처럼 이 메서드는 또한 <xref:System.ServiceModel.Syndication.SyndicationFeed.AttributeExtensions%2A> 및 <xref:System.ServiceModel.Syndication.SyndicationFeed.ElementExtensions%2A>의 내용을 작성기에 씁니다.  
  
```  
public void WriteXml(System.Xml.XmlWriter writer)  
{  
    if (this.Ref != null)  
    {  
        writer.WriteAttributeString("ref", InReplyToElement.NsUri,   
                                            this.Ref);  
    }  
    if (this.Href != null)  
    {  
        writer.WriteAttributeString("href", InReplyToElement.NsUri,   
                                                this.Href.ToString());  
    }  
    if (this.Source != null)  
    {  
        writer.WriteAttributeString("source", InReplyToElement.NsUri,   
                                              this.Source.ToString());  
    }  
    if (this.MediaType != null)  
    {  
        writer.WriteAttributeString("type", InReplyToElement.NsUri,   
                                                    this.MediaType);  
    }  
  
    foreach (KeyValuePair<XmlQualifiedName, string> kvp in   
                                             this.AttributeExtensions)  
    {  
        writer.WriteAttributeString(kvp.Key.Name, kvp.Key.Namespace,   
                                                   kvp.Value);  
    }  
  
    foreach (XElement element in this.ElementExtensions)  
    {  
        element.WriteTo(writer);  
    }  
}  
```  
  
## <a name="threadedfeed-and-threadeditem"></a>ThreadedFeed 및 ThreadedItem  
 이 샘플에서는 `SyndicationItems` 확장을 포함하는 `InReplyTo`가 `ThreadedItem` 클래스에 의해 모델링됩니다. 마찬가지로 `ThreadedFeed` 클래스는 항목이 `SyndicationFeed`의 모든 인스턴스인 `ThreadedItem`입니다.  
  
 `ThreadedFeed` 클래스는 `SyndicationFeed`에서 상속되고 `OnCreateItem`을 재정의하여 `ThreadedItem`을 반환합니다. 다음 코드에 나온 것처럼 이 클래스는 또한 `Items` 컬렉션에 액세스하기 위한 메서드를 `ThreadedItems`로 구현합니다.  
  
```  
public class ThreadedFeed : SyndicationFeed  
{  
    public ThreadedFeed()  
    {  
    }  
  
    public IEnumerable<ThreadedItem> ThreadedItems  
    {  
        get  
        {  
            return this.Items.Cast<ThreadedItem>();  
        }  
    }  
  
    protected override SyndicationItem CreateItem()  
    {  
        return new ThreadedItem();  
    }  
}  
```  
  
 `ThreadedItem` 클래스는 `SyndicationItem`에서 상속되고 `InReplyToElement`를 강력한 형식의 속성으로 만듭니다. 이 클래스는 `InReplyTo` 확장 데이터에 대한 편리한 프로그래밍 액세스를 제공하며, 다음 코드에 나온 것처럼 이 클래스는 또한 확장 데이터를 읽고 쓰기 위한 `TryParseElement` 및 `WriteElementExtensions`를 구현합니다.  
  
```  
public class ThreadedItem : SyndicationItem  
{  
    private InReplyToElement inReplyTo;  
    // Constructors  
        public ThreadedItem()  
        {  
            inReplyTo = new InReplyToElement();  
        }  
  
        public ThreadedItem(string title, string content, Uri itemAlternateLink, string id, DateTimeOffset lastUpdatedTime) : base(title, content, itemAlternateLink, id, lastUpdatedTime)  
        {  
            inReplyTo = new InReplyToElement();  
        }  
  
    public InReplyToElement InReplyTo  
    {  
        get { return this.inReplyTo; }  
    }  
  
    protected override bool TryParseElement(  
                        System.Xml.XmlReader reader,   
                        string version)  
    {  
        if (version == SyndicationVersions.Atom10 &&  
            reader.NamespaceURI == InReplyToElement.NsUri &&  
            reader.LocalName == InReplyToElement.ElementName)  
        {  
            this.inReplyTo = new InReplyToElement();  
  
            this.InReplyTo.ReadXml(reader);  
  
            return true;  
        }  
        else  
        {  
            return base.TryParseElement(reader, version);  
        }  
    }  
  
    protected override void WriteElementExtensions(XmlWriter writer,   
                                                 string version)  
    {  
        if (this.InReplyTo != null &&   
                     version == SyndicationVersions.Atom10)  
        {  
            writer.WriteStartElement(InReplyToElement.ElementName,   
                                           InReplyToElement.NsUri);  
            this.InReplyTo.WriteXml(writer);  
            writer.WriteEndElement();  
        }  
  
        base.WriteElementExtensions(writer, version);  
    }  
}  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Syndication\StronglyTypedExtensions`  
