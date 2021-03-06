---
title: 选项卡栏和 Xamarin.iOS 中的选项卡栏控制器
description: 本文档介绍 iOS 选项卡栏控制器和如何使用 Xamarin.iOS。 它演示了如何设置 UITabBarController、 处理图像、 设置徽章值、 处理事件，和的详细信息。
ms.prod: xamarin
ms.assetid: 7C772899-2900-F139-D642-F3C4F3F14DDC
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/21/2017
ms.openlocfilehash: 25d8563288cce614bc2823b0146e5121688c6f02
ms.sourcegitcommit: db422e33438f1b5c55852e6942c3d1d75dc025c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2020
ms.locfileid: "76725482"
---
# <a name="tab-bars-and-tab-bar-controllers-in-xamarinios"></a>Xamarin.ios의 탭 모음 및 탭 모음 컨트롤러

在 iOS 中使用选项卡式应用程序以支持多个屏幕可以访问其中的用户界面不按特定顺序。 通过`UITabBarController`类，应用程序可以轻松地添加对此类多屏幕方案的支持。 `UITabBarController` 负责多屏显示管理，从而使应用程序开发人员可以专注于每个屏幕的详细信息。

通常情况下，选项卡式应用程序生成的`UITabBarController`正在`RootViewController`的主窗口。 但是，与一些其他代码，选项卡式应用程序还可在其他一些初始屏幕，如应用程序首先显示登录屏幕，跟选项卡式界面的方案的连续。

이 페이지에서는 탭이 응용 프로그램 뷰 계층 구조의 루트에 있고`RootViewController` 되지 않은 시나리오에 대 한 두 가지 시나리오를 모두 설명 합니다.

## <a name="introducing-uitabbarcontroller"></a>引入 UITabBarController

`UITabBarController`支持通过以下选项卡式应用程序开发：

- 允许多个控制器添加到它。
- 通过提供一个选项卡式的用户界面，`UITabBar`类，以允许用户控制器和其视图之间进行切换。

控制器被添加至`UITabBarController`通过其`ViewControllers`属性，它是`UIViewController`数组。 `UITabBarController`本身处理加载正确的控制器并显示其视图基于所选的选项卡。

选项卡为的实例`UITabBarItem`类，该类中包含`UITabBar`实例。 每个`UITabBar`实例是可通过访问`TabBarItem`属性的每个选项卡中的控制器。

若要了解如何使用`UITabBarController`，让我们看一下构建的简单应用程序使用一个。

## <a name="tabbed-application-walkthrough"></a>탭 응용 프로그램 연습

在本演练中我们将创建以下应用程序：

