
<img src ="C:\Users\1\Desktop\python_image.jpg" width= "150px" alt="python_logo"></img>

# 파이썬 문법
------------------
> 인덴트
: 파이썬의 인덴트(Indent)는 공식 가이드인 PEP 8에 따라 공백 4칸을 원칙으로 한다.

> 네이밍 컨벤션
: 파이썬의 변수명 네이밍 컨벤션(Naming Convention)은 각 단어를 밑줄(_)로 구분하여 표기하는 스네이크 케이스(Snake Case)를 따른다.

### 타입힌트
: 파이썬은 동적 타이핑 언어임에도 , 타입을 지정할 수 있는 타입힌트(Type Hint)가 PEP484에서 추가되었다.
가독성을 높이고 버그 발생확률을 줄일 수 있다.

```

def fn(a: int) -> bool:
    ...

```
fn()함수의 파라미터 a가 정수형임을 알 수 있고, 리턴 값으로 True 또는 False 를 리턴할 것이라는 점을 알 수 있게된다.
물론 실제로는 강제 규약이 아니다 보니, 여전히 동적으로 할당될 수 있으므로 주의해야 한다.

mypy를 통해서 타입힌트에 오류가 있는지 자동 확인가능하다.
```
    $ pip install mypy

    $ mypy solution.py

```
타입힌트가 잘못 지정되면 Incompatible return value type 오류가 발생하므로 확인 후 수정할 수 있다.

### 리스트 컴프리헨션
:파이썬은 map,filter 와 같은 함수형 기능을 지원하며 다음과 같은 람다 표현식도 지원한다.

```
    >>> list(map(lamda x:x + 10,[1, 2, 3]))
    [11,12,13]

```

파이썬에서는 람다표현식에 map이나 filter를 섞어 사용하는 것보다 가독성이 높은 리스트 컴프리헨션을 지원한다.
```
    // 홀수인 경우 2를 곱해 출력하라는 리스트 컴프리헨션
    >>> [n*2 for n in range(1, 10 + 1) if n % 2 == 1]
    [2, 6, 10, 14, 18]
```

딕셔너리에서도 리스트 컴프리헨션 가능하다.
```
    a = {}
    for key, value in original.items():
        a[key] = value

    // 리스트 컴프리헨션 적용시
    a = {key: value for key, value in original.items()}
```

### 제너레이터(generator)
:제너레이터는 루프의 반복동작(Iteration)을 제어할 수 있는 루틴 형태를 말한다.


### range 
:제너레이터의 방식을 활용하는 대표적인 함수로 range()가 있다. 주로 for 문에서 쓰이는 range() 함수의 쓰임은 다음과 같다.

```
    >>> list(range(5))
    [0, 1, 2, 3, 4]
    
    >>> type(range(5))
    <class 'range'>

    >>> for i in range(5):
        print(i, end=' ')
    
    0 1 2 3 4

```
range()는 range클래스를 리턴하며, for 문에서 사용할 경우 내부적으로는 제너레이터의 next()를 호출하듯 매번 다음 숫자를 생성해낸다.
버전 3부터 range()함수가 제너레이터 역할을 하는 range()클래스를 리턴하는 형태로 변경됐고 xrange() 함수는 사라졌다.

### enumerate
enumerate()는 '열거하다'는 뜻의 함수로, 순서가 있는 자료형(list, set, tuple등)을 인덱스를 포함한 enumerate객체로 리턴한다.

```
    >>>a = [1,2,3,2,45,2,5]
    >>>a 
    [1, 2, 3, 2, 45 ,2, 5]
    >>>enumerate(a)
    <enumerate object at 0x1010f83f0>
    >>>list(enumerate(a))
    [(0, 1), (1, 2), (2, 3), (3, 2), (4, 45), (5, 2), (6, 5)]
```

이처럼 list()로 결과를 추출할 수 있는데 , index를 자동으로 부여해주기 때문에 편리하게 사용된다.