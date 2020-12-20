---
date: 2020-12-18 20:55:45 +0900
layout: post
title: 우아한 테크코스 프리코스 후기
description: 2020년 겨울, 3주간 진행한 우아한 프리코스 후기
image: https://res.cloudinary.com/dtttkj2mc/image/upload/v1608292767/etc/woowa_precourse_j0usgf.png
optimized_image: https://res.cloudinary.com/dtttkj2mc/image/upload/c_pad,w_380,h_200/v1608292767/etc/woowa_precourse_j0usgf.png
---

<p class="callout"> 💡 우아한 테크코스 3기 - 프리코스 후기 </p>

우아한 테크코스를 신청하여 지난 3주간 프리코스를 진행했다. 이제 프리코스가 끝났다. 오늘 이 포스팅에서는 프리코스 기간동안의 후기를 정리한다. 미션 내용과 각 미션을 하면서 가장 신경썼던 점을 기록하려 한다.


## 지원동기

가이드가 필요했다.

학교에서 팀 프로젝트도 몇 번 해봤고, 혼자서 프로젝트도 몇 번 했었다. 하지만 무작정 프로젝트를 한다고 실력이 느는 건 아닌것같았다. 동굴 속에서 방향을 잃은 채 돌아다니는 느낌이었다. 앞으로 나아가긴 하는데, 그 방향이 곧은지 알 수 없는 기분. 그래서 신청했다. 동굴 속에서 잡고 갈 수 있는 밧줄이 될 것 같았다.


## 1주차

<p class = "callout">
🚩 과제: 숫자 야구게임 / 목표: 커밋 메세지, 코드 컨벤션, 인덴트 지키기
</p>

1주차 과제는 무난했다. 구현부분은 그렇게 어려운 부분이 없었다. 구현보다 어려웠던 건 다른 부분이었다. 

### 커밋 메세지 작성
커밋 템플릿을 적용하고, 메세지 규칙을 지키려고 노력했다.

