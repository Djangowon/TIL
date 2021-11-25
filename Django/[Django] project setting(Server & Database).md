# Django project setting(Server & Database)
#### 가상환경 생성
```python
conda create -n '가상환경 이름' python=3.8
conda activate '가상환경 이름'
```
#### Database 생성
```python
$ mycli -u root -p

mycli > create database '데이터 베이스 이름' character set utf8mb4 collate utf8mb4_general_ci;
```
#### Project Python Package 설치
```python
$ pip install django
$ pip install mysqlclient
$ pip install PyMySQL
  (M1 사용할 경우)
$ pip install django-cors-headers
```
#### Django Project 생성
```python
$ django-admin startproject '프로젝트 이름'
$ cd '프로젝트 이름'
```
#### Settings.py 설정
* IP 허용
```
ALLOWED_HOSTS = ['*']
```
* 주석처리 (admin, csrf, auth) & corsheaders
```python
INSTALLED_APPS = [
    #'django.contrib.admin',
    #'django.contrib.auth',
    'corsheaders', #추가
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]

MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware', #추가
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    #'django.middleware.csrf.CsrfViewMiddleware',
    #'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

##CORS 추가 설정
CORS_ORIGIN_ALLOW_ALL = True
CORS_ALLOW_CREDENTIALS = True

CORS_ALLOW_METHODS = (
    'DELETE',
    'GET',
    'OPTIONS',
    'PATCH',
    'POST',
    'PUT',
)

CORS_ALLOW_HEADERS = (
    'accept',
    'accept-encoding',
    'authorization',
    'content-type',
    'dnt',
    'origin',
    'user-agent',
    'x-csrftoken',
    'x-requested-with',
)
```
* '/' 관련 에러 제거
```
APPEND_SLASH     = False
```
#### project urls.py 수정
```
from django.urls import path

urlpatterns = [
]
```
#### my_settings.py 생성(DATABASES, SECRET_KEY)
```python
cd '생성한 프로젝트 폴더명'
touch my_settings.py
```
```python
DATABASES = {
    'default' : {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'DATABASE 명',
        'USER': 'DB접속 계정명',
        'PASSWORD': 'DB접속용 비밀번호',
        'HOST': '127.0.0.1',
        'PORT': '3306',
				'OPTIONS': {'charset': 'utf8mb4'}
    }
}

SECRET_KEY = '시크릿키'
```

#### settings.py <-> my_settings.py 연동
```python
from pathlib        import Path #기존에 settings.py 에 있는 코드
from my_settings    import DATABASES, SECRET_KEY

import pymysql

pymysql.install_as_MySQLdb()

...

DATABASES = DATABASES

SECRET_KEY = SECRET_KEY
```
```python
python manage.py runserver
```
## Git & Github
#### git 초기화
```python
git init
```
#### .gitignore 생성
python, pycharm, VisualStudioCode, vim, macOS, Linux, zsh
[gitignore.io](https://www.toptal.com/developers/gitignore/api/python,pycharm,visualstudiocode,vim,macos,linux,zsh/)
```python
cd '프로젝트 폴더명'
touch .gitignore
vi .gitignore

############################
# gitignore.io 결과 전체 복사 #
############################

# 가장 하단 my_settings.py 추가
```
```python
git add .
git commit -m "Add: Django Project Setting"
```
## Branch
#### Branch 생성
```python
git branch 브랜치 이름 # 브랜치 생성
git checkout 브랜치 이름 # 해당 브랜치로 이동 

# 생성과 동시에 이동하는 방법
git checkout -b 브랜치 이름
```
#### App 생성
```python
$ python manage.py startapp products
```
settings.py installed_apps 에 app 추가 
```python
INSTALLED_APPS = [
	...
	'products', 
```
```python
#### Github push
```python
git add .
git commit -m "Add: products application"
```
```python
git push origin "브랜치 이름"
```
