---
title: iOS 6 소개
description: 이 문서는 iOS 6에서 도입 된 기능을 설명 하는 가이드로 연결 됩니다. 컬렉션 보기, PassKit, 소셜 프레임 워크 및 미디어 키트에 대 한 변경 내용이 모두 설명 되어 있습니다.
ms.prod: xamarin
ms.assetid: 242DA7E3-8FD8-5F20-285D-603259CA622D
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/19/2017
ms.openlocfilehash: d30789a33eb8023f4ce77b4a7c2445fabca0f2db
ms.sourcegitcommit: 2fbe4932a319af4ebc829f65eb1fb1816ba305d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73031831"
---
# <a name="introduction-to-ios-6"></a>iOS 6 소개

_iOS 6에는 앱을 개발 하기 위한 다양 한 새 기술이 포함 되어 있으며, Xamarin.ios 6 C# 은 개발자에 게 제공 됩니다._

[![](images/ios6-large.jpg "The iOS 6 logo")](images/ios6-large.jpg#lightbox)

Ios 6 및 Xamarin.ios 6을 사용 하면 개발자는 iPhone 5를 대상으로 하는 응용 프로그램을 포함 하 여 iOS 응용 프로그램을 만들 수 있는 다양 한 기능이 있습니다.
이 문서에서는 사용 가능한 흥미로운 새 기능 중 일부와 각 항목에 대 한 문서에 대 한 링크를 제공 합니다. 또한 개발자가 iOS 6으로 이동 하 고 iPhone 5의 새로운 해상도를 사용할 때 중요 한 몇 가지 변경 내용을 다룹니다.

## <a name="introduction-to-collection-viewsiosuser-interfacecontrolsuicollectionviewmd"></a>[컬렉션 뷰 소개](~/ios/user-interface/controls/uicollectionview.md)

컬렉션 뷰를 사용 하면 임의의 레이아웃을 사용 하 여 콘텐츠를 표시할 수 있습니다. 또한 사용자 지정 레이아웃을 지 원하는 동시에 즉시 표 형태의 레이아웃을 쉽게 만들 수 있습니다. 자세한 내용은 [컬렉션 뷰 소개 가이드](~/ios/user-interface/controls/uicollectionview.md)[를 참조하세요.

## <a name="introduction-to-passkitiosplatformpasskitmd"></a>[PassKit 소개](~/ios/platform/passkit.md)

PassKit 프레임 워크를 사용 하면 응용 프로그램이 Passbook 앱에서 관리 되는 디지털 패스와 상호 작용할 수 있습니다. 자세한 내용은 [Pass Kit 소개 가이드](~/ios/platform/passkit.md)를 참조 하세요.

## <a name="introduction-to-eventkitiosplatformeventkitmd"></a>[EventKit 소개](~/ios/platform/eventkit.md)

EventKit 프레임 워크는 일정 데이터베이스에서 저장 하는 일정, 일정 이벤트 및 미리 알림 데이터에 액세스 하는 방법을 제공 합니다. IOS 4부터 달력 및 일정 이벤트에 대 한 액세스를 사용할 수 있었지만 이제 iOS 6은 미리 알림 데이터에 대 한 액세스를 노출 합니다. 자세한 내용은 [I](~/ios/platform/eventkit.md) [소개 to eventkit](~/ios/platform/eventkit.md) guide를 참조 하세요.

## <a name="introduction-to-the-social-frameworkiosplatformsocial-frameworkmd"></a>[소셜 프레임 워크 소개](~/ios/platform/social-framework.md)

소셜 프레임 워크는 Twitter 및 Facebook을 비롯 한 소셜 네트워크와의 상호 작용을 위한 통합 API 뿐만 아니라 중국의 사용자를 위한 SinaWeibo을 제공 합니다. 자세한 내용은 [소셜 프레임 워크 소개](~/ios/platform/social-framework.md) 가이드를 참조 하세요.

## <a name="changes-to-storekitchanges-to-storekitmd"></a>[StoreKit 변경 내용](changes-to-storekit.md)

Apple은 스토어 키트에 두 가지 새로운 기능인 앱 내에서 iTunes 또는 App Store 콘텐츠를 구매 및 다운로드 하 고 앱 내 구매를 위한 콘텐츠 파일을 호스트 하는 두 가지 새로운 기능을 도입 했습니다. 자세한 내용은 [스토어 키트에 대 한 변경 사항](changes-to-storekit.md) 가이드를 참조 하세요.

## <a name="other-changes"></a>기타 변경 내용

### <a name="viewwillunload-and-viewdidunload-deprecated"></a>ViewWillUnload 및 ViewDidUnload 사용 되지 않음

`UIViewController`의 `ViewWillUnload` 및 `ViewDidUnload` 메서드는 iOS 6에서 더 이상 호출 되지 않습니다. 이전 버전의 iOS에서 이러한 메서드는 응용 프로그램에서 뷰가 언로드 되기 전의 상태를 저장 하는 데 사용 했을 수 있습니다.

예를 들어, Mac용 Visual Studio는 아래와 같이 `ReleaseDesignerOutlets`라는 메서드를 만들어 `ViewDidUnload`에서 호출 됩니다.

```csharp
void ReleaseDesignerOutlets ()
{
    if (myOutlet != null) {
        myOutlet.Dispose ();
        myOutlet = null;
    }
}
```

그러나 iOS 6에서는 더 이상 `ReleaseDesignerOutlets`를 호출할 필요가 없습니다.   

정리 코드의 경우 iOS 6 응용 프로그램은 `DidReceiveMemoryWarning`를 사용 해야 합니다. 그러나 `Dispose`를 호출 하는 코드는 아래와 같이 메모리를 많이 사용 하는 개체에 대해서만 사용 해야 합니다.

```csharp
if (myImageView != null){
    if (myImageView.Superview == null){
        myImageView.Dispose();
        myImageView = null;
    }
}
```

다시, 위와 같이 `Dispose`를 호출 하는 것은 거의 필요 하지 않습니다. 일반적으로 대부분의 응용 프로그램은 이벤트 처리기를 제거 하는 것입니다.

상태를 저장 하는 경우 응용 프로그램은 `ViewWillUnload`대신 `ViewWillDisappear` 및 `ViewDidDisappear`에서이를 수행할 수 있습니다.

### <a name="iphone-5-resolution"></a>iPhone 5 해상도

iPhone 5 장치에는 640x1136 해상도가 있습니다. 이전 버전의 iOS를 대상으로 하는 응용 프로그램은 아래와 같이 iPhone 5에서 실행 될 때 letterboxed 표시 됩니다.

 [![](images/01-letterboxed.png "Applications that targeted previous versions of iOS will appear letterboxed when run on an iPhone 5")](images/01-letterboxed.png#lightbox)

응용 프로그램이 iPhone 5에서 전체 화면에 표시 되려면 640x1136의 해상도를 가진 `Default-568h@2x.png` 이라는 이미지를 추가 하기만 하면 됩니다. 다음 스크린샷은이 이미지가 포함 된 후 실행 되는 응용 프로그램을 보여 줍니다.

 [![](images/02-fullscreen.png "This screenshot shows the application running after this image has been included")](images/02-fullscreen.png#lightbox)

### <a name="subclassing-uinavigationbar"></a>UINavigationBar 하위 클래스

IOS 6에서는 `UINavigationBar` 서브클래싱 할 수 있습니다. 이렇게 하면 `UINavigationBar`의 모양과 느낌을 더욱 세밀 하 게 제어할 수 있습니다. 예를 들어 응용 프로그램은 하위 뷰를 추가 하 고, 해당 뷰에 애니메이션 효과를 적용 하 고, `UINavigationBar`범위를 수정할 수 있습니다.

아래 코드는 `UIImageView`를 추가 하는 서브클래싱된 `UINavigationBar`의 예를 보여 줍니다.

```csharp
public class CustomNavBar : UINavigationBar
{
    UIImageView iv;
    public CustomNavBar (IntPtr h) : base(h)
    {
        iv = new UIImageView (UIImage.FromFile ("monkey.png"));
        iv.Frame = new CGRect (75, 0, 30, 39);
    }
    public override void Draw (RectangleF rect)
    {
        base.Draw (rect);
        TintColor = UIColor.Purple;
        AddSubview (iv);
    }
}
```

`UINavigationController`에 서브클래싱된 `UINavigationBar`를 추가 하려면 아래와 같이 `UINavigationBar` 및 `UIToolbar`의 형식을 사용 하는 `UINavigationController` 생성자를 사용 합니다.

```csharp
navController = new UINavigationController (typeof(CustomNavBar), typeof(UIToolbar));
```

이 `UINavigationBar` 하위 클래스를 사용 하면 다음 스크린샷에 표시 된 것 처럼 이미지 뷰가 표시 됩니다.

 [![](images/03-navbar.png "Using this UINavigationBar subclass results in the image view being displayed as shown in this screenshot")](images/03-navbar.png#lightbox)

### <a name="interface-orientation"></a>인터페이스 방향

IOS 6 응용 프로그램이 `ShouldAutorotateToInterfaceOrientation`를 재정의 하 고 특정 컨트롤러에서 지 원하는 모든 방향에 대해 true를 반환 합니다. 예를 들어 다음 코드는 세로만 지 원하는 데 사용 됩니다.

```csharp
public override bool ShouldAutorotateToInterfaceOrientation (UIInterfaceOrientation toInterfaceOrientation)
    {
        return (toInterfaceOrientation == UIInterfaceOrientation.Portrait);
    }
```

IOS 6 `ShouldAutorotateToInterfaceOrientation`은 더 이상 사용 되지 않습니다.
대신 응용 프로그램은 아래와 같이 루트 뷰 컨트롤러에서 `GetSupportedInterfaceOrientations`를 재정의할 수 있습니다.

```csharp
public override UIInterfaceOrientationMask GetSupportedInterfaceOrientations ()
    {
        return UIInterfaceOrientationMask.Portrait;
    }
```

IPad에서는 `GetSupportedInterfaceOrientation` 구현 되지 않은 경우이 기본값은 모두 네 방향으로 설정 됩니다. IPhone 및 iPod Touch에서 기본값은 `PortraitUpsideDown`를 제외한 모든 방향입니다.
