---
title: iOS 디자이너에서 사용자 지정 컨트롤 사용
description: 이 문서에서는 사용자 지정 컨트롤을 만들고 Xamarin Designer for iOS와 함께 사용 하는 방법을 설명 합니다. 이 예제에서는 iOS 디자이너의 도구 상자에서 컨트롤을 사용할 수 있도록 하는 방법을 보여 주고, 컨트롤을 구현 하 여 정확 하 고 디자인 타임에 렌더링 하는 등의 작업을 수행 합니다.
ms.prod: xamarin
ms.assetid: 9032B32E-97BD-4DA6-9955-811B84682578
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/22/2017
ms.openlocfilehash: 4b8c72da1e280b83e215bca9316bc0b9de99402c
ms.sourcegitcommit: 2fbe4932a319af4ebc829f65eb1fb1816ba305d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73003798"
---
# <a name="using-custom-controls-with-the-ios-designer"></a>iOS 디자이너에서 사용자 지정 컨트롤 사용

## <a name="requirements"></a>요구 사항

Xamarin Designer for iOS는 Windows의 Mac용 Visual Studio 및 Visual Studio 2017 이상에서 사용할 수 있습니다.

이 가이드에서는 [시작 가이드](~/ios/get-started/index.md)에 설명 된 내용에 대해 잘 알고 있다고 가정 합니다.

## <a name="walkthrough"></a>연습

> [!IMPORTANT]
> Xamarin Studio 5.5부터 사용자 지정 컨트롤이 생성 되는 방식은 이전 버전과 약간 다릅니다. 사용자 지정 컨트롤을 만들려면 연결 된 구현 메서드를 사용 하 여 `IComponent` 인터페이스가 필요 하거나 `[DesignTimeVisible(true)]`로 클래스에 주석을 달 수 있습니다. 후자 메서드는 다음 연습 예제에서 사용 됩니다.

