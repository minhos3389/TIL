# 파이썬 문법
![python_logo](https://user-images.githubusercontent.com/62383573/105018878-d88b6c00-5a88-11eb-835a-a04dab7af48a.png)
------------------------------------------------------------------------------------------------------------------------------------------------------------
### 인덴트
: 파이썬의 인덴트(Indent)는 공식 가이드인 PEP 8에 따라 공백 4칸을 원칙으로 한다.



### 네이밍 컨벤션
: 파이썬의 변수명 네이밍 컨벤션(Naming Convention)은 각 단어를 밑줄(_)로 구분하여 표기하는 스네이크 케이스(Snake Case)를 따른다.



### 타입힌트
: 파이썬은 동적 타이핑 언어임에도 , 타입을 지정할 수 있는 타입힌트(Type Hint)가 PEP484에서 추가되었다.<br>
가독성을 높이고 버그 발생확률을 줄일 수 있다.

```Python
def fn(a: int) -> bool:
    ...
```

fn()함수의 파라미터 a가 정수형임을 알 수 있고, 리턴 값으로 True 또는 False 를 리턴할 것이라는 점을 알 수 있게된다.<br>
물론 실제로는 강제 규약이 아니다 보니, 여전히 동적으로 할당될 수 있으므로 주의해야 한다.

mypy를 통해서 타입힌트에 오류가 있는지 자동 확인가능하다.

```Python
    $pip install mypy

    $mypy solution.py
```

타입힌트가 잘못 지정되면 Incompatible return value type 오류가 발생하므로 확인 후 수정할 수 있다.

### 리스트 컴프리헨션
:파이썬은 map,filter 와 같은 함수형 기능을 지원하며 다음과 같은 람다 표현식도 지원한다.

```Python
    >>> list(map(lamda x:x + 10,[1, 2, 3]))
    [11,12,13]
```

파이썬에서는 람다표현식에 map이나 filter를 섞어 사용하는 것보다 가독성이 높은 리스트 컴프리헨션을 지원한다.

```Python
    # 홀수인 경우 2를 곱해 출력하라는 리스트 컴프리헨션
    >>> [n*2 for n in range(1, 10 + 1) if n % 2 == 1]
    [2, 6, 10, 14, 18]
```

딕셔너리에서도 리스트 컴프리헨션 가능하다.

```Python
    a = {}
    for key, value in original.items():
        a[key] = value

    #  리스트 컴프리헨션 적용시
    a = {key: value for key, value in original.items()}
```

### 제너레이터(generator)
:제너레이터는 루프의 반복동작(Iteration)을 제어할 수 있는 루틴 형태를 말한다.


### range 
:제너레이터의 방식을 활용하는 대표적인 함수로 range()가 있다. 주로 for 문에서 쓰이는 range() 함수의 쓰임은 다음과 같다.

```Python
    >>> list(range(5))
    [0, 1, 2, 3, 4]
    
    >>> type(range(5))
    <class 'range'>

    >>> for i in range(5):
        print(i, end=' ')
    0 1 2 3 4
```
range()는 range클래스를 리턴하며, for 문에서 사용할 경우 내부적으로는 제너레이터의 next()를 호출하듯 매번 다음 숫자를 생성해낸다.<br>
버전 3부터 range()함수가 제너레이터 역할을 하는 range()클래스를 리턴하는 형태로 변경됐고 xrange() 함수는 사라졌다.

### enumerate
enumerate()는 '열거하다'는 뜻의 함수로, 순서가 있는 자료형(list, set, tuple등)을 인덱스를 포함한 enumerate객체로 리턴한다.

```Python
    a = [1,2,3,2,45,2,5]
    a 
    # [1, 2, 3, 2, 45 ,2, 5]
    
    enumerate(a)
    <enumerate object at 0x1010f83f0>
    >>> list(enumerate(a))
    [(0, 1), (1, 2), (2, 3), (3, 2), (4, 45), (5, 2), (6, 5)]
```

이처럼 list()로 결과를 추출할 수 있는데 , index를 자동으로 부여해주기 때문에 편리하게 사용된다.

### 나눗셈 연산자 
/ 는 나눗셈 연산자, // 는 정수형태의 몫(Quotient)를 구하는 Floor Division 기능을 수행한다. (수행시 type int형 반환)<br>
나머지는 %를 사용한다.

divmod() 함수를 사용하면 몫과 나머지를 동시에 구할 수 있다.
```Python
    >>>divmod(5, 3)
    (1, 2)
```




### print

```Python
    >>>print('A1', 'B2')
    A1 B2

    >>>print('A1', 'B2', sep=',')
    A1,B2

    >>>print('aa', end=' ')
    >>>print('bb')
    aa bb

    >>> a = ['A', 'B']
    >>>print(' '.join(a))
    A B

    >>> idx = 1
    >>> fruit = "Apple"
    >>> print('{0}: {1}'.format(idx + 1, fruit))
    2: Apple

    >>> print('{}: {}'.format(idx + 1, fruit))
    2: Apple

    # f-string을 사용하면 변수를 뒤에 별도로 부여할 필요도 없고 직관적이고 속도도 빠르다. (추천)
    # python 3.6+ 부터 지원한다.
    >>> print(f'{idx+1}:{fruit}')
    2: Apple
```

### pass 
pass는 널 연산(Null Operation)으로 아무것도 하지 않는 기능이다. <br>이처럼 아무 역할을 하지 않는 pass를 지정하면 , 인덴트 오류 같은 불필요한 오류를 방지할 수 있다.<br> pass는 먼저 목업(mockup)인터페이스부터 구현한 후 ,추후 구현을 진행할 수 있게하여 코딩 테스트시에도 유용하다.
```Python
    class Myclass(object):
        def method_a(self):
            # method_a()가 아무런 처리를 하지 않았음에도 pass를 통해서 오류 발생을 막을 수 있다.
            pass       

        def method_b(self):
            print("Method B")

    c = MyClass()
```

### locals
:locals()는 로컬 심볼 테이블딕셔너리를 가져오는 메소드로 업데이트또한 가능하다. ( global()은글로벌 심볼 테이블딕셔너리를 반환 )<br>
로컬에 선언된모든 변수를 조회할 수 있는 강력한명령이므로 디버깅에 도움이 된다.<br>
특히 로컬 스코프에 제한해 정보를 조회할 수 있어 클래스의특정메소드 내부에서나 함수 내부의 로컬정보를 조회해 잘못 선언한 부분이 없는지 확인하는 용도로 활용할 수 있다.<br>  변수명을 일일이 찾아낼 필요 없이로컬 스코프에 정의된 모든 변수를 출력하기 때문에 편리하다.

```Python
    # pprint로 출력하게 되면 보기좋게 줄바꿈처리해준다.
    import pprint
    pprint.pprint(locals())

    # 클래스 메소드내부의모든 로컬변수를 테이블딕셔너리 형태로 반환
    {'nums':[2, 6, 13, 15],
    'pprint': <module 'pprint' from '/usr/lib/python3.8/pprint.py'>,
    'self':<__main__.Solution object at 0x7f0994769d90>,
    'target':9
    }
```

### 코딩스타일
> [파이썬의 PEP 8](https://www.python.org/dev/peps/pep-0008/)
  [구글의파이썬 스타일가이드](http://google.github.io/styleguide/pyguide.html)

### 변수명과 주석
: 스네이크 케이스로 함수명과 변수명을 작성하고, 간단한 주석을 통해서 가독성을 높인다.<br>
변수명을 작성할 때는 의미를 부여하는 편이 가독성을 높이기에 추천

```Python
    # Example for CleanCode
    # LeetsCode에서 카멜표기법으로 작성된 함수명으로 변경하지 않았을뿐,  SnakeCode가 파이썬기본이다.
    def numMatchingSubseq(self, S:str, words:List[str])-> int:
        matched_count = 0
    
        for word in words:
            pos = 0
            for i in range(len(word)):
                # Find matching position for each character.
                found_pos = S[pos:].find(word[i])
                if found_pos < 0:
                    matched_count -= 1
                    break
                else:  # If found, take step position forward.
                    pos += found_pos + 1
            matched_count += 1
        
        return matched_count
```

### 리스트컴프리헨션
가독성이 떨어지지 않게 표현식이 2개를 넘지 않도록 하고 여러줄에 표시하지 않도록 한다.
```Python
# 리스트 컴프리헨션의 예시 (참고만 할것)
strls = [
    strl[i:i + 2].lower() for i in range(len(strl) - 1)
    if re.findall('[a-z]{2}',strl[i:i + 2].lower())
]
```

### 구글 파이썬 스타일 가이드
1. 함수의 기본 값으로 가변객체(Mutable Object)를 사용하지 않아야 한다. 함수가 객체를 수정하면 기본값이 변경되기 때문이다. <br>기본값으로 []나 {}를 사용하는 것은 지양해야 한다.<br>
불변 객체(Immutable object)를 사용한다. <br> None을 명시적으로 할당하는 것도 좋은 방법이다.
```Python
    # Bad Example
    No: def foo(a, b=[]):
            ...

    No: def foo(a, b: Mapping = {}):
            ...


    # Good Example
    Yes: def foo(a, b=None):
            if b is None:
                b = []

    Yes: def foo(a, b:Optional[Sequence] = None):
            if b is None:
                b = []
```

2. True, False를 판별할 때는 암시적(Implicit)인 방법을 사용하는 편이 간결하고 가독성이 좋다.
```Python

    Yes:
        #1 길이가 없다는 말은 값이 없다는 의미로 not users로 충분.
        if not users:
            print('no users')
        #2 비교 대상이 되는 정수값을 직접 비교하는 편이 덜 위험.
        if foo == 0:
            self.handle_zero()
        #3  명시적으로 값을 비교하는 편이 좋다.
        if i % 10 == 0:
            self.handle_multiple_of_ten()


    No:
        #1
        if len(users) == 0:
            print('no users')
        #2
        if foo is not None and not foo:
            self.handle_zero()
        #3
        if not i % 10:
            self.handle_multiple_of_ten()
```
3. 최대 줄 길이는 80자로 한다. (암묵적인 약속)

>파이썬 철학
    The Zen of Python, by Tim Peters

    Beautiful is better than ugly.
    Explicit is better than implicit.
    Simple is better than complex.
    Complex is better than complicated.
    Flat is better than nested.
    Sparse is better than dense.
    Readability counts.
    Special cases aren't special enough to break the rules.
    Although practicality beats purity.
    Errors should never pass silently.
    Unless explicitly silenced.
    In the face of ambiguity, refuse the temptation to guess.
    There should be one-- and preferably only one --obvious way to do it.
    Although that way may not be obvious at first unless you're Dutch.
    Now is better than never.
    Although never is often better than *right* now.
    If the implementation is hard to explain, it's a bad idea.
    If the implementation is easy to explain, it may be a good idea.
    Namespaces are one honking great idea -- let's do more of those!