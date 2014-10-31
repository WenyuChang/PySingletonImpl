PySingletonImpl
===============

Python Based Singleton Implementation

There are three ways to implement singleton with Python

* **Override** `__new__` **method. **
```python
 def __new__(cls, *args, **kwargs):
        if not cls.__instance:
            cls.__instance = super(Singleton, cls).__new__(cls, *args, **kwargs)
        return cls.__instance
```

* **Write a decorator which can be used before class.**
```python
def singleton_decorator(cls):
    instances = {}
    def get_instance():
        if cls not in instances:
            instances[cls] = cls()
        return instances[cls]
    return get_instance
```

* **Write a META type and override its** `__call__` **method**
```python
class SingletonType(type):
    def __call__(cls, *args, **kwargs):
        try:
            return cls.__instance
        except AttributeError:
            cls.__instance = super(SingletonType, cls).__call__(*args, **kwargs)
            return cls.__instance
```
