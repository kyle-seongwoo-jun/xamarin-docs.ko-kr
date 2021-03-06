---
title: 컨테이너화된 마이크로 서비스
description: 이 장에서는 마이크로 서비스 및 컨테이너를 사용 하 여 민첩 하 고 확장 가능 하며 안정적인 최신 클라우드 응용 프로그램을 빌드하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: 5872ad92-04e0-4f1a-9691-79d5602f5683
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/07/2017
ms.openlocfilehash: dc71da512519cdd7fcc56df1ff987ffbc1354663
ms.sourcegitcommit: eca3b01098dba004d367292c8b0d74b58c4e1206
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79306334"
---
# <a name="containerized-microservices"></a>컨테이너화된 마이크로 서비스

클라이언트-서버 응용 프로그램을 개발 하면 각 계층에서 특정 기술을 사용 하는 계층화 된 응용 프로그램을 구축 하는 데 집중 했습니다. 이러한 응용 프로그램을 종종 *모놀리식* 응용 프로그램 이라고 하며, 최대 부하를 위해 미리 확장 된 하드웨어로 패키지 됩니다. 이 개발 방법의 주요 단점은 각 계층 내의 구성 요소 간 긴밀 한 결합, 개별 구성 요소를 쉽게 확장할 수 없고 테스트 비용입니다. 간단한 업데이트는 계층의 나머지 부분에 예기치 않은 영향을 미칠 수 있으므로 응용 프로그램 구성 요소를 변경 하려면 전체 계층을 retested 하 고 다시 배포 해야 합니다.

특히 클라우드의 연령와 관련 하 여 개별 구성 요소를 쉽게 확장할 수 없습니다. 모놀리식 응용 프로그램은 도메인별 기능을 포함 하며 일반적으로 프런트 엔드, 비즈니스 논리 및 데이터 저장소와 같은 기능 계층으로 구분 됩니다. 모놀리식 응용 프로그램은 그림 8-1에 나와 있는 것 처럼 전체 응용 프로그램을 여러 컴퓨터에 복제 하 여 크기를 조정 합니다.

![](containerized-microservices-images/monolithicapp.png "Monolithic application scaling approach")

**그림 8-1**: 모놀리식 응용 프로그램 크기 조정 방법

## <a name="microservices"></a>마이크로 서비스

마이크로 서비스는 최신 클라우드 응용 프로그램의 민첩성, 확장성 및 안정성 요구 사항에 적합 한 방법인 응용 프로그램 개발 및 배포에 대 한 다양 한 접근 방식을 제공 합니다. 마이크로 서비스 응용 프로그램은 응용 프로그램의 전체 기능을 제공 하기 위해 함께 작동 하는 독립적인 구성 요소로 분해 됩니다. 마이크로 서비스 라는 용어는 각 마이크로 서비스 단일 함수를 구현 하도록 응용 프로그램을 독립적인 문제를 반영 하기에 충분 한 작은 서비스로 구성 해야 함을 강조 합니다. 또한 각 마이크로 서비스는 잘 정의 된 계약을 사용 하 여 다른 마이크로 서비스에서 데이터와 통신 하 고 데이터를 공유할 수 있도록 합니다. 마이크로 서비스의 일반적인 예로는 쇼핑 카트, 재고 처리, 구매 하위 시스템, 지불 처리 등이 있습니다.

마이크로 서비스는 함께 확장 되는 자이언트 모놀리식 응용 프로그램에 비해 독립적으로 확장 될 수 있습니다. 즉, 요청을 지 원하는 데 더 많은 처리 능력 또는 네트워크 대역폭이 필요한 특정 기능 영역은 응용 프로그램의 다른 영역을 불필요 하 게 확장 하는 대신 크기를 조정할 수 있습니다. 그림 8-2에서는 마이크로 서비스를 독립적으로 배포 및 확장 하 여 여러 컴퓨터에서 서비스 인스턴스를 만들어이 접근 방식을 보여 줍니다.

![](containerized-microservices-images/microservicesapp.png "Microservices application scaling approach")

**그림 8-2**: 마이크로 서비스 응용 프로그램 크기 조정 방법

마이크로 서비스 확장은 거의 즉시 수행할 수 있으므로 응용 프로그램을 변경 하는 로드에 대응할 수 있습니다. 예를 들어 응용 프로그램의 웹 연결 기능에서 단일 마이크로 서비스는 추가 들어오는 트래픽을 처리 하기 위해 규모를 확장 해야 하는 응용 프로그램의 유일한 마이크로 서비스 수 있습니다.

