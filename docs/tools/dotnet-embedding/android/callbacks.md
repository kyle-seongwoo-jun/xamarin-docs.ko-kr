---
title: Android의 콜백
ms.prod: xamarin
ms.assetid: F3A7A4E6-41FE-4F12-949C-96090815C5D6
author: davidortinau
ms.author: daortin
ms.date: 11/14/2017
ms.openlocfilehash: 2d1d5b8985d132e5a5839e3cd23aaec32fc3815a
ms.sourcegitcommit: db422e33438f1b5c55852e6942c3d1d75dc025c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2020
ms.locfileid: "76725115"
---
# <a name="callbacks-on-android"></a>Android의 콜백

에서 C# Java로 호출 하는 것은 매우 *위험한 비즈니스*입니다. 즉,에서 C# Java로의 콜백에 대 한 *패턴이* 있다고 가정 합니다. 그러나 원하는 것 보다 더 복잡 합니다.

Java에 가장 적합 한 콜백을 수행 하기 위한 세 가지 옵션을 살펴보겠습니다.

- 추상 클래스
- 인터페이스
- 가상 메서드

## <a name="abstract-classes"></a>추상 클래스

이는 콜백에 가장 쉬운 경로 이기 때문에 가장 간단한 형태로 콜백을 작동 하려는 경우 `abstract`를 사용 하는 것이 좋습니다.

Java를 구현할 C# 클래스부터 살펴보겠습니다.

```csharp
[Register("mono.embeddinator.android.AbstractClass")]
public abstract class AbstractClass : Java.Lang.Object
{
    public AbstractClass() { }

    public AbstractClass(IntPtr handle, JniHandleOwnership transfer) : base(handle, transfer) { }

    [Export("getText")]
    public abstract string GetText();
}
```

이 작업을 수행 하기 위한 세부 정보는 다음과 같습니다.

- Java에서 유용한 패키지 이름을 생성 하는 `[Register]` .이를 제외 하 고 자동으로 생성 된 패키지 이름을 가져옵니다.
- Xamarin을 통해 클래스를 실행 하기 위해 .NET 포함에 `Java.Lang.Object` 신호를 서브클래싱 합니다.
- 빈 생성자: Java 코드에서 사용 하려는 것입니다.
- `(IntPtr, JniHandleOwnership)` 생성자: Xamarin은 Java 개체와 동등한 C#기능을 만드는 데 사용 됩니다.
- `[Export]`은 메서드를 Java에 노출 하도록 Xamarin.ios에 신호를 보냅니다. Java 세계에서 소문자 메서드를 사용 하는 것이 선호 되므로 메서드 이름을 변경할 수도 있습니다.

그런 다음 시나리오를 테스트 C# 하는 메서드를 살펴보겠습니다.

```csharp
[Register("mono.embeddinator.android.JavaCallbacks")]
public class JavaCallbacks : Java.Lang.Object
{
    [Export("abstractCallback")]
    public static string AbstractCallback(AbstractClass callback)
    {
        return callback.GetText();
    }
}
```

`JavaCallbacks`은 `Java.Lang.Object`인 한이를 테스트 하는 모든 클래스가 될 수 있습니다.

이제 .NET 어셈블리에 .NET 포함을 실행 하 여 AAR를 생성 합니다. 자세한 내용은 [시작 가이드](~/tools/dotnet-embedding/get-started/java/android.md) 를 참조 하세요.

AAR 파일을 Android Studio로 가져온 후에는 단위 테스트를 작성 하겠습니다.

```java
@Test
public void abstractCallback() throws Throwable {
    AbstractClass callback = new AbstractClass() {
        @Override
        public String getText() {
            return "Java";
        }
    };

    assertEquals("Java", callback.getText());
    assertEquals("Java", JavaCallbacks.abstractCallback(callback));
}
```

따라서 다음 작업을 수행 합니다.

- 무명 형식을 사용 하 여 Java에서 `AbstractClass` 구현 됨
- 인스턴스가 Java에서 `"Java"`을 반환 하도록 했습니다.
- 인스턴스가 `"Java"`를 반환 하도록 했습니다.C#
- 생성자가 현재로 C# 표시 되어 있기 때문에 `throws Throwable`추가 되었습니다 `throws`

이 단위 테스트를 있는 그대로 실행 하면 다음과 같은 오류가 발생 하 여 실패 합니다.

```csharp
System.NotSupportedException: Unable to find Invoker for type 'Android.AbstractClass'. Was it linked away?
```

