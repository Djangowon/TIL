# JavaScript on the browser
## The Document Object
* console에 document를 입력하면, 작성한 HTML을 가져올 수 있다.
* document는 브라우저에 존재하는 object
* console에 console.dir(document)를 호출해 보면, document.title이 HTML에서 정의한 title이랑 같다.
* JS에서 HTML document 객체로 부터 title을 가져올 수 있다.
* JS는 HTML에 접근하고 읽을 수 있게 설정되어 있다.
* js를 통해 html를 바꿀 수도 있다. document.title = "HO";
* 모든 것들은 document로부터 시작한다. web site를 의미하기 때문.
* document.body를 호출하면 body항목만 가지고 온다.

</br>

## HTML in JavaScript
* 브라우저에서 그냥 사용할 수 있는 'document'라는 object
* document의 함수 중에는 getElementById 라는 함수가 있는데, 이 함수가 HTML에서 id를 통해 element를 찾아준다.
* element를 찾고 나면, JS로 해당 HTML의 무엇이든 바꿀 수 있다.
    * ex. element의 innerText를 바꾼다던가 (title.innerText = "Got you!";)
    * id, className 등을 가져올 수 있음. (cosole.log(title.id);)

</br>

## Searching For Elements
* getElementsByClassName() : 많은 element를 가져올때 씀(array를 반환)
* getElementsByTagName() : name을 할당할 수 있음(array를 반환)
* querySelector : element를 CSS selector방식으로 검색할 수 있음 
    * (ex. h1:first-child)
        * 단 하나의 element를 return해줌
        * hello란 class 내부에 있는 h1을 가지고 올 수 있다(id도 가능함)
        * 첫번째 element만 가져옴
    * 조건에 맞는 세개 다 가져오고 싶으면 querySelectorAll
        * 세개의 h1이 들어있는 array를 가져다 줌
* querySelector("#hello); 와 getElementById("hello"); 는 같은 일을 하는 것임
    * 하지만 후자는 하위요소 가져오는 것을 못하므로 전자를 주로 사용

</br>

## Events
* 지금 js파일이 있기 때문에 js를 통해 html의 내용을 가져올 수 있는 거임
* document가 html이 js파일을 load하기 때문에 존재 → 그 다음에 browser가 우리가 document에 접근할 수 있게 해줌
    * element의 내부를 보고 싶으면 console.dir()
        * 기본적으로 object로 표시한 element를 보여줌(전부 js object임)
    * 그 element 중 앞에 on이 붙은 것들은 event임
* event: 어떤 행위를 하는 것
* 모든 event는 js가 listen할 수 있음
* eventListener : event를 listen함 → js에게 무슨 event를 listen하고 싶은 지 알려줘야 함
* title.addEventListener("click") : 누군가가 title을 click하는 것을 listen할 거임 → 무언가를 해줘야함

```JavaScript
const title = document.querySelector("div.hello:first-child h1");

function handleTitleClick(){
title.style.color = "blue";
}
title.addEventListener("click",handleTitleClick); 
```
* function이 js에게 넘겨주고 유저가 title을 click할 경우에 js가 실행버튼을 대신 눌러주길 바라는 것임( 직접 handleTitleClick(); 이렇게 하는 것이 아니라)
* 함수에서 () 이 두 괄호를 추가함으로써 실행버튼을 누를 수 있는 것

</br>

## Events part Two
* listen하고 싶은 event를 찾는 가장 좋은 방법은, 구글에 찾고 싶은 element의 이름, 예를들어 h1 html element mdn을 검색.
* 우리는 javascript의 element를 원하니, 링크에 Web APIs라는 문장이 포함된 페이지를 찾기 → 이건 JS관점의 HTML Heading Element란 의미
* 너무 복잡하면 element를 console.dir로 출력해서 on~ 이라고 적혀있는걸 사용하면 됨.

```JavaScript
function handleMouseEnter() {
title.innerText = "Mouse is here!"
}
function handleMouseLeave() {
title.innerText = "Mouse is gone!"
}
title.addEventListener("mouseenter", handleMouseEnter);
title.addEventListener("mouseleave", handleMouseLeave);
```

* 하지만 대부분의 경우에는 style은 CSS를 통해 변경되어야 함.

</br>

## More Events
```JavaScript
title.onclick = handleMouseEnter;
title.addEventListener(“mouseenter”, handleMouseEnter);
```
* 위에 두 코드는 동일하나 addEventListener를 선호하는 이유는 removeEventListener을 통해서 event listener을 제거할 수 있기 때문이다.

> document에서 body,head,title 은 중요해서 언제든  
> ex) document.body 로 가져올수있지만  
> div나 h1 등 element 들은 querySelector getElementById등으로 찾아야한다.  
> ex) document.querySelector(“h1”);

* window는 기본제공
```JavaScript
function handleWindowResize() {
    document.body.style.backgroundColor = "tomato";
}

function handleWindowCopy() {
    alert("copier!")
}

function handleWindowOffline() {
    alert("SOS no WIFI");
}

function handleWindowOnline() {
    alert("ALL GOOOD")
}

window.addEventListener("resize", handleWindowResize);
window.addEventListener("copy", handleWindowCopy);
window.addEventListener("offline", handleWindowOffline);
window.addEventListener("online", handleWindowOnline);
```
