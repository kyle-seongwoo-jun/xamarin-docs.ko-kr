---
title: 대체 레이아웃 보기
description: 이 항목에서는 리소스 한정자를 사용 하 여 레이아웃의 버전을 지정 하는 방법에 대해 설명 합니다. 예를 들어 장치가 가로 모드에 있을 때만 사용 되는 레이아웃 버전과 세로 모드에만 사용 되는 레이아웃 버전이 있을 수 있습니다.
ms.prod: xamarin
ms.assetid: 5EBF51FC-9048-F0CF-624A-D8782A91C1FD
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 07/25/2018
ms.openlocfilehash: 017d2d05c04dfaf2378ad1b0129eb4a75be2e777
ms.sourcegitcommit: 2fbe4932a319af4ebc829f65eb1fb1816ba305d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73019483"
---
# <a name="alternative-layout-views"></a>대체 레이아웃 뷰

_이 항목에서는 리소스 한정자를 사용 하 여 레이아웃을 버전으로 지정할 수 있는 방법에 대해 설명 합니다. 예를 들어 장치가 가로 모드에 있을 때만 사용 되는 레이아웃 버전을 만들고 세로 모드에만 사용 되는 레이아웃 버전을 만듭니다._

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

## <a name="creating-alternative-layouts"></a>대체 레이아웃 만들기

**장치**왼쪽에 있는 **대체 레이아웃 보기** 아이콘을 클릭 하면 프로젝트에서 사용할 수 있는 대체 레이아웃을 나열 하는 미리 보기 창이 열립니다. 대체 레이아웃이 없으면 **기본** 보기가 표시 됩니다. 