여기에는 `Invoker` 형식이 없습니다. Java에 대 한 호출을 전달 C# 하는 `AbstractClass`의 서브 클래스입니다. Java 개체가 C# 전 세계에 있고 동일한 C# 형식이 abstract 인 경우 xamarin.ios는 코드 내에서 C# C# 사용 하기 위해 `Invoker` 접미사가 포함 된 형식을 자동으로 찾습니다.

Xamarin.ios는 Java 바인딩 프로젝트에서이 `Invoker` 패턴을 사용 합니다.

다음은 `AbstractClassInvoker`의 구현입니다.

```csharp
class AbstractClassInvoker : AbstractClass
{
    IntPtr class_ref, id_gettext;

    public AbstractClassInvoker(IntPtr handle, JniHandleOwnership transfer) : base(handle, transfer)
    {
        IntPtr lref = JNIEnv.GetObjectClass(Handle);
        class_ref = JNIEnv.NewGlobalRef(lref);
        JNIEnv.DeleteLocalRef(lref);
    }

    protected override Type ThresholdType
    {
        get { return typeof(AbstractClassInvoker); }
    }

    protected override IntPtr ThresholdClass
    {
        get { return class_ref; }
    }

    public override string GetText()
    {
        if (id_gettext == IntPtr.Zero)
            id_gettext = JNIEnv.GetMethodID(class_ref, "getText", "()Ljava/lang/String;");
        IntPtr lref = JNIEnv.CallObjectMethod(Handle, id_gettext);
        return GetObject<Java.Lang.String>(lref, JniHandleOwnership.TransferLocalRef)?.ToString();
    }

    protected override void Dispose(bool disposing)
    {
        if (class_ref != IntPtr.Zero)
            JNIEnv.DeleteGlobalRef(class_ref);
        class_ref = IntPtr.Zero;

        base.Dispose(disposing);
    }
}
```

여기서는 약간의 차이가 있습니다.

- 해당 서브 클래스 `Invoker` 접미사를 사용 하 여 클래스를 추가 `AbstractClass`
- C# 클래스를 서브클래싱하는 Java 클래스에 대 한 JNI 참조를 보유 하는 `class_ref` 추가 되었습니다.
- JNI 참조를 포함 하는 `id_gettext`를 Java `getText` 메서드에 추가 했습니다.
- `(IntPtr, JniHandleOwnership)` 생성자를 포함 합니다.
- `Invoker`에 대 한 세부 정보를 확인 하기 위해 Xamarin.ios에 대 한 요구 사항으로 `ThresholdType` 및 `ThresholdClass` 구현 됨
- `GetText` 적절 한 JNI 서명으로 Java `getText` 메서드를 조회 하 고 호출 하는 데 필요 합니다.
- `Dispose`은에 대 한 참조를 지우는 데만 필요 `class_ref`

이 클래스를 추가 하 고 새 AAR를 생성 한 후 단위 테스트를 통과 합니다. 이는 콜백에 대 한이 패턴을 볼 수 있지만 심지어는 *적합*하지 않습니다.

Java interop에 대 한 자세한 내용은이 주제에 대 한 놀라운 [Xamarin Android 설명서](~/android/platform/java-integration/working-with-jni.md) 를 참조 하세요.

## <a name="interfaces"></a>인터페이스

인터페이스는 한 가지 세부 정보를 제외 하 고 추상 클래스와 거의 동일 합니다. Android는이에 대 한 Java를 생성 하지 않습니다. 이는 .NET을 포함 하기 전에 Java가 인터페이스를 C# 구현 하는 시나리오는 많지 않기 때문입니다.

다음 C# 인터페이스가 있다고 가정해 보겠습니다.

```csharp
[Register("mono.embeddinator.android.IJavaCallback")]
public interface IJavaCallback : IJavaObject
{
    [Export("send")]
    void Send(string text);
}
```

이는 Xamarin.ios 인터페이스 이지만 .NET 포함에 `IJavaObject` 신호를 전달 하는 것이 고, 그렇지 않은 경우 `abstract` 클래스와 동일 합니다.

Xamarin.ios는 현재이 인터페이스에 대 한 Java 코드를 생성 하지 않으므로 C# 프로젝트에 다음 java를 추가 합니다.

```java
package mono.embeddinator.android;

public interface IJavaCallback {
    void send(String text);
}
```

어디에 나 파일을 저장할 수 있지만, 빌드 작업을 `AndroidJavaSource`으로 설정 해야 합니다. 그러면 AAR 파일로 컴파일하기 위해 적절 한 디렉터리에 복사 하는 .NET 포함을 알립니다.

다음으로 `Invoker` 구현은 매우 동일 합니다.