1. **IOS > 앱 > 단일 뷰 응용 프로그램 > C#**  템플릿에서 새 솔루션을 만들고 이름을`ScratchTicket`로 표시 한 다음 새 프로젝트 마법사를 계속 진행 합니다.

    [![](ios-designable-controls-walkthrough-images/01new.png "Create a new solution")](ios-designable-controls-walkthrough-images/01new.png#lightbox)

1. `ScratchTicketView`라는 비어 있는 새 클래스 파일을 만듭니다.

    [![](ios-designable-controls-walkthrough-images/02new.png "Create a new ScratchTicketView class")](ios-designable-controls-walkthrough-images/02new.png#lightbox)

1. `ScratchTicketView` 클래스에 대해 다음 코드를 추가 합니다.

    ```csharp
    using System;
    using System.ComponentModel;
    using CoreGraphics;
    using Foundation;
    using UIKit;

    namespace ScratchTicket
    {
        [Register("ScratchTicketView"), DesignTimeVisible(true)]
        public class ScratchTicketView : UIView
        {
            CGPath path;
            CGPoint initialPoint;
            CGPoint latestPoint;
            bool startNewPath = false;
            UIImage image;

            [Export("Image"), Browsable(true)]
            public UIImage Image
            {
                get { return image; }
                set
                {
                    image = value;
                    SetNeedsDisplay();
                }
            }

            public ScratchTicketView(IntPtr p)
                : base(p)
            {
                Initialize();
            }

            public ScratchTicketView()
            {
                Initialize();
            }

            void Initialize()
            {
                initialPoint = CGPoint.Empty;
                latestPoint = CGPoint.Empty;
                BackgroundColor = UIColor.Clear;
                Opaque = false;
                path = new CGPath();
                SetNeedsDisplay();
            }

            public override void TouchesBegan(NSSet touches, UIEvent evt)
            {
                base.TouchesBegan(touches, evt);

                var touch = touches.AnyObject as UITouch;

                if (touch != null)
                {
                    initialPoint = touch.LocationInView(this);
                }
            }

            public override void TouchesMoved(NSSet touches, UIEvent evt)
            {
                base.TouchesMoved(touches, evt);

                var touch = touches.AnyObject as UITouch;

                if (touch != null)
                {
                    latestPoint = touch.LocationInView(this);
                    SetNeedsDisplay();
                }
            }

            public override void TouchesEnded(NSSet touches, UIEvent evt)
            {
                base.TouchesEnded(touches, evt);
                startNewPath = true;
            }

            public override void Draw(CGRect rect)
            {
                base.Draw(rect);

                using (var g = UIGraphics.GetCurrentContext())
                {
                    if (image != null)
                        g.SetFillColor((UIColor.FromPatternImage(image).CGColor));
                    else
                        g.SetFillColor(UIColor.LightGray.CGColor);
                    g.FillRect(rect);

                    if (!initialPoint.IsEmpty)
                    {
                        g.SetLineWidth(20);
                        g.SetBlendMode(CGBlendMode.Clear);
                        UIColor.Clear.SetColor();

                        if (path.IsEmpty || startNewPath)
                        {
                            path.AddLines(new CGPoint[] { initialPoint, latestPoint });
                            startNewPath = false;
                        }
                        else
                        {
                            path.AddLineToPoint(latestPoint);
                        }

                        g.SetLineCap(CGLineCap.Round);
                        g.AddPath(path);
                        g.DrawPath(CGPathDrawingMode.Stroke);
                    }
                }
            }
        }
    }
    ```

1. [GitHub에서](https://github.com/xamarin/ios-samples/blob/master/ScratchTicket/Resources/images.zip?raw=true)사용할 수 있는 `FillTexture.png`, `FillTexture2.png` 및 `Monkey.png` 파일을 **Resources** 폴더에 추가 합니다.

1. `Main.storyboard` 파일을 두 번 클릭 하 여 디자이너에서 엽니다.

    [![](ios-designable-controls-walkthrough-images/03new.png "The iOS Designer")](ios-designable-controls-walkthrough-images/03new.png#lightbox)

1. **도구 상자** 의 **이미지 뷰** 를 스토리 보드의 뷰로 끌어 놓습니다.

    [![](ios-designable-controls-walkthrough-images/04new.png "An Image View added to the layout")](ios-designable-controls-walkthrough-images/04new.png#lightbox)

1. **이미지 뷰** 를 선택 하 고 **이미지** 속성을 `Monkey.png`로 변경 합니다.

    [![](ios-designable-controls-walkthrough-images/05new.png "Setting Image View Image property to Monkey.png")](ios-designable-controls-walkthrough-images/05new.png#lightbox)

1. Size 클래스를 사용할 때이 이미지 뷰를 제한 해야 합니다. 이미지를 두 번 클릭 하 여 제약 조건 모드로 전환 합니다. 중심 고정 핸들을 클릭 하 여 가운데로 제한 하 고 가로 및 세로로 정렬 합니다.

    [![](ios-designable-controls-walkthrough-images/06new.png "Centering the image")](ios-designable-controls-walkthrough-images/06new.png#lightbox)

1. 높이 및 너비를 제한 하려면 크기 고정 핸들 (' 뼈 ' 모양 핸들)을 클릭 하 고 너비와 높이를 각각 선택 합니다.

    [![](ios-designable-controls-walkthrough-images/07new.png "Adding Constraints")](ios-designable-controls-walkthrough-images/07new.png#lightbox)

1. 도구 모음에서 업데이트 단추를 클릭 하 여 제약 조건에 따라 프레임을 업데이트 합니다.

    [![](ios-designable-controls-walkthrough-images/08new.png "The Constraints toolbar")](ios-designable-controls-walkthrough-images/08new.png#lightbox)

1. 그런 다음 도구 상자의 **사용자 지정 구성 요소** 아래에 **스크래치 티켓 보기가** 표시 되도록 프로젝트를 빌드합니다.

    [![](ios-designable-controls-walkthrough-images/09new.png "The Custom Components toolbox")](ios-designable-controls-walkthrough-images/09new.png#lightbox)

1. 원숭이 이미지 위에 나타나도록 **스크래치 티켓 보기** 를 끌어서 놓습니다. 아래와 같이 스크래치 티켓 보기가 원숭이 전체를 포괄 하도록 끌기 핸들을 조정 합니다.

    [![](ios-designable-controls-walkthrough-images/10new.png "A Scratch Ticket View over the Image View")](ios-designable-controls-walkthrough-images/10new.png#lightbox)

1. 두 뷰를 모두 선택 하는 경계 사각형을 그려 이미지 뷰로 스크래치 티켓 보기를 제한 합니다. 아래와 같이 제약 조건에 따라 너비, 높이, 가운데 및 중간 및 업데이트 프레임으로 제한 하는 옵션을 선택 합니다.

    [![](ios-designable-controls-walkthrough-images/11new.png "Centering and adding Constraints")](ios-designable-controls-walkthrough-images/11new.png#lightbox)

1. 응용 프로그램을 실행 하 고 이미지를 "스크래치" 하 여 원숭이를 표시 합니다.

    [![](ios-designable-controls-walkthrough-images/10-app.png "A sample app run")](ios-designable-controls-walkthrough-images/10-app.png#lightbox)

## <a name="adding-design-time-properties"></a>디자인 타임 속성 추가

또한 디자이너에는 숫자, 열거형, 문자열, bool, CGSize, UIColor 및 UIImage 형식의 사용자 지정 컨트롤에 대 한 디자인 타임 지원이 포함 됩니다. 이를 설명 하기 위해 `ScratchTicketView`에 속성을 추가 하 여 "긁힌 끔" 이미지를 설정 하겠습니다.

속성의 `ScratchTicketView` 클래스에 다음 코드를 추가 합니다.

```csharp
[Export("Image"), Browsable(true)]
public UIImage Image
{
    get { return image; }
    set {
            image = value;
              SetNeedsDisplay ();
        }
}
```

다음과 같이 `Draw` 메서드에 null 검사를 추가 하려고 할 수도 있습니다.

```csharp
public override void Draw(CGRect rect)
{
    base.Draw(rect);

    using (var g = UIGraphics.GetCurrentContext())
    {
        if (image != null)
            g.SetFillColor ((UIColor.FromPatternImage (image).CGColor));
        else
            g.SetFillColor (UIColor.LightGray.CGColor);

        g.FillRect(rect);

        if (!initialPoint.IsEmpty)
        {
             g.SetLineWidth(20);
             g.SetBlendMode(CGBlendMode.Clear);
             UIColor.Clear.SetColor();

             if (path.IsEmpty || startNewPath)
             {
                 path.AddLines(new CGPoint[] { initialPoint, latestPoint });
                 startNewPath = false;
             }
             else
             {
                 path.AddLineToPoint(latestPoint);
             }

             g.SetLineCap(CGLineCap.Round);
             g.AddPath(path);
             g.DrawPath(CGPathDrawingMode.Stroke);
        }
    }
}
```

`true`로 설정 된 `ExportAttribute` 및 `BrowsableAttribute`를 포함 하 여 속성이 디자이너의 **속성** 패널에 표시 됩니다. 속성을 프로젝트에 포함 된 다른 이미지로 변경 하면 (예: `FillTexture2.png`) 아래와 같이 디자인 타임에 컨트롤이 업데이트 됩니다.

 [![](ios-designable-controls-walkthrough-images/11-customproperty.png "Editing Design Time properties")](ios-designable-controls-walkthrough-images/10-app.png#lightbox)

## <a name="summary"></a>요약

이 문서에서는 사용자 지정 컨트롤을 만드는 방법과 iOS 디자이너를 사용 하 여 iOS 응용 프로그램에서 사용자 지정 컨트롤을 사용 하는 방법을 살펴보았습니다. 디자이너의 **도구 상자**에서 응용 프로그램에 사용할 수 있도록 컨트롤을 만들고 빌드하는 방법에 대해 살펴보았습니다. 또한 디자인 타임 및 런타임 모두에서 적절히 렌더링 하 고 디자이너에서 사용자 지정 컨트롤 속성을 노출 하는 방법에 맞게 컨트롤을 구현 하는 방법을 살펴보았습니다.

## <a name="related-links"></a>관련 링크

- [ScratchTicket (샘플)](https://docs.microsoft.com/samples/xamarin/ios-samples/scratchticket)
- [필수 이미지 (샘플)](https://github.com/xamarin/ios-samples/blob/master/ScratchTicket/Resources/images.zip?raw=true)
