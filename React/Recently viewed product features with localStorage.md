# Recently viewed product features with localStorage

<br>

## localStorage와 sessionStorage
웹 스토리지 객체(web storage object)인 localStorage와 sessionStorage는 브라우저 내에 key-value 쌍을 저장할 수 있게 해준다.

## localStorage
* localStorage는 key: value 형태로 저장 가능함
* 최대 5mb까지 문자만 저장가능(only string)
* 유저가 브라우저 청소하지 않는 이상 영구적으로 남아있음(사이트 재접속해도)

## sessionStorage
* sessionStorage도 마찬가지, key: value 형태로 저장 가능함
* 브라우저 끄면 날아감(휘발성)

## method
* 두 스토리지 객체는 동일한 메서드와 프로퍼티를 제공한다.
    * setItem(key, value) – 키-값 쌍을 보관  
    * getItem(key) – 키에 해당하는 값을 꺼내옴  
    * removeItem(key) – 키와 해당 값을 삭제  
    * clear() – 모든 것을 삭제  
    * key(index) – 인덱스(index)에 해당하는 키를 꺼내옴  
    * length – 저장된 항목의 개수


<br>


## Example
꺼내서 수정 한번에 하는 문법은 없음, 꺼내서 수정하고 집어넣으면 된다.
```js
useEffect(() => {
    let getProduct = localStorage.getItem("watched");
    getProduct = JSON.parse(getProduct);
    getProduct.push(findProduct.id);
    localStorage.setItem("watched", JSON.stringify(getProduct));
  }, []);
```

* string만 저장이 된다고 했는데, array/object 를 저장하려면? -> JSON으로 바꾸면 됨
    * object를 그냥 넣게 되면 object 자료가 깨짐, Object object 이런 식으로

* JSON 변환하는 JavaScript문법
    ```js
    JSON.stringify(object)
    ```
* JSON은 문자이기 때문에 . 문법을 쓸 수 없음  
* 그래서, JSON 에서 obj 변환하는 문법
    ```js
    JSON.parse()
    ```
    
array에서 중복제거 쉽게 하려면 SET 자료형을 사용하자
array -> set -> array
```js
useEffect(() => {
    let getProduct = localStorage.getItem("watched");
    getProduct = JSON.parse(getProduct);
    getProduct.push(findProduct.id);
    getProduct = new Set(getProduct);
    getProduct = Array.from(getProduct);
    localStorage.setItem("watched", JSON.stringify(getProduct));
  }, []);
```

<br>


* 모든 state를 로컬스토리지에 자동저장하려면?
    * redux-persist
        * 리덕스 스토어 안에 있던 state들을 로컬스토리지에 자동으로 저장해 줄 수 있음


<br>


## Differences from cookies
* 쿠키과 다르게 웹 스토리지 객체는 네트워크 요청 시 서버로 전송되지 않음. 이런 특징때문에 쿠키보다 더 많은 자료 보관 가능함
* 서버가 HTTP 헤더를 통해 스토리지 객체를 조작할 수 없음, 웹 스토리지 객체 조작은 모두 자바스크립트 내에서 수행된다.
* 웹 스토리지 객체는 도메인·프로토콜·포트로 정의되는 오리진(origin)에 묶여있다. 따라서 프로토ㅗㄹ과 서브 도메인이 다르면 데이터에 접근 불가능함


<br>


## Ref
https://codingapple.com/course/react-basic/  
https://ko.javascript.info/localstorage
