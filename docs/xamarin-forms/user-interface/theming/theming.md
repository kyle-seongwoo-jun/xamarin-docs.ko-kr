---
title: 테마 a Xamarin.ios 응용 프로그램
description: 테마는 각 테마에 대 한 ResourceDictionary를 만든 다음 DynamicResource 태그 확장을 사용 하 여 리소스를 로드 하 여 Xamarin.ios 응용 프로그램에서 구현할 수 있습니다.
ms.prod: xamarin
ms.assetId: B7B17F66-4E37-4B50-9A57-351B62BE4FED
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/07/2019
ms.openlocfilehash: 3cac3714901e592d90823ae4878baf408b7d1369
ms.sourcegitcommit: 524fc148bad17272bda83c50775771daa45bfd7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486279"
---
# <a name="theme-a-xamarinforms-application"></a>테마 a Xamarin.ios 응용 프로그램

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-theming/)

Xamarin Forms 응용 프로그램은 `DynamicResource` 태그 확장을 사용 하 여 런타임에 동적으로 스타일 변경에 응답할 수 있습니다. 이 태그 확장은 둘 다 사전 키를 사용 하 여 [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary)에서 값을 인출 한다는 점에서 `StaticResource` 태그 확장과 비슷합니다. 그러나 `StaticResource` 태그 확장은 단일 사전 조회를 수행 하지만 `DynamicResource` 태그 확장은 사전 키에 대 한 링크를 유지 합니다. 따라서 키와 연결 된 값이 대체 되 면 변경 내용이 [`VisualElement`](xref:Xamarin.Forms.VisualElement)적용 됩니다. 그러면 Xamarin.ios 응용 프로그램에서 런타임 테마를 구현할 수 있습니다.

Xamarin.ios 응용 프로그램에서 런타임 테마를 구현 하는 프로세스는 다음과 같습니다.

1. [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary)에서 각 테마에 대 한 리소스를 정의 합니다.
1. `DynamicResource` 태그 확장을 사용 하 여 응용 프로그램의 테마 리소스를 사용 합니다.
1. 응용 프로그램의 **app.xaml** 파일에서 기본 테마를 설정 합니다.
1. 런타임에 테마를 로드 하는 코드를 추가 합니다.

다음 스크린샷은 테마 페이지를 표시 하며, 진한 테마를 사용 하 여 밝은 테마와 Android 응용 프로그램을 사용 하는 iOS 응용 프로그램입니다.

