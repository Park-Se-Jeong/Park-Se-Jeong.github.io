---
layout: post
title: React DevTools 써먹어보기
# date: 2017-09-12 13:32:20 +0900
date: 2023-12-06 13:35:20 +0900
description: From React Devtools to Chrome Devtools # Add post description (optional)
img: /2023-12-06/2023-12-06.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [react debugging, react devtools, debugging]
---

*해당 글은 모던 리액트 Deep Dive 6장부터 7-5장까지 읽고 정리한 내용입니다.*

## 이번 글에서는?

>
> ### React Dev Tools 와 Chrome Dev Tools 에 대해 자세히 살펴봅니다! 
>
> 디버깅하는 방법에 대해 자세히 알 수 있습니다.
> 


>
> **중요한 개념 위주로 정리되어 있습니다.**   
> 저는 이제 리액트를 공부하고 있기 때문에, 핵심 위주로 정리하고 있는 점 참고해주세요!


<br>

---

<br>
## 뭘 살펴볼 지 우선 살짝!

오늘은 이런 것들을 살펴봅니다.

>
> **React DevTools 로 디버깅하는 법**
> - Components 활용하기 
> - Profiler 활용하기
> 
> **Chrome DevTools 로 디버깅하는 법**
> - Elements 활용하기
> - Source 활용하기
> - Network 활용하기
> - Memory 활용하기
> - vm 인스턴스 확인하기
>



<br>

---

<br>

## 시작 전 기억해둬야 할 Point

> 평소 궁금했던 사이트를 직접 분석해보면서 어떻게 활용하면 좋을 지 익숙해져보세요!    
> 특히, `Chrome DevTools` 는 눈 감고도 쓸 줄 알아야 할 정도로 익숙해져야해요!


<br>

---

<br>



## 브라우저에서 React DevTools 설치하기
크롬, 파이어폭스, 엣지 브라우저를 지원하고 있습니다.   
본인이 주로 개발하는 브라우저에 설치해주세요.   
저는 크롬을 사용해서, 크롬에서 설치했습니다. 

아마.. 다들 크롬 사용하시겠죠?   
전 크롬 링크만 올려놓을게요. ㅎ_ㅎ;;

