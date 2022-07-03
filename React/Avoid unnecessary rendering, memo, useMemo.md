# Avoid unnecessary rendering, memo, useMemo

<br>

## 자식 컴포넌트 재렌더링 막기
* 부모 컴포넌트 안에 차일드 컴포넌트가 있을 때 부모가 재렌더링 되면 차일드도 재렌더링 됨
    * 원래 리액트가 이런 방식으로 동작함

* 이때 차일드가 렌더링이 느린 컴포넌트라면 성능저하의 원인이 됨 -> 렌더링 될 때마다 버벅일 것이기 때문

<br>


## memo
* memo는 꼭 필요할 때만 <Child>컴포넌트 재렌더링하는 함수
* memo로 재렌더링 오래 걸리는 컴포넌트 감싸놓으면 쓸데없는 재렌더링을 막을 수 있음
    

```js
const Child = memo(function () {
  console.log("재렌더링됨");
  return <div>자식임</div>;
});
```

## memo의 원리
* props가 변할 때만 재렌더링 해줌
* 그래서 memo 함수를 남발하면 안 좋음, 기존 props와 신규 props를 계속 비교해서 재렌더링 여부를 결정하기 때문 -> 성능저하
    * 즉, 꼭 필요한 무거운 컴포넌트에만 붙이는 게 좋다.
    
<br>
    

## memoization
> memoization이란 기존에 수행한 연산의 결과값을 어딘가에 저장해두고 동일한 입력이 들어오면 재활용하는 프로그래밍 기법을 말함  
> memoization을 절적히 적용하면 중복 연산을 피할 수 있기 때문에 메모리를 조금 더 쓰더라도 애플리케이션의 성능을 최적화할 수 있음
    

<br>
    

## useMemo
* 컴포넌트 렌더링시 1회만 실행해줌
* useEffect와 비슷한 문법, 디펜던시 넣기 가능
    
```js
const result = useMemo(() => {
    return 함수();
  }, []);
```

* useMemo & useEffect ?
    * 실행시점의 차이밖에 없음
    * useEffect는 html이 다 보여진 뒤에 실행되고, useMemo는 처음 렌더링 될 때 실행됨

<br>
    
    
## memo & useMemo
### 공통점
* React.memo와 useMemo 모두 props가 변하지 않으면(이전 props와 동일하면) 인자로 넘긴 함수는 재실행되지 않고, 이전의 메모이즈된 결과를 반환한다는 점에서 공통점이 있음

### 차이점
1. React.memo는 HOC, useMemo는 hook이다.
2. React.memo는 HOC이기 때문에 클래스형 컴포넌트, 함수형 컴포넌트 모두 사용 가능하지만, useMemo는 hook이기 때문에 오직 함수형 컴포넌트 안에서만 사용 가능함
    
<br>
    
    
## Ref
https://codingapple.com/course/react-basic/  
https://ko.reactjs.org/docs/hooks-reference.html#usememo  
https://www.daleseo.com/react-hooks-use-memo/  
https://sustainable-dev.tistory.com/137