[![](theming-images/main-page-both-themes.png "테마가 적용 된 앱의 기본 페이지")](theming-images/main-page-both-themes-large.png#lightbox "테마가 적용 된 앱의 기본 페이지") Ios 및 android에서 테마가 적용 된 앱의 [ ![세부 정보 페이지](theming-images/detail-page-both-themes.png "테마가 적용 된 앱의 세부 정보 페이지") 에 있는 ios 및 Android
의 기본 페이지 스크린샷](theming-images/detail-page-both-themes-large.png#lightbox "테마가 적용 된 앱의 세부 정보 페이지")

## <a name="define-themes"></a>테마 정의

테마는 [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary)에 저장 된 리소스 개체의 컬렉션으로 정의 됩니다.

다음 예제에서는 예제 응용 프로그램의 `LightTheme`을 보여 줍니다.

```xaml
<ResourceDictionary xmlns="http://xamarin.com/schemas/2014/forms"
                    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                    x:Class="ThemingDemo.LightTheme">
    <Color x:Key="PageBackgroundColor">White</Color>
    <Color x:Key="NavigationBarColor">WhiteSmoke</Color>
    <Color x:Key="PrimaryColor">WhiteSmoke</Color>
    <Color x:Key="SecondaryColor">Black</Color>
    <Color x:Key="PrimaryTextColor">Black</Color>
    <Color x:Key="SecondaryTextColor">White</Color>
    <Color x:Key="TertiaryTextColor">Gray</Color>
    <Color x:Key="TransparentColor">Transparent</Color>
</ResourceDictionary>
```

다음 예제에서는 예제 응용 프로그램의 `DarkTheme`을 보여 줍니다.

```xaml
<ResourceDictionary xmlns="http://xamarin.com/schemas/2014/forms"
                    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                    x:Class="ThemingDemo.DarkTheme">
    <Color x:Key="PageBackgroundColor">Black</Color>
    <Color x:Key="NavigationBarColor">Teal</Color>
    <Color x:Key="PrimaryColor">Teal</Color>
    <Color x:Key="SecondaryColor">White</Color>
    <Color x:Key="PrimaryTextColor">White</Color>
    <Color x:Key="SecondaryTextColor">White</Color>
    <Color x:Key="TertiaryTextColor">WhiteSmoke</Color>
    <Color x:Key="TransparentColor">Transparent</Color>
</ResourceDictionary>
```

각 [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary) 에는 각각의 테마를 정의 하는 [`Color`](xref:Xamarin.Forms.Color) 리소스가 포함 되며 각 `ResourceDictionary` 동일한 키 값을 사용 합니다. 리소스 사전에 대 한 자세한 내용은 [리소스 사전](~/xamarin-forms/xaml/resource-dictionaries.md)을 참조 하세요.

> [!IMPORTANT]
> `InitializeComponent` 메서드를 호출 하는 각 `ResourceDictionary`에 코드 숨김이 필요 합니다. 이는 런타임에 선택 된 테마를 나타내는 CLR 개체를 만들 수 있도록 하는 데 필요 합니다.

## <a name="set-a-default-theme"></a>기본 테마 설정

응용 프로그램에는 기본 테마가 필요 하므로 컨트롤에 사용 되는 리소스에 대 한 값이 있습니다. 테마의 [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary) 를 **app.xaml**에 정의 된 응용 프로그램 수준 `ResourceDictionary`에 병합 하 여 기본 테마를 설정할 수 있습니다.

```xaml
<Application xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="ThemingDemo.App">
    <Application.Resources>
        <ResourceDictionary Source="Themes/LightTheme.xaml" />
    </Application.Resources>
</Application>
```

리소스 사전을 병합 하는 방법에 대 한 자세한 내용은 [병합 된 리소스 사전](~/xamarin-forms/xaml/resource-dictionaries.md#merged-resource-dictionaries)을 참조 하세요.

## <a name="consume-theme-resources"></a>테마 리소스 사용

응용 프로그램에서 테마를 나타내는 [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary) 에 저장 된 리소스를 사용 하려는 경우 `DynamicResource` 태그 확장을 사용 하 여이 작업을 수행 해야 합니다. 이렇게 하면 런타임에 다른 테마를 선택 하면 새 테마의 값이 적용 됩니다.

다음 예제에서는 [`Label`](xref:Xamarin.Forms.Label) 개체에 적용할 수 있는 샘플 응용 프로그램의 세 가지 스타일을 보여 줍니다.

```xaml
<Application xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="ThemingDemo.App">
    <Application.Resources>

        <Style x:Key="LargeLabelStyle"
               TargetType="Label">
            <Setter Property="TextColor"
                    Value="{DynamicResource SecondaryTextColor}" />
            <Setter Property="FontSize"
                    Value="30" />
        </Style>

        <Style x:Key="MediumLabelStyle"
               TargetType="Label">
            <Setter Property="TextColor"
                    Value="{DynamicResource PrimaryTextColor}" />
            <Setter Property="FontSize"
                    Value="25" />
        </Style>

        <Style x:Key="SmallLabelStyle"
               TargetType="Label">
            <Setter Property="TextColor"
                    Value="{DynamicResource TertiaryTextColor}" />
            <Setter Property="FontSize"
                    Value="15" />
        </Style>

    </Application.Resources>
</Application>
```

이러한 스타일은 여러 페이지에서 사용할 수 있도록 응용 프로그램 수준 리소스 사전에 정의 됩니다. 각 스타일은 `DynamicResource` 태그 확장을 사용 하 여 테마 리소스를 사용 합니다.

이러한 스타일은 페이지에서 사용 됩니다.

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ThemingDemo"
             x:Class="ThemingDemo.UserSummaryPage"
             Title="User Summary"
             BackgroundColor="{DynamicResource PageBackgroundColor}">
    ...
    <ScrollView>
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="200" />
                <RowDefinition Height="120" />
                <RowDefinition Height="70" />
            </Grid.RowDefinitions>
            <Grid BackgroundColor="{DynamicResource PrimaryColor}">
                <Label Text="Face-Palm Monkey"
                       VerticalOptions="Center"
                       Margin="15"
                       Style="{StaticResource MediumLabelStyle}" />
                ...
            </Grid>
            <StackLayout Grid.Row="1"
                         Margin="10">
                <Label Text="This monkey reacts appropriately to ridiculous assertions and actions."
                       Style="{StaticResource SmallLabelStyle}" />
                <Label Text="  &#x2022; Cynical but not unfriendly."
                       Style="{StaticResource SmallLabelStyle}" />
                <Label Text="  &#x2022; Seven varieties of grimaces."
                       Style="{StaticResource SmallLabelStyle}" />
                <Label Text="  &#x2022; Doesn't laugh at your jokes."
                       Style="{StaticResource SmallLabelStyle}" />
            </StackLayout>
            ...
        </Grid>
    </ScrollView>
</ContentPage>
```

테마 리소스를 직접 사용 하는 경우 `DynamicResource` 태그 확장과 함께 사용 해야 합니다. 그러나 `DynamicResource` 태그 확장을 사용 하는 스타일을 사용 하는 경우 `StaticResource` 태그 확장과 함께 사용 해야 합니다.

스타일 지정에 대 한 자세한 내용은 [XAML 스타일을 사용 하 여 Xamarin.ios 앱 스타일](~/xamarin-forms/user-interface/styles/xaml/index.md)지정을 참조 하세요. `DynamicResource` 태그 확장에 대 한 자세한 내용은 [xamarin.ios의 동적 스타일](~/xamarin-forms/user-interface/styles/xaml/dynamic.md)(영문)을 참조 하세요.

## <a name="load-a-theme-at-runtime"></a>런타임에 테마 로드

런타임에 테마를 선택 하면 응용 프로그램은 다음을 수행 해야 합니다.

1. 응용 프로그램에서 현재 테마를 제거 합니다. 이렇게 하려면 응용 프로그램 수준 [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary)의 [`MergedDictionaries`](xref:Xamarin.Forms.ResourceDictionary.MergedDictionaries) 속성을 선택 취소 합니다.
2. 선택한 테마를 로드 합니다. 이렇게 하려면 선택한 테마의 인스턴스를 응용 프로그램 수준 `ResourceDictionary`의 `MergedDictionaries` 속성에 추가 합니다.

`DynamicResource` 태그 확장을 사용 하 여 속성을 설정 하는 모든 [`VisualElement`](xref:Xamarin.Forms.VisualElement) 개체는 새 테마 값을 적용 합니다. 이는 `DynamicResource` 태그 확장이 사전 키에 대 한 링크를 유지 관리 하기 때문에 발생 합니다. 따라서 키와 연결 된 값이 대체 되 면 변경 내용이 `VisualElement` 개체에 적용 됩니다.

샘플 응용 프로그램에서 테마는 [`Picker`](xref:Xamarin.Forms.Picker)포함 된 모달 페이지를 통해 선택 됩니다. 다음 코드에서는 선택 된 테마가 변경 될 때 실행 되는 `OnPickerSelectionChanged` 메서드를 보여 줍니다.

```csharp
void OnPickerSelectionChanged(object sender, EventArgs e)
{
    Picker picker = sender as Picker;
    Theme theme = (Theme)picker.SelectedItem;

    ICollection<ResourceDictionary> mergedDictionaries = Application.Current.Resources.MergedDictionaries;
    if (mergedDictionaries != null)
    {
        mergedDictionaries.Clear();

        switch (theme)
        {
            case Theme.Dark:
                mergedDictionaries.Add(new DarkTheme());
                break;
            case Theme.Light:
            default:
                mergedDictionaries.Add(new LightTheme());
                break;
        }
    }
}
```

## <a name="related-links"></a>관련 링크

- [테마 (샘플)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-theming/)
- [리소스 사전](~/xamarin-forms/xaml/resource-dictionaries.md)
- [Xamarin.ios의 동적 스타일](~/xamarin-forms/user-interface/styles/xaml/dynamic.md)
- [XAML 스타일을 사용하여 Xamarin.Forms 앱 스타일 지정](~/xamarin-forms/user-interface/styles/xaml/index.md)
- [어둡게 모드](dark-mode.md)
