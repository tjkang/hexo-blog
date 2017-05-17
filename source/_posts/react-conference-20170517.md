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

1. EditorConfig(editorconfig.org) => 대부분의 에디터들이 지원. react github 에서 보면 .enditorconfig 가 있다
2. stylefmt => css 코드 자동정리
3. prettier => JS 코드 자동정리 => 이거 쓰자!
4. husky + lint-staged
	- husky: Git hook을 편하게 작성
	- lint-staged: 커밋할 파일에 대해 린터 실행

<br>
## 리액트 퍼포먼스 개선기 - 천민호
[다시보기 영상](https://www.facebook.com/groups/react.ko/permalink/1842958372630993)

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

<br>
## React 어플리케이션 아키텍처 (부제 : 아무도 알려주지 않아서 혼자 삽질했다) - 손병대
[다시보기 영상](https://www.facebook.com/groups/react.ko/permalink/1842982715961892)

### 좋은 디자인을 위해 알아야 할것들
1. 컴포넌트의 역할 정의
2. 컴포넌트 분리
3. 리덕스 아키텍쳐
	- 리듀서
	- 액션 생성자
	- 리덕스 미들웨어
	- 비동기 제어 => redux-saga






