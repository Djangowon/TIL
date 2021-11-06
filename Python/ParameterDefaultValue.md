# Parameter Default Value
함수의 parameter에 default 값을 정의해 줄 수 있다.  
Default 값이 정의된 paramter는 함수가 호출될 때 값이 넘겨지 않아도 괜찮은데,  
이유는 값이 넘겨지 않은 경우 default 값이 자동으로 넘겨지게 되기 때문이다.
#### 주의할 점 :heavy_check_mark: 
반대로, default 값이 정의된 parameter가 default 값이 정의 되지 않은 parameter보다 먼저 위치해 있으면 안된다.  
만일 default value parameter를 non-default value parameter 앞에 선언하면 syntax error가 난다.
```python
def love_you(my_name = "조이", your_name):
    print(f"{my_name} loves {your_name}")
    
#SyntaxError: non-default argument follows default argument
```
## default value parameter를 non-default value parameter 앞에 정의하면 안 되는 이유
dafault value parameter가 있으면 실제 parameter의 개수보다 적은 parameter를 입력하게 된다. 이 때 비어있는 non-default value parameter에 값이 순차적으로 입력하게 되는데, 정의되는 순서없이 무작위로 입력시 함수는 어떤 parameter에 어떤 값을 받아야 할 지 정할 수 없기 때문이라 생각한다. 또는, 위에 SyntaxError가 난 코드를 예로 들어보자면, my_name은 default값이 정의되었기 때문에 함수 호출시 한 개의 parameter를 받으면 되고 받은 한 개의 parameter를 순차적으로 입력하려는데 이미 default 값이 있는 my_name이 먼저 나오게 되니 error가 나는 것이 아닐까. 그렇기 때문에 default value parameter는 가장 끝에 위치하고 non-default value parameter를 처음부터 순차적으로 인식하는 구조로 되어있는 방식이라면 error가 나지 않는 것이다.