응용 프로그램 확장성을 위한 클래식 모델은 영구 데이터를 저장 하기 위해 공유 외부 데이터 저장소를 사용 하 여 부하 분산 된 상태 비저장 계층을 보유 하는 것입니다. 상태 저장 마이크로 서비스는 자체의 영구 데이터를 관리 하며, 일반적으로 이러한 데이터를 저장 된 서버에 로컬로 저장 하 여 네트워크 액세스와 서비스 간 작업의 복잡성을 방지 합니다. 이렇게 하면 데이터를 가장 빨리 처리할 수 있으며 시스템을 캐시할 필요가 없습니다. 또한 확장 가능한 상태 저장 마이크로 서비스는 일반적으로 단일 서버에서 지원할 수 있는 데이터 크기 및 전송 처리량을 관리 하기 위해 인스턴스 간에 데이터를 분할 합니다.

마이크로 서비스는 독립 업데이트도 지원 합니다. 마이크로 서비스 간의 이러한 느슨한 결합은 빠르고 안정적인 응용 프로그램 진화를 제공 합니다. 독립적인 분산 특성은 특정 시간에 단일 마이크로 서비스 인스턴스의 하위 집합만 업데이트 하는 롤링 업데이트를 지원 합니다. 따라서 문제가 감지 되 면 모든 인스턴스를 잘못 된 코드나 구성으로 업데이트 하기 전에 버그가 있는 업데이트를 롤백할 수 있습니다. 마찬가지로, 마이크로 서비스는 일반적으로 스키마 버전 관리를 사용 하므로, 어떤 마이크로 서비스 인스턴스가 통신 하 고 있는지에 관계 없이 업데이트가 적용 되는 경우 클라이언트가 일관 된 버전을 볼 수 있습니다.

따라서 마이크로 서비스 응용 프로그램은 모놀리식 응용 프로그램에 비해 많은 이점을 제공 합니다.

- 각 마이크로 서비스는 상대적으로 작고 관리 하기 쉬우며 진화 하 고 있습니다.
- 각 마이크로 서비스는 다른 서비스와 독립적으로 개발 및 배포할 수 있습니다.
- 각 마이크로 서비스은 독립적으로 확장 될 수 있습니다. 예를 들어 카탈로그 서비스 또는 시장 바구니 서비스는 주문 서비스 보다 확장 해야 할 수 있습니다. 따라서 결과 인프라는 규모 확장 시 더 효율적으로 리소스를 사용 합니다.
- 각 마이크로 서비스는 문제를 격리 합니다. 예를 들어 서비스에 문제가 있는 경우 해당 서비스에만 영향을 줍니다. 다른 서비스는 계속 해 서 요청을 처리할 수 있습니다.
- 각 마이크로 서비스는 최신 기술을 사용할 수 있습니다. 마이크로 서비스는 자치이 고 side-by-side로 실행 되기 때문에 모놀리식 응용 프로그램에서 사용할 수 있는 이전 프레임 워크를 사용 하는 대신 최신 기술 및 프레임 워크를 사용할 수 있습니다.

그러나 마이크로 서비스 기반 솔루션은 잠재적인 단점이 있습니다.

- 응용 프로그램을 마이크로 서비스로 분할 하는 방법을 선택 하는 것은 각 마이크로 서비스 데이터 원본에 대 한 책임을 포함 하 여 완벽 하 게 완전 하 게 자율적으로 수행 해야 하기 때문에 어려울 수 있습니다.
- 개발자는 응용 프로그램에 복잡성 및 대기 시간을 추가 하는 서비스 간 통신을 구현 해야 합니다.
- 여러 마이크로 서비스 간의 원자성 트랜잭션은 일반적으로 불가능 합니다. 따라서 비즈니스 요구 사항은 마이크로 서비스 간의 최종 일관성을 수용 해야 합니다.
- 프로덕션 환경에서는 많은 독립 서비스의 시스템 손상을 배포 하 고 관리 하는 작업 복잡성이 있습니다.
- 클라이언트-마이크로 서비스 간 직접 통신을 통해 마이크로 서비스의 계약을 리팩터링 하기가 어려울 수 있습니다. 예를 들어 시스템을 서비스로 분할 하는 방법을 시간이 지남에 따라 변경 해야 할 수도 있습니다. 단일 서비스를 두 개 이상의 서비스로 분할 하 고 두 서비스를 병합할 수 있습니다. 클라이언트가 마이크로 서비스와 직접 통신 하는 경우이 리팩터링 작업은 클라이언트 앱과의 호환성을 손상 시킬 수 있습니다.

