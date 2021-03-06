---
title: 나는 자바스크립트 개발자다 ReactJS 컨퍼런스 - 2017.05.17
date: 2017-05-17 23:43:15
description: "React Korea 컨퍼런스 내용 정리"
tags: 
- react
- conference
---
<!-- more -->

<br>
## 프론트엔드 코딩 컨벤션 자동화 도구 - 김태곤
[다시보기 영상](https://www.facebook.com/groups/react.ko/permalink/1842951499298347)
[발표자료](https://www.slideshare.net/taggon/ss-76076338)

1. EditorConfig(editorconfig.org) => 대부분의 에디터들이 지원. react github 에서 보면 .enditorconfig 가 있다
2. stylefmt => css 코드 자동정리
3. prettier => JS 코드 자동정리 => 이거 쓰자!
4. husky + lint-staged
	- husky: Git hook을 편하게 작성
	- lint-staged: 커밋할 파일에 대해 린터 실행

<br>
## 리액트 퍼포먼스 개선기 - 천민호
[다시보기 영상](https://www.facebook.com/groups/react.ko/permalink/1842958372630993)
[발표자료](/assets/react-conference-20170517_performance.pdf)

1. 성능측정도구
	- npm react-addons-perf => 이거 써보자!
	- Chrome react-devtools
	
2. 성능개선 (react-addons-perf)
	- shouldComponenetUpdate() => 좀 복잡해져서 머 하나 빠지면 버그 발생
	- PureComonent 이용! => 단 shallow Compare 이기 때문 주의
	- advanced 한 구조로 짜자 => selector 이용: memoizing
	- event 함수는 constructor 에서 바인딩하자 => 바인딩(arrow function)할떄마다 새로운 메모리 할당하기 때문에

<br>
## TDD로 구현하는 초간단 React 컴포넌트 - 김훈민
[다시보기 영상](https://www.facebook.com/groups/react.ko/permalink/1842969479296549)
[발표자료](https://www.slideshare.net/jeokrang/react-tdd-76066004)

1. 테스트 환경 설정은 잘 되어있는가
	- 두개창으로 split 하여 오른쪽에만 테스트 코드작성
2. 테스트 시나리오
	- // given(조건 및 상황)
	- // when
	- // then
	혹은
	- // setup
	- // exercise
	- // verify
3. 어디에서 시작하지?
	- 요구사항 정리 => 그중 가장 단순하고 쉬운것부터 시작
	- 명세 작성
4. 테스트후 성공하면 리팩토링
	* 테스트 fail 된 상태에서는 리팩토링은 하지 말자
	* fail 전으로 성공으로 돌아가서 (test fail 된 케이스는 skip 후) 리팩토링
5. 구현 코드 리팩토링후 테스트 코드 리팩토링 하기


##훈민님 커멘트

안녕하세요, 어제 “React로 TDD 쵸큼 맛보기”를 발표한 김훈민입니다. 슬라이드 쉐어에 올린 발표 자료 공유드립니다.
https://www.slideshare.net/jeokrang/react-tdd-76066004
발표 자료 만들 때 작성한 예제 코드도 함께 공유드립니다.
https://github.com/CoderK/spinbox-tdd-example
저도 계속 연습하면서 방향을 잡아나가는 과정이라 "이 사람은 이렇게 하고 있구나" 정도로 봐주시면 감사하겠습니다.
Q&A 할 때 제 답변에 오해의 소지가 있거나, 내용이 불충분했던 것 같다는 생각이 드는 부분이 있어서 아래에 보충합니다. 질문을 제가 재정리했는데 행여나 본래의 의도랑 다르게 표현이 되었다면 코멘트 주세요~.
어제 질문하고 싶었는데 못하신 분도 코멘트 주시면 제가 아는 한에서 의견 드리겠습니다.

1. 테스트가 없는 레거시 코드를 TDD하고 싶습니다. 좋은 방법이 있을까요?
답)
TDD의 “빨강-녹색-리팩터링” 프로세스에서 리팩터링은 매우 중요한 단계입니다. 레거시 코드에 TDD를 할 때도 마찬가지로 리팩터링 단계를 피할 수 없고, 그렇다면 변경 후 버그가 없음을 보장해 줄 장치들이 필요할 텐데 테스트 커버리지가 불충분한 상태에서는 안심을 할 수가 없겠죠. 저라면 레거시 코드에 대한 단위 테스트를 먼저 작성해서 커버리지를 확보할 것 같아요~. 만약 더 좋은 방법이 있다면 저도 배우고 싶네요.
2. 비동기 로직에 대한 단위 테스트는 어떻게?
답)
비동기 로직에 대한 테스트는 테스트 환경에서 비동기 로직이 동기로 작동하도록 만드는 게 요령인 것 같아요. 이를 위해서 테스트 대역을 주로 이용합니다. 저는 주로 Sinon.js를 이용합니다. setTimeout, setInterval을 사용하는 로직은 fake-timers(http://sinonjs.org/releases/v2.2.0/fake-timers/)를 이용하고 XMLHttpRequest 객체를 이용하는 비동기 통신은 Fake XMLHttpRequest나 Fake Server(http://sinonjs.org/releases/v2.2.0/fake-xhr-and-server/)를 이용합니다. Jest는 테스트 대역 API를 일부 제공하는데 공식 문서에 잘 나와있으니 참고하시면 좋겠습니다.
3. 테스트 코드에 작성한 셀렉터가 마크업 구조와 강하게 결합하는 것을 막기 위해서 데이터 어트리뷰트(data-*)를 사용하셨는데 테스트를 위해 억지로 불필요한 코드를 작성한다는 느낌입니다. 혹시 다른 방법을 생각해보시지는 않았나요?
답)
저도 그 부분이 마음에 걸리긴하는데 트레이드 오프했다고 생각하고 있습니다. ref를 이용하기도 했었는데, 불필요한 내부 프로퍼티를 만든다는 느낌이 강하게 들어서 지금은 데이터 어트리뷰트나 셀렉터용 클래스(prefix를 붙이는 방식으로 구분)를 따로 정의하는 걸 선호합니다. 물론 모든 경우에 이렇게 구현하는 건 아니고, 마크업 구조와 강하게 결합(복합 셀렉터를 써야한다는 등)하지 않는다면 그냥 있는 장치들(클래스나 아이디)을 이용합니다. "구현 코드와 테스트 코드 사이의 의존성을 잘 고려하라"는 이야기를 UI 프로그래밍 버전으로 하고 싶었는데 예제가 적절하지 않아서 의도를 충분히 전달하지 못한 것 같네요 ㅠㅜ.
4. UI 단위 테스트는 투자 대비 효과가 별로인 것 같은데 어떻게 생각하시나요? 그리고 현재 진행하고 계신 프로젝트의 커버리지는 어느 정도 수준인가요?
답)
논란이 많은 부분이라 이야기가 길어질 것 같습니다만 가능한 짧게 말씀드려볼게요. 정답이라기 보다는 "오늘" 저의 생각이 그렇다 정도로 이해해주시면 감사하겠습니다.
예전에는 저도 UI 단위 테스트 작성은 무척 수고롭지만, 단위 수준을 벗어나는 행위에서 발생하는 문제는 잘 짚어주지 못해서 얻는 이점은 별로 없다고 생각했던 적이 있었어요. 게다가 UI는 변경도 잦죠. 요즘처럼 린, 애자일 뭐 이런 적응적인 개발 프로세스를 강조하는 시대에는 더 그런 것 같아요. 테스트가 리팩터링에 방해가 된다는 느낌을 간혹 받을 때도 있었습니다.
그런데 TDD를 수련하면서 단위 테스트의 가장 큰 목적이 “오류를 방지한다” 보다는 “오류를 가능한 빨리 발견한다”에 있다는 걸 깨달은 후에는 생각이 달라졌어요. 요즘은 생산성 관점에서 단위 테스트를 바라보고 있습니다. 구현과 오류 발견 사이의 간격이 벌어질수록 버그 수정 비용이 더 발생한다는 구글의 발표 자료가 있습니다. 제 경험에 비춰 여기에 공감합니다. 그래서 단위 수준에서 발생한 문제를 QA까지 넘기지 않고 구현단계에서 찾겠다는거고 그렇다면 단위 테스트의 목적은 “생산성”에 더 초점이 맞춰져 있는 것 같습니다. UI 단위 테스트 역시 마찬가지 일테구요.
그런 의미에서 단위 테스트로 UI를 완벽하게 테스트할 수 없다는 걸 인정하고, 목적이 다른 테스트를 중첩(예, 단위 테스트 -> 통합 테스트 -> 기능 테스트 등)해서 수행하여 보완하는 게 좋을 것 같아요. 다행히도 저희 회사는 그런 프로세스가 잘 되어 있는 편입니다.
UI 테스트 작성의 어려움이 전에 비해 많이 줄어든 것도 제가 UI 테스트에 적극적인 이유 중 하나입니다. 예전에는 프론트엔드의 UI 코드를 단위 테스트하는 게 상당히 어려웠었는데 DOM을 직접 수다스럽게 스크립팅하던 방식에서 UI를 추상화한 객체가 가진 상태를 기반으로 렌더링을 하는 방식이 주가 되면서 테스트 작성이 많이 쉬워졌죠.
UI는 변경이 잦기 때문에 테스트 코드는 불필요하다고 이야기 하는 경우를 가끔 보는데, 이걸 저는 반대로 생각하고 있어요. 오히려 “변경이 잦으니까 테스트 코드가 필요하다”는 쪽입니다. 변경 후에 “사이드 이펙트 없음을 무엇으로 확인하지?”라는 질문을 던져보면 어떤 식의 테스트든 필요하다는 결론에 도달할 수밖에 없었고, 개발 단계에서 잡아야 하는 버그가 QA까지 넘어감으로써 발생하는 비용, 정신적 스트레스 등이 저는 단위 테스트 구현 비용 보다 더 크게 느껴졌습니다.
현재 진행하고 있는 프로젝트의 커버리지는 오늘 확인해보니 라인 커버리지 86 %, 브랜치 커버리지 77%네요. 브랜치 빠졌네 ㅜㅜ.
***

<br>
## React 어플리케이션 아키텍처 (부제 : 아무도 알려주지 않아서 혼자 삽질했다) - 손병대
[다시보기 영상](https://www.facebook.com/groups/react.ko/permalink/1842982715961892)
[발표자료](https://www.slideshare.net/byungdaesohn/react-76078368)

### 좋은 디자인을 위해 알아야 할것들
1. 컴포넌트의 역할 정의
2. 컴포넌트 분리
3. 리덕스 아키텍쳐
	- 리듀서
	- 액션 생성자
	- 리덕스 미들웨어
	- 비동기 제어 => redux-saga






