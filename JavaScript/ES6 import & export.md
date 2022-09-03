# ES6 import & export

<br>
<br>

> React, Angular 등 사용할 때 또는 js파일 나눌 때 쓰는 import/export 문법

```html
<!--index.html-->
<script type="module">

    import a from '/library.js';
    
</script>
```

```javascript
//library.js
const a = 10;

export default a;
```

<br>
<br>

## export default 문법
* import 가져올 거 from '경로'
* export default 내보낼 거
* export default를 쓰면 import 할 때 이름 변경 가능함
* export default는 파일당 1회만 사용 가능

<br>
<br>

## export 문법
* 여러개를 내보낼 때 사용함
* import {가져올 것들} from '경로'
* export {내보낼 것들}

<br>

* export/import시 변수이름 똑같이 써야 함
```javascript
import {변수명} from '경로';
```
* 변수명을 변경하고 싶으면 as 문법
```javascript
import {변수 as 새변수명} From '경로';
```
* 모든 것을 다 import 해오는 * 문법
```javascript
import * as 변수들명 from '경로';
```


<br>
<br>


## Ref
https://codingapple.com/course/javascript-es6/
