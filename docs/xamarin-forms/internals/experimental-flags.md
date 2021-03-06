---
title: Xamarin 양식 실험적 플래그
description: Xamarin 양식 실험적 플래그를 사용 하면 엔지니어링 팀에서 사용자에 게 새 기능을 보다 신속 하 게 제공할 수 있으며, 기능 Api를 안정적인 릴리스로 전환 하기 전에 변경할 수 있습니다.
ms.prod: xamarin
ms.assetid: AF4BDD27-89F6-48AE-A8CD-D7E4DDA2CCA2
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 03/20/2020
ms.openlocfilehash: cebb996da992058616f9cf96ef3212c9ce27022a
ms.sourcegitcommit: 6c60914b380ff679bbffd7790edd4d5e18005d0a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80112602"
---
# <a name="xamarinforms-experimental-flags"></a>Xamarin 양식 실험적 플래그

새 Xamarin.ios 기능이 구현 되 면 종종 실험적 플래그 뒤에 배치 됩니다. 이를 통해 엔지니어링 팀은 새로운 기능을 보다 신속 하 게 제공할 수 있으며, 기능 Api를 안정적인 릴리스로 전환 하기 전에 계속 해 서 변경할 수 있습니다. 그러면 기능이 안정적인 릴리스로 이동 되 면 실험적 플래그가 제거 됩니다.

Xamarin.ios에는 다음과 같은 실험적 플래그가 포함 되어 있습니다.

- `CarouselView_Experimental`
- `IndicatorView_Experimental`
- `Markup_Experimental`
- `MediaElement_Experimental`
- `Shell_UWP_Experimental`
- `StateTriggers_Experimental`
- `SwipeView_Experimental`

실험적 플래그 뒤에 있는 기능을 사용 하려면 응용 프로그램에서 플래그 또는 플래그를 사용 하도록 설정 해야 합니다. 실험적 플래그를 사용 하는 방법에는 두 가지가 있습니다.

- 플랫폼 프로젝트에서 실험적 플래그 또는 플래그를 사용 하도록 설정 합니다.
- `App` 클래스에서 실험적 플래그 또는 플래그를 사용 하도록 설정 합니다.

> [!WARNING]
> 플래그를 사용 하지 않고 실험적 플래그를 사용 하는 기능을 사용 하면 응용 프로그램에서 사용 해야 하는 플래그를 나타내는 예외를 throw 합니다.

## <a name="enable-flags-in-platform-projects"></a>플랫폼 프로젝트에서 플래그 사용

`Xamarin.Forms.Forms.SetFlags` 메서드를 사용 하 여 플랫폼 프로젝트에서 실험적 플래그를 사용 하도록 설정할 수 있습니다.

```csharp
Xamarin.Forms.Forms.SetFlags("CarouselView_Experimental");
```

`SetFlags` 메서드는 iOS의 `AppDelegate` 클래스, Android의 `MainActivity` 클래스 및 UWP의 `App` 클래스에서 호출 해야 합니다.

> [!IMPORTANT]
> 플랫폼 프로젝트에서 실험적 플래그를 사용 하도록 설정 하는 것은 `Forms.Init` 메서드가 호출 되기 전에 발생 해야 합니다.

`Xamarin.Forms.Forms.SetFlags` 메서드는 단일 메서드 호출에서 여러 실험적 플래그를 사용 하도록 설정할 수 있는 `string` 배열 인수를 수락 합니다.

```csharp
Xamarin.Forms.Forms.SetFlags(new string[] { "CarouselView_Experimental", "IndicatorView_Experimental", "SwipeView_Experimental" });
```

> [!WARNING]
> 후속 호출이 이전 호출의 결과를 덮어쓰기 때문에 `SetFlags` 메서드를 두 번 이상 호출 해서는 안 됩니다.

## <a name="enable-flags-in-your-app-class"></a>앱 클래스에서 플래그 사용

`Device.SetFlags` 메서드를 사용 하 여 공유 코드 프로젝트의 `App` 클래스에서 실험적 플래그를 사용 하도록 설정할 수 있습니다.

```csharp
Device.SetFlags(new string[]{ "MediaElement_Experimental" });
```

`Device.SetFlags` 메서드는 단일 메서드 호출에서 여러 실험적 플래그를 사용 하도록 설정할 수 있는 `IReadOnlyList<string>` 인수를 수락 합니다.

```csharp
Device.SetFlags(new string[]{ "CarouselView_Experimental", "MediaElement_Experimental", "SwipeView_Experimental" });
```

> [!WARNING]
> 후속 호출이 이전 호출의 결과를 덮어쓰기 때문에 `SetFlags` 메서드를 두 번 이상 호출 해서는 안 됩니다.
