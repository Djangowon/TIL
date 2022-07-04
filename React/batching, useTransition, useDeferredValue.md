# batching, useTransition, useDeferredValue

<br>


### 기존의 React 17버전
* state 변경함수를 연달아서 3개 사용하면 재렌더링이 3번 되어야하지만, 마지막에 1회만 처리하는 재렌더링 방지기능 => batching 이라고 함  
* 이벤트 핸들러에서만 batching을 지원했고, promise, setTimeout, native 이벤트 핸들러 등에서는 batching이 되지 않았음
* 즉, ajax요청이나 setTimeout안에 state 변경함수가 있으면 batching이 일어나지 않았음

<br>
<br>

> React 18버전부터 추가된 기능 3가지
## 1. automatic batching
* Batching이란 React가 더 나은 성능을 위해 여러개의 state 업데이트를 한 번의 리렌더링으로 묶어서 진행하는 것
* 즉, 18버전 이후부터 state 변경함수가 어디 있던지 재렌더링은 마지막에 한 번만 됨
* automatic batching 되는 것이 싫고, state 변경함수 실행마다 재렌더링하고 싶으면 flushSync 사용하면 됨

<br>

### flushSync 
* state 업데이트 호출을 batching 대상에서 제외시킬 수 있음
* 간단하게 말하면 `async await`. 비동기적인 코드를 강제로 동기적으로 만들고 react에서 리렌더링을 강제하도록 함
* 성능을 크게 저하시킬 수 있음

```js
flushSync(() => {
  setCount(count + 1);
});
```

<br>
<br>

## 2. useTransition
* 렌더링 성능이 저하되는 컴포넌트에서 쓸 수 있음
* 오래 걸리는 부분을 감싸면 렌더링시 버벅이지 않게 해줌 -> 코드 실행시점만 조절해주는 원리
* 보통 isPending, startTransition 사용하는 문법
    * isPending: boolean; 
    * startTransition: callback을 받는 함수


```js
const [isPending, startTransition] = useTransition()   

startTransition(() => {
	setName(e.target.value)
})
```

### startTransition 동작원리
* 브라우저는 싱글스레드이기 때문에 동시작업을 못 하는데, 동시에 여러가지를 처리하려고 할 때 버벅이고 성능저하가 일어남
* startTransition은 startTransition 안에 있는 코드를 약간 늦게 처리함 -> 코드 시작을 뒤로 늦춰줌
* isPending은 startTransition 이 처리 중일 때 true로 변함
    * 아래 예시처럼 사용 가능


```js
isPending ? '로딩중' : (보여줄 거 보여줌)
```

<br>
<br>

## 3. useDeferredValue
* 특정 update를 지연시킬수 있음, 급하지 않은 트리를 리렌더링 하는 것을 지연하게 해줌
* 지연시킴으로써, 렌더링 순서제어가 가능
    * 디바운싱 / 쓰로틀링 기법과 유사하지만 timeout을 직접 지정할 필요 없이 리액트가 다른 급한 작업이 완료 되는 즉시 실행을 시킴
* 지연된 렌더링은 중단될 수 있고, 사용자의 입력을 방해하지 않음 


```js
let state = useDeferredValue(state) // 여기 넣은 state 값이 변동사항이 생기면 늦게 처리해줌
```

<br>
<br>

## Ref
https://codingapple.com/course/react-basic/  
https://nukw0n-dev.tistory.com/33  
https://yrnana.dev/post/2022-04-12-react-18  
https://velog.io/@katanazero86/React-18-%EC%97%90%EC%84%9C-%EB%8B%AC%EB%9D%BC%EC%A7%80%EB%8A%94%EC%A0%90  
https://kyounghwan01.github.io/blog/React/React18/flushsync/#%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%A9%E1%86%AF-%E1%84%8B%E1%85%A8%E1%84%89%E1%85%B5  
https://velog.io/@j_user0719/React-18%EC%9D%98-%EC%83%88%EB%A1%9C%EC%9A%B4-%EA%B8%B0%EB%8A%A5  