## <a name="containerization"></a>컨테이너화

컨테이너 화는 응용 프로그램과 해당 버전의 종속성 및 배포 매니페스트 파일로 추상화 되는 환경 구성을 포함 하는 소프트웨어 개발에 대 한 방법으로, 컨테이너 이미지로 함께 패키지 되 고 하나의 단위로 테스트 됩니다. 호스트 운영 체제에 배포 됩니다.

컨테이너는 다른 컨테이너 또는 호스트의 리소스를 건드리지 않고도 응용 프로그램을 실행할 수 있는 격리 된 리소스 제어 및 휴대용 운영 환경입니다. 따라서 컨테이너는 새로 설치 된 물리적 컴퓨터 또는 가상 컴퓨터 처럼 보이고 작동 합니다.

그림 8-3에 나와 있는 것 처럼 컨테이너와 가상 컴퓨터 간에는 많은 유사점이 있습니다.

![](containerized-microservices-images/containersvsvirtualmachines.png "Microservices application scaling approach")

**그림 8-3**: 가상 컴퓨터 및 컨테이너 비교

컨테이너는 운영 체제를 실행 하 고, 파일 시스템을 포함 하며, 네트워크를 통해 실제 또는 가상 머신과 같이 액세스할 수 있습니다. 그러나 컨테이너에서 사용 하는 기술 및 개념은 가상 머신과 매우 다릅니다. 가상 컴퓨터에는 응용 프로그램, 필요한 종속성 및 전체 게스트 운영 체제가 포함 됩니다. 컨테이너에는 응용 프로그램 및 해당 종속성이 포함 되지만, 운영 체제를 호스트 운영 체제에서 격리 된 프로세스로 실행 되는 다른 컨테이너와 공유 합니다 .이 컨테이너는 컨테이너 당 특수 한 가상 컴퓨터 내에서 실행 되는 Hyper-v 컨테이너와는 별도로 실행 됩니다. 따라서 컨테이너는 리소스를 공유 하 고 일반적으로 가상 컴퓨터 보다 리소스가 덜 필요 합니다.

컨테이너 지향 개발 및 배포 방법의 장점은 일관 되지 않은 환경에서 발생 하는 문제를 대부분 제거 하 고 발생 하는 문제를 제거 하는 것입니다. 또한 컨테이너는 필요에 따라 새 컨테이너를 등록 하 여 빠른 응용 프로그램 확장 기능을 허용 합니다.

컨테이너를 만들고 작업 하는 경우 주요 개념은 다음과 같습니다.

