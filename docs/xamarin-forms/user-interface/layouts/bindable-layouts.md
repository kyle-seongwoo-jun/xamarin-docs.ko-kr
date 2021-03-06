---
title: Xamarin.ios의 바인딩 가능한 레이아웃
description: 바인딩 가능한 레이아웃을 사용 하면 레이아웃 클래스가 항목 컬렉션에 바인딩하여 콘텐츠를 생성할 수 있으며,이 옵션을 사용 하 여 각 항목의 모양을 DataTemplate로 설정할 수 있습니다.
ms.prod: xamarin
ms.assetid: 824C3319-20A0-42D0-8632-CDECD98349C3
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 12/18/2018
ms.openlocfilehash: a824c892d21df9264b772bed09a4aef893f3b949
ms.sourcegitcommit: 9bfedf07940dad7270db86767eb2cc4007f2a59f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2019
ms.locfileid: "68647901"
---
# <a name="bindable-layouts-in-xamarinforms"></a>Xamarin.ios의 바인딩 가능한 레이아웃

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-bindablelayouts)

바인딩 가능한 레이아웃을 사용 하면 [`Layout<T>`](xref:Xamarin.Forms.Layout`1) 클래스에서 파생 되는 모든 레이아웃 클래스가 항목 컬렉션에 바인딩하여 [`DataTemplate`](xref:Xamarin.Forms.DataTemplate)를 사용 하 여 각 항목의 모양을 설정 하는 옵션을 사용 하 여 콘텐츠를 생성할 수 있습니다. 바인딩 가능한 레이아웃은 다음과 같은 연결 된 속성을 노출 하는 `BindableLayout` 클래스에서 제공 합니다.

- `ItemsSource` – 레이아웃에 표시 되는 `IEnumerable` 항목의 컬렉션을 지정 합니다.
- `ItemTemplate` – 레이아웃에 의해 표시 되는 항목의 컬렉션에 있는 각 항목에 적용할 [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) 를 지정 합니다.
- `ItemTemplateSelector` – 런타임에 항목에 대 한 [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) 를 선택 하는 데 사용 되는 [`DataTemplateSelector`](xref:Xamarin.Forms.DataTemplateSelector) 를 지정 합니다.

이러한 속성은 모두 [`StackLayout`](xref:Xamarin.Forms.Layout`1) 클래스에서 파생 되는 [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout), [`FlexLayout`](xref:Xamarin.Forms.FlexLayout), [`Grid`](xref:Xamarin.Forms.Grid), [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout)및 [1](xref:Xamarin.Forms.StackLayout) 클래스에 연결할 수 있습니다.

> [!NOTE]
> @No__t_1 및 `ItemTemplateSelector` 속성이 모두 설정 된 경우 `ItemTemplate` 속성이 우선적으로 적용 됩니다.

@No__t_0 클래스는 레이아웃의 자식 요소가 추가 되는 [`Children`](xref:Xamarin.Forms.Layout`1.Children) 컬렉션을 노출 합니다. @No__t_0 속성이 항목의 컬렉션으로 설정 되 고 [`Layout<T>`](xref:Xamarin.Forms.Layout`1)파생 클래스에 연결 되 면 컬렉션의 각 항목이 레이아웃에 표시 하기 위해 `Layout<T>.Children` 컬렉션에 추가 됩니다. 그러면 `Layout<T>` 파생 클래스는 기본 컬렉션이 변경 될 때 자식 뷰를 업데이트 합니다. Xamarin.ios 레이아웃 주기에 대 한 자세한 내용은 [사용자 지정 레이아웃 만들기](~/xamarin-forms/user-interface/layouts/custom.md)를 참조 하세요.

