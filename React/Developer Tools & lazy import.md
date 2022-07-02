# Developer Tools & lazy import


<br>


> props를 보냈는데 출력이 안 될 때? 코드를 확인하거나 개발자도구 보면 됨


## React Developer Tools

### Components Tab
* 개발자도구에서 components 탭  
    * 디버깅, 버그 찾기에 편리
    * 어떤 컴포넌트인지 알려주고, 특히 props를 다 출력해주기 때문에 유용함
    * state 확인 가능

* <> 누르면 소스코드 확인
    * 어떤 파일에 몇 번째에 있는지 알려줌


### Profiler Tab
* Profiler 탭
    * 성능 저하되는 컴포넌트 범인찾는 탭
    * 녹화버튼 눌러서 여러 컴포넌트 테스트 해본 후, 녹화가 끝나면 내가 했던 액션들을 bar 들을 생성해서 보여줌
    * 몇 초에 걸쳐서 렌더링 됐는지 렌더링 속도 보여줌

* 보통 0.x ms 인데, 보통은 렌더링 속도 걱정할 필요가 없음. 대부분의 지연시간은 서버에서 데이터 늦게와서 그렇기 때문에

<br>

## Redux Devtools
* Redux Tab
    * store 한눈에 보여줌
    * state 변경한 내역 알려줌


## lazy import

리액트로 개발한 사이트들은 기본적으로 single page application임

### single page application 특징
* 발행하면 js파일 하나에 모든 코드를 다 쑤셔넣기 때문에 사이즈가 매우 클 수 밖에 없음
* 보통 유저가 메인페이지 접속하면, 1. html파일 2. css파일 3. 큰 js파일 을 다운받기 때문에 기본적으로 로딩속도가 좀 느림
    * 이것을 잘게 분할하고 싶을 때 lazy import 쓰면 가능

```js
import { lazy } from 'react';

const Detail = lazy(() => import('/routes/Detail.js'));  
```
* lazy import 한 코드는 사이트를 발행할 때도 별도의 js 파일로 분리됨
* 단점은?
    * Detail 컴포넌트 로딩 시간 발생, 즉, 컴포넌트를 로드되기 전까지 하얀화면을 봐야된단 소리임 -> 로딩되는 시간동안 로딩바 같은 거 띄워주고 싶으면 Suspense 사용

```js
import { Suspense } from 'react';

<Suspense fallback={<div>로딩중임</div>} // Suspense로 감싸면 로딩 중 UI 넣기 가능
	<Detail />
</Suspense>
```
> 보통 route 안에 있는 모든 컴포넌트를 lazy 로드하도록 하기 때문에 <Suspense>로 <Routes> 전체를 감싸도 된다.
    
결론: 기능구현을 다했으면 성능개선이다~
    
<br>
    
## Ref
https://codingapple.com/course/react-basic/  
https://ko.reactjs.org/docs/react-api.html#reactsuspense  
https://ko.reactjs.org/docs/concurrent-mode-suspense.html