```csharp
class IJavaCallbackInvoker : Java.Lang.Object, IJavaCallback
{
    IntPtr class_ref, id_send;

    public IJavaCallbackInvoker(IntPtr handle, JniHandleOwnership transfer) : base(handle, transfer)
    {
        IntPtr lref = JNIEnv.GetObjectClass(Handle);
        class_ref = JNIEnv.NewGlobalRef(lref);
        JNIEnv.DeleteLocalRef(lref);
    }

    protected override Type ThresholdType
    {
        get { return typeof(IJavaCallbackInvoker); }
    }

    protected override IntPtr ThresholdClass
    {
        get { return class_ref; }
    }

    public void Send(string text)
    {
        if (id_send == IntPtr.Zero)
            id_send = JNIEnv.GetMethodID(class_ref, "send", "(Ljava/lang/String;)V");
        JNIEnv.CallVoidMethod(Handle, id_send, new JValue(new Java.Lang.String(text)));
    }

    protected override void Dispose(bool disposing)
    {
        if (class_ref != IntPtr.Zero)
            JNIEnv.DeleteGlobalRef(class_ref);
        class_ref = IntPtr.Zero;

        base.Dispose(disposing);
    }
}
```

AAR 파일을 생성 한 후에는 다음을 전달 하는 단위 테스트를 작성할 수 Android Studio.

```java
class ConcreteCallback implements IJavaCallback {
    public String text;
    @Override
    public void send(String text) {
        this.text = text;
    }
}

@Test
public void interfaceCallback() {
    ConcreteCallback callback = new ConcreteCallback();
    JavaCallbacks.interfaceCallback(callback, "Java");
    assertEquals("Java", callback.text);
}
```

## <a name="virtual-methods"></a>가상 메서드

Java에서 `virtual`를 재정의 하는 것은 가능 하지만 좋은 환경은 아닙니다.

다음 C# 클래스가 있다고 가정해 보겠습니다.

```csharp
[Register("mono.embeddinator.android.VirtualClass")]
public class VirtualClass : Java.Lang.Object
{
    public VirtualClass() { }

    public VirtualClass(IntPtr handle, JniHandleOwnership transfer) : base(handle, transfer) { }

    [Export("getText")]
    public virtual string GetText() { return "C#"; }
}
```

위의 `abstract` 클래스 예제를 수행한 경우에는 한 가지 세부 사항을 제외 하 고 작동 합니다. 즉, _Xamarin. Android는 `Invoker`를 조회 하지 않습니다_ .

이 문제를 해결 하려면 `abstract`C# 되도록 클래스를 수정 합니다.

```csharp
public abstract class VirtualClass : Java.Lang.Object
```

이는 이상적이 지 않지만이 시나리오를 작동 하 게 됩니다. Xamarin.ios는 `VirtualClassInvoker`를 선택 하 고 Java는 메서드에서 `@Override`를 사용할 수 있습니다.

## <a name="callbacks-in-the-future"></a>미래의 콜백

이러한 시나리오를 향상 시킬 수 있는 몇 가지 작업이 있습니다.

1. 이 PR C# 에서 생성자에 대 한 [PR](https://github.com/xamarin/java.interop/pull/170)`throws Throwable` 고정 되어 있습니다.
1. Xamarin Android 지원 인터페이스에서 Java 생성기를 만듭니다.
    - 이렇게 하면 `AndroidJavaSource`의 빌드 작업을 사용 하 여 Java 소스 파일을 추가 하지 않아도 됩니다.
1. Xamarin.ios에서 가상 클래스에 대 한 `Invoker`를 로드 하는 방법을 만듭니다.
    - 이렇게 하면 `virtual` 예제 `abstract`에 클래스를 표시 하지 않아도 됩니다.
1. 자동으로 .NET 포함에 대 한 `Invoker` 클래스 생성
    - 이는 복잡 하지만 심지어. Xamarin.ios는 Java 바인딩 프로젝트에 대해 이미 이와 유사한 작업을 수행 하 고 있습니다.

여기에서는 많은 작업을 수행 해야 하지만 .NET 포함의 이러한 향상 된 기능을 사용할 수 있습니다.

## <a name="further-reading"></a>추가 참고 자료

- [Android 시작](~/tools/dotnet-embedding/get-started/java/android.md)
- [예비 Android 연구](~/tools/dotnet-embedding/android/index.md)
- [.NET 포함 제한 사항](~/tools/dotnet-embedding/limitations.md)
- [오류 코드 및 설명](~/tools/dotnet-embedding/errors.md)
