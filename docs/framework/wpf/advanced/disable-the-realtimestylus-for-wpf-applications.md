---
title: WPF 애플리케이션에 대해 RealTimeStylus를 사용하지 않도록 설정
ms.date: 03/30/2017
ms.assetid: e0525309-5ede-4782-837d-dbf6e5554859
ms.openlocfilehash: acae177e1c49a6a1161bcf48f8e2e8ac1bfe13b8
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991847"
---
# <a name="disable-the-realtimestylus-for-wpf-applications"></a>WPF 애플리케이션에 대해 RealTimeStylus를 사용하지 않도록 설정
WPF (Windows Presentation Foundation)는 Windows 7 touch 입력 처리를 기본적으로 지원 합니다. 지원은 태블릿 플랫폼의 실시간 스타일러스 입력을 <xref:System.Windows.UIElement.OnStylusDown%2A> <xref:System.Windows.UIElement.OnStylusUp%2A>통해, 및 <xref:System.Windows.UIElement.OnStylusMove%2A> 이벤트로 제공 됩니다. 또한 Windows 7은 Win32 WM_TOUCH 창 메시지로 다중 터치 입력을 제공 합니다. 이러한 두 Api는 동일한 HWND에서 함께 사용할 수 없습니다. 태블릿 플랫폼 (WPF 응용 프로그램의 경우 기본값)을 통해 터치식 입력을 사용 하면 WM_TOUCH 메시지를 사용할 수 없습니다. 따라서 WPF 창에서 WM_TOUCH를 사용 하 여 터치 메시지를 받으려면 WPF에서 기본 제공 스타일러스 지원을 사용 하지 않도록 설정 해야 합니다. 이는 WM_TOUCH를 사용 하는 구성 요소를 호스팅하는 WPF 창과 같은 시나리오에서 적용 됩니다.  
  
 스타일러스 입력을 수신 하는 WPF를 사용 하지 않도록 설정 하려면 WPF 창에 의해 추가 된 태블릿 지원을 제거 합니다.  
  
## <a name="example"></a>예제  
 다음 샘플 코드에서는 리플렉션을 사용 하 여 기본 태블릿 플랫폼 지원을 제거 하는 방법을 보여 줍니다.  
  
```csharp  
public static void DisableWPFTabletSupport()  
{  
    // Get a collection of the tablet devices for this window.    
    TabletDeviceCollection devices = System.Windows.Input.Tablet.TabletDevices;  
  
    if (devices.Count > 0)  
    {     
        // Get the Type of InputManager.  
        Type inputManagerType = typeof(System.Windows.Input.InputManager);  
  
        // Call the StylusLogic method on the InputManager.Current instance.  
        object stylusLogic = inputManagerType.InvokeMember("StylusLogic",  
                    BindingFlags.GetProperty | BindingFlags.Instance | BindingFlags.NonPublic,  
                    null, InputManager.Current, null);  
  
        if (stylusLogic != null)  
        {  
            //  Get the type of the stylusLogic returned from the call to StylusLogic.  
            Type stylusLogicType = stylusLogic.GetType();  
  
            // Loop until there are no more devices to remove.  
            while (devices.Count > 0)  
            {  
                // Remove the first tablet device in the devices collection.  
                stylusLogicType.InvokeMember("OnTabletRemoved",  
                        BindingFlags.InvokeMethod | BindingFlags.Instance | BindingFlags.NonPublic,  
                        null, stylusLogic, new object[] { (uint)0 });  
            }                  
        }  
  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- [스타일러스에서 입력 가로채기](intercepting-input-from-the-stylus.md)
