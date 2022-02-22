# passlib.context CryptContext
```
>>> from passlib.context import CryptContext
```
```
>>> pwd_context = CryptContext(schemes=['bcrypt'], deprecated = 'auto')
```
```
>>> pwd_context.hash('asdf1234')
```
```
>>> '$2b$12$GRsLdvQYxMxuQss2XDa0zevZhKSuYJKBVkx.neDUA8gp1CA5eWxyC'
```
[Ref](https://passlib.readthedocs.io/en/stable/narr/context-tutorial.html/)  
[Ref](https://passlib.readthedocs.io/en/stable/lib/passlib.context.html/)
