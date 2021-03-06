---
title: 목적-C 지원
description: 이 문서에서는 .NET 포함의 목적-C 지원에 대 한 설명을 제공 합니다. 자동 참조 계산, NSString, 프로토콜, Nsstring 프로토콜, 예외 등에 대해 설명 합니다.
ms.prod: xamarin
ms.assetid: 3367A4A4-EC88-4B75-96D0-51B1FCBCE614
author: davidortinau
ms.author: daortin
ms.date: 11/14/2017
ms.openlocfilehash: e72f950dc6fcf12e70714e0fbb996ad5ea432548
ms.sourcegitcommit: 2fbe4932a319af4ebc829f65eb1fb1816ba305d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73029702"
---
# <a name="objective-c-support"></a>목적-C 지원

## <a name="specific-features"></a>특정 기능

목적-C의 세대에는 주목할 만한 몇 가지 특수 기능이 있습니다.

### <a name="automatic-reference-counting"></a>자동 참조 계산

생성 된 바인딩을 호출 하려면 자동 참조 계산 (ARC)을 사용 **해야** 합니다. .NET 포함 기반 라이브러리를 사용 하는 프로젝트는 `-fobjc-arc`를 사용 하 여 컴파일해야 합니다.

### <a name="nsstring-support"></a>NSString 지원

`System.String` 형식을 노출 하는 Api는 `NSString`으로 변환 됩니다. 이렇게 하면 `char*`를 처리할 때 보다 메모리 관리가 쉬워집니다.

### <a name="protocols-support"></a>프로토콜 지원

관리 되는 인터페이스는 모든 멤버가 `@required`되는 객관적인 C 프로토콜로 변환 됩니다.

### <a name="nsobject-protocol-support"></a>NSObject 프로토콜 지원

기본적으로 .NET 및 목표 C 런타임의 기본 해시와 같음은 유사한 의미 체계를 공유 하므로 교환 가능한 것으로 간주 됩니다.

관리 되는 형식이 `Equals(Object)` 또는 `GetHashCode`를 재정의 하는 경우 일반적으로 기본 (.NET) 동작이 충분 하지 않음을 의미 합니다. 이는 기본 목표 C 동작으로 충분 하지 않을 가능성이 있음을 의미 합니다.