바인딩 가능한 레이아웃은 표시할 항목 컬렉션이 작고 스크롤 및 선택이 필요 하지 않은 경우에만 사용 해야 합니다. [@No__t_1](xref:Xamarin.Forms.ScrollView)에서 바인딩 가능한 레이아웃을 래핑하여 스크롤을 제공할 수 있지만, 바인딩 가능한 레이아웃에 UI 가상화가 없으면 권장 되지 않습니다. 스크롤이 필요한 경우 [`ListView`](xref:Xamarin.Forms.ListView) 또는 [`CollectionView`](xref:Xamarin.Forms.CollectionView)와 같은 UI 가상화를 포함 하는 스크롤 가능한 뷰를 사용 해야 합니다. 이 권장 사항을 관찰 하지 못하면 성능 문제가 발생할 수 있습니다.

> [!IMPORTANT]
>기술적으로는 [`Layout<T>`](xref:Xamarin.Forms.Layout`1) 클래스에서 파생 되는 레이아웃 클래스에 바인딩할 수 있는 레이아웃을 연결할 수 있지만 특히 [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout), [`Grid`](xref:Xamarin.Forms.Grid)및 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) 클래스의 경우에는이 작업을 수행 하는 것이 실용적이 지 않습니다. 예를 들어, 바인딩 가능한 레이아웃을 사용 하 여 [`Grid`](xref:Xamarin.Forms.Grid) 에 데이터 컬렉션을 표시 하려는 경우를 예로 들어 보겠습니다. 컬렉션의 각 항목은 여러 속성을 포함 하는 개체입니다. @No__t_0의 각 행에는 컬렉션의 개체가 표시 되 고 `Grid`의 각 열은 개체의 속성 중 하나를 표시 합니다. 바인딩 가능한 레이아웃에 대 한 [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) 는 단일 개체만 포함할 수 있으므로 해당 개체는 특정 `Grid` 열의 개체 속성 중 하나를 표시 하는 여러 뷰를 포함 하는 레이아웃 클래스 여야 합니다. 이 시나리오는 바인딩 가능한 레이아웃을 사용 하 여 realised 수 있지만 바인딩 컬렉션의 각 항목에 대 한 자식 `Grid`를 포함 하는 부모 `Grid` 발생 합니다 .이는 `Grid` 레이아웃의 매우 비효율적 이며 문제가 있는 사용입니다.

## <a name="populating-a-bindable-layout-with-data"></a>데이터를 사용 하 여 바인딩 가능한 레이아웃 채우기

바인딩 가능한 레이아웃은 해당 `ItemsSource` 속성을 `IEnumerable`를 구현 하는 컬렉션으로 설정 하 고 [`Layout<T>`](xref:Xamarin.Forms.Layout`1)파생 클래스에 연결 하 여 데이터로 채워집니다.

```xaml
<Grid BindableLayout.ItemsSource="{Binding Items}" />
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
IEnumerable<string> items = ...;
var grid = new Grid();
BindableLayout.SetItemsSource(grid, items);
```

@No__t_0 연결 된 속성이 레이아웃에 설정 되어 있지만 `BindableLayout.ItemTemplate` 연결 된 속성이 설정 되지 않은 경우 `IEnumerable` 컬렉션의 모든 항목은 `BindableLayout` 클래스에서 만든 [`Label`](xref:Xamarin.Forms.Label) 표시 됩니다.

## <a name="defining-item-appearance"></a>항목 모양 정의

바인딩 가능한 레이아웃에서 각 항목의 모양은 [`DataTemplate`](xref:Xamarin.Forms.DataTemplate)연결 된 `BindableLayout.ItemTemplate` 속성을 설정 하 여 정의할 수 있습니다.

```xaml
<StackLayout BindableLayout.ItemsSource="{Binding User.TopFollowers}"
             Orientation="Horizontal"
             ...>
    <BindableLayout.ItemTemplate>
        <DataTemplate>
            <controls:CircleImage Source="{Binding}"
                                  Aspect="AspectFill"
                                  WidthRequest="44"
                                  HeightRequest="44"
                                  ... />
        </DataTemplate>
    </BindableLayout.ItemTemplate>
</StackLayout>
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
DataTemplate circleImageTemplate = ...;
var stackLayout = new StackLayout();
BindableLayout.SetItemsSource(stackLayout, viewModel.User.TopFollowers);
BindableLayout.SetItemTemplate(stackLayout, circleImageTemplate);
```

