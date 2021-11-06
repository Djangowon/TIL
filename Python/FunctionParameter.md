# Function Parameters
## Function Parameters
함수는 input parameter를 받아서 return 값을 output으로 리턴한다.  
그리고 함수를 호출할 때 parameter를 함수에 건내주어서(pass) 호출한다.  
함수의 parameter에는 여러 형태가 있으며, 가장 기본적인 형태는 순서대로 값이 parameter로 함수에 전해지는 경우이다.  
```python
def love_you(my_name, your_name):
    print(f"{my_name} loves {your_name}")

love_you("조이", "이즈리얼")

#조이 loves 이즈리얼
```
## Keyword Arguments
순서 대신에 parameter 이름으로 맞추어서 값을 전해줄 수 있다.  
keyword arguments 방식으로 parameter 값을 전해주면 실제 parameter 순서가 바뀌어도 상관없다.  
기본적인 형태로 parameter 순서에 맞추어 값을 함수에 넘기는 경우, 실수로 값이 바뀌어도 알기가 힘들다는 단점이 있는데,  
keyword arguments는 parameter 이름에 맞추어서 값을 함수에 넘기기 때문에 실수로 값이 바뀔 확률이 상대적으로 적다.  
또한, 코드를 읽는 사람도 어떠한 값을 넘기는 건지 명확하게 알 수 있기 때문에 가독성도 높아진다.  
```python
def love_you(my_name, your_name):
    print(f"{my_name} loves {your_name}")

love_you(your_name="이즈리얼", my_name="조이")

#조이 loves 이즈리얼
```
## Mixing positional arguments and keyword arguments
순서를 맞추어서 parameter 값을 전해주는 positional arguments와 keyword arguments를 혼용하여 사용하는 것도 가능.
#### 주의할 점 :heavy_check_mark: 
keyword arguments는 순서가 바뀌어도 상관없지만 positional arguments 부분은 순서를 지켜줘야 함.
```python
def love_you(my_name, your_name):
    print(f"{my_name} loves {your_name}")

love_you(your_name="이즈리얼", "조이")

#  File "main.py", line 4
#    love_you(your_name="이즈리얼", "조이")
#                                       ^
#SyntaxError: positional argument follows keyword argument
```
위에 작성된 코드가 error가 난 이유는 keyword arguments가 positional argument보다 더 앞으로 위치되어 함수가 호출되었기 때문이다.
positional arguments는 순서를 지켜줘야 하는데 순서가 틀렸기 때문.

## Parameter Default Value
함수의 parameter에 default 값을 정의해 줄 수 있다.  
Default 값이 정의된 paramter는 함수가 호출될 때 값이 넘겨지 않아도 괜찮은데,  
이유는 값이 넘겨지 않은 경우 default 값이 자동으로 넘겨지게 되기 때문이다.
#### 주의할 점 :heavy_check_mark: 
반대로, default 값이 정의된 parameter가 default 값이 정의 되지 않은 parameter보다 먼저 위치해 있으면 안된다.  
만일 default value parameter를 non-default value parameter 앞에 선언하면 syntax error가 난다.
```python
def love_you(my_name = "조이", your_name):
    print(f"{my_name} loves {your_name}")
    
#  File "main.py", line 1
#    def love_you(my_name = "조이", your_name):
#                 ^
#SyntaxError: non-default argument follows default argument
```
## default value parameter를 non-default value parameter 앞에 정의하면 안 되는 이유
dafault value parameter가 있으면 실제 parameter의 개수보다 적은 parameter를 입력하게 된다. 이 때 비어있는 non-default value parameter에 값이 순차적으로 입력하게 되는데, 정의되는 순서없이 무작위로 입력시 함수는 어떤 parameter에 어떤 값을 받아야 할 지 정할 수 없기 때문이라 생각한다. 또는, 위에 SyntaxError가 난 코드를 예로 들어보자면, my_name은 default값이 정의되었기 때문에 함수 호출시 한 개의 parameter를 받으면 되고 받은 한 개의 parameter를 순차적으로 입력하려는데 이미 default 값이 있는 my_name이 먼저 나오게 되니 error가 나는 것이 아닐까. 그렇기 때문에 default value parameter는 가장 끝에 위치하고 non-default value parameter를 처음부터 순차적으로 인식하는 구조로 되어있는 방식이라면 error가 나지 않는 것이다.