- 컨테이너 호스트: 컨테이너를 호스트 하도록 구성 된 물리적 또는 가상 컴퓨터입니다. 컨테이너 호스트는 하나 이상의 컨테이너를 실행 합니다.
- 컨테이너 이미지: 이미지는 서로 위에 누적 된 계층화 된 파일 시스템의 합집합으로 구성 되며 컨테이너의 기반이 됩니다. 이미지는 상태가 없으며 다른 환경에 배포 될 때 변경 되지 않습니다.
- 컨테이너: 컨테이너는 이미지의 런타임 인스턴스입니다.
- 컨테이너 OS 이미지: 컨테이너가 이미지에서 배포됩니다. 컨테이너 운영 체제 이미지는 컨테이너를 구성 하는 잠재적으로 많은 이미지 계층에서 첫 번째 계층입니다. 컨테이너 운영 체제는 변경할 수 없으며 수정할 수 없습니다.
- 컨테이너 리포지토리: 컨테이너 이미지가 만들어질 때마다 이미지와 해당 종속성이 로컬 리포지토리에 저장 됩니다. 이러한 이미지는 컨테이너 호스트에서 여러 번 다시 사용할 수 있습니다. 컨테이너 이미지는 다른 컨테이너 호스트에서 사용할 수 있도록 [Docker 허브](https://hub.docker.com/)와 같은 공용 또는 개인 레지스트리에 저장할 수도 있습니다.

마이크로 서비스 기반 응용 프로그램을 구현할 때 기업이 점점 더 많은 컨테이너를 채택 하 고 있으며 Docker가 대부분의 소프트웨어 플랫폼과 클라우드 공급 업체에서 채택 하는 표준 컨테이너 구현이 되었습니다.

EShopOnContainers reference 응용 프로그램은 그림 8-4에 나와 있는 것 처럼 Docker를 사용 하 여 4 개의 컨테이너 화 된 백 엔드 마이크로 서비스를 호스팅합니다.

![](containerized-microservices-images/microservicesarchitecture.png "eShopOnContainers reference application back-end microservices")

**그림 8-4**: eShopOnContainers reference 응용 프로그램 백 엔드 마이크로 서비스

참조 응용 프로그램의 백 엔드 서비스 아키텍처는 공동 마이크로 서비스 및 컨테이너 형식의 여러 자치 하위 시스템으로 분해 됩니다. 각 마이크로 서비스는 id 서비스, 카탈로그 서비스, 주문 서비스 및 바구니 서비스의 단일 기능 영역을 제공 합니다.

각 마이크로 서비스에는 자체 데이터베이스가 있으므로 다른 마이크로 서비스에서 완전히 분리 될 수 있습니다. 필요한 경우에는 응용 프로그램 수준 이벤트를 사용 하 여 서로 다른 마이크로 서비스의 데이터베이스 간 일관성을 달성 합니다. 자세한 내용은 [마이크로 서비스 간 통신](#communication_between_microservices)을 참조 하세요.

참조 응용 프로그램에 대 한 자세한 내용은 [.Net 마이크로 서비스: 컨테이너 화 된 .Net 응용 프로그램 아키텍처](https://aka.ms/microservicesebook)를 참조 하세요.

<a name="communication_between_client_and_microservices" />

## <a name="communication-between-client-and-microservices"></a>클라이언트와 마이크로 서비스 간의 통신

EShopOnContainers 모바일 앱은 그림 8-5에 표시 된 *직접 클라이언트-마이크로 서비스* 통신을 사용 하 여 컨테이너 화 된 백 엔드 마이크로 서비스와 통신 합니다.

![](containerized-microservices-images/directclienttomicroservicecommunication.png "Microservices application scaling approach")

**그림 8-5**: 클라이언트-마이크로 서비스 간 직접 통신

클라이언트-마이크로 서비스 간 직접 통신을 사용 하면 모바일 앱은 각 마이크로 서비스에 대 한 요청을 각 마이크로 서비스에 대해 다른 TCP 포트를 사용 하 여 공용 끝점을 통해 직접 요청 합니다. 프로덕션에서 끝점은 일반적으로 사용 가능한 인스턴스 간에 요청을 분산 하는 마이크로 서비스의 부하 분산 장치에 매핑됩니다.

> [!TIP]
> API 게이트웨이 통신을 사용 하는 것이 좋습니다. 클라이언트-마이크로 서비스 간 직접 통신은 크고 복잡 한 마이크로 서비스 기반 응용 프로그램을 빌드할 때 단점이 있을 수 있지만 작은 응용 프로그램에는 적합 하지 않습니다. 수십 개의 마이크로 서비스를 사용 하 여 초대형 마이크로 서비스 기반 응용 프로그램을 디자인 하는 경우 API 게이트웨이 통신을 사용 하는 것이 좋습니다. 자세한 내용은 [.Net 마이크로 서비스: 컨테이너 화 된 .Net 응용 프로그램 아키텍처](https://aka.ms/microservicesebook)를 참조 하세요.

<a name="communication_between_microservices" />

## <a name="communication-between-microservices"></a>마이크로 서비스 간 통신

마이크로 서비스 기반 응용 프로그램은 여러 컴퓨터에서 실행 될 수 있는 분산 시스템입니다. 각 서비스 인스턴스는 일반적으로 프로세스입니다. 따라서 서비스는 각 서비스의 특성에 따라 HTTP, TCP, 고급 메시지 큐 프로토콜 (AMQP) 또는 이진 프로토콜과 같은 프로세스 간 통신 프로토콜을 사용 하 여 상호 작용 해야 합니다.

마이크로 서비스 간 통신에 대 한 두 가지 일반적인 방법은 데이터를 쿼리할 때 HTTP 기반 REST 통신을 사용 하 고 여러 마이크로 서비스에서 업데이트를 통신할 때 간단한 비동기 메시징을 사용 하는 것입니다.

비동기 메시징 기반 통신은 여러 마이크로 서비스에서 변경 내용을 전파 하는 경우에 중요 합니다. 이 접근 방식을 사용 하는 경우 마이크로 서비스는 비즈니스 엔터티를 업데이트할 때 처럼 주목할 만한 문제가 발생 하면 이벤트를 게시 합니다. 다른 마이크로 서비스는 이러한 이벤트를 구독 합니다. 그런 다음 마이크로 서비스가 이벤트를 받으면 자체 비즈니스 엔터티를 업데이트 하 여 더 많은 이벤트를 게시 하 게 될 수 있습니다. 이 게시-구독 기능은 일반적으로 이벤트 버스를 사용 하 여 구현 됩니다.

그림 8-6에 표시 된 것 처럼 이벤트 버스는 구성 요소가 서로를 명시적으로 인식 하지 않고도 마이크로 서비스 간의 게시-구독 통신을 허용 합니다.

![](containerized-microservices-images/eventbus.png "Publish-subscribe with an event bus")

**그림 8-6:** 게시-이벤트 버스를 사용 하 여 구독

응용 프로그램 관점에서 이벤트 버스는 단순히 인터페이스를 통해 노출 되는 게시-구독 채널입니다. 그러나 이벤트 버스가 구현 되는 방식은 달라질 수 있습니다. 예를 들어 이벤트 버스 구현에서는 RabbitMQ, Azure Service Bus 또는 NServiceBus 및 MassTransit와 같은 다른 서비스 버스를 사용할 수 있습니다. 그림 8-7에서는 eShopOnContainers reference 응용 프로그램에서 이벤트 버스를 사용 하는 방법을 보여 줍니다.

![](containerized-microservices-images/microservicesarchitecturewitheventbus.png "Asynchronous event-driven communication in the reference application")

**그림 8-7:** 참조 응용 프로그램의 비동기 이벤트 기반 통신

RabbitMQ를 사용 하 여 구현 된 eShopOnContainers 이벤트 버스는 일대다 비동기 게시-구독 기능을 제공 합니다. 즉, 이벤트를 게시 한 후 동일한 이벤트를 수신 하는 여러 구독자가 있을 수 있습니다. 그림 8-9에서는이 관계를 보여 줍니다.

![](containerized-microservices-images/eventdrivencommunication.png "One-to-many communication")

**그림 8-9**: 일대다 통신

이 일대다 통신 방법은 이벤트를 사용 하 여 여러 서비스에 걸쳐 있는 비즈니스 트랜잭션을 구현 하 여 서비스 간의 최종 일관성을 보장 합니다. 궁극적으로 일관 된 트랜잭션은 일련의 분산 단계로 구성 됩니다. 따라서 사용자 프로필 마이크로 서비스가 UpdateUser 명령을 받으면 해당 데이터베이스에서 사용자의 세부 정보를 업데이트 하 고 UserUpdated 이벤트를 이벤트 버스에 게시 합니다. 바구니 마이크로 서비스 및 주문 마이크로 서비스 모두이 이벤트를 수신 하 고 해당 데이터베이스에서 해당 구매자 정보를 업데이트 하는 것을 구독 합니다.

> [!NOTE]
> RabbitMQ를 사용 하 여 구현 된 eShopOnContainers 이벤트 버스는 개념 증명 으로만 사용 하기 위한 것입니다. 프로덕션 시스템의 경우 대체 이벤트 버스 구현을 고려해 야 합니다.

이벤트 버스 구현에 대 한 자세한 내용은 [.Net 마이크로 서비스: 컨테이너 화 된 .Net 응용 프로그램 아키텍처](https://aka.ms/microservicesebook)를 참조 하세요.

## <a name="summary"></a>요약

마이크로 서비스는 최신 클라우드 응용 프로그램의 민첩성, 확장성 및 안정성 요구 사항에 적합 한 응용 프로그램 개발 및 배포에 대 한 접근 방식을 제공 합니다. 마이크로 서비스의 주요 이점 중 하나는 독립적으로 확장 될 수 있다는 것입니다. 즉, 필요에 따라의 영역을 불필요 하 게 확장 하지 않고도 요구를 지원 하기 위해 더 많은 처리 능력과 네트워크 대역폭이 필요한 특정 기능 영역을 확장할 수 있습니다. 요구가 증가 하지 않은 응용 프로그램입니다.

컨테이너는 다른 컨테이너 또는 호스트의 리소스를 건드리지 않고도 응용 프로그램을 실행할 수 있는 격리 된 리소스 제어 및 휴대용 운영 환경입니다. 마이크로 서비스 기반 응용 프로그램을 구현할 때 기업이 점점 더 많은 컨테이너를 채택 하 고 있으며 Docker가 대부분의 소프트웨어 플랫폼과 클라우드 공급 업체에서 채택 하는 표준 컨테이너 구현이 되었습니다.

## <a name="related-links"></a>관련 링크

- [다운로드 전자책 (2Mb PDF)](https://aka.ms/xamarinpatternsebook)
- [eShopOnContainers (GitHub) (샘플)](https://github.com/dotnet-architecture/eShopOnContainers)