이 예제에서 `TopFollowers` 컬렉션의 모든 항목은 [`DataTemplate`](xref:Xamarin.Forms.DataTemplate)에 정의 된 `CircleImage` 뷰로 표시 됩니다.

![DataTemplate를 사용 하 여 바인딩 가능한 레이아웃](bindable-layouts-images/top-followers.png "데이터 템플릿을 사용 하 여 바인딩 가능한 레이아웃")

데이터 템플릿에 대한 자세한 내용은 [Xamarin.Forms 데이터 템플릿](~/xamarin-forms/app-fundamentals/templates/data-templates/index.md)을 참조하세요.

## <a name="choosing-item-appearance-at-runtime"></a>런타임에 항목 모양 선택

바인딩 가능한 레이아웃에 있는 각 항목의 모양은 런타임에 `BindableLayout.ItemTemplateSelector` 연결 된 속성을 [`DataTemplateSelector`](xref:Xamarin.Forms.DataTemplateSelector)설정 하 여 항목 값을 기준으로 하 여 선택할 수 있습니다.

```xaml
<FlexLayout BindableLayout.ItemsSource="{Binding User.FavoriteTech}"
            BindableLayout.ItemTemplateSelector="{StaticResource TechItemTemplateSelector}"
            ... />
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
DataTemplateSelector dataTemplateSelector = new TechItemTemplateSelector { ... };
var flexLayout = new FlexLayout();
BindableLayout.SetItemsSource(flexLayout, viewModel.User.FavoriteTech);
BindableLayout.SetItemTemplateSelector(flexLayout, dataTemplateSelector);
```

예제 응용 프로그램에 사용 되는 [`DataTemplateSelector`](xref:Xamarin.Forms.DataTemplateSelector) 은 다음 예제에 나와 있습니다.

```csharp
public class TechItemTemplateSelector : DataTemplateSelector
{
    public DataTemplate DefaultTemplate { get; set; }
    public DataTemplate XamarinFormsTemplate { get; set; }

    protected override DataTemplate OnSelectTemplate(object item, BindableObject container)
    {
        return (string)item == "Xamarin.Forms" ? XamarinFormsTemplate : DefaultTemplate;
    }
}
```

@No__t_0 클래스는 다른 데이터 템플릿으로 설정 된 `DefaultTemplate` 및 `XamarinFormsTemplate` [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) 속성을 정의 합니다. @No__t_0 메서드는 항목이 "Xamarin.ios"와 같은 경우 항목을 옆에 있는 진한 빨간색으로 표시 하는 `XamarinFormsTemplate`을 반환 합니다. 항목이 "Xamarin.ios"와 같지 않은 경우 `OnSelectTemplate` 메서드는 [`Label`](xref:Xamarin.Forms.Label)의 기본 색을 사용 하 여 항목을 표시 하는 `DefaultTemplate` 반환 합니다.

![DataTemplateSelector를 사용 하 여 바인딩 가능한 레이아웃](bindable-layouts-images/favorite-tech.png "데이터 템플릿 선택기를 사용 하 여 바인딩 가능한 레이아웃")

데이터 템플릿 선택기에 대 한 자세한 내용은 [DataTemplateSelector 만들기](~/xamarin-forms/app-fundamentals/templates/data-templates/selector.md)를 참조 하세요.

## <a name="related-links"></a>관련 링크

- [바인딩 가능한 레이아웃 데모 (샘플)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-bindablelayouts)
- [사용자 지정 레이아웃 만들기](~/xamarin-forms/user-interface/layouts/custom.md)
- [Xamarin Forms 데이터 템플릿](~/xamarin-forms/app-fundamentals/templates/data-templates/index.md)
- [Xamarin. Forms DataTemplateSelector 만들기](~/xamarin-forms/app-fundamentals/templates/data-templates/selector.md)
