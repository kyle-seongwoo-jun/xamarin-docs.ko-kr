---
title: Xamarin.Forms 데이터 템플릿
description: DataTemplate은 지원되는 컨트롤의 데이터 모양을 지정하는 데 사용되며 일반적으로 표시할 데이터에 바인딩됩니다.
ms.prod: xamarin
ms.assetid: 838F4BDB-B719-457F-8633-27E9B267A2A0
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 09/11/2017
ms.openlocfilehash: 5d130a6644af4e5831263c6de137513c021e0b6a
ms.sourcegitcommit: 57f815bf0024b1afe9754c0e28054fc0a53ce302
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70760797"
---
# <a name="xamarinforms-data-templates"></a>Xamarin.Forms 데이터 템플릿

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/templates-datatemplates)

_DataTemplate은 지원되는 컨트롤의 데이터 모양을 지정하는 데 사용되며 일반적으로 표시할 데이터에 바인딩됩니다._

## <a name="introductionintroductionmd"></a>[소개](introduction.md)

Xamarin.Forms 데이터 템플릿은 지원되는 컨트롤의 데이터 표현을 정의하는 기능을 제공합니다. 이 문서에서는 데이터 템플릿이 필요한 이유를 검토하면서 데이터 템플릿을 소개합니다.

## <a name="creating-a-datatemplatecreatingmd"></a>[DataTemplate 만들기](creating.md)

데이터 템플릿은 [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary)에서 인라인으로 만들거나 사용자 지정 형식 또는 적절한 Xamarin.Forms 셀 형식으로 만들 수 있습니다. 다른 곳에서 데이터 템플릿을 다시 사용할 필요가 없으면 인라인 템플릿을 사용해야 합니다. 또는 데이터 템플릿을 사용자 지정 유형으로 정의하거나 컨트롤 수준, 페이지 수준 또는 애플리케이션 수준 리소스로 정의하여 다시 사용할 수 있습니다.

## <a name="creating-a-datatemplateselectorselectormd"></a>[DataTemplateSelector 만들기](selector.md)

[`DataTemplateSelector`](xref:Xamarin.Forms.DataTemplateSelector)는 데이터 바인딩된 속성의 값에 기반하여 런타임 시 [`DataTemplate`](xref:Xamarin.Forms.DataTemplate)을 선택하는 데 사용됩니다. 이렇게 하면 여러 `DataTemplate` 인스턴스를 같은 유형의 개체에 적용하여 특정 개체의 모양을 사용자 지정할 수 있습니다. 이 문서에서는 `DataTemplateSelector`를 만들고 사용하는 방법을 보여줍니다.

## <a name="related-links"></a>관련 링크

- [데이터 템플릿(샘플)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/templates-datatemplates)
