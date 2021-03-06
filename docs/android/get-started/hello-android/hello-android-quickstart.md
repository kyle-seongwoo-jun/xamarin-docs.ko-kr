---
title: 'Hello, Android: 빠른 시작'
description: 두 부분으로 구성된 이 가이드에서는 Mac용 Visual Studio 또는 Visual Studio를 사용하여 첫 번째 Xamarin.Android 애플리케이션을 빌드하고, Xamarin을 사용하여 Android 애플리케이션 개발에 대한 기본 사항을 이해하기 시작합니다. 이 과정에서 Xamarin.Android 애플리케이션을 빌드하고 배포하는 데 필요한 도구, 개념 및 단계를 소개합니다.
zone_pivot_groups: platform
ms.topic: quickstart
ms.prod: xamarin
ms.assetid: 44007FA1-3ABC-4935-BF52-4613AF0553A6
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 10/05/2018
ms.openlocfilehash: ab401c24fc486ba69fe01aff76e1a9b7d53122d0
ms.sourcegitcommit: 2fbe4932a319af4ebc829f65eb1fb1816ba305d3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73028026"
---
# <a name="hello-android-quickstart"></a>Hello, Android: 빠른 시작

_두 부분으로 구성된 이 가이드에서는 Visual Studio를 사용하여 첫 번째 Xamarin.Android 애플리케이션을 빌드하고, Xamarin을 사용하여 Android 애플리케이션 개발에 대한 기본 사항을 이해하기 시작합니다._

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/monodroid-samples/phoneword)

사용자가 입력한 영숫자 전화 번호를 숫자 전화 번호로 변환하고 해당 숫자 전화 번호를 사용자에게 표시하는 애플리케이션을 만듭니다. 최종 애플리케이션은 다음과 같습니다.