💁‍♀️ [Chrome React Developer Tools 설치하기](https://bit.ly/3GvX0Gn)  

<br>

설치하면 이렇게 보일거에요!

![설치하면 이렇게 보여요!]({{site.baseurl}}/assets/img/2023-12-06/plugin.png)

왼쪽에서 세번 째 녀석이 `React Developer Tools` 에요!   
사이트에서 리액트를 감지하면 활성화됩니다.   
옆에 있는 건 Vue 툴인데, 이것도 같이 깔아놓고 보다보면 재밌어요.   
보통 리액트나 뷰 둘 중 하나가 뾰롱~ 하고 보이는데,   
가끔 사이트 들어가면서 뭐가 뜰 지 맞춰보는 것도 나름 재밌습니다. ㅎ.ㅎ   

한 번 받아서 같이 써보세요! 

💁‍♀️ [Chrome Vue Developer Tools 설치하기](https://bit.ly/488anIJ)

<br>

---

## Components

자, 이제 개발자 도구를 켜고 살펴보면! `Components`와 `Profiler`라는 탭을 볼 수 있을거에요.   
안 보이면, 탭 옆에 조그맣게 화살표가 있는데요. 그걸 눌러서 보면 이렇게 보이실거에요.   

![리액트 개발자 도구 탭]({{site.baseurl}}/assets/img/2023-12-06/react-devtool-tap.png)

`Components` 를 눌러봅시다.   
책에선 넷플릭스로 살펴보셨는데, 전 배민 페이지를 봐볼게요!   
배민 페이지는 리액트가 감지되고, 우아한형제들 페이지는 뷰가 감지되더라구요 ㅎㅎ


클릭하면...

![Components 탭 클릭 시 화면]({{site.baseurl}}/assets/img/2023-12-06/components-tree.png){: width="" height="600"}

`컴포넌트의 트리 구조`를 살펴볼 수 있습니다!   

`기명 함수`로 선언된 컴포넌트는 컴포넌트명이 보이고,   
`익명 함수`로 선언된 컴포넌트는 `Anonymous`라는 이름으로 보여집니다.


![컴포넌트명 예시]({{site.baseurl}}/assets/img/2023-12-06/anonymous-example.png){: width="" height=""}

요기, `Anonymous` 보이시죠? 얜 익명 함수로 정의되었네요!   
고 밑에 다른 녀석들은 넵, 읽어보시면 아실 것 같네요 ㅎㅎ

<br>
### 익명 함수에 이름을 도저히 붙여줄 수 없다면

리액트 버전이 16.8 버전 이하라면, 익명 함수 명칭이 제대로 추론되지 않을 수 있어요.   
16.9 버전 이후부터는, 일부 해결되어 Anonymous 로 보이지 않고, 구분 가능하게 보인다고 합니다.   
그래도 구분 가능한 명칭을 붙여주면 좋을텐데요, `displayName`을 이용할 수 있다고 해요 !
```javascript
const SomeComponent = memo(function() {
  return <>SomeComponent</>
})

SomeComponent.displayName = 'SomeComponent 입니다~'

```

이렇게 해주면, Components 를 눌러서 트리 구조를 볼 때, 
제가 지정해 준 displayName으로 보입니다.   
그럼... `SomeComponent 입니다~` 가 보이겠네요 💃   

**다만, 개발 모드에서만 사용하는 걸 추천해요!**   
빌드될 때, 사용하지 않는 코드로 인식해서 삭제될 수도 있다고 합니다.   

<br>

### 컴포넌트명과 key

![컴포넌트명과 key 예시]({{site.baseurl}}/assets/img/2023-12-06/key-example.png){: width="" height=""}

여기 길게 늘어져 있는 건 컴포넌트의 `key 값` 이구요,   
옆에 짤려서 안 보이겠지만 컴포넌트명은 `tQ` 라고 나와 있어요.  

음.. 이게 익명 함수에 붙은거라기보단 뭔가 난독화 된 느낌이긴 한데, 어쨌든...   
컴포넌트명은 tQ 로 나와있습니다. ㅎㅎ

경고 표시가 떠있는 건, strict mode 로 실행되지 않았음을 의미한다고 합니다.

<br>


### 컴포넌트 도구
3개의 아이콘이 있을텐데요.

`눈 아이콘`은 클릭하면 해당 HTML 요소로 바로 이동돼요. Elements 탭으로 이동됩니다.   
`벌레 아이콘`은 클릭하면 `컴포넌트의 정보`를 `console`에 바로 찍어줍니다.   
`코드 아이콘`은 클릭하면 `그 컴포넌트의 소스코드`를 확인할 수 있어요.


요녀석들은 리액트로 만들어 진 사이트 한 번 들어가서 눌러보세요!   
소스코드 볼 때 밑에 `{} 아이콘`을 누르면 난독화 된 코드를 보기 좋게 정리해줍니다.

<br> 

---

<br>

### 이젠 props 를 봅시다!

오른쪽에는 이렇게 `props` 구조와 어떤 것으로 render 됐는 지 `rendered by`에 명시되어 있네요.   
`react-dom 의 버전을 확인`할 수 있는데요. 개발 모드에서는 부모 컴포넌트까지 확인할 수 있습니다.   

![props 구조를 보여주는 화면]({{site.baseurl}}/assets/img/2023-12-06/props-example.png){: width="" height=""}


`props`에서는 컴포넌트가 받은 `props`를 확인할 수 있는데요.   
`함수`도 포함되어 있습니다. 마우스 오른쪽을 클릭해서,   

- `Copy value to clipboard`로 props의 정보를 복사할 수도 있고,   
- `Store as global variable`로 `window.$r`에 정보를 담아줄 수도 있습니다.
- 값이 `함수`인 props 는 `Go to definition` 이 나오는데, 정의된 부분으로 이동됩니다.

전역변수로 저장하고, 콘솔에 $r로 찍어봤어요~

![variable 찍어보기]({{site.baseurl}}/assets/img/2023-12-06/global-example.png){: width="" height=""}

요렇게, props 를 좀 더 편하게 볼 수 있네요!

<br> 

### hook 정보도 볼 수 있어요

`hooks`에서 컴포넌트가 사용하고 있는 훅의 정보를 볼 수 있는데요.   
`useState`는 `State`로 `use가 생략`되어 나타납니다.

![hooks 살펴보기]({{site.baseurl}}/assets/img/2023-12-06/hook-example.png)

여기 State랑 Effect 가 있네요. Effect는 useEffect 겠네요 ㅎㅎ   

볼 수 있는 hook 들은 이러합니다.

> **State**: useState   
> **Reducer**: useReducer   
> **Context**: useContext   
> **Memo**: useMemo   
> **Callback**: useCallback   
> **Ref**: useRef   
> **id**: useId   
> **LayoutEffect**: useLayoutEffect   
> **Effect**: useEffect
>   
> **사용자 정의 훅**: 위에 해당하지 않는데 useXXX로 나온다면, 사용자 정의 훅

 
<br>

---

<br>


## Profiler
`컴포넌트 메뉴`가 `정적인 현재 리액트 컴포넌트 트리의 내용을 디버깅`한다면,   
`프로파일러`는 `리액트가 렌더링하는 과정에서 발생하는 일`을 확인합니다.

- 어떤 컴포넌트가 렌더링 됐는 지
- 몇 차례나 렌더링이 일어났는 지
- 어떤 작업이 오래 걸렸는지 

등을 `Profile` 해줍니다.

프로덕션에서 실행되는 애플리케이션엔 사용할 수 없습니다.   
렌더링에 필요한 내용을 기록하기 때문입니다.   

<br>

### Profiler 설정

> 1. 렌더링을 쉽게 보기 위해 **General > Highlight updates when components render 켜두기!**      
> 2. **Debugging > Hide logs during second render in Strict Mode** 를 끄는 건 선택   
> 🤔 strict mode 에선 useEffect에 작성한 console.log가 2번 찍히기도 하는데, 이걸 막고싶다면
> 
> 3. **Profiler > Record why each component rendered while profiling** 은 렌더링을 기록하니 개발할 땐 켜보자


### 예제 코드
길어서 두 장으로 잘려 있습니다! 


![프로파일링 실습 예제코드1]({{site.baseurl}}/assets/img/2023-12-06/profiler-code1.png){: width="" height=""}

![프로파일링 실습 예제코드2]({{site.baseurl}}/assets/img/2023-12-06/profiler-code2.png){: width="" height=""}

렌더링 되는 화면은 이러하네요 ㅎㅎ

![예제코드 렌더링 화면]({{site.baseurl}}/assets/img/2023-12-06/profiler-result.png){: width="" height=""}

<br>

---

<br>


## 프로파일링 탭을 파헤쳐보자

이건 제가 이미지로 간단하게 정리해봤어요!   
이 이미지면 충분합니다 ㅎㅎ

![프로파일링 메뉴 정리]({{site.baseurl}}/assets/img/2023-12-06/profiler-wrapup.jpg){: width="" height=""}


<br> 
### 렌더링 원인을 파악하고 수정하기

예제 코드에서 useEffect 내부의 `setTimeout 이 최초 렌더링 후 3초 뒤에 text 의 상태를 업데이트`할텐데요.   
`상태가 변경됐기 때문에 리렌더링`이 일어날겁니다. (예제 코드는 문제 있는 코드!)   

Flamegraph 로 프로파일링 해보면 이렇게 나와요. 

![프로파일링 Flamegraph 결과]({{site.baseurl}}/assets/img/2023-12-06/profile-flame.png){: width="" height=""}

2번 렌더링됐고, 문제의 두 번째 렌더링이 일어나는 원인은 `App`이라고 적혀있습니다.
`Committed at: 3s` 를 보면 최초 렌더링 되고 3초 후에 commit 된 게 있군요

`Components` 탭으로 넘어가서 살펴보면 State가 코드대로 `1000`으로 바뀌어 있는데요.
setTimeout을 지워주면 한 번만 렌더링 될 거에요. 

<br>

<div class="divider"></div>

### input에 값을 입력하면...
이제 input에 값을 와랄랄라 입력해볼텐데요.   
분석 결과는 이렇게 나왔네요.   

![프로파일링 Flamegraph 결과2 - 인풋 값 입력]({{site.baseurl}}/assets/img/2023-12-06/profile-input.png){: width="" height="600"}

<div class="divider"></div>
제가 입력한 대로 좌라라락 렌더링이 일어났죠?   
input에 값을 입력하면 text를 업데이트 해주는 데, `리액트는 상태가 변화되면?` **리렌더링하죠..**  
왜 입력값을 받는 녀석들은 다 컴포넌트화 하는 지 저도 좀 더 감이오네요..
이렇게 분리가 되었군요! 
<div class="divider"></div>

![컴포넌트 분리 후 코드 1]({{site.baseurl}}/assets/img/2023-12-06/profile-refactor1.png){: width="" height=""}

![컴포넌트 분리 후 코드 2]({{site.baseurl}}/assets/img/2023-12-06/profile-refactor2.png){: width="" height=""}


이제 다시 프로파일링해보면.. `App은 리렌더링 되지 않고`,   
`InputText 만 값을 입력할 때마다 리렌더링`이 되고 있어요.

![컴포넌트 분리 후 결과 1 - App]({{site.baseurl}}/assets/img/2023-12-06/refactor-result1.png){: width="400" height=""}

![컴포넌트 분리 후 결과 2 - InputText]({{site.baseurl}}/assets/img/2023-12-06/refactor-result2.png){: width="" height="500"}


**InputText 내부에 다른 컴포넌트가 있을 때도 한 번 볼까요?**   
copyright 문구를 보여주는 컴포넌트를 한 번 넣어봅시다.

![InputText 안에 또 다른 컴포넌트]({{site.baseurl}}/assets/img/2023-12-06/compo-in-compo.png){: width="" height=""}

**InputText 자체가 계속 리렌더링**되니까, `CopyrightComponent` 도 계속 렌더링 될 거에요.

![InputText 안에 또 다른 컴포넌트 profile 결과]({{site.baseurl}}/assets/img/2023-12-06/profile-compocompo.png){: width="" height=""}


요렇게 memo 로 감싸줍시다 :) 

```javascript
const CopyrightComponent = memo(function CopyrightComponent({
  text,
}: {
  text: string
}) {
  return <p>{text}</p>
})
```
<div class="divider"></div>

memo로 감싸주고 다시 profiler 를 돌리니까, CopyrightComponent 는 리렌더링되지 않았어요!

![memo로 CopyrightCompo 감싸준 결과]({{site.baseurl}}/assets/img/2023-12-06/memo-result.png){: width="" height=""}








<br> 




<br>

### 크롬 개발자도구는 곧 업데이트 예정...이었는데,   
예시를 좀 더 구체적으로 적어야 할 것 같아서   
좀 더 보완해와야 할 것 같아요!   
이것도 작성하면 링크드인에 올릴게요 :)

읽어주셔서 감사합니다..~!!
---













<br>
