[![대체 레이아웃 뷰 창](alternative-layout-views-images/vs/01-alt-layout-view-pane-sml.png "대체 레이아웃 뷰 창")](alternative-layout-views-images/vs/01-alt-layout-view-pane.png#lightbox)

**새 버전**옆에 있는 녹색 더하기 기호를 클릭 하면 레이아웃 변형 **만들기** 대화 상자가 열리며,이 레이아웃 변형에 대 한 리소스 한정자를 선택할 수 있습니다. 

[![레이아웃 변형 만들기](alternative-layout-views-images/vs/02-create-layout-variation-sml.png "레이아웃 변형 만들기")](alternative-layout-views-images/vs/02-create-layout-variation.png#lightbox)

다음 예제에서 **화면 방향** 에 대 한 리소스 한정자는 **가로**로 설정 되 고 **화면 크기** 는 **크게**변경 됩니다. 이렇게 하면 새 레이아웃 버전이 생성 됩니다 **.**

[![대량 변형](alternative-layout-views-images/vs/03-large-land-sml.png "대량 변형")](alternative-layout-views-images/vs/03-large-land.png#lightbox)

왼쪽의 미리 보기 창에는 리소스 한정자 선택의 영향이 표시 됩니다. **추가** 를 클릭 하면 대체 레이아웃이 만들어지고 디자이너가 해당 레이아웃으로 전환 됩니다. **대체 레이아웃 뷰** 미리 보기 창에는 다음 스크린샷에 표시 된 대로 작은 오른쪽 포인터를 통해 디자이너로 로드 되는 레이아웃이 표시 됩니다. 

[![로드 된 레이아웃 표시기](alternative-layout-views-images/vs/04-new-layout-sml.png "로드 된 레이아웃 표시기")](alternative-layout-views-images/vs/04-new-layout.png#lightbox)

## <a name="editing-alternative-layouts"></a>대체 레이아웃 편집

다른 레이아웃을 만들 때 레이아웃의 모든 분기 버전에 적용 되는 단일 변경을 수행 하는 것이 좋습니다. 예를 들어 모든 레이아웃에서 단추 텍스트를 노란색으로 변경 하는 것이 좋습니다. 레이아웃이 많은 경우 단일 변경 내용을 모든 버전으로 전파 해야 하는 경우에는 유지 관리가 어렵고 오류가 발생할 수 있습니다.

여러 레이아웃 버전의 유지 관리를 간소화 하기 위해 디자이너는 하나 이상의 레이아웃에 변경 내용을 전파 하는 **다중 편집** 모드를 제공 합니다. 둘 이상의 레이아웃이 있는 경우 **다중 편집** 아이콘이 표시 됩니다. 

[![다중 편집 아이콘](alternative-layout-views-images/vs/05-multi-layout-icon-sml.png "다중 편집 아이콘")](alternative-layout-views-images/vs/05-multi-layout-icon.png#lightbox)

**다중 편집** 아이콘을 클릭 하면 아래와 같이 레이아웃이 연결 되었음을 나타내는 줄이 표시 됩니다. 즉, 한 레이아웃을 변경 하면 해당 변경 내용이 연결 된 레이아웃으로 전파 됩니다. 다음 스크린샷에 표시 된 원 모양의 아이콘을 클릭 하 여 모든 레이아웃의 연결을 해제할 수 있습니다. 

[![모든 레이아웃 연결 해제](alternative-layout-views-images/vs/06-multi-linked-sml.png "모든 레이아웃 연결 해제")](alternative-layout-views-images/vs/06-multi-linked.png#lightbox)

세 개 이상의 레이아웃이 있는 경우 각 레이아웃 미리 보기의 왼쪽에 있는 편집 단추를 선택적으로 전환 하 여 함께 연결 되는 레이아웃을 확인할 수 있습니다. 예를 들어 세 레이아웃의 첫 번째 및 마지막에 전파 되는 단일 변경을 수행 하려는 경우에는 다음과 같이 중간 레이아웃의 연결을 해제 합니다. 

[![중간 레이아웃 연결 해제](alternative-layout-views-images/vs/07-unlink-middle-layout-sml.png "중간 레이아웃 연결 해제")](alternative-layout-views-images/vs/07-unlink-middle-layout.png#lightbox)

이 예제에서는 **기본** 또는 **긴** 레이아웃에 대 한 변경 내용이 다른 레이아웃으로 전파 되지만, **이 레이아웃에** 는 적용 되지 않습니다.

### <a name="multi-edit-example"></a>다중 편집 예제 

일반적으로 하나의 레이아웃을 변경 하는 경우 동일한 변경 내용이 다른 모든 연결 된 레이아웃으로 전파 됩니다. 예를 들어 **기본** 레이아웃에 새 `TextView` 위젯을 추가 하 고 해당 텍스트 문자열을 `Portrait`로 변경 하면 모든 연결 된 레이아웃에 동일한 변경 내용이 적용 됩니다. **기본** 레이아웃은 다음과 같습니다. 

[![TextView 추가](alternative-layout-views-images/vs/08-add-textview-sml.png "TextView 추가")](alternative-layout-views-images/vs/08-add-textview.png#lightbox)

이 `TextView`는 **기본** 레이아웃에 연결 되어 있으므로, 다음의 경우에도 **커다란** 모양 레이아웃 뷰에 추가 됩니다. 

[![가로 TextView](alternative-layout-views-images/vs/09-landscape-textview-sml.png "가로 TextView")](alternative-layout-views-images/vs/09-landscape-textview.png#lightbox)

그러나 하나의 레이아웃에만 적용 되는 변경 내용을 적용 하려면 어떻게 해야 하나요? 변경 내용을 다른 레이아웃으로 전파 하지 않으려면 어떻게 해야 하나요? 이렇게 하려면 다음에 설명 된 대로 수정 하기 전에 변경 하려는 레이아웃의 연결을 해제 해야 합니다. 

### <a name="making-local-changes"></a>로컬 변경 

두 레이아웃 모두에 추가 된 `TextView`를 갖도록 하는 것은 아니지만,이 경우에는 `Portrait` 대신에 `Landscape`으로 **대기업** 레이아웃의 텍스트 문자열을 변경 하려고 할 수도 있습니다. 두 레이아웃을 연결 하는 동안이를 **대량** 으로 변경 하면 변경 내용이 **기본** 레이아웃으로 다시 전파 됩니다. 따라서 변경 하기 전에 먼저 두 레이아웃의 연결을 해제 해야 합니다. `Landscape`에 대 한 텍스트를 **수정 하는** 경우 디자이너는이 변경 내용을 빨간색 프레임으로 표시 하 여 변경 내용이 **대기업** 레이아웃에 로컬인 후 **기본** 레이아웃으로 다시 전파 *되지* 않음을 나타냅니다. 

[![로컬 변경](alternative-layout-views-images/vs/10-local-change-sml.png "로컬 변경")](alternative-layout-views-images/vs/10-local-change.png#lightbox)

**기본** 레이아웃을 클릭 하 여이를 볼 때 `TextView` 텍스트 문자열은 여전히 `Portrait`로 설정 됩니다. 

## <a name="handling-conflicts"></a>충돌 처리 

**기본** 레이아웃의 텍스트 색을 녹색으로 변경 하기로 결정 한 경우 링크 된 레이아웃에 경고 아이콘이 표시 됩니다. 해당 레이아웃을 클릭 하면 레이아웃이 열리며 충돌을 표시 합니다. 충돌을 일으킨 위젯을 빨간색 프레임으로 강조 표시 하 고 다음 메시지를 표시 합니다. *최근 변경 내용으로 인해이 대체 레이아웃에서 충돌이 발생 했습니다*. 

[![변경 내용 충돌](alternative-layout-views-images/vs/11-conflicting-change-sml.png "변경 내용 충돌")](alternative-layout-views-images/vs/11-conflicting-change.png#lightbox)

충돌을 설명 하기 위해 위젯의 오른쪽에 *충돌 상자가* 표시 됩니다. 

[![충돌 경고](alternative-layout-views-images/xs/11-warning-sml.png)](alternative-layout-views-images/xs/11-warning.png#lightbox)

충돌 상자에는 변경 된 속성 목록이 표시 되 고 해당 값이 나열 됩니다. **충돌 무시** 를 클릭 하면이 위젯에만 속성 변경 내용이 적용 됩니다. **적용** 을 클릭 하면이 위젯에 대 한 속성 변경 뿐만 아니라 연결 된 **기본** 레이아웃의 해당 위젯에 적용 됩니다. 모든 속성 변경 내용이 적용 되 면 충돌이 자동으로 삭제 됩니다. 

### <a name="view-group-conflicts"></a>그룹 충돌 보기 

속성 변경은 충돌의 유일한 원인이 아닙니다. 위젯을 삽입 하거나 제거할 때 충돌을 검색할 수 있습니다. 예를 들어, **크게** **레이아웃을** **기본** 레이아웃에서 연결 해제 하 고, `TextView`를 `Button` 위에 끌어서 놓으면 디자이너는 이동 된 위젯을 표시 하 여 충돌을 나타냅니다.

[![그룹 충돌 보기](alternative-layout-views-images/vs/12-view-group-conflict-sml.png "그룹 충돌 보기")](alternative-layout-views-images/vs/12-view-group-conflict.png#lightbox)

그러나 `Button`에는 마커가 없습니다. `Button` 위치가 변경 되었지만 `Button`에는 **대기업** 구성과 관련 된 적용 된 변경 내용이 표시 되지 않습니다. 

`CheckBox` **기본** **레이아웃에** 추가 되 면 다른 충돌이 생성 되 고, 경고 아이콘이 다음과 같이 표시 됩니다. 

[![Checkbox 충돌](alternative-layout-views-images/vs/13-checkbox-conflict-sml.png "Checkbox 충돌")](alternative-layout-views-images/vs/13-checkbox-conflict.png#lightbox)

**대기업** 레이아웃을 클릭 하면 충돌이 발생 합니다. 다음 메시지가 표시 됩니다. *최근 변경 내용으로 인해이 대체 레이아웃에서 충돌이 발생 했습니다*. 

[![Alt 레이아웃 충돌](alternative-layout-views-images/vs/14-alt-layout-conflict-sml.png "Alt 레이아웃 충돌")](alternative-layout-views-images/vs/14-alt-layout-conflict.png#lightbox)

또한 충돌 상자는 다음과 같은 메시지를 표시 합니다.

[![충돌 메시지](alternative-layout-views-images/xs/15-conflict-message-sml.png)](alternative-layout-views-images/xs/15-conflict-message.png#lightbox)

`CheckBox`를 추가 하면이를 포함 하는 `LinearLayout`에서 **많은** 부분 레이아웃이 변경 되므로 충돌이 발생 합니다. 그러나이 경우 충돌 상자에는 **기본** 레이아웃 (`CheckBox`)에 방금 삽입 된 위젯이 표시 됩니다.

**충돌 무시**를 클릭 하면 디자이너에서 충돌을 해결 하 여 위젯이 누락 된 레이아웃 (이 경우에는 **대기업** 의 레이아웃)에 표시 되는 위젯을 끌어서 놓을 수 있도록 합니다. 

[![확인 된 그룹 충돌](alternative-layout-views-images/vs/15-resolved-group-conflict-sml.png "확인 된 그룹 충돌")](alternative-layout-views-images/vs/15-resolved-group-conflict.png#lightbox)

`Button`를 사용 하는 이전 예제에서 볼 수 있듯이 `CheckBox`는 `LinearLayout`에만 **커다란** 레이아웃에 적용 된 변경 내용이 있으므로 빨강 변경 표식이 없습니다.

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio for Mac](#tab/macos)

## <a name="creating-alternative-layouts"></a>대체 레이아웃 만들기

**장치**왼쪽에 있는 **대체 레이아웃 보기** 아이콘을 클릭 하면 프로젝트에서 사용할 수 있는 대체 레이아웃을 나열 하는 미리 보기 창이 열립니다. 대체 레이아웃이 없으면 **기본** 보기가 표시 됩니다. 

[![대체 레이아웃 뷰 창](alternative-layout-views-images/xs/01-alt-layout-view-pane-sml.png)](alternative-layout-views-images/xs/01-alt-layout-view-pane.png#lightbox)

**새 버전**옆에 있는 녹색 더하기 기호를 클릭 하면 레이아웃 변형 **만들기** 대화 상자가 열리며,이 레이아웃 변형에 대 한 리소스 한정자를 선택할 수 있습니다. 

[![레이아웃 변형 만들기](alternative-layout-views-images/xs/02-create-layout-variation-sml.png)](alternative-layout-views-images/xs/02-create-layout-variation.png#lightbox)

다음 예제에서 **화면 방향** 에 대 한 리소스 한정자는 **가로**로 설정 되 고 **화면 크기** 는 **크게**변경 됩니다. 이렇게 하면 새 레이아웃 버전이 생성 됩니다 **.**

[![큼 변형](alternative-layout-views-images/xs/03-large-land-sml.png)](alternative-layout-views-images/xs/03-large-land.png#lightbox)

왼쪽의 미리 보기 창에는 리소스 한정자 선택의 영향이 표시 됩니다. **추가** 를 클릭 하면 대체 레이아웃이 만들어지고 디자이너가 해당 레이아웃으로 전환 됩니다. **대체 레이아웃 뷰** 미리 보기 창에는 다음 스크린샷에 표시 된 대로 작은 오른쪽 포인터를 통해 디자이너로 로드 되는 레이아웃이 표시 됩니다. 

[![로드 된 레이아웃 표시기](alternative-layout-views-images/xs/04-new-layout-sml.png)](alternative-layout-views-images/xs/04-new-layout.png#lightbox)

## <a name="editing-alternative-layouts"></a>대체 레이아웃 편집

다른 레이아웃을 만들 때 레이아웃의 모든 분기 버전에 적용 되는 단일 변경을 수행 하는 것이 좋습니다. 예를 들어 모든 레이아웃에서 단추 텍스트를 노란색으로 변경 하는 것이 좋습니다. 레이아웃이 많은 경우 단일 변경 내용을 모든 버전으로 전파 해야 하는 경우에는 유지 관리가 어렵고 오류가 발생할 수 있습니다.

여러 레이아웃 버전의 유지 관리를 간소화 하기 위해 디자이너는 하나 이상의 레이아웃에 변경 내용을 전파 하는 **다중 편집** 모드를 제공 합니다. 둘 이상의 레이아웃이 있는 경우 **다중 편집** 아이콘이 표시 됩니다. 

[![다중 편집 아이콘](alternative-layout-views-images/xs/05-multi-layout-icon-sml.png)](alternative-layout-views-images/xs/05-multi-layout-icon.png#lightbox)

**다중 편집** 아이콘을 클릭 하면 아래와 같이 레이아웃이 연결 되었음을 나타내는 줄이 표시 됩니다. 즉, 한 레이아웃을 변경 하면 해당 변경 내용이 연결 된 레이아웃으로 전파 됩니다. 다음 스크린샷에 표시 된 원 모양의 아이콘을 클릭 하 여 모든 레이아웃의 연결을 해제할 수 있습니다. 

[모든 레이아웃![연결 해제](alternative-layout-views-images/xs/06a-linked-sml.png)](alternative-layout-views-images/xs/06a-linked.png#lightbox)

세 개 이상의 레이아웃이 있는 경우 각 레이아웃 미리 보기의 왼쪽에 있는 편집 단추를 선택적으로 전환 하 여 함께 연결 되는 레이아웃을 확인할 수 있습니다. 예를 들어 세 레이아웃의 첫 번째 및 마지막에 전파 되는 단일 변경을 수행 하려는 경우에는 다음과 같이 중간 레이아웃의 연결을 해제 합니다. 

[중간 레이아웃![연결 해제](alternative-layout-views-images/xs/06b-multi-linked-sml.png)](alternative-layout-views-images/xs/06b-multi-linked.png#lightbox)

이 예제에서는 **기본** 또는 **긴** 레이아웃에 대 한 변경 내용이 다른 레이아웃으로 전파 되지만, **이 레이아웃에** 는 적용 되지 않습니다. 

### <a name="multi-edit-example"></a>다중 편집 예제 

일반적으로 하나의 레이아웃을 변경 하는 경우 동일한 변경 내용이 다른 모든 연결 된 레이아웃으로 전파 됩니다. 예를 들어 **기본** 레이아웃에 새 `TextView` 위젯을 추가 하 고 해당 텍스트 문자열을 `Portrait`로 변경 하면 모든 연결 된 레이아웃에 동일한 변경 내용이 적용 됩니다. **기본** 레이아웃은 다음과 같습니다. 

[TextView 추가![](alternative-layout-views-images/xs/07-add-textview-sml.png)](alternative-layout-views-images/xs/07-add-textview.png#lightbox)

이 `TextView`는 **기본** 레이아웃에 연결 되어 있으므로, 다음의 경우에도 **커다란** 모양 레이아웃 뷰에 추가 됩니다. 

[![가로 TextView](alternative-layout-views-images/xs/08-landscape-textview-sml.png)](alternative-layout-views-images/xs/08-landscape-textview.png#lightbox)

그러나 하나의 레이아웃에만 적용 되는 변경 내용을 적용 하려면 어떻게 해야 하나요? 변경 내용을 다른 레이아웃으로 전파 하지 않으려면 어떻게 해야 하나요? 이렇게 하려면 다음에 설명 된 대로 수정 하기 전에 변경 하려는 레이아웃의 연결을 해제 해야 합니다. 

### <a name="making-local-changes"></a>로컬 변경 

두 레이아웃 모두에 추가 된 `TextView`를 갖도록 하는 것은 아니지만,이 경우에는 `Portrait` 대신에 `Landscape`으로 **대기업** 레이아웃의 텍스트 문자열을 변경 하려고 할 수도 있습니다. 두 레이아웃을 연결 하는 동안이를 **대량** 으로 변경 하면 변경 내용이 **기본** 레이아웃으로 다시 전파 됩니다. 따라서 변경 하기 전에 먼저 두 레이아웃의 연결을 해제 해야 합니다. `Landscape`에 대 한 텍스트를 **수정 하는** 경우 디자이너는이 변경 내용을 빨간색 프레임으로 표시 하 여 변경 내용이 **대기업** 레이아웃에 로컬인 후 **기본** 레이아웃으로 다시 전파 *되지* 않음을 나타냅니다. 

[![로컬 변경](alternative-layout-views-images/xs/09-local-change-sml.png)](alternative-layout-views-images/xs/09-local-change.png#lightbox)

**기본** 레이아웃을 클릭 하 여이를 볼 때 `TextView` 텍스트 문자열은 여전히 `Portrait`로 설정 됩니다. 

## <a name="handling-conflicts"></a>충돌 처리 

**기본** 레이아웃의 텍스트 색을 녹색으로 변경 하기로 결정 한 경우 링크 된 레이아웃에 경고 아이콘이 표시 됩니다. 해당 레이아웃을 클릭 하면 레이아웃이 열리며 충돌을 표시 합니다. 충돌을 일으킨 위젯을 빨간색 프레임으로 강조 표시 하 고 다음 메시지를 표시 합니다. *최근 변경 내용으로 인해이 대체 레이아웃에서 충돌이 발생 했습니다*. 

[충돌 하는 변경![](alternative-layout-views-images/xs/10-conflict-sml.png)](alternative-layout-views-images/xs/10-conflict.png#lightbox)

충돌을 설명 하기 위해 위젯의 오른쪽에 *충돌 상자가* 표시 됩니다. 

[![충돌 경고](alternative-layout-views-images/xs/11-warning-sml.png)](alternative-layout-views-images/xs/11-warning.png#lightbox)

충돌 상자에는 변경 된 속성 목록이 표시 되 고 해당 값이 나열 됩니다. **충돌 무시** 를 클릭 하면이 위젯에만 속성 변경 내용이 적용 됩니다. **적용** 을 클릭 하면이 위젯에 대 한 속성 변경 뿐만 아니라 연결 된 **기본** 레이아웃의 해당 위젯에 적용 됩니다. 모든 속성 변경 내용이 적용 되 면 충돌이 자동으로 삭제 됩니다. 

### <a name="view-group-conflicts"></a>그룹 충돌 보기 

속성 변경은 충돌의 유일한 원인이 아닙니다. 위젯을 삽입 하거나 제거할 때 충돌을 검색할 수 있습니다. 예를 들어, **크게** **레이아웃을** **기본** 레이아웃에서 연결 해제 하 고, `TextView`를 `Button` 위에 끌어서 놓으면 디자이너는 이동 된 위젯을 표시 하 여 충돌을 나타냅니다.

[![보기 그룹 충돌](alternative-layout-views-images/xs/12-view-group-conflict-sml.png)](alternative-layout-views-images/xs/12-view-group-conflict.png#lightbox)

그러나 `Button`에는 마커가 없습니다. `Button` 위치가 변경 되었지만 `Button`에는 **대기업** 구성과 관련 된 적용 된 변경 내용이 표시 되지 않습니다. 

`CheckBox` **기본** **레이아웃에** 추가 되 면 다른 충돌이 생성 되 고, 경고 아이콘이 다음과 같이 표시 됩니다. 

[![Checkbox 충돌](alternative-layout-views-images/xs/13-checkbox-conflict-sml.png)](alternative-layout-views-images/xs/13-checkbox-conflict.png#lightbox)

**대기업** 레이아웃을 클릭 하면 충돌이 발생 합니다. 다음 메시지가 표시 됩니다. *최근 변경 내용으로 인해이 대체 레이아웃에서 충돌이 발생 했습니다*. 

[![Alt 레이아웃 충돌](alternative-layout-views-images/xs/14-alt-layout-conflict-sml.png)](alternative-layout-views-images/xs/14-alt-layout-conflict.png#lightbox)

또한 충돌 상자는 다음과 같은 메시지를 표시 합니다.

[![충돌 메시지](alternative-layout-views-images/xs/15-conflict-message-sml.png)](alternative-layout-views-images/xs/15-conflict-message.png#lightbox)

`CheckBox`를 추가 하면이를 포함 하는 `LinearLayout`에서 **많은** 부분 레이아웃이 변경 되므로 충돌이 발생 합니다. 그러나이 경우 충돌 상자에는 **기본** 레이아웃 (`CheckBox`)에 방금 삽입 된 위젯이 표시 됩니다.

**충돌 무시**를 클릭 하면 디자이너에서 충돌을 해결 하 여 위젯이 누락 된 레이아웃 (이 경우에는 **대기업** 의 레이아웃)에 표시 되는 위젯을 끌어서 놓을 수 있도록 합니다. 

[![해결 된 그룹 충돌](alternative-layout-views-images/xs/16-resolved-group-conflict-sml.png)](alternative-layout-views-images/xs/16-resolved-group-conflict.png#lightbox)

`Button`를 사용 하는 이전 예제에서 볼 수 있듯이 `CheckBox`는 `LinearLayout`에만 **커다란** 레이아웃에 적용 된 변경 내용이 있으므로 빨강 변경 표식이 없습니다.

-----

### <a name="conflict-persistence"></a>충돌 지 속성

충돌은 다음과 같이 레이아웃 파일에서 XML 주석으로 유지 됩니다.

```xml
<!-- Widget Inserted Conflict | id:__root__ | @+id/checkBox1 -->
```

따라서 프로젝트를 닫았다가 다시 열면 모든 충돌도 무시 된 상태를 포함 하 여 &ndash; 됩니다.