[![완료 시 앱 스크린샷](hello-android-quickstart-images/vs/15-running-app-sml.png)](hello-android-quickstart-images/vs/15-running-app.png#lightbox)

::: zone pivot="windows"

## <a name="windows-requirements"></a>Windows 요구 사항

이 연습을 수행하려면 다음이 필요합니다.

- Windows 10

- Visual Studio 2019 또는 Visual Studio 2017(버전 15.8 이상): Community, Professional 또는 Enterprise.

::: zone-end
::: zone pivot="macos"

## <a name="macos-requirements"></a>macOS 요구 사항

이 연습을 수행하려면 다음이 필요합니다.

- 최신 버전의 Mac용 Visual Studio

- macOS High Sierra(10.13) 이상을 실행하는 Mac

::: zone-end

이 연습에서는 최신 버전의 Xamarin.Android를 설치하고 선택한 플랫폼에서 실행하고 있다고 가정합니다. Xamarin.Android를 설치하는 가이드는 [Xamarin.Android 설치](~/android/get-started/installation/index.md) 가이드를 참조하세요.

## <a name="configuring-emulators"></a>에뮬레이터 구성

Android Emulator를 사용하는 경우 하드웨어 가속을 사용하도록 에뮬레이터를 구성하는 것이 좋습니다. 하드웨어 가속을 구성하는 지침은 [에뮬레이터 성능에 대한 하드웨어 가속](~/android/get-started/installation/android-emulator/hardware-acceleration.md)에서 제공됩니다.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

::: zone pivot="windows"

Visual Studio를 시작합니다. **파일 > 새로 만들기 > 프로젝트**를 클릭하여 새 프로젝트를 만듭니다.

**새 프로젝트** 대화 상자에서 **Android 앱** 템플릿을 클릭합니다.
새 프로젝트 이름을 `Phoneword`로 지정하고 **확인**을 클릭합니다.

[![새 프로젝트는 Phoneword입니다.](hello-android-quickstart-images/vs/01-new-project-name-w158-sml.png)](hello-android-quickstart-images/vs/01-new-project-name-w158.png#lightbox)

**새 Android 앱** 대화 상자에서 **비어 있는 앱**을 클릭하고 **확인**을 클릭하여 새 프로젝트를 만듭니다.

[![비어 있는 앱 템플릿 선택](hello-android-quickstart-images/vs/02-blank-app-w158-sml.png)](hello-android-quickstart-images/vs/02-blank-app-w158.png#lightbox)

## <a name="create-a-layout"></a>레이아웃 만들기

> [!TIP]
> 최신 버전의 Visual Studio에서는 Android Designer 내에서 .xml을 여는 것을 지원합니다.
>
> Android Designer에서는 .axml 파일과 .xml 파일이 모두 지원됩니다.

새 프로젝트를 만든 후에 **솔루션 탐색기**에서 **리소스** 폴더 및 **레이아웃** 폴더를 차례로 확장합니다.
**activity_main.axml**을 두 번 클릭하여 Android Designer에서 엽니다. 앱의 화면에 대한 레이아웃 파일입니다.

[![activity axml 파일 열기](hello-android-quickstart-images/vs/03-open-layout-w158-sml.png)](hello-android-quickstart-images/vs/03-open-layout-w158.png#lightbox)

> [!TIP]
> Visual Studio의 최신 릴리스는 약간 다른 앱 템플릿을 포함합니다.
>
> 1. 레이아웃은 **activity_main.axml** 대신 **content_main.axml**에 있습니다.
> 2. 기본 레이아웃은 `RelativeLayout`입니다. 이 페이지의 나머지 단계를 수행하려면 `<RelativeLayout>` 태그를 `<LinearLayout>`으로 변경하고 `LinearLayout` 여는 태그에 다른 특성 `android:orientation="vertical"`을 추가해야 합니다.

**도구 상자**(왼쪽 영역)에서 검색 표시줄에 `text`을 입력하고,**큰 텍스트** 위젯을 디자인 화면(가운데 영역)으로 끌어옵니다.

[![큰 텍스트 위젯 추가](hello-android-quickstart-images/vs/04-large-text-w158-sml.png)](hello-android-quickstart-images/vs/04-large-text-w158.png#lightbox)

디자인 화면에서 선택한 **큰 텍스트** 컨트롤에서 **속성** 창을 사용하여 **큰 텍스트** 위젯의 `Text` 속성을 `Enter a Phoneword:`로 변경합니다.

[![큰 텍스트 속성 설정](hello-android-quickstart-images/vs/05-enter-a-phoneword-w158-sml.png)](hello-android-quickstart-images/vs/05-enter-a-phoneword-w158.png#lightbox)

**도구 상자**에서 **일반 텍스트** 위젯을 디자인 화면으로 끌어와서 **큰 텍스트** 위젯 아래에 놓습니다. 위젯을 사용할 수 있는 레이아웃의 위치로 마우스 포인터를 이동할 때가지 위젯을 배치할 수 없습니다. 아래 스크린샷에서 마우스 포인터를 이전의 `TextView` 바로 아래로 이동할 때까지(오른쪽과 같이) 위젯을 배치할 수 없습니다(왼쪽과 같이).

[![마우스는 위젯을 어디에 배치할 수 있는지 나타냅니다.](hello-android-quickstart-images/vs/06a-cant-drop-w158-sml.png)](hello-android-quickstart-images/vs/06a-cant-drop-w158.png#lightbox)

**일반 텍스트**(`EditText` 위젯)가 올바르게 배치되면 다음 스크린샷에 표시된 것처럼 나타납니다.

[![일반 텍스트 위젯 추가](hello-android-quickstart-images/vs/06b-plain-text-w158-sml.png)](hello-android-quickstart-images/vs/06b-plain-text-w158.png#lightbox)

디자인 화면에서 선택한 **일반 텍스트** 위젯에서 **속성** 창을 사용하여 **일반 텍스트** 위젯의 `Id` 속성을 `@+id/PhoneNumberText`로 변경하고 `Text` 속성을 `1-855-XAMARIN`로 변경합니다.

[![일반 텍스트 속성 설정](hello-android-quickstart-images/vs/07-add-properties-w158-sml.png)](hello-android-quickstart-images/vs/07-add-properties-w158.png#lightbox)

**도구 상자**에서 **단추**를 디자인 화면으로 끌어와서 **일반 텍스트** 위젯 아래에 놓습니다.

[![디자인에 변환 단추 끌어오기](hello-android-quickstart-images/vs/08-drag-button-w158-sml.png)](hello-android-quickstart-images/vs/08-drag-button-w158.png#lightbox)

디자인 화면에서 선택한 **단추**에서 **속성** 창을 사용하여 `Text` 속성을 `Translate`으로 변경하고 `Id` 속성을 `@+id/TranslateButton`로 변경합니다.

[![변환 단추 속성 설정](hello-android-quickstart-images/vs/09-translate-button-w158-sml.png)](hello-android-quickstart-images/vs/09-translate-button-w158.png#lightbox)

**도구 상자**에서 **TextView**를 디자인 화면으로 끌어와서 **단추** 위젯 아래에 놓습니다. **TextView**의 `Text` 속성을 빈 문자열로 변경하고 `Id` 속성을 `@+id/TranslatedPhoneword`로 설정합니다.

[![텍스트 보기에서 속성 설정](hello-android-quickstart-images/vs/10-textview-properties-w158-sml.png)](hello-android-quickstart-images/vs/10-textview-properties-w158.png#lightbox)

**CTRL+S** 키를 눌러 작업을 저장합니다.

## <a name="write-some-code"></a>일부 코드 작성

다음 단계는 전화 번호를 영숫자에서 숫자로 변환하는 코드를 추가하는 것입니다. **솔루션 탐색기**에서 **Phoneword** 프로젝트를 마우스 오른쪽 단추로 클릭하고, 아래에 표시된 대로 **추가 > 새 항목...** 을 선택하여 프로젝트에 새 파일을 추가합니다.

[![새 항목 추가](hello-android-quickstart-images/vs/12-add-new-item-w158-sml.png)](hello-android-quickstart-images/vs/12-add-new-item-w158.png#lightbox)

**새 항목 추가** 대화 상자에서 **Visual C# > 코드 > 코드 파일**을 선택하고, 새 코드 파일에 **PhoneTranslator.cs**라는 이름을 지정합니다.

[![PhoneTranslator.cs 추가](hello-android-quickstart-images/vs/14-add-class-w158-sml.png)](hello-android-quickstart-images/vs/14-add-class-w158.png#lightbox)

그러면 비어 있는 새 C# 클래스가 만들어집니다. 다음 코드를 파일에 삽입합니다.

```csharp
using System.Text;
using System;
namespace Core
{
    public static class PhonewordTranslator
    {
        public static string ToNumber(string raw)
        {
            if (string.IsNullOrWhiteSpace(raw))
                return "";
            else
                raw = raw.ToUpperInvariant();

            var newNumber = new StringBuilder();
            foreach (var c in raw)
            {
                if (" -0123456789".Contains(c))
                {
                    newNumber.Append(c);
                }
                else
                {
                    var result = TranslateToNumber(c);
                    if (result != null)
                        newNumber.Append(result);
                }
                // otherwise we've skipped a non-numeric char
            }
            return newNumber.ToString();
        }
        static bool Contains (this string keyString, char c)
        {
            return keyString.IndexOf(c) >= 0;
        }
        static int? TranslateToNumber(char c)
        {
            if ("ABC".Contains(c))
                return 2;
            else if ("DEF".Contains(c))
                return 3;
            else if ("GHI".Contains(c))
                return 4;
            else if ("JKL".Contains(c))
                return 5;
            else if ("MNO".Contains(c))
                return 6;
            else if ("PQRS".Contains(c))
                return 7;
            else if ("TUV".Contains(c))
                return 8;
            else if ("WXYZ".Contains(c))
                return 9;
            return null;
        }
    }
}
```

**파일 > 저장**을 클릭(하거나 **CTRL+S** 키를 눌러서)하여 **PhoneTranslator.cs** 파일에 변경 내용을 저장한 다음, 파일을 닫습니다.

## <a name="wire-up-the-user-interface"></a>사용자 인터페이스 연결

다음 단계는 `MainActivity` 클래스에 백업 코드를 삽입하여 사용자 인터페이스를 연결하는 코드를 추가하는 것입니다. **변환** 단추를 마무리합니다. `MainActivity` 클래스에서 `OnCreate` 메서드를 찾습니다. 다음 단계는 `base.OnCreate(savedInstanceState)` 및 `SetContentView(Resource.Layout.activity_main)` 호출 아래의 `OnCreate` 내부에 단추 코드를 추가하는 것입니다. 먼저 `OnCreate` 메서드가 다음과 유사하도록 템플릿 코드를 수정합니다.

```csharp
using Android.App;
using Android.OS;
using Android.Support.V7.App;
using Android.Runtime;
using Android.Widget;

namespace Phoneword
{
    [Activity(Label = "@string/app_name", Theme = "@style/AppTheme", MainLauncher = true)]
    public class MainActivity : AppCompatActivity
    {
        protected override void OnCreate(Bundle savedInstanceState)
        {
            base.OnCreate(savedInstanceState);

            // Set our view from the "main" layout resource
            SetContentView(Resource.Layout.activity_main);

            // New code will go here
        }
    }
}
```

Android Designer를 통해 레이아웃 파일에서 생성된 컨트롤에 대한 참조를 가져옵니다. `SetContentView` 호출 후에 `OnCreate` 메서드 내부에 다음 코드를 추가합니다.

```csharp
// Get our UI controls from the loaded layout
EditText phoneNumberText = FindViewById<EditText>(Resource.Id.PhoneNumberText);
TextView translatedPhoneWord = FindViewById<TextView>(Resource.Id.TranslatedPhoneword);
Button translateButton = FindViewById<Button>(Resource.Id.TranslateButton);
```

사용자가 **변환** 단추를 누르면 응답하는 코드를 추가합니다.
(이전 단계에서 추가한 줄 뒤에)`OnCreate` 메서드에 다음 코드를 추가합니다.

```csharp
// Add code to translate number
translateButton.Click += (sender, e) =>
{
    // Translate user's alphanumeric phone number to numeric
    string translatedNumber = Core.PhonewordTranslator.ToNumber(phoneNumberText.Text);
    if (string.IsNullOrWhiteSpace(translatedNumber))
    {
        translatedPhoneWord.Text = string.Empty;
    }
    else
    {
        translatedPhoneWord.Text = translatedNumber;
    }
};
```

**파일 &gt; 모두 저장**을 선택(하거나 **CTRL-SHIFT-S** 키를 눌러서)하여 작업을 저장하고, **빌드 &gt; 솔루션 다시 빌드**를 선택(하거나 **CTRL-SHIFT-B** 키를 눌러서)하여 애플리케이션을 빌드합니다. 

오류가 있는 경우 이전 단계를 진행하고, 애플리케이션이 성공적으로 빌드될 때까지 모든 오류를 수정합니다. _현재 컨텍스트에서 리소스가 존재하지 않습니다._ 와 같은 빌드 오류가 발생할 경우 **MainActivity.cs**의 네임스페이스 이름이 프로젝트 이름(`Phoneword`)과 일치하는지 확인한 다음, 솔루션을 완전히 다시 빌드합니다. 빌드 오류가 여전히 발생하는 경우 최신 Visual Studio 업데이트를 설치했는지 확인합니다.

## <a name="set-the-app-name"></a>앱 이름 설정

이제 애플리케이션을 만들었습니다. &ndash; 앱 이름을 설정하겠습니다. **값** 폴더(**리소스** 폴더 내부)를 확장하고 **strings.xml** 파일을 엽니다. 다음과 같이 앱 이름 문자열을 `Phone Word`로 변경합니다.

```xml
<resources>
    <string name="app_name">Phone Word</string>
    <string name="action_settings">Settings</string>
</resources>
```

## <a name="run-the-app"></a>앱 실행

Android 디바이스 또는 에뮬레이터에서 애플리케이션을 실행하여 테스트합니다.
**좌표 이동** 단추를 눌러 **1-855-XAMARIN**을 전화 번호로 변환합니다.

[![실행 중인 앱의 스크린샷](hello-android-quickstart-images/vs/15-running-app-sml.png)](hello-android-quickstart-images/vs/15-running-app.png#lightbox)

Android 디바이스에서 앱을 실행하려면 [개발용 디바이스 설정](~/android/get-started/installation/set-up-device-for-development.md) 방법을 참조하세요.

::: zone-end
::: zone pivot="macos"

**애플리케이션** 폴더 또는 **스포트라이트**에서 Mac용 Visual Studio를 시작합니다.

**새 프로젝트...** 를 클릭하여 새 프로젝트를 만듭니다.

**새 프로젝트의 템플릿 선택** 대화 상자에서 **Android > 앱**을 클릭하고 **Android 앱** 템플릿을 선택합니다. **다음**을 클릭합니다.

[![Android 앱 템플릿 선택](hello-android-quickstart-images/xs/03-choose-template-sml.png)](hello-android-quickstart-images/xs/03-choose-template.png#lightbox)

**Android 앱 구성** 대화 상자에서 새 앱의 이름을 `Phoneword`으로 지정하고 **다음**을 클릭합니다.

[![Android 앱 구성](hello-android-quickstart-images/xs/04-configure-android-app-sml.png)](hello-android-quickstart-images/xs/04-configure-android-app.png#lightbox)

**새 Android 앱 구성** 대화 상자에서 솔루션 및 프로젝트 이름을 `Phoneword`로 설정해 두고 **만들기**를 클릭하여 프로젝트를 만듭니다.

## <a name="create-a-layout"></a>레이아웃 만들기

> [!TIP]
> 최신 버전의 Visual Studio에서는 Android Designer 내에서 .xml을 여는 것을 지원합니다.
>
> Android Designer에서는 .axml 파일과 .xml 파일이 모두 지원됩니다.

새 프로젝트를 만든 후에 **솔루션** 패드에서 **리소스** 폴더 및 **레이아웃** 폴더를 차례로 확장합니다.
**Main.axml**을 두 번 클릭하여 Android Designer에서 엽니다. Android Designer에서 볼 때 화면에 대한 레이아웃 파일입니다.

[![Main.axml 열기](hello-android-quickstart-images/xs/05-open-layout-sml.png)](hello-android-quickstart-images/xs/05-open-layout.png#lightbox)

**Hello World, 클릭하세요.** 를 선택합니다. 디자인 화면의 **단추** 및 **삭제** 키를 눌러서 제거합니다. 

**도구 상자**(오른쪽 영역)에서 검색 표시줄에 `text`을 입력하고,**큰 텍스트** 위젯을 디자인 화면(가운데 영역)으로 끌어옵니다.

[![큰 텍스트 위젯 추가](hello-android-quickstart-images/xs/06-large-text-sml.png)](hello-android-quickstart-images/xs/06-large-text.png#lightbox)

디자인 화면에서 선택한 **큰 텍스트** 위젯에서 **속성** 패드를 사용하여 다음과 같이 **큰 텍스트** 위젯의 `Text` 속성을 `Enter a Phoneword:`로 변경할 수 있습니다.

[![큰 텍스트 위젯 속성 설정](hello-android-quickstart-images/xs/07-enter-a-phoneword-sml.png)](hello-android-quickstart-images/xs/07-enter-a-phoneword.png#lightbox)

다음으로 **도구 상자**에서 **일반 텍스트** 위젯을 디자인 화면으로 끌어와서 **큰 텍스트** 위젯 아래에 놓습니다. 필드를 사용하여 위젯을 이름으로 찾을 수 있습니다.

[![일반 텍스트 위젯 추가](hello-android-quickstart-images/xs/08-plain-text-sml.png)](hello-android-quickstart-images/xs/08-plain-text.png#lightbox)

디자인 화면에서 선택한 **일반 텍스트** 위젯에서 **속성** 패드를 사용하여 **일반 텍스트** 위젯의 `Id` 속성을 `@+id/PhoneNumberText`로 변경하고 `Text` 속성을 `1-855-XAMARIN`로 변경할 수 있습니다.

[![일반 텍스트 위젯 속성 설정](hello-android-quickstart-images/xs/09-add-properties-sml.png)](hello-android-quickstart-images/xs/09-add-properties.png#lightbox)

**도구 상자**에서 **단추**를 디자인 화면으로 끌어와서 **일반 텍스트** 위젯 아래에 놓습니다.

[![단추 추가](hello-android-quickstart-images/xs/10-drag-button-sml.png)](hello-android-quickstart-images/xs/10-drag-button.png#lightbox)

디자인 화면에서 선택한 **단추**에서 **속성** 패드를 사용하여 **단추**의 `Id` 속성을 `@+id/TranslateButton`로 변경하고 `Text` 속성을 `Translate`로 변경할 수 있습니다.

[![변환 단추로 구성](hello-android-quickstart-images/xs/11-translate-button-sml.png)](hello-android-quickstart-images/xs/11-translate-button.png#lightbox)

**도구 상자**에서 **TextView**를 디자인 화면으로 끌어와서 **단추** 위젯 아래에 놓습니다. **TextView**를 선택하여 **TextView**의 `id` 속성을 `@+id/TranslatedPhoneWord`로 설정하고 `text`를 빈 문자열로 변경합니다.

[![텍스트 보기에서 속성 설정](hello-android-quickstart-images/xs/12-textview-properties-sml.png)](hello-android-quickstart-images/xs/12-textview-properties.png#lightbox)    

**&#8984; + S** 키를 눌러 작업을 저장합니다.

## <a name="write-some-code"></a>일부 코드 작성

이제 전화 번호를 영숫자에서 숫자로 변환하는 코드 추가합니다. **솔루션** 패드에서 **Phoneword** 프로젝트의 옆에 있는 기어 아이콘을 클릭하고 **추가 > 새 파일...** 을 선택하하여 프로젝트에 새 파일을 추가합니다.

[![프로젝트에 새 파일 추가](hello-android-quickstart-images/xs/14-add-new-file-sml.png)](hello-android-quickstart-images/xs/14-add-new-file.png#lightbox)

**새 파일** 대화 상자에서 **General > Empty Class**를 선택하고, 새 파일에 **PhoneTranslator**라는 이름을 지정하고 **새로 만들기**를 클릭합니다. 이렇게 하면 비어 있는 새 C# 클래스가 만들어집니다.

새 클래스에서 템플릿 코드를 모두 제거하고 다음 코드로 바꿉니다.

```csharp
using System.Text;
using System;
namespace Core
{
    public static class PhonewordTranslator
    {
        public static string ToNumber(string raw)
        {
            if (string.IsNullOrWhiteSpace(raw))
                return "";
            else
                raw = raw.ToUpperInvariant();

            var newNumber = new StringBuilder();
            foreach (var c in raw)
            {
                if (" -0123456789".Contains(c))
                {
                    newNumber.Append(c);
                }
                else
                {
                    var result = TranslateToNumber(c);
                    if (result != null)
                        newNumber.Append(result);
                }
                // otherwise we've skipped a non-numeric char
            }
            return newNumber.ToString();
        }
        static bool Contains (this string keyString, char c)
        {
            return keyString.IndexOf(c) >= 0;
        }
        static int? TranslateToNumber(char c)
        {
            if ("ABC".Contains(c))
                return 2;
            else if ("DEF".Contains(c))
                return 3;
            else if ("GHI".Contains(c))
                return 4;
            else if ("JKL".Contains(c))
                return 5;
            else if ("MNO".Contains(c))
                return 6;
            else if ("PQRS".Contains(c))
                return 7;
            else if ("TUV".Contains(c))
                return 8;
            else if ("WXYZ".Contains(c))
                return 9;
            return null;
        }
    }
}
```

**파일 > 저장**을 선택(하거나 **&#8984; + S** 키를 눌러서)하여 **PhoneTranslator.cs** 파일에 변경 내용을 저장한 다음, 파일을 닫습니다. 솔루션을 다시 빌드하여 컴파일 시간 오류가 없는지 확인합니다.

## <a name="wire-up-the-user-interface"></a>사용자 인터페이스 연결

다음 단계는 `MainActivity` 클래스에 백업 코드를 추가하여 사용자 인터페이스를 연결하는 코드를 추가하는 것입니다.
**Solution Pad**에서 **MainActivity.cs**를 두 번 클릭하여 엽니다.

이벤트 처리기를 **변환** 단추에 추가하여 시작합니다. `MainActivity` 클래스에서 `OnCreate` 메서드를 찾습니다. `base.OnCreate(bundle)` 및 `SetContentView (Resource.Layout.Main)` 호출 아래의 `OnCreate` 내부에 단추 코드를 추가합니다. `OnCreate` 메서드가 다음과 유사하도록 기존 단추 처리 코드(`Resource.Id.myButton`을 참조하고 클릭 처리기를 만드는 코드)를 제거합니다.

```csharp
using System;
using Android.App;
using Android.Content;
using Android.Runtime;
using Android.Views;
using Android.Widget;
using Android.OS;

namespace Phoneword
{
    [Activity (Label = "Phone Word", MainLauncher = true)]
    public class MainActivity : Activity
    {
        protected override void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Our code will go here
        }
    }
}
```

다음으로 Android Designer를 사용하여 레이아웃 파일에서 생성된 컨트롤에 참조가 필요합니다. (`SetContentView` 호출 후에)`OnCreate` 메서드 내부에 다음 코드를 추가합니다.

```csharp
// Get our UI controls from the loaded layout
EditText phoneNumberText = FindViewById<EditText>(Resource.Id.PhoneNumberText);
TextView translatedPhoneWord = FindViewById<TextView>(Resource.Id.TranslatedPhoneWord);
Button translateButton = FindViewById<Button>(Resource.Id.TranslateButton);
```

(마지막 단계에서 추가한 줄 뒤에) 다음 코드를 `OnCreate` 메서드에 추가하여 사용자가 **변환** 단추를 누르면 응답하는 코드를 추가합니다.

```csharp
// Add code to translate number
string translatedNumber = string.Empty;

translateButton.Click += (sender, e) =>
{
    // Translate user's alphanumeric phone number to numeric
    translatedNumber = PhonewordTranslator.ToNumber(phoneNumberText.Text);
    if (string.IsNullOrWhiteSpace(translatedNumber))
    {
        translatedPhoneWord.Text = string.Empty;
    }
    else
    {
        translatedPhoneWord.Text = translatedNumber;
    }
};
```

**빌드 > 모두 빌드**를 선택(하거나 **&#8984; + B** 키를 눌러)하여 작업 내용을 저장하고 애플리케이션을 빌드합니다. 애플리케이션을 컴파일하는 경우 Mac용 Visual Studio 맨 위에서 성공 메시지가 표시됩니다.

오류가 있는 경우 이전 단계를 진행하고, 애플리케이션이 성공적으로 빌드될 때까지 모든 오류를 수정합니다. _현재 컨텍스트에서 리소스가 존재하지 않습니다._ 와 같은 빌드 오류가 발생할 경우 **MainActivity.cs**의 네임스페이스 이름이 프로젝트 이름(`Phoneword`)과 일치하는지 확인한 다음, 솔루션을 완전히 다시 빌드합니다. 빌드 오류가 여전히 발생하는 경우 최신 Xamarin.Android 및 Mac용 Visual Studio 업데이트를 설치했는지 확인합니다.

## <a name="set-the-label-and-app-icon"></a>레이블 및 앱 아이콘 설정

이제 애플리케이션을 만들었습니다. 마무리 작업을 추가하겠습니다. `MainActivity`에 대한 `Label`을 편집하여 시작합니다.
`Label`은 사용자가 애플리케이션에서 현재 위치를 알 수 있도록 Android가 화면 맨 위에 표시하는 항목입니다. `MainActivity` 클래스의 맨 위에서 다음과 같이 `Label`을 `Phone Word`로 변경합니다.

```csharp
namespace Phoneword
{
    [Activity (Label = "Phone Word", MainLauncher = true)]
    public class MainActivity : Activity
    {
        ...
    }
}
```

이제 애플리케이션 아이콘을 설정하겠습니다. 기본적으로 Mac용 Visual Studio는 프로젝트에 기본 아이콘을 제공합니다. 솔루션에서 이러한 파일을 삭제하고 다른 아이콘으로 바꿉니다. **Solution Pad**에서 **리소스** 폴더를 확장합니다. **mipmap-** 을 접두사로 지정한 5개의 폴더가 있고 해당 폴더에는 각각 단일 **Icon.png** 파일이 포함됩니다.

[![mipmap- 폴더 및 Icon.png 파일](hello-android-quickstart-images/xs/23-mipmap-folders-sml.png)](hello-android-quickstart-images/xs/23-mipmap-folders.png#lightbox)

이러한 아이콘 파일을 각 프로젝트에서 삭제해야 합니다. 각 **Icon.png** 파일을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **제거**를 선택합니다.

[![기본 Icon.png 삭제](hello-android-quickstart-images/xs/23-delete-icon-sml.png)](hello-android-quickstart-images/xs/23-delete-icon.png#lightbox)

대화 상자에서 **삭제** 단추를 클릭합니다.

다음으로 [Xamarin 앱 아이콘 설정](https://github.com/xamarin/monodroid-samples/blob/master/Phoneword/Resources/XamarinAndroidIcons.zip?raw=true)을 다운로드하고 압축을 풉니다. 이 zip 파일은 애플리케이션에 대한 아이콘을 보관합니다. 각 아이콘은 시각적으로 거의 동일하지만 다양한 화면 밀도를 가진 다양한 디바이스에서 다른 해상도로 올바르게 렌더링합니다.  파일 집합을 Xamarin.Android 프로젝트에 복사해야 합니다. Mac용 Visual Studio의 **Solution Pad**에서 **mipmap-hdpi** 폴더를 마우스 오른쪽 단추로 클릭하고 **추가 > 파일 추가**를 선택합니다.

[![파일 추가](hello-android-quickstart-images/xs/24-add-files-sml.png)](hello-android-quickstart-images/xs/24-add-files.png#lightbox)

선택 영역 대화 상자에서 압축을 푼 Xamarin AdApp 아이콘 디렉터리로 이동하고 **mipmap-hdpi** 폴더를 엽니다. **Icon.png**를 선택하고 **열기**를 클릭합니다.

**폴더에 파일 추가** 대화 상자에서 **디렉터리에 파일 복사**를 선택하고 **확인**을 클릭합니다.

[![디렉터리 대화 상자에 파일 복사](hello-android-quickstart-images/xs/26-copy-to-directory-sml.png)](hello-android-quickstart-images/xs/26-copy-to-directory.png#lightbox)

**Phoneword** 프로젝트에서 **mipmap-** Xamarin 앱 아이콘 폴더의 콘텐츠를 해당하는 **mipmap-** 폴더에 복사할 때까지 **mipmap-** 폴더의 각각에 대해 이러한 단계를 반복합니다.

모든 아이콘을 Xamarin.Android 프로젝트에 복사한 후에 **Solution Pad**에서 프로젝트를 마우스 오른쪽 단추로 클릭하여 **프로젝트 옵션** 대화 상자를 엽니다. **빌드 &gt; Android 애플리케이션**을 선택하고 **애플리케이션 아이콘** 콤보 상자에서 `@mipmap/icon`을 선택합니다.

[![프로젝트 아이콘 설정](hello-android-quickstart-images/xs/28-set-project-icon-sml.png)](hello-android-quickstart-images/xs/28-set-project-icon.png#lightbox)

## <a name="run-the-app"></a>앱 실행

마지막으로 Android 디바이스 또는 에뮬레이터에서 애플리케이션을 실행하고 Phoneword를 변환하여 테스트합니다.

[![완료 시 앱 스크린샷](hello-android-quickstart-images/intro-app-examples-sml.png)](hello-android-quickstart-images/intro-app-examples.png#lightbox)

Android 디바이스에서 앱을 실행하려면 [개발용 디바이스 설정](~/android/get-started/installation/set-up-device-for-development.md) 방법을 참조하세요.

::: zone-end

첫 번째 Xamarin.Android 애플리케이션을 완성한 것을 축하합니다!
이제 방금 알아본 도구와 기술을 분석하겠습니다. 다음 단계는 [Hello, Android 심층 분석](~/android/get-started/hello-android/hello-android-deepdive.md)입니다.

## <a name="related-links"></a>관련 링크

- [Xamarin Android 앱 아이콘(ZIP)](https://github.com/xamarin/monodroid-samples/blob/master/Phoneword/Resources/XamarinAndroidIcons.zip?raw=true)
- [Phoneword(샘플)](https://docs.microsoft.com/samples/xamarin/monodroid-samples/phoneword)