[![샘플 앱 탭](creating-tabbed-applications-images/00-app.png)](creating-tabbed-applications-images/00-app.png#lightbox)

Mac용 Visual Studio에서 사용할 수 있는 탭 응용 프로그램 템플릿이 이미 있지만이 예에서는 빈 프로젝트에서 이러한 지침을 사용 하 여 응용 프로그램의 구성 방식을 보다 잘 이해할 수 있습니다.

### <a name="creating-the-application"></a>응용 프로그램 만들기

새 응용 프로그램을 만들어 시작 합니다.

选择**文件 > 新建 > 解决方案**菜单项在 Visual Studio for Mac，然后选择**iOS > 应用程序 > 空项目**模板中，将项目命名`TabbedApplication`，如下所示：

[![](creating-tabbed-applications-images/newsolution1.png "Select the Empty Project template")](creating-tabbed-applications-images/newsolution1.png#lightbox)

[![](creating-tabbed-applications-images/newsolution2.png "Name the project TabbedApplication")](creating-tabbed-applications-images/newsolution2.png#lightbox)

### <a name="adding-the-uitabbarcontroller"></a>添加 UITabBarController

接下来，通过选择添加一个空类**文件 > 新建文件**，然后选择**常规： 空类**模板。 将文件命名`TabController`，如下所示：

[![](creating-tabbed-applications-images/02-newclass.png "Add the TabController class")](creating-tabbed-applications-images/02-newclass.png#lightbox)

`TabController`类将包含的实现`UITabBarController`用于将管理的数组`UIViewControllers`。 当用户选择一个选项卡，`UITabBarController`将负责显示相应的视图控制器的视图。

若要实现`UITabBarController`我们需要执行以下操作：

1. 设置类的基类`TabController`到`UITabBarController`。
1. 创建`UIViewController`实例将添加到`TabController`。
1. 添加`UIViewController`实例为数组分配给`ViewControllers`属性的`TabController`。

将以下代码添加到`TabController`类来实现这些步骤：

```csharp
using System;
using UIKit;

namespace TabbedApplication {
    public class TabController : UITabBarController {

        UIViewController tab1, tab2, tab3;

        public TabController ()
        {
            tab1 = new UIViewController();
            tab1.Title = "Green";
            tab1.View.BackgroundColor = UIColor.Green;

            tab2 = new UIViewController();
            tab2.Title = "Orange";
            tab2.View.BackgroundColor = UIColor.Orange;

            tab3 = new UIViewController();
            tab3.Title = "Red";
            tab3.View.BackgroundColor = UIColor.Red;

            var tabs = new UIViewController[] {
                tab1, tab2, tab3
            };

            ViewControllers = tabs;
        }
    }
}
```

请注意，每个`UIViewController`实例中，我们将设置`Title`属性的`UIViewController`。 当将控制器添加到`UITabBarController`，则`UITabBarController`将读取`Title`针对每个控制器并将其显示在关联选项卡的标签，如下所示：

[![](creating-tabbed-applications-images/00-app.png "The sample app run")](creating-tabbed-applications-images/00-app.png#lightbox)

#### <a name="setting-the-tabcontroller-as-the-rootviewcontroller"></a>设置为 RootViewController TabController

控制器放置在选项卡中的顺序对应于它们添加到的顺序`ViewControllers`数组。

若要获取`UITabController`若要加载作为第一个屏幕，我们需要使其窗口的`RootViewController`，如以下代码中所示`AppDelegate`:

```csharp
[Register ("AppDelegate")]
public partial class AppDelegate : UIApplicationDelegate
{
    UIWindow window;
    TabController tabController;

    public override bool FinishedLaunching (UIApplication app, NSDictionary options)
    {
        window = new UIWindow (UIScreen.MainScreen.Bounds);

        tabController = new TabController ();
        window.RootViewController = tabController;

        window.MakeKeyAndVisible ();

        return true;
    }
}
```

如果我们运行该应用程序现在，`UITabBarController`默认情况下选择第一个选项卡中将加载。 导致关联的控制器选择任何其他选项卡查看由`UITabBarController,`最终用户已在其中选择第二个选项卡如下所示：

![표시 되는 두 번째 탭](creating-tabbed-applications-images/03-secondtab-sml.png)

### <a name="modifying-tabbaritems"></a>修改 TabBarItems

现在，我们只需运行选项卡上的应用程序，让我们修改`TabBarItem`若要更改的图像和文本显示，以及用于将一个徽章添加到其中一个选项卡。

#### <a name="setting-a-system-item"></a>시스템 항목 설정

首先，让我们来设置要使用系统项的第一个选项卡。 中的构造函数`TabController`，删除设置控制器的行`Title`有关`tab1`实例，并替换为以下代码以设置控制器的`TabBarItem`属性：

```csharp
tab1.TabBarItem = new UITabBarItem (UITabBarSystemItem.Favorites, 0);
```

创建时`UITabBarItem`使用`UITabBarSystemItem`，标题和图像由自动提供 iOS，下面显示的屏幕截图中所示**收藏夹**图标和标题的第一个选项卡上：

 ![별표 아이콘을 사용 하는 첫 번째 탭](creating-tabbed-applications-images/04a-tabimage-sml.png)

#### <a name="setting-the-image"></a>이미지 설정

除了使用系统项目、 标题和图像的`UITabBarItem`可设置为自定义值。 例如，更改设置的代码`TabBarItem`属性的名为控制器`tab2`，如下所示：

```csharp
tab2 = new UIViewController ();
tab2.TabBarItem = new UITabBarItem ();
tab2.TabBarItem.Image = UIImage.FromFile ("second.png");
tab2.TabBarItem.Title = "Second";
tab2.View.BackgroundColor = UIColor.Orange;
```

위의 코드에서는 `second.png` 라는 이미지가 프로젝트의 루트 또는 **Resources** 디렉터리에 추가 된 것으로 가정 합니다. 모든 화면 밀도를 지원 하려면 아래와 같이 세 개의 이미지가 필요 합니다.

![프로젝트에 추가 된 이미지](creating-tabbed-applications-images/tabbedimages7new.png)

올바른 차원에 대 한 지침은 [Apple 사용자 지정 아이콘 페이지](https://developer.apple.com/design/human-interface-guidelines/ios/icons-and-images/custom-icons/) 의 **탭 모음 아이콘 크기** 섹션을 참조 하세요. 권장 되는 크기는 이미지의 스타일 (원형, 사각형, 와이드 또는 높이)에 따라 달라 집니다.

`Image` 속성은 **두 번째 .png** 파일 이름 으로만 설정 해야 하며, 필요할 때 iOS에서 더 높은 해상도 파일을 자동으로 로드 합니다. 你可以阅读更多有关此信息[处理图像](~/ios/app-fundamentals/images-icons/index.md)指南。 默认选项卡栏项都是灰色、 用蓝色的浅色选择时。

#### <a name="overriding-the-title"></a>제목 재정의

`Title` 속성이 `TabBarItem`에서 직접 설정 되 면 컨트롤러 자체에서 `Title`에 대해 설정 된 모든 값이 재정의 됩니다.

이 스크린샷에서 두 번째 (가운데) 탭에는 사용자 지정 제목 및 이미지가 표시 됩니다.

![사각형 아이콘이 있는 두 번째 탭](creating-tabbed-applications-images/05-customtab-sml.png)

#### <a name="setting-the-badge-value"></a>배지 값 설정

一个选项卡还可以显示一个徽章。 例如，添加代码以将一个徽章设置第三个选项卡上的以下行：

```csharp
tab3.TabBarItem.BadgeValue = "Hi";
```

运行此命令会导致具有如下所示的选项卡的左上角中的字符串"Hi"的红色标签：

![Hi 배지를 포함 하는 두 번째 탭](creating-tabbed-applications-images/06-badge-sml.png)

徽章通常用于显示未读邮件的数字指示新项。 若要删除该徽标，请设置`BadgeValue`为 null，如下所示：

```csharp
tab3.TabBarItem.BadgeValue = null;
```

## <a name="tabs-in-non-rootviewcontroller-scenarios"></a>비 RootViewController 시나리오의 탭

在上述示例中，我们介绍了如何使用`UITabBarController`时`RootViewController`的窗口。 在此示例中我们将说明如何使用`UITabBarController`它不是`RootViewController`和创建方式展示了使用情节提要。

### <a name="initial-screen-example"></a>초기 화면 예제

对于此方案中，初始屏幕加载从控制器不是`UITabBarController`。 同一个视图控制器时用户与屏幕交互时点击一个按钮，将加载到`UITabBarController`，然后提供给用户。 下面的屏幕截图显示了应用程序流：

[![](creating-tabbed-applications-images/inital-screen-application.png "This screenshot shows the application flow")](creating-tabbed-applications-images/inital-screen-application.png#lightbox)

首先，此示例中的新应用程序。 同样，我们将使用**iPhone > 应用程序 > 空项目 (C#)** 模板，这一次在命名项目`InitialScreenDemo`。

이 예에서는 storyboard를 사용 하 여 뷰 컨트롤러를 레이아웃 합니다. 스토리 보드를 추가 하려면:

- 右键单击项目名称，然后选择**添加 > 新文件**。

- 新的文件对话框出现时，导航到**iOS > 空 iPhone 情节提要**。

让我们称此新情节提要**MainStoryboard** ，如下所示：

[![](creating-tabbed-applications-images/new-file-dialog.png "Add a MainStoryboard file to the project")](creating-tabbed-applications-images/new-file-dialog.png#lightbox)

有几个重要步骤中涉及到以前非演示图板文件中，添加情节提要时，请注意[情节提要简介](~/ios/user-interface/storyboards/index.md)指南。 이러한 설정은 다음과 같습니다.

1. 添加到你的情节提要的名称**主界面**一部分`Info.plist`:

    [![](creating-tabbed-applications-images/project-options.png "Set the Main Interface to MainStoryboard")](creating-tabbed-applications-images/project-options.png#lightbox)
1. 在你`App Delegate`，重写窗口方法，使用以下代码：

    ```csharp
    public override UIWindow Window {
        get;
        set;
    }
    ```

我们将此示例需要三个视图控制器。 이름이 `ViewController1`인 하나는 초기 뷰 컨트롤러로 사용 되 고 첫 번째 탭에서는 사용 됩니다. 두 번째 및 세 번째 탭에서 각각 사용 되는 다른 두 개의 명명 된 `ViewController2` 및 `ViewController3`입니다.

以打开 mainstoryboard.storyboard 文件中，打开设计器拖到设计图面上的三个视图控制器。 我们希望这些视图控制器具有其自身与上述名称相对应的类的每个这样的情况下下,**标识 > 类**，键入其名称，如下面的屏幕截图中所示：

[![](creating-tabbed-applications-images/class-name.png "Set the Class to ViewController1")](creating-tabbed-applications-images/class-name.png#lightbox)

Visual Studio for Mac 将自动生成的类和设计器所需的文件，这可以看到在解决方案面板中，如下图所示：

[![](creating-tabbed-applications-images/solution-pad2.png "Auto-generated files in the project")](creating-tabbed-applications-images/solution-pad2.png#lightbox)

#### <a name="creating-the-ui"></a>创建 UI

接下来，我们将为每个 ViewController 的视图，使用 Xamarin iOS 设计器创建一个简单的用户界面。

我们想要拖动`Label`和一个`Button`到从 ViewController1**工具箱**右侧。 接下来我们将使用属性面板来编辑在名称和文本的控件所示：

- **标签**: `Text`  = **一个**
- **按钮**: `Title`  = **用户会执行一些初始操作**

我们将控制在我们按钮的可见性`TouchUpInside`事件，并且我们需要在后面的代码中引用它。 让我们来确定其与**名称**`aButton`中属性面板，下面的屏幕截图中所示：

[![](creating-tabbed-applications-images/abutton-properties.png "Set the Name to aButton in the Properties Pad")](creating-tabbed-applications-images/abutton-properties.png#lightbox)

设计图面上应类似于下面的屏幕截图：

[![](creating-tabbed-applications-images/design-surface1.png "Your Design Surface should now look similar to this screenshot")](creating-tabbed-applications-images/design-surface1.png#lightbox)

让我们添加到稍微详细地`ViewController2`和`ViewController3`，方法是将标签添加到每个，并分别将文本更改为两个' 和 'Three'。 它突出显示了向用户正在查看的选项卡/视图。

#### <a name="wiring-up-the-button"></a>단추를 연결 합니다.

我们将加载`ViewController1`应用程序的第一次启动。 当用户点击按钮时，我们将隐藏按钮，并加载`UITabBarController`与`ViewController1`第一个选项卡中的实例。

当用户释放`aButton`，我们希望 TouchUpInside 事件被触发。 让我们选择按钮，然后在**事件选项卡**的属性面板中，声明事件处理程序 – `InitialActionCompleted` -以便可以在代码中引用。 下面的屏幕截图所示：

[![](creating-tabbed-applications-images/event-handler.png "When the user releases the aButton, trigger a TouchUpInside event")](creating-tabbed-applications-images/event-handler.png#lightbox)

现在，我们需要告诉视图控制器，若要在事件激发时隐藏按钮`InitialActionCompleted`。 在`ViewController1`，添加下面的分部方法：

```csharp
partial void InitialActionCompleted (UIButton sender)
{
    aButton.Hidden = true;  
}
```

保存该文件，并运行应用程序。 应该会看到其中一个出现的屏幕和上不显示修饰按钮。

#### <a name="adding-the-tab-bar-controller"></a>탭 표시줄 컨트롤러 추가

现在，我们有初始视图按预期方式工作。 接下来，我们想要将其添加到`UITabBarController`，以及视图 2 和 3。 让我们在设计器中打开情节提要。

在**工具箱**，搜索**选项卡栏控制器**在控制器和对象下并将此拖到设计图面。 您可以看到以下屏幕截图中，选项卡栏控制器是无用户界面，并因此使其与默认情况下的两个视图控制器：

[![](creating-tabbed-applications-images/tabbarcontroller.png "Adding a Tab Bar Controller to the layout")](creating-tabbed-applications-images/tabbarcontroller.png#lightbox)

通过选择底部的黑色栏并按 delete 键删除这些新的视图控制器。

在我们的情节提要，我们可以使用 segues 设计来处理 TabBarController 和我们的视图控制器之间的转换。 后与初始视图进行交互，我们想要将其加载到 TabBarController 向用户显示。 让我们对此进行设置设计器中。

**按住 Ctrl 键单击**和**拖动**从 TabBarController 的按钮。 鼠标弹起上将显示一个上下文菜单。 我们想要使用模式的 segue。

若要设置的我们选项卡上，每个**按住 Ctrl 键单击**从一到三种类型，然后选择关系到每个订单中我们视图控制器 TabBarController**选项卡**从上下文菜单，如下图所示：

[![](creating-tabbed-applications-images/context-menu.png "Select the Tab Relationship")](creating-tabbed-applications-images/context-menu.png#lightbox)

你的情节提要应类似于下面的屏幕截图：

[![](creating-tabbed-applications-images/segue-layout.png "The Storyboard should resemble this screenshot")](creating-tabbed-applications-images/segue-layout.png#lightbox)

如果我们单击其中一个选项卡栏项并探索属性面板，可以看到大量不同的选项，如下图所示：

[![](creating-tabbed-applications-images/properties-panel.png "Setting the tab options in the Properties Explorer")](creating-tabbed-applications-images/properties-panel.png#lightbox)

이를 사용 하 여 배지, 제목 및 iOS 식별자와 같은 특정 특성을 편집할 수 있습니다.

如果我们保存并运行应用程序现在，我们会发现该按钮 ViewController1 实例加载到 TabBarController 时再次出现。 让我们来解决此问题通过检查以查看当前视图是否具有父视图控制器。 如果是这样，我们知道我们位于 TabBarController，且因此应隐藏按钮。 让我们将以下代码添加到 ViewController1 类：

```csharp
public override void ViewDidLoad ()
{
    if (ParentViewController != null){
        aButton.Hidden = true;
    }
}
```

加载时在应用程序运行与用户点击第一个屏幕，UITabBarController 按钮，从放置在第一个选项卡中，如下所示的第一个屏幕视图：

[샘플 앱 출력 ![](creating-tabbed-applications-images/first-view-sml.png)](creating-tabbed-applications-images/first-view.png#lightbox)

## <a name="summary"></a>요약

本文介绍如何使用`UITabBarController`应用程序中。 我们介绍了如何将控制器加载到每个选项卡，以及如何在选项卡上设置属性，此类的标题、 图像和徽章。 我们然后检查，使用演示图板，如何加载`UITabBarController`在运行时不时`RootViewController`的窗口。

## <a name="related-links"></a>관련 링크

- [创建选项卡式应用程序 （示例）](https://docs.microsoft.com/samples/xamarin/ios-samples/creatingtabbedapplications)
- [Images.zip](https://github.com/xamarin/ios-samples/blob/master/CreatingTabbedApplications/Resources/images.zip?raw=true)
- [UITabBarController 类引用](https://developer.apple.com/library/ios/#documentation/uikit/reference/UITabBarController_Class/Reference/Reference.html)
