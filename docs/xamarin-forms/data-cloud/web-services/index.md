---
title: Xamarin.Forms 및 웹 서비스
description: 이 가이드를 제공 하려면 다른 웹 서비스와 통신 하는 방법에 설명 만들기, 읽기, 업데이트 및 삭제 (CRUD) Xamarin.Forms 응용 프로그램에는 기능입니다. 다룹니다 ASMX 서비스, WCF 서비스, REST 서비스와 통신 합니다.
ms.prod: xamarin
ms.assetid: 8B360BDA-E4E3-4A3F-9004-0E35362F49F
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 06/27/2019
ms.openlocfilehash: 1cf2714191528c5619b4f877bcb43e80464c44d1
ms.sourcegitcommit: c1d85b2c62ad84c22bdee37874ad30128581bca6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/08/2019
ms.locfileid: "67659010"
---
# <a name="xamarinforms-and-web-services"></a>Xamarin.Forms 및 웹 서비스

## <a name="introductionintroductionmd"></a>[소개](introduction.md)

이 문서에서는 Xamarin.Forms 샘플 응용 프로그램이 다른 웹 서비스와 통신 하는 방법을 보여 주는 연습을 제공 합니다. 다룹니다 응용 프로그램 페이지, 데이터 모델을 분석 하 고 웹 서비스 작업을 호출 합니다.

## <a name="consume-an-aspnet-web-service-asmxxamarin-formsdata-cloudweb-servicesasmxmd"></a>[ASP.NET 웹 서비스 (ASMX) 사용](~/xamarin-forms/data-cloud/web-services/asmx.md)

ASP.NET 웹 서비스 (ASMX) 액세스 프로토콜 SOAP (Simple Object)를 사용 하 여 HTTP를 통해 메시지를 전송 하는 웹 서비스를 구축 하는 기능을 제공 합니다. SOAP는 빌드하고 웹 서비스에 액세스 하기 위한 플랫폼 독립적인 및 언어 독립적 프로토콜입니다. ASMX 서비스의 소비자는 플랫폼, 개체 모델 또는 서비스를 구현 하는 데 사용 되는 프로그래밍 언어에 대 한 알 필요가 없습니다. 만 SOAP 메시지를 수신 하는 방법을 이해 해야 합니다. 이 문서에서는 Xamarin.Forms 응용 프로그램에서 ASMX 웹 서비스를 사용 하는 방법에 설명 합니다.

## <a name="consume-a-windows-communication-foundation-wcf-web-servicexamarin-formsdata-cloudweb-serviceswcfmd"></a>[Windows Communication Foundation (WCF) 웹 서비스를 사용 합니다.](~/xamarin-forms/data-cloud/web-services/wcf.md)

WCF는 서비스 지향 응용 프로그램을 빌드하기 위한 Microsoft의 통합 된 프레임 워크입니다. 개발자가 보안, 신뢰할 수 있는, 트랜잭션 및 상호 운용 가능한 분산된 응용 프로그램을 빌드할 수 있습니다. ASP.NET 웹 서비스 (ASMX)와 WCF 사이의 차이가 이지만 WCF ASMX 제공 하는 동일한 기능을 지원 하는지 이해 해야-HTTP 통한 SOAP 메시지입니다. 이 문서에서는 Xamarin.Forms 응용 프로그램에서 WCF SOAP 서비스를 사용 하는 방법에 설명 합니다.

## <a name="consume-a-restful-web-servicexamarin-formsdata-cloudweb-servicesrestmd"></a>[RESTful 웹 서비스 사용](~/xamarin-forms/data-cloud/web-services/rest.md)

REST representational State Transfer ()는 웹 서비스 구축을 위한 아키텍처 스타일입니다. REST 요청 웹 페이지를 검색 하 고 서버에 데이터를 보내도록 웹 브라우저를 사용 하는 동일한 HTTP 동사를 사용 하 여 HTTP를 통해 수행 됩니다. 이 문서에서는 Xamarin.Forms 응용 프로그램에서 RESTful 웹 서비스를 사용 하는 방법에 설명 합니다.
