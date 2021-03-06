---
title: Android에서 웹 보기 확대/축소
description: 플랫폼별를 사용 하면 사용자 지정 렌더러 나 효과를 구현 하지 않고 특정 플랫폼 에서만 사용할 수 있는 기능을 사용할 수 있습니다. 이 문서에서는 웹 보기에서 확대/축소를 사용 하도록 설정 하는 Android 플랫폼 관련 기능을 사용 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: DC1A3762-6A42-4298-929C-445F416C3E60
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 05/09/2019
ms.openlocfilehash: 2142882add91d613263d11fa4c1e6d7ad142c7c7
ms.sourcegitcommit: 9bfedf07940dad7270db86767eb2cc4007f2a59f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2019
ms.locfileid: "68655995"
---
# <a name="webview-zoom-on-android"></a>Android에서 웹 보기 확대/축소

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

이 Android 플랫폼별는 [`WebView`](xref:Xamarin.Forms.WebView)에 대 한 확대/축소 및 확대/축소 컨트롤을 사용 합니다. @No__t_0를 설정 하 고 바인딩 가능한 속성 `WebView.DisplayZoomControls` 값을 `boolean` 하 여 XAML에서 사용 됩니다.

```xaml
<ContentPage ...
             xmlns:android="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific;assembly=Xamarin.Forms.Core">
    <WebView Source="https://www.xamarin.com"
             android:WebView.EnableZoomControls="true"
             android:WebView.DisplayZoomControls="true" />
</ContentPage>
```

바인딩 가능한 `WebView.EnableZoomControls` 속성은 [`WebView`](xref:Xamarin.Forms.WebView)에 대 한 확대/축소를 사용 하는지 여부를 제어 `WebView.DisplayZoomControls` 하 고, 바인딩 가능한 속성은 `WebView`에 확대/축소 컨트롤을 표시할지 여부를 제어 합니다.

또는 흐름 API를 C# 사용 하 여 플랫폼별를 사용할 수 있습니다.

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.AndroidSpecific;
...

webView.On<Android>()
    .EnableZoomControls(true)
    .DisplayZoomControls(true);
```

@No__t_0 메서드는이 플랫폼별가 Android 에서만 실행 되도록 지정 합니다. [@No__t_2](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific) 네임 스페이스의 `WebView.EnableZoomControls` 메서드는 [`WebView`](xref:Xamarin.Forms.WebView)에서 확대/축소를 사용 하도록 설정할지 여부를 제어 하는 데 사용 됩니다. 같은 네임 스페이스의 `WebView.DisplayZoomControls` 메서드는 확대/축소 컨트롤이 `WebView`에 중첩 되는지 여부를 제어 하는 데 사용 됩니다. 또한 `WebView.ZoomControlsEnabled` 및 `WebView.ZoomControlsDisplayed` 메서드를 사용 하 여 확대/축소 및 확대/축소 컨트롤을 각각 사용할 수 있는지 여부를 반환할 수 있습니다.

따라서 [`WebView`](xref:Xamarin.Forms.WebView)에 대 한 확대/축소를 사용 하도록 설정 하 고 확대/축소 컨트롤을 `WebView`에 겹쳐서 표시할 수 있습니다.

[![Android에서 확대 된 웹 보기의 스크린샷](webview-zoom-controls-images/webview-zoom.png "확대/축소 웹 보기")](webview-zoom-controls-images/webview-zoom-large.png#lightbox "확대/축소 웹 보기")

> [!IMPORTANT]
> 확대/축소 컨트롤을 사용 하도록 설정 하 고 각각의 바인딩 가능한 속성이 나 메서드를 통해 [`WebView`](xref:Xamarin.Forms.WebView)에 겹쳐서 표시 해야 합니다.

## <a name="related-links"></a>관련 링크

- [PlatformSpecifics (샘플)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [플랫폼별 만들기](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [AndroidSpecific API](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific)
- [AndroidSpecific AppCompat API](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat)
