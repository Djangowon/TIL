# If real-time data is important, react-query

<br>

## React-Query
* React Query는 React 애플리케이션에서 서버 상태를 가져오고, 캐싱하고, 동기화하고, 업데이트하는 작업을 쉽게 만듬

* ajax 요청을 하다보면 가끔가다 필요한 기능들
    * 몇 초마다 자동으로 데이터 다시 가져오기
    * 요청 실패할 경우 몇 초 간격으로 재요청 하기
    * 다음 페이지 미리 가져오기
    * ajax 성공/실패 시 각각 다른 html 보여주기

* 즉, 실시간 데이터를 계속 가져와야하는 사이트들이 쓰면 좋다. ex) 실시간 sns, 코인거래소 등


<br>

## Advantages
1. react-query 이용해서 ajax 요청하면 성공/실패/로딩 중 등등 쉽게 파악이 가능함(쌩 리액트는 state 만들어줘야)

```
data: {name: 'Mark', email: 'mark123@gmail.com'}
dataUpdatedAt: 1656694418674
error: null
errorUpdateCount: 0
errorUpdatedAt: 0
failureCount: 0
isError: false
isFetched: true
isFetchedAfterMount: true
isFetching: false
isIdle: false
isLoading: false
isLoadingError: false
isPlaceholderData: false
isPreviousData: false
isRefetchError: false
isRefetching: false
isStale: true
isSuccess: true
refetch: ƒ ()
remove: ƒ ()
status: "success"
```

2. 틈만나면 자동으로 재요청해줌
    * refetch되는 간격이 너무 잦다면? {stateTime: 2000} 이런 타이머 기능
    * 자동 refetch도 끌 수 있음


3. 실패시 알아서 retry 해줌
    * refetchOnWindowFocus: false
        * 재실행 여부 옵션, react-query는 사용자가 사용하는 윈도우가 다른 곳을 갔다가 다시 화면으로 돌아오면 이 함수를 재실행함
    * retry: 0
        * 실패시 재호출 몇 번 할지

4. state 공유 안해도 됨
    * react-query는 똑같은 곳으로 요청을 두번하지 않음. 즉, react-query는 똑똑해서 요청 알아서 하나만 해준다.


5. ajax 결과 캐싱기능
    * 12시 13분에 GET요청을 했다고 가정했을 때, react-query가 12시 10분 결과를 우선적으로 보여주고, 그 뒤에 GET 요청을 함
    * 즉, 이전에 성공한 결과부터 보여주고 GET요청 시작하니까 더 빠른 느낌을 줄 수 있음

<br>

> redux toolkit 설치하면 RTK Query 도 자동 설치되는데 react-query랑 유사함  
> but, 문법이 좀 드러우니까 react-query 쓰는 걸 추천

<br>

## Ref
https://codingapple.com/course/react-basic/  
https://react-query.tanstack.com/overview  
https://kyounghwan01.github.io/blog/React/react-query/basic/