이 경우 생성기는 [`NSObject` 프로토콜](https://developer.apple.com/reference/objectivec/1418956-nsobject?language=objc)에 정의 된 [`isEqual:`](https://developer.apple.com/reference/objectivec/1418956-nsobject/1418795-isequal?language=objc) 메서드 및 [`hash`](https://developer.apple.com/reference/objectivec/1418956-nsobject/1418859-hash?language=objc) 속성을 재정의 합니다. 이렇게 하면 사용자 지정 관리 되는 구현을 목적-C 코드에서 투명 하 게 사용할 수 있습니다.

### <a name="exceptions-support"></a>예외 지원

`--nativeexception`를 `objcgen`에 인수로 전달 하면 관리 되는 예외를 catch 하 고 처리할 수 있는 목표-C 예외로 변환 합니다. 

### <a name="comparison"></a>비교

`IComparable` (또는 제네릭 버전 `IComparable<T>`)를 구현 하는 관리 되는 형식은 `NSComparisonResult`을 반환 하 고 `nil` 인수를 허용 하는 객관적인 방법으로 사용할 수 있는 메서드를 생성 합니다. 이렇게 하면 생성 된 API를 목표 C 개발자에 게 더 친숙 하 게 만들 수 있습니다. 예를 들면,

```objc
- (NSComparisonResult)compare:(XAMComparableType * _Nullable)other;
```

### <a name="categories"></a>범주

관리 되는 확장 메서드는 범주로 변환 됩니다. 예를 들어 `Collection`의 다음 확장 메서드는 다음과 같습니다.

```csharp
public static class SomeExtensions {
    public static int CountNonNull (this Collection collection) { ... }
    public static int CountNull (this Collection collection) { ... }
}
```

다음과 같은 목표-C 범주를 만듭니다.

```objc
@interface Collection (SomeExtensions)

- (int)countNonNull;
- (int)countNull;

@end
```

단일 관리 되는 형식이 여러 형식을 확장 하면 여러 개의 목표-C 범주가 생성 됩니다.

### <a name="subscripting"></a>첨자

관리 되는 인덱싱된 속성은 첨자 개체로 변환 됩니다. 예를 들면,

```csharp
public bool this[int index] {
    get { return c[index]; }
    set { c[index] = value; }
}
```

는 다음과 유사한 목표 C를 만듭니다.

```objc
- (id)objectAtIndexedSubscript:(int)idx;
- (void)setObject:(id)obj atIndexedSubscript:(int)idx;
```

목표-C 첨자 구문을 통해 사용할 수 있습니다.

```objc
if ([intCollection [0] isEqual:@42])
    intCollection[0] = @13;
```

인덱서의 유형에 따라 적절 한 경우에는 인덱스 또는 키가 지정 된 첨자 생성 됩니다.

이 [문서](https://nshipster.com/object-subscripting/) 는 첨자에 대 한 유용한 소개입니다.

## <a name="main-differences-with-net"></a>.NET과의 주요 차이점

### <a name="constructors-vs-initializers"></a>생성자 및 이니셜라이저

목적-C에서는 사용할 수 없는 것으로 표시 된 경우 (`NS_UNAVAILABLE`) 상속 체인에서 부모 클래스의 모든 이니셜라이저 프로토타입을 호출할 수 있습니다.

에서는 C# 생성자가 상속 되지 않음을 의미 하는 클래스 내에서 생성자 멤버를 명시적으로 선언 해야 합니다.

목표-C에 대 한 C# API의 올바른 표현을 노출 하기 위해 부모 클래스의 자식 클래스에 없는 모든 이니셜라이저에`NS_UNAVAILABLE`추가 됩니다.

C# API:

```csharp
public class Unique {
    public Unique () : this (1)
    {
    }

    public Unique (int id)
    {
    }
}

public class SuperUnique : Unique {
    public SuperUnique () : base (911)
    {
    }
}
```

목표-C 노출 API:

```objc
@interface SuperUnique : Unique

- (instancetype)initWithId:(int)id NS_UNAVAILABLE;
- (instancetype)init;

@end
```

여기에서 `initWithId:`은 사용할 수 없는 것으로 표시 되었습니다.

### <a name="operator"></a>연산자

목적-C는 연산자 오버 로드를 처럼 C# 지원 하지 않으므로 연산자는 클래스 선택기로 변환 됩니다.

```csharp
public static AllOperators operator + (AllOperators c1, AllOperators c2)
{
    return new AllOperators (c1.Value + c2.Value);
}
```

다음으로 변경:

```objc
+ (instancetype)add:(Overloads_AllOperators *)anObjectC1 c2:(Overloads_AllOperators *)anObjectC2;
```

그러나 일부 .NET 언어는 연산자 오버 로드를 지원 하지 않으므로 연산자 오버 로드 외에도 ["친숙 한"](https://docs.microsoft.com/dotnet/standard/design-guidelines/operator-overloads) 명명 된 메서드도 포함 하는 것이 일반적입니다.

연산자 버전과 "친숙 한" 버전이 모두 있는 경우 동일한 목표-C 이름을 생성 하므로 친근 한 버전만 생성 됩니다.

```csharp
public static AllOperatorsWithFriendly operator + (AllOperatorsWithFriendly c1, AllOperatorsWithFriendly c2)
{
    return new AllOperatorsWithFriendly (c1.Value + c2.Value);
}

public static AllOperatorsWithFriendly Add (AllOperatorsWithFriendly c1, AllOperatorsWithFriendly c2)
{
    return new AllOperatorsWithFriendly (c1.Value + c2.Value);
}
```

다음과 같이 사용하십시오.

```objc
+ (instancetype)add:(Overloads_AllOperatorsWithFriendly *)anObjectC1 c2:(Overloads_AllOperatorsWithFriendly *)anObjectC2;
```

### <a name="equality-operator"></a>같음 연산자

일반 연산자에서 `==` C# 은 위에서 설명한 대로 일반 연산자로 처리 됩니다.

그러나 "친숙 한" Equals 연산자가 있는 경우에는 연산자 `==`와 연산자 `!=` 생성에서 건너뜁니다.

### <a name="datetime-vs-nsdate"></a>DateTime vs NSDate

[`NSDate`](https://developer.apple.com/reference/foundation/nsdate?language=objc) 설명서에서:

> `NSDate` 개체는 특정 calendrical 시스템 또는 표준 시간대에 관계 없이 단일 시점을 캡슐화 합니다. 날짜 개체는 변경할 수 없으며, 절대 참조 날짜 (00:00:00 1 월 1 2001 일 UTC)에 상대적인 고정 시간 간격을 나타냅니다.

`NSDate` 참조 날짜로 인해이와 `DateTime` 간의 모든 변환은 UTC로 수행 해야 합니다.

#### <a name="datetime-to-nsdate"></a>DateTime에서 NSDate

`DateTime`에서 `NSDate`로 변환할 때 `DateTime`의 `Kind` 속성은 다음과 같이 고려 됩니다.

|Kind|결과|
|---|---|
|`Utc`|제공 된 `DateTime` 개체를 있는 그대로 사용 하 여 변환이 수행 됩니다.|
|`Local`|제공 된 `DateTime` 개체에서 `ToUniversalTime()`를 호출한 결과는 변환에 사용 됩니다.|
|`Unspecified`|제공 된 `DateTime` 개체는 UTC로 간주 되므로 `Kind` `Utc`때와 동일한 동작이 발생 합니다.|

변환은 다음 수식을 사용 합니다.

```
TimeInterval = DateTimeObjectTicks - NSDateReferenceDateTicks / TicksPerSecond
```

이 수식에서 다음을 수행 합니다. 

- `NSDateReferenceDateTicks`는 2001 년 1 월 1 일 00:00:00 UTC의 `NSDate` 참조 날짜를 기반으로 계산 됩니다. 

    ```csharp
    new DateTime (year:2001, month:1, day:1, hour:0, minute:0, second:0, kind:DateTimeKind.Utc).Ticks;
    ```

- [`TicksPerSecond`](https://docs.microsoft.com/dotnet/api/system.timespan.tickspersecond) 은 [`TimeSpan`](https://docs.microsoft.com/dotnet/api/system.timespan) 에 정의 되어 있습니다.

`NSDate` 개체를 만들기 위해 `TimeInterval` `NSDate` [dateWithTimeIntervalSinceReferenceDate:](https://developer.apple.com/reference/foundation/nsdate/1591577-datewithtimeintervalsincereferen?language=objc) 선택기와 함께 사용 됩니다.

#### <a name="nsdate-to-datetime"></a>NSDate to DateTime

`NSDate`에서 `DateTime`로의 변환은 다음 수식을 사용 합니다.

```
DateTimeTicks = NSDateTimeIntervalSinceReferenceDate * TicksPerSecond + NSDateReferenceDateTicks
```

이 수식에서 다음을 수행 합니다. 

- `NSDateReferenceDateTicks`는 2001 년 1 월 1 일 00:00:00 UTC의 `NSDate` 참조 날짜를 기반으로 계산 됩니다. 

    ```csharp
    new DateTime (year:2001, month:1, day:1, hour:0, minute:0, second:0, kind:DateTimeKind.Utc).Ticks;
    ```

- [`TicksPerSecond`](https://docs.microsoft.com/dotnet/api/system.timespan.tickspersecond) 은 [`TimeSpan`](https://docs.microsoft.com/dotnet/api/system.timespan) 에 정의 되어 있습니다.

계산 `DateTimeTicks` 후 `DateTime`[생성자](https://docs.microsoft.com/dotnet/api/system.datetime.-ctor?#System_DateTime__ctor_System_Int64_System_DateTimeKind_)가 호출되어 `kind`가 `DateTimeKind.Utc`으로 설정됩니다.

> [!NOTE]
> `NSDate` `nil`수 있지만 `DateTime`은 .NET의 구조체로, 정의에 따라 `null`수 없습니다. `nil` `NSDate`지정 하면 `DateTime.MinValue`에 매핑되는 기본 `DateTime` 값으로 변환 됩니다.

`NSDate`는 `DateTime`보다 더 높은 최대값과 최소값을 지원 합니다. `NSDate`에서 `DateTime`로 변환하는 경우, 이러한 더 높거나 낮은 값이 각각 `DateTime`[int32.maxvalue](https://docs.microsoft.com/dotnet/api/system.datetime.maxvalue) 또는 [MinValue](https://docs.microsoft.com/dotnet/api/system.datetime.minvalue)로 변경 됩니다.
