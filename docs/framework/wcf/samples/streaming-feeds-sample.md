---
title: 스트리밍 피드 샘플
ms.date: 03/30/2017
ms.assetid: 1f1228c0-daaa-45f0-b93e-c4a158113744
ms.openlocfilehash: f37e7791bc407a57432fb9f6900ad8f19ff4eb52
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044687"
---
# <a name="streaming-feeds-sample"></a>스트리밍 피드 샘플
이 샘플에서는 많은 수의 항목이 포함된 배포 피드를 관리하는 방법을 보여 줍니다. 서버에서 이 샘플은 항목을 네트워크 스트림에 쓰기 바로 전까지 피드 내에 개별 <xref:System.ServiceModel.Syndication.SyndicationItem> 개체를 만드는 동작을 지연시키는 방법을 보여 줍니다.  
  
 클라이언트에서 이 샘플은 사용자 지정 배포 피드 포맷터를 사용하여 읽고 있는 피드가 메모리에 완전히 버퍼링되지 않도록 네트워크 스트림에서 개별 항목을 읽을 수 있는 방법을 보여 줍니다.  
  
 배포 API의 스트리밍 기능을 가장 잘 보여 주기 위해 이 샘플에서는 서버가 매우 많은 수의 항목이 포함된 피드를 노출하는 경우와 같이 실제로 드문 시나리오를 사용합니다. 이 경우 서버는 클라이언트가 피드에서 지정된 수의 항목(기본값: 10개)을 읽었다고 확인할 때까지 계속해서 피드에 새 항목을 생성합니다. 단순성을 위해 클라이언트와 서버는 모두 동일한 프로세스로 구현되며 공유 `ItemCounter` 개체를 사용하여 클라이언트가 생성한 항목의 수를 추적합니다. `ItemCounter` 형식은 샘플 시나리오를 간단히 종료할 목적으로만 사용되며 설명하려는 패턴의 핵심 요소는 아닙니다.  
  
 이 데모에서는 `yield return` 키워드 구문을 사용 C# 하 여 Visual 반복기를 사용 합니다. 반복기에 대 한 자세한 내용은 MSDN의 "반복기 사용" 항목을 참조 하십시오.  
  
## <a name="service"></a>서비스  
 이 서비스는 다음 코드에서와 같이 하나의 작업으로 구성된 기본 <xref:System.ServiceModel.Web.WebGetAttribute> 계약을 구현합니다.  
  
```  
[ServiceContract]  
interface IStreamingFeedService  
{  
    [WebGet]  
    [OperationContract]  
    Atom10FeedFormatter StreamedFeed();  
}  
```  
  
 이 서비스는 다음 코드에서와 같이 `ItemGenerator` 클래스에서 반복기를 사용하여 <xref:System.ServiceModel.Syndication.SyndicationItem> 인스턴스의 무한 스트림을 만드는 방식으로 이 계약을 구현합니다.  
  
```  
class ItemGenerator  
{  
    public IEnumerable<SyndicationItem> GenerateItems()  
    {  
        while (counter.GetCount() < maxItemsRead)  
        {  
            itemsReturned++;  
            yield return CreateNextItem();  
        }  
  
    }  
    ...  
}  
```  
  
 서비스 구현에서 피드를 만들면 버퍼링된 항목 컬렉션 대신 `ItemGenerator.GenerateItems()`의 출력이 사용됩니다.  
  
```  
public Atom10FeedFormatter StreamedFeed()  
{  
    SyndicationFeed feed = new SyndicationFeed("Streamed feed", "Feed to test streaming", null);  
    //Generate an infinite stream of items. Both the client and the service share  
    //a reference to the ItemCounter, which allows the sample to terminate  
    //execution after the client has read 10 items from the stream  
    ItemGenerator itemGenerator = new ItemGenerator(this.counter, 10);  
  
    feed.Items = itemGenerator.GenerateItems();  
    return feed.GetAtom10Formatter();  
}  
```  
  
 결과적으로 항목 스트림은 메모리에 완전히 버퍼링되지 않습니다. 메서드 내의 `yield return` 문에 중단점을 설정 하 고 서비스가 `StreamedFeed()` 메서드의 결과를 반환한 후 처음으로이 중단점이 발생 하는 것을 확인 하 여이 동작을 관찰할 수 있습니다. `ItemGenerator.GenerateItems()`  
  
