---
title: Xamarin을 사용 하 여 빌드된 tvOS 10 앱 문제 해결
description: 이 문서에서는 Xamarin 앱에서 tvOS 10으로 작업 하기 위한 몇 가지 문제 해결 팁을 제공 합니다. 앱 스토어, 이진 호환성, CFNetwork HttpProtocol, CloudKit, Core 이미지, NSUserActivity 및 UIKit와 관련 된 문제를 설명 합니다.
ms.prod: xamarin
ms.assetid: EA5564BB-C415-49A2-B70C-3DBF5E0F3FAB
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/16/2017
ms.openlocfilehash: a6588dee675aee3e2580b70dfdea2920c6235775
ms.sourcegitcommit: 2fbe4932a319af4ebc829f65eb1fb1816ba305d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73030609"
---
# <a name="troubleshooting-tvos-10-apps-built-with-xamarin"></a>Xamarin을 사용 하 여 빌드된 tvOS 10 앱 문제 해결

다음 섹션에는 Xamarin에서 tvOS 10을 사용 하 고 해당 문제에 대 한 해결 방법을 사용할 때 발생할 수 있는 몇 가지 알려진 문제가 나와 있습니다.

- [App Store](#App-Store)
- [이진 호환성](#Binary-Compatibility)
- [CFNetwork HTTP 프로토콜](#CFNetwork-HTTP-Protocol)
- [CloudKit](#CloudKit)
- [핵심 이미지](#CoreImage)
- [NSUserActivity](#NSUserActivity)
- [UIKit](#UIKit)

<a name="App-Store" />

## <a name="app-store"></a>App Store

알려진 문제:

- 샌드박스 환경에서 앱에서 바로 구매를 테스트할 때 인증 대화 상자가 두 번 표시 될 수 있습니다.
- 샌드박스 환경에서 호스팅된 콘텐츠를 사용 하 여 앱 내 구매를 테스트할 때 콘텐츠 다운로드가 완료 될 때까지 앱이 포그라운드로 전환 될 때마다 암호 대화 상자가 표시 됩니다.

<a name="Binary-Compatibility" />

## <a name="binary-compatibility"></a>이진 호환성

알려진 문제:

- `NSObject.ValueForKey`를 호출 하면 `null` 키가 발생 하 여 예외가 발생 합니다.
- `UIFont.WithName`를 호출할 때 이름을 기준으로 글꼴을 참조 하면 충돌이 발생 합니다.
- `NSURLSession` 및 `NSURLConnection`는 모두 `http://` Url에 대 한 TLS 핸드셰이크 중에 더 이상 RC4 암호 그룹을 사용할 필요가 없습니다.
- 앱이 `ViewWillLayoutSubviews` 또는 `LayoutSubviews` 방법 중 하나에서 슈퍼 뷰의 기 하 도형을 수정 하면 중단 될 수 있습니다.
- 모든 SSL/TLS 연결의 경우 이제 RC4 대칭 암호화가 기본적으로 사용 하지 않도록 설정 됩니다. 또한 보안 전송 API는 더 이상 SSLv3을 지원 하지 않으며, 가능한 한 빨리 SHA-1 및 3DES 암호화를 사용 하 여 앱을 중지 하는 것이 좋습니다.

<a name="CFNetwork-HTTP-Protocol" />

## <a name="cfnetwork-http-protocol"></a>CFNetwork HTTP 프로토콜

`NSURLConnection` 및 `NSURLSession`에서이 요구 사항을 엄격 하 게 적용 하기 때문에 `NSMutableURLRequest` 클래스의 `HTTPBodyStream` 속성을 열지 않은 스트림으로 설정 해야 합니다.

<a name="CloudKit" />

## <a name="cloudkit"></a>CloudKit

장기 실행 작업은 _"파일을 저장할 수 있는 권한이 없습니다."를 반환 합니다._ 메시지가.

<a name="CoreImage" />

## <a name="core-image"></a>핵심 이미지

`CIImageProcessor` API는 이제 임의의 입력 이미지 수를 지원 합니다. tvOS 10 beta 1에 포함 된 `CIImageProcessor` API가 제거 됩니다.

<a name="NSUserActivity" />

## <a name="nsuseractivity"></a>NSUserActivity

전달 작업 후에 `NSUserActivity` 개체의 `UserInfo` 속성이 비어 있을 수 있습니다. 현재 해결 방법으로 `BecomeCurrent` NSUserActivity ' 개체를 명시적으로 호출 합니다.

<a name="UIKit" />

## <a name="uikit"></a>UIKit

알려진 문제:

- `UINavigationBar`, `UITabBar` 또는 `UIToolBar`의 배경 모양이 변경 되 면 레이아웃 패스가 새 모양을 확인 하 게 됩니다. `LayoutSubviews`, `UpdateConstraints`, `WillLayoutSubviews` 또는 `DidUpdateSubviews` 이벤트 내에서 이러한 모양새를 수정 하려고 하면 무한 레이아웃 루프가 발생할 수 있습니다.
- TvOS 10에서 `UIView` 개체의 `RemoveGestureRecognizer` 메서드를 호출 하면 진행 중인 제스처 인식기가 명시적으로 취소 됩니다.
- 표시 된 뷰 컨트롤러는 이제 상태 표시줄의 모양에 영향을 줄 수 있습니다.
- tvOS 10에서는 `UIViewController`를 서브클래싱 하 고 `AwakeFromNib` 메서드를 재정의할 때 개발자가 `base.AwakeFromNib`를 호출 해야 합니다.
- `base.LayoutSubviews`를 호출 하기 전에 `LayoutSubviews`를 재정의 하 고 레이아웃을 변경 하는 사용자 지정 `UIView` 서브 클래스가 있는 앱은 tvOS 10에서 무한 레이아웃 루프를 트리거할 수 있습니다.
- 방향 관련 이미지 또는 flippable 이미지 자산은 `UIButton` 개체에 할당 될 때 대칭 이동 하지 않습니다.

## <a name="related-links"></a>관련 링크

- [tvOS 샘플](https://docs.microsoft.com/samples/browse/?products=xamarin&term=Xamarin.iOS+tvOS)
- [TvOS 10의 새로운 기능](https://developer.apple.com/library/prerelease/content/releasenotes/General/WhatsNewinTVOS/Articles/tvOS10.html#//apple_ref/doc/uid/TP40017259-SW1)
