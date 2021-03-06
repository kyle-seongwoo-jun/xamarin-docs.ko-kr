---
title: Google Play 서비스 구성 요소 및 NuGet 통합
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 5D962EB4-2CB3-4B7D-9D77-889DEACDAE02
author: davidortinau
ms.author: daortin
ms.date: 05/08/2018
ms.openlocfilehash: 0b2fd92eb9157b561708eafe10d341381fa21543
ms.sourcegitcommit: 4691b48f14b166afcec69d1350b769ff5bf8c9f6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2020
ms.locfileid: "75728202"
---
# <a name="unifying-google-play-services-components-and-nuget"></a>Google Play 서비스 구성 요소 및 NuGet 통합

## <a name="history"></a>기록

여러 Google Play 서비스 구성 요소와 NuGet 패키지를 사용 하는 데 사용 됩니다.

- Google Play 서비스 (안)
- Google Play 서비스 (Gingerbread)
- Google Play 서비스 (ICS)
- Google Play 서비스 (JellyBean)
- Google Play 서비스 (KitKat)

Google은 실제로 Google Play 서비스에 대해 두 개의 jar 파일만 제공 합니다.

- `google-play-services-froyo.jar`
- `google-play-services.jar`

이러한 불일치는 지정 된 앱에 사용 되는 최대 리소스 API 수준을 `aapt.exe` 올바르게 알 수 없기 때문에 존재 하지 않습니다. 즉, Gingerbread와 같은 더 낮은 API 수준에서 Google Play 서비스 (KitKat) 바인딩을 사용 하려고 시도 하는 경우 컴파일 오류를 수신 했습니다.

## <a name="unifying-google-play-services"></a>Google Play 서비스 통합

최신 버전의 Xamarin.ios에서 이제는 사용할 수 있는 최대 리소스 버전을 `aapt.exe` 설명 하므로이 문제가 사라집니다.

즉, Gingerbread/ICS/JellyBean/KitKat에 대 한 별도의 패키지를 포함 하는 실제 이유가 없습니다. 그러나 다른 jar 파일 이기 때문에에 대 한 별도의 바인딩이 필요 합니다.

개발자의 작업을 용이 하 게 하기 위해 이제 구성 요소와 NuGet 패키지를 두 가지로 통합 했습니다.

- Google Play 서비스 (안) (`google-play-services-froyo.jar`바인딩)
- Google Play 서비스 (`google-play-services.jar`바인딩)

### <a name="which-one-should-be-used"></a>어떤 것을 사용 해야 하나요?

거의 모든 경우에 Google Play 서비스를 사용 해야 합니다. (안 됨) 패키지를 사용 하는 유일한 이유는 대기를 대상으로 하는 경우입니다. 이 별도의 jar 파일이 Google에서 존재 하는 유일한 이유는이는 적은 수의 장치에서의 장치에 대 한 지원 중지를 결정 하는 것 이므로,이 jar 파일은 고정 되 고 지원 되지 않는 Google Play 서비스 스냅숏입니다.

### <a name="note-about-gingerbread"></a>Gingerbread에 대 한 참고 사항

Gingerbread에는 기본적으로 단편이 지원 되지 않으므로이로 인해 바인딩의 일부 클래스는 Gingerbread 장치의 런타임에 응용 프로그램에서 사용할 수 없습니다. `MapFragment`와 같은 클래스는 Gingerbread에서 작동 하지 않으며 `SupportMapFragment`대신 지원 변형을 사용 해야 합니다. 개발자가 사용할 수 있는 것을 알 수 있습니다. 이러한 비 호환성은 Google에서 Google Play 서비스 설명서에 나와 있습니다.

### <a name="what-happens-to-the-old-componentsnugets"></a>이전 구성 요소/s s i d의 경우 어떻게 되나요?

더 이상 필요 하지 않으므로 다음 구성 요소/Nuget를 사용 하지 않도록 설정 하거나 나열 하지 않습니다.

- Google Play 서비스 (Gingerbread)
- Google Play 서비스 (JellyBean)
- Google Play 서비스 (KitKat)

기존 _Google Play 서비스 (ICS)_ 구성 요소/s s o n t e r s/s e r v e r s i o n의 이름이 _Google Play 서비스_ 로 바뀌고 앞으로 최신 사용 하지 않거나 나열 되지 않은 패키지 중 하나를 참조 하는 모든 프로젝트는이를 사용 하도록 업데이트 되어야 합니다.

사용 하지 않도록 설정 된 구성 요소는 여전히 존재 하며, 중단 되지 않도록 하기 위해에서 여전히 참조 되는 프로젝트에 대해 복원 가능한 되어야 합니다. 마찬가지로 나열 되지 않은 NuGet 패키지도 존재 하 고 복원할 수 있습니다. 앞으로는 업데이트 되지 않습니다.