add, feat, docs, style등 커밋 메세지 앞에 머릿말을 달아주었다.\
커밋 템플릿은 [이 블로그 글](https://junwoo45.github.io/2020-02-06-commit_template/)을 참고했다.

커밋 메세지를 작성하는 것이 어려웠다. ReadMe나 커밋 메세지 템플릿 (add, feat 등)을 지켜 커밋 메세지에 커밋한 내용을 요약해 담으려고 노력했다.


### 가독성 - 인덴트 맞추기
indent를 2까지만 사용했다.

코드를 짜다보면 인덴트가 길어진 적이 많았다. while안에 if안에 또다른 if...\
인덴트를 줄이면 가독성이 크게 향상되는 것을 알 수 있었다. 보기 좋은 떡이 먹기도 좋다고, 코드를 '>'가 아닌 'ㅁ'모양으로 작성하면 코드의 흐름도 더 파악하기 쉬웠다.


### 코드 컨벤션 맞추기
자바스크립트 코드 컨벤션을 맞춰 작성했다.

코딩 스타일이라는것이 사람에 따라 들쑥날쑥하다보니, 좀 더 통일된 규칙을 적용할 필요가 있었나보다. 그래서 코드 컨벤션을 지켜서 작성하는 연습을 했다. eslint와 prettier를 사용하면 코드 포맷팅을 지켜주긴 한다. 그럼에도 잡히지 않는 부분들은 수동으로 지켜주며 코드를 작성했다. 

컨벤션은 아래 두 곳을 참고했다.
- <https://ui.toast.com/fe-guide/ko_CODING-CONVENTION/>
- <https://google.github.io/styleguide/jsguide.html>



## 2주차

<p class = "callout">
🚩 과제: 레이싱게임 / 목표: 1주차 미션 + 모듈 분리
</p>

2주차 미션도 무난했다. 모듈화를 하는 과정이 조금 시간이 걸렸다. 

### 함수 길이 맞추기
함수 길이를 15라인 이내로 작성했다.

그 당시에는 몰랐는데 지금 생각해보니 함수를 짧게 나누는 것도 모듈화의 일종인 것 같다. *함수명에 축약어를 사용하지 말아라*라는 조건과 *함수의 길이를 15라인 이내로 작성해라*라는 조건이 서로 충돌해서 고생했었다. '함수에 축약어를 사용하지 않음 → 함수명이 길어짐 → 라인이 길어짐'의 연쇄작용이 일어났기 때문이었다.

지금 생각해보니 함수 길이를 15라인 이내로 작성하는 문제는 ***함수의 역할을 분리하는 것***으로 해결할 수 있었다. 당시 작성했던 함수 하나를 보자.

자동차 리스트를 받아, 우승자를 printContainer에 출력하는 함수다. 11줄짜리 코드였기 때문에 잘 짰다고 생각했었다.

```js
 static printWinner(printContainer, carList) {
    const carGameResultContainer = printContainer;
    const winnerResultDiv = document.createElement('div');
    const winPosition = Math.max(...carList.map(car => car.getPosition()));
    const winners = carList
      .filter(car => car.getPosition() === winPosition)
      .map(car => car.getName());
    winnerResultDiv.innerHTML = `최종 우승자: ${winners.join(', ')}`;
    carGameResultContainer.appendChild(winnerResultDiv);
  }
```

위 함수는 다음처럼 더 분리할 수 있다.

```js
 static printWinner(printContainer, winners) {
    const carGameResultContainer = printContainer;
    const winnerResultDiv = document.createElement('div');
    winnerResultDiv.innerHTML = `최종 우승자: ${winners.join(', ')}`;
    carGameResultContainer.appendChild(winnerResultDiv);
  }

  static calculateWinners(carList) {
    const winPosition = Math.max(...carList.map(car => car.getPosition()));
    const winners = carList
      .filter(car => car.getPosition() === winPosition)
      .map(car => car.getName());
    return winners;
  }
```

printWinner함수를 printWinner와 calculateWinner 두 함수로 나눴다. 두 함수를 나누자 함수 길이가 짧아진 것 뿐 아니라, 비즈니스 로직과 UI 로직을 구분하는 장점도 생겼다. 중요한 것은 함수의 길이가 짧은 것이 아니었다. 함수의 역할을 구분하는 것이었다.

### 함수명, 변수명 짓기
이름을 명료하게 짓기 

제일 시간이 많이 들었다. 내가 원래 코드를 짜는 속도가 느린데, 이름까지 고민하는 시간이 더 걸리니 더더욱 느려졌다. 한국말도 못하는데 영어로 딱 맞는 단어로 표현하려니 어려웠다.\
'읽기 좋은 코드가 좋은 코드다' 책을 다시 폈다. 책에 나온대로 ***"다른 사람들이 다른 의미로 해석할 수 있을까?"***라는 질문을 기준으로 메소드 이름을 지었다.

'읽기 좋은 코드가 좋은 코드다'는 예전에 읽었던 책인데, 이번 프리코스를 진행하면서 다시 읽었다. 잊고 있었던 내용이 많았다. 다시 봐도 좋은 책이다.

이름을 짓는 데 도움을 준 목록:
- 읽기 좋은 코드가 좋은 코드다
- 다른 분의 코드 (buttonHandler 라는 이름을 차용했다!)
- 유의어사전 (<https://m.wordnet.co.kr/>)


### eslint, prettier 설정

eslint와 prettier를 사용하는 방법은 알고 있었는데, 이번 기회에 다시 정리해봤다.\
다음에 내가 보고 쓸 용도로 작성했다.

블로그 글 링크 : <https://sunmon.github.io/vscode-eslint-prettier-setting/>

## 3주차
<p class = "callout">
🚩 과제: 지하철 노선도 / 목표: 2주차 미션 + 모듈 분리 + 모듈간 관계맺기
</p>

3주차 미션은 제일 재밌었다! 연습이 아니라 실전같은 느낌이었다. 제일 재밌었고 제일 어려웠고 제일 열심히 했다.\
이런저런 일이 겹쳐 3주차에는 시간이 좀 부족했다. 처음 보자마자 시간 좀 걸리겠네, 라고 생각했는데... 결국 맘에 안들게 냈다. 예외처리 더 할 수 있는데 👿 함수 더 나눌 수 있는데 👿 모듈 더 나눌수 있는데 👿


### 엘리먼트 생성 / 렌더링 함수 분리
엘리먼트를 생성하는 함수와 DOM에 붙이는 함수를 분리했다. 

이 과정이 시간이 정말 많이 걸렸다. 그냥 HTML을 작성하면 뚝딱인것을... 😢\
그래도 덕분에 브라우저 렌더링과 최적화에 대한 이해를 할 수 있었다.

1.\
브라우저가 동작하는 원리를 알아봤다. *DOM트리*와 *스타일 트리*를 만들어서 둘을 합친다. 그러면 *렌더 트리*가 된다. 이 렌더트리를 이용해 화면에 그리는 과정이 `reflow(= Layout)` 고, 그 이후 색깔을 덧입히는 과정이 `repaint`다.\
reflow와 repaint 를 한 결과물이 우리가 보는 화면인 것이다. 

reflow(화면에 객체를 배치하기)와 repaint(색깔, 투명도 등)는 리소스 연산을 많이 잡아먹는다. DOM이나 Style을 수정할때마다 reflow, repaint가 수행되고, 많이 발생하면 브라우저가 느려지게 된다.

위 내용들은 아래 링크에 더 자세히 나와 있다.
- <https://www.sitepoint.com/10-ways-minimize-reflows-improve-performance/>
- <https://velopert.com/3236>
- <http://blog.drakejin.me/React-VirtualDOM-And-Repaint-Reflow/>
- <https://d2.naver.com/helloworld/59361>


2.\
엘리먼트 변화를 모아놨다가 한번에 DOM을 수정하면 repaint와 reflow 횟수를 줄일 수 있다. 그래서 이를 구현하기 위해 엘리먼트를 생성하는 함수와 렌더링하는 함수를 분리했다. 원래 계획은 캐시를 만들어뒀다가 변하는 부분만 한번에 렌더링하는것이었는데 시간이 없어서 거기까진 구현하지 못했다.

가상 엘리먼트를 만들었다. 예를 들어 root라는 div안에 title이라는 h1이 있다면 아래처럼 조직된다. 

```js
const root = {
    $el: createElement('div'),
    $children: {
        title: {
            $el: createElement('h1')
        }
    }
}
```

이 가상 엘리먼트 오브젝트를 만든 다음, 나중에 render 함수를 통해 실제 DOM에 append하는 과정을 거쳤다.
시간이 있었으면 더 잘 만들었을텐데... 아쉽다.




## 후기

어떤 식으로 코드를 작성해야할지 많이 배웠다.\
이전에는 스파게티 코드를 작성하는 느낌이 강했었다. 이제는 꼬인 코드를 풀어가는 방법에 대한 감을 얻은 느낌이다.\
지원 동기에 '가이드가 필요하다'라고 적었었다. 이번 프리코스에서 지원 동기대로 가이드를 얻을 수 있어 만족스러웠다.

다른 분들이 짠 코드도 볼 수 있던 점도 장점이었다. 과제와 피드백 외에도 다른 분들의 코드를 보고 괜찮은 점들을 차용할 수 있었다. 나는 함수명을 작성하는 방법과 모듈화를 하는 방식에 대한 아이디어를 얻을 수 있었다.

물론 프리코스 3주만으로 극적인 변화가 생기지는 않았다. 여전히 코딩 속도는 느리며, 급할때는 허둥지둥 스파게티를 만들어낸다. 하지만 이번 코스에서 배운 것들을 바탕으로 좀 더 연습하다보면 나아질 것이라 믿는다.

---

길이 길어져서 후기에는 생략했지만 기억할만한 부분은 따로 적어둔다.
- 커밋을 '기록하는 용도'로 사용하게 되었다
- 주석이 많다고 좋은 것이 아니다. 주석 없이도 이해할 수 있는 코드가 좋은 코드다.
- MVC와 DAO-DTO 패턴을 다시 보았다
- js의 dataset과 template 기능을 새로 배웠다
- `add-remove / insert-delete / begin-end` 등 이름 쌍을 알아보았다
- map, reduce, filter, for의 속도를 고려하여 코드를 짰다 (<https://github.com/dg92/Performance-Analysis-JS>)
- 시멘틱 태그를 이용했다
- Object안 프로퍼티에 접근할 때 `.`과 `[]`가 다르다! (<https://medium.com/sjk5766/javascript-object-key-vs-object-key-%EC%B0%A8%EC%9D%B4-3c21eb49b763>)
- append를 여러번 한다고 노드가 여러번 추가되지 않는다. 이미 DOM에 존재하는 경우는 위치가 이동된다.
- localStorage에 대해 새로 배웠다.
- localStorage는 문자열 형태 (더 편하게 쓰려면 JSON형태로 변환하여 넣자) 로 사용한다. 클래스로 안 들어간다!!!
- 그래서 링크드 리스트를 쓰려고 했는데 못 썼다.
- 클로저와 변수의 유효범위에 대해 다시 정리했다. 관련 포스팅 작성중이다.
- 세상엔 잘하는 사람들이 정말 많다. 우물안 개구리였다 난.
