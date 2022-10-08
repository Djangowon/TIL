# React Custom Hooks


<br>
<br>


* hooks는 react의 state machine에 연결하는 기본적인 방법임
* hooks가 생기기전에는 state를 함수형 컴포넌트에 사용할 수 없었음
* state를 사용하려면 this 키워드나 render()를 쓰는 어려운 문법의 클래스 컴포넌트 형태로 만들어야 했음

<br>
<br>


## 커스텀 훅 만들기
* 비슷한 로직이 여러 컴포넌트에서 쓰이는 경우에 커스텀 훅을 사용하면 중복되는 로직을 최소화할 수 있음


<br>
<br>


## useInput
```javascript
const useInput = (initialValue, validator) => {
    const [value, setValue] = useState(initialValue);
    const onChange = event => {
	    target: { value }
    } = event;
    let willUpdate = true;
    if (typeof validator === "function") {
    	willUpdate = validator(value);
    }
    if (willUpdate) {
    	setValue(value);
    }
    return { value, onChange };
};

const App = () => {
const maxLength = (value) => value.length <= 10;
    const name = useInput("Ex", maxLength);
    return (
    	<div className="App">
    		<h1>Hello</h1>
    		<input lpaceholder="Name" {...name} />
    	</div>
    );
};
```


<br>
<br>


## Ref
https://nomadcoders.co/react-hooks-introduction
