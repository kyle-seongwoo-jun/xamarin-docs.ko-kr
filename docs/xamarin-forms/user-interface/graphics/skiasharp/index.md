---
title: Xamarin.Forms의 SkiaSharp 그래픽
description: SkiaSharp는.NET 및 Google 제품에 광범위 하 게 사용 되는 오픈 소스 Skia 그래픽 엔진에서 제공 하는 C#에 대 한 2D 그래픽 시스템. 이 가이드에서는 SkiaSharp 2D 그래픽 Xamarin.Forms 응용 프로그램에서 사용 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: 2C348BEA-81DF-4794-8857-EB1DFF5E11DB
author: davidbritch
ms.author: dabritch
ms.date: 09/11/2017
ms.openlocfilehash: 6b85cdcd92c4680ced9f75d7b8c5a69c9512d6c4
ms.sourcegitcommit: 3ea9ee034af9790d2b0dc0893435e997bd06e587
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68656145"
---
# <a name="skiasharp-graphics-in-xamarinforms"></a>Xamarin.Forms의 SkiaSharp 그래픽

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/skiasharpforms-demos)

_Xamarin.Forms 응용 프로그램에서 2D 그래픽 SkiaSharp 사용_

SkiaSharp는.NET 및 Google 제품에 광범위 하 게 사용 되는 오픈 소스 Skia 그래픽 엔진에서 제공 하는 C#에 대 한 2D 그래픽 시스템. 2D 벡터 그래픽, 비트맵, 텍스트를 그리려면 SkiaSharp Xamarin.Forms 응용 프로그램에서 사용할 수 있습니다. 참조 된 [2D 그리기](~/graphics-games/skiasharp/index.md) SkiaSharp 라이브러리에 대 한 자세한 내용 및 일부 다른 자습서를 위한 가이드입니다.

이 가이드에서는 Xamarin.Forms 프로그래밍 잘 알고 있다고 가정 합니다.

> [!VIDEO https://channel9.msdn.com/Events/Xamarin/Xamarin-University-Presents-Webinar-Series/SkiaSharp-Graphics-for-XamarinForms/player]

**웹 세미나 Xamarin.ios에 대 한 SkiaSharp**

## <a name="skiasharp-preliminaries"></a>SkiaSharp 준비

SkiaSharp Xamarin.Forms에 대 한 NuGet 패키지로 패키지 됩니다. Mac 용 Visual Studio 또는 Visual Studio에서 Xamarin.Forms 솔루션을 만들었습니다, 후 검색 하려면 NuGet 패키지 관리자를 사용할 수 있습니다 합니다 **SkiaSharp.Views.Forms** 패키지 및 솔루션에 추가 합니다. 확인 하는 경우는 **참조가** 섹션 SkiaSharp를 추가한 후 각 프로젝트를 볼 수 있습니다 다양 한 **SkiaSharp** 라이브러리 각 솔루션의 프로젝트에 추가 되었습니다.

Xamarin.Forms 응용 프로그램에서 iOS를 대상으로 하는 경우 iOS 8.0에 최소 배포 대상을 변경 하려면 프로젝트 속성 페이지를 사용 합니다.

SkiaSharp 사용 하는 모든 C# 페이지에 포함 하려는 `using` 에 대 한 지시문의 [ `SkiaSharp` ](xref:SkiaSharp) 모든 SkiaSharp 클래스, 구조체 및 그래픽에서 사용 하는 열거형을 포함 하는 네임 스페이스 프로그래밍합니다. 할 수는 `using` 지시문에 대 한 합니다 [ `SkiaSharp.Views.Forms` ](xref:SkiaSharp.Views.Forms) Xamarin.Forms 관련 클래스에 대 한 네임 스페이스입니다. 가장 중요 한 클래스는 훨씬 더 작은 네임 스페이스를 이것이 [ `SKCanvasView` ](xref:SkiaSharp.Views.Forms.SKCanvasView)합니다. 이 클래스는 Xamarin.Forms에서 파생 됩니다 `View` 클래스 하 고 SkiaSharp 그래픽 출력을 호스트 합니다.

> [!IMPORTANT]
> 합니다 `SkiaSharp.Views.Forms` 네임 스페이스는 포함을 `SKGLView` 에서 파생 된 클래스 `View` 하지만 OpenGL을 사용 하 여 그래픽 렌더링에 대 한 합니다. 단순성을 위해이 가이드를 제한 하려면 자체 `SKCanvasView`, 하지만 사용 하 여 `SKGLView` 대신 매우 비슷합니다.

## <a name="skiasharp-drawing-basicsbasicsindexmd"></a>[SkiaSharp 그리기 기본 사항](basics/index.md)

일부 SkiaSharp를 사용 하 여 그릴 수 있습니다 가장 간단한 그래픽 수치는 원과 타원, 사각형입니다. 이러한 수치를 표시, SkiaSharp 좌표, 크기 및 색에 대 한 배웁니다. 텍스트 및 비트맵을 표시 더 복잡 하지만 이러한 문서는 또한 이러한 기법을 소개 합니다.

## <a name="skiasharp-lines-and-pathspathsindexmd"></a>[SkiaSharp 선 및 경로](paths/index.md)

그래픽 경로 일련의 연결 된 직선 및 곡선입니다. 경로 수 스트로크를 입력, 또는 둘 다. 이 문서는 스트로크 끝과 조인 등 파선 선 그리기 하며 점선, 기 하 도형 커브 짧은 중지의 다양 한 측면을 포함 합니다.

## <a name="skiasharp-transformstransformsindexmd"></a>[SkiaSharp 변환](transforms/index.md)

변환 균일 하 게 변환, 배율 조정, 회전 또는 기울어진 그래픽 개체를 허용 합니다. 이 문서에는 비 관계 변환 만들고 변환 경로에 적용 하기 위한 표준 3-3 하 여 변환 매트릭스를 사용 하는 방법을 보여 줍니다.

## <a name="skiasharp-curves-and-pathscurvesindexmd"></a>[SkiaSharp 곡선 및 경로](curves/index.md)

탐색 경로의 경로 개체에 곡선을 추가 하 고 다른 강력한 경로 기능을 악용을 사용 하 여 계속 합니다. 간단한 텍스트 문자열의 전체 경로 지정 하는 방법, 경로 효과 사용 하는 방법 및 내부 경로를 더 자세히 살펴보고 하는 방법을 배웁니다.

## <a name="skiasharp-bitmapsbitmapsindexmd"></a>[SkiaSharp 비트맵](bitmaps/index.md)

비트맵은 비트에 해당 하는 디스플레이 장치의 픽셀 사각형 배열입니다. 이 문서 시리즈에서는 로드, 저장, 표시, 만들기,, 애니메이션 및 SkiaSharp 비트맵의 비트에 액세스 하는 방법을 보여 줍니다.

## <a name="skiasharp-effectseffectsindexmd"></a>[SkiaSharp 효과](effects/index.md)

효과 바둑판식 배열 비트맵, 혼합 모드, blur 및 기타 그래픽, 순환 및 선형 그라데이션을 포함 하 여 기본 표시 크기를 변경 하는 속성입니다.

## <a name="related-links"></a>관련 링크

- [SkiaSharp Api](https://docs.microsoft.com/dotnet/api/skiasharp)
- [SkiaSharpFormsDemos (샘플)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/skiasharpforms-demos)
- [SkiaSharp Xamarin.Forms 웹 세미나 (비디오)를 사용 하 여](https://channel9.msdn.com/Events/Xamarin/Xamarin-University-Presents-Webinar-Series/SkiaSharp-Graphics-for-XamarinForms)
