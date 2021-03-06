---
title: Xamarin.ios에서 앱 검토 요청
description: 이 문서에서는 Apple에서 iOS 10에 추가 하는 RequestReview 방법에 대해 설명 하 고 Xamarin.ios에서이를 구현 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: 6408e707-b7dc-4557-b931-16a4d79b8930
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/29/2017
ms.openlocfilehash: 0522e6b1bcf3e0f927a403c12a9c27bb6b3bb3ff
ms.sourcegitcommit: 2fbe4932a319af4ebc829f65eb1fb1816ba305d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73031597"
---
# <a name="request-app-review-in-xamarinios"></a>Xamarin.ios에서 앱 검토 요청

_이 문서에서는 Apple에서 iOS 10에 추가 하는 RequestReview 방법과 Xamarin.ios에서이를 구현 하는 방법에 대해 설명 합니다._

IOS 10.3의 새로운 기능으로, `RequestReview()` 방법을 사용 하면 iOS 앱에서 사용자에 게 평가 또는 검토를 요청할 수 있습니다. 사용자가 앱 스토어에서 설치한 배송 앱에서이 메서드를 호출 하면 iOS 10은 개발자에 대 한 전체 등급 및 검토 프로세스를 처리 합니다. 이 프로세스는 앱 스토어 정책에 의해 제어 되므로 경고가 표시 될 수도 있고 표시 되지 않을 수도 있습니다.

![](request-app-review-images/review01.png "A sample Review Request alert")

## <a name="requesting-a-rating-or-review"></a>등급 또는 리뷰 요청

사용자 환경에 적합 한 지점에서 `SKStoreReviewController` 클래스의 `RequestReview()` 정적 메서드를 호출할 수 있지만, 검토 프로세스는 앱 스토어 정책에 의해 제어 되 고 처리 됩니다. 결과적으로이 메서드는 경고를 표시 하거나 표시 하지 않을 수 있으며 단추 누르기와 같은 사용자 동작에 대 한 응답으로 호출 되 면 안 됩니다.

예를 들어 앱은 지정 된 횟수 만큼 시작 된 후에 검토를 요청 하거나, 플레이어가 수준을 완료 한 후에 검토를 요청할 수 있습니다.

Xamarin.ios 앱이 시작 되는 즉시 검토를 요청 하려면 `AppDelegate.cs` 파일을 다음과 같이 변경 합니다.

```csharp
using Foundation;
using StoreKit;
using UIKit;

namespace iOSTenThree
{
    [Register ("AppDelegate")]
    public class AppDelegate : UIApplicationDelegate
    {
        ...

        public override bool FinishedLaunching (UIApplication application, NSDictionary launchOptions)
        {
            // Request a review from the user
            SKStoreReviewController.RequestReview ();

            return true;
        }

        ...

    }
}
```

> [!NOTE]
> 개발 중인 앱에서 `RequestReview()`를 호출 하면 항상 등급 및 검토 대화 상자가 표시 되므로 테스트를 수행할 수 있습니다. 이는 TestFlight를 통해 배포 된 앱에는 적용 되지 않습니다 .이 경우 메서드 호출은 무시 됩니다.

사용자가 앱 스토어에서 설치한 배송 앱에서 `RequestReview()` 메서드가 호출 되 면 iOS 10은 개발자를 위한 전체 등급 및 검토 프로세스를 처리 합니다. 이 프로세스는 앱 스토어 정책에 의해 제어 되므로 경고가 표시 되거나 표시 되지 않을 수 있습니다.

## <a name="linking-to-an-app-store-product-page"></a>앱 스토어 제품 페이지에 연결 

새 `RequestReview` 메서드 외에도 개발자는 앱 내에서 앱 스토어에 있는 앱의 제품 페이지에 대 한 심층 링크를 제공할 수 있습니다. 제품 페이지 URL의 끝에 `action=write-review`을 추가 하면 사용자가 자동으로 앱의 검토를 작성할 수 있는 페이지가 열립니다. 

## <a name="summary"></a>요약

이 문서에서는 Apple에서 iOS 10에 추가 하 고 Xamarin.ios에서 구현 하는 방법에 대 한 RequestReview 방법에 대해 설명 했습니다.

## <a name="related-links"></a>관련 링크

- [iOSTenThree 샘플](https://docs.microsoft.com/samples/xamarin/ios-samples/ios10-iostenthree/)