## <a name="client"></a>클라이언트  
 이 샘플의 클라이언트는 피드에 있는 개별 항목을 메모리에 버퍼링하는 대신 이 항목의 구체화를 지연시키는 사용자 지정 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> 구현을 사용합니다. 사용자 지정 `StreamedAtom10FeedFormatter` 인스턴스는 다음과 같이 사용됩니다.  
  
```  
XmlReader reader = XmlReader.Create("http://localhost:8000/Service/Feeds/StreamedFeed");  
StreamedAtom10FeedFormatter formatter = new StreamedAtom10FeedFormatter(counter);  
  
SyndicationFeed feed = formatter.ReadFrom(reader);  
```  
  
 일반적으로 네트워크에서 피드의 전체 콘텐츠를 읽고 메모리에 버퍼링할 때까지는 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter.ReadFrom%28System.Xml.XmlReader%29>에 대한 호출이 반환되지 않습니다. 반면 `StreamedAtom10FeedFormatter` 개체는 다음 코드에서와 같이 <xref:System.ServiceModel.Syndication.Atom10FeedFormatter.ReadItems%28System.Xml.XmlReader%2CSystem.ServiceModel.Syndication.SyndicationFeed%2CSystem.Boolean%40%29>를 재정의하고 버퍼링된 컬렉션 대신 반복기를 반환합니다.  
  
```  
protected override IEnumerable<SyndicationItem> ReadItems(XmlReader reader, SyndicationFeed feed, out bool areAllItemsRead)  
{  
    areAllItemsRead = false;  
    return DelayReadItems(reader, feed);  
}  
  
private IEnumerable<SyndicationItem> DelayReadItems(XmlReader reader, SyndicationFeed feed)  
{  
    while (reader.IsStartElement("entry", "http://www.w3.org/2005/Atom"))  
    {  
        yield return this.ReadItem(reader, feed);  
    }  
  
    reader.ReadEndElement();  
}  
```  
  
 따라서 `ReadItems()`의 결과를 이동하는 클라이언트 애플리케이션에서 사용 준비를 마칠 때까지는 네트워크에서 각 항목을 읽지 않습니다. 의 `yield return` `ReadFrom()` 내부 문에 중단점을 설정 하 고에 대 한 호출이 완료 된 후 처음으로이 중단점이 발생 하는 것을 확인 하 여이 동작을 관찰할 수 있습니다. `StreamedAtom10FeedFormatter.DelayReadItems()`  
  
 다음 지침에서는 샘플을 빌드하고 실행하는 방법을 보여 줍니다. 클라이언트에서 10개의 항목을 읽고 나면 서버에서 항목 생성을 중지하지만 출력에는 클라이언트에서 10개 항목보다 훨씬 많은 항목을 읽는 것으로 표시됩니다. 이는 샘플에서 사용되는 네트워킹 바인딩에서 데이터를 4KB 단위의 세그먼트로 전송하기 때문입니다. 따라서 클라이언트는 한 항목을 읽을 기회가 생기기도 전에 4KB의 항목 데이터를 받습니다. 이는 정상적인 동작입니다. 스트리밍된 HTTP 데이터를 적절한 크기의 세그먼트로 보내면 성능이 향상됩니다.  
  
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
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Syndication\StreamingFeeds`  
  
## <a name="see-also"></a>참고자료

- [독립형 진단 피드](../../../../docs/framework/wcf/samples/stand-alone-diagnostics-feed-sample.md)
