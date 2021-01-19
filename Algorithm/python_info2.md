# 파이썬 문법
---------------------------------------

### 가변객체와 불변객체
: str,tuple,int는 불변객체 , list는 가변객체 이다.<br>
int,str과 달리 list는 값이 변형될 수 있다.<br>
이 말은 다른 변수가 참조하고 있을 때 그 변수의 값 또한 변경된다는 얘기다.

```Python
    >>> a = [1, 2, 3, 4, 5]
    >>> b = a
    >>> b
    [1, 2, 3, 4, 5]
    
    >>> a[2] = 4
    >>> a
    [1, 2, 3, 4, 5]
    
    >>> b 
    [1, 2, 3, 4, 5]

    # list는 mutable object이기 때문에 동일한 id주소값을 지니고 있다. (str,int와 다르다.)
    # 하지만  str, int 와 마찬가지로 변수에 새로운 값을 = 연산자를 통해 재할당할 시에는 메모리주소값 변경됨에 주의하자.
    >>>print(id(a),id(b),sep='\n')
    2885447916232
    2885447916232
```

C++,와 Python의 참조를 비교해보자.

```Python
    >>> a = 10
    >>> b = a
    >>> id(a), id(b)
    (140724329554608, 140724329554608)
    
    # b 변수의 새로운 객체 참조 (주의!: C++에서는 참조 변수에 값을 할당시 참조의 대상 또한 할당된 값으로 변경된다.)
    >>> b = 7
    
    # b = a를 통해 a와 b는 동일한 메모리 주소를 가졌지만, b = 7 로 b에 새로운 값을 할당하게 되면 더 이상 b변수는 a변수를 참조하지 않게 된다. 
    >>> a,id(a),id(b)
    (10, 140724329554608, 140724329554512)
```
### is 와 ==

> is는 id() 값을 비교하는 함수 

None은 널(null)로서 값 자체가 정의되어 있지 않으므로 ==로 비교가 불가능하다. 
따라서 is로만 비교가 가능하다.

```Python
    if a is None:
        pass
```

> == 는 값을 비교하는 연산자다.

```Python
    >>> a = [1, 2, 3]
    >>> a == a
    True
    >>> a == list(a)
    True
    >>> a is list(a)
    True
    >>> a is a
    True

    '''
    값은 동일하지만 list()로 한 번 더 묶어주면, 별도의 객체로 복사가 되고 다른 ID를 갖게 된다. 
    따라서 is는 False가 된다.
    '''
    >>> a is list(a)
    False

    '''
    copy.deepcopy()로 복사한 결과 또한 값은 같지만 ID는 다르기 때문에 ,
    == 로 비교시 True, is 로 비교시 False가 나온다.
    '''
    >>> a = [1, 2, 3]
    >>> a == copy.deepcopy(a)
    True
    >>> a is copy.deepcopy(a)
    False
```
## 리스트
: 파이썬의 리스트는 말 그대로 순서를 저장하는 시퀀스이자 변경 가능한 목록(Mutable List)을 의미한다.<br>
입력 순서가 유지되며, 내부적으로는 동적 배열로 구현되어 있다. <br>
다른 언어들은 동적배열에 삽입할 수 있는 자료형을 동일한 타입으로 제한하는 경우가 많은데 파이썬에서는 자유롭게 삽입할 수 있다.

|언어|동적배열|
|:--|:-:|
|**Python**|list()|
|**C++**|std::vector|
|**자바**|ArrayList|


|연산|시간복잡도|설명|
|:--|:-:|:--|
|len(a)|O(1)|전체 요소의 개수를 리턴한다.|
|a[i]|O(1)|인덱스 i의 요소를 가져온다.|
|a[i:j]|O(k)|i부터 j까지 슬라이스의 길이만큼인 k개의 요소를 가져온다. 이경우 객체 k개에 대한 조회가 필요하므로 O(k)이다.|
|elem ina|O(n)|elem요소가 존재하는지 확인한다. 처음부터 순차 탐색하므로 n마큼 시간이 소요된다.|
|a.count(elem)|O(n)|elem 요소의 개수를 리턴한다.|
|a.index(elem)|O(n)|elem 요소의 인덱스를 리턴한다.|
|a.append(elem)|O(1)|리스트 마지막에 elem요소를 추가한다.|
|a.pop()|O(1)|리스트 마지막 요소를 추출한다. 스택의 연산이다.|
|a.pop(0)|O(n)|리스트 첫 번째 요소를 추출한다. 큐의 연산이다. 이 경우전체 복사가 필요하므로 O(n)이다. 나중에 다시 살펴보겠지만 큐의 연산을 주로 사용한다면 리스트보다는 O(1)에 가능한 데크(deque)를 권장한다.|
|del a[i]|O(n)|i에 따라 다르다.최악의 경우 O(n)이다.|
|a.sort()|O(n logn)|정렬한다. 팀소트(Timsort)를 사용하며, 최선의 경우(On)에도 실행될 수 있다.|
|min(a), max(a)|O(n)|최솟값/최댓값을 계산하기 위해서는 전체를 선형탐색해야 한다.|
|a.reverse()|O(n)|뒤집는다. 리스트는 입력순서가 유지되므로 뒤집게 되면 순서가 반대가 된다.|

```Python
    # 선언방법 1
    a = list()
    # 선언방법 2
    a = []

    >>> a = [1, 2, 3]
    >>> a 
    [1, 2, 3]
    >>> a.append(4)
    >>> a
    [1, 2, 3, 4]

    >>> a.insert(3, 5)
    >>> a
    [1, 2, 3, 5, 4]

    # Python can append string or boolean to List
    >>> a.append('Hi')
    >>> a.append(True)
    >>> a
    [1, 2, 3, 5, 4, 'Hi', True]

    # Python 인덱스는 0 부터시작하며, 값을 꺼낼때는 인덱스 지정.
    >>> a[3]
    5

    # 마지막 인덱스는 제외 -> 1~2까지.
    >>> a[1:3]
    [2, 3]
    
    # 처음인 index 0부터 2까지.
    >>> a[:3]
    [1, 2, 3]

    # 4부터 index 끝까지
    >>> a[4:]
    [4, 'Hi', True]

    # 인덱스 1, 2, 3의 값
    >>> a[1:4]
    [2, 3, 5]
    
    '''
    인덱스 1, 3의 값 (1부터 3까지 2 건너띄어라.) 
    [a:b:c] a부터 b이전까지 c씩 건너띄운값 인덱스가져온다. 
    ''' 
    >>> a[1:4:2]  # -> 홀수 번째 인덱스의 값만 가져올 때 사용적용해볼 수 있다.

    # 존재하지 않는 인덱스를 조회할 경우 IndexError 발생
    >>> a[9]
    '''
    Traceback(most recent call last):
      File "<stdin>",line 1, in <module>
    IndexError: list index out of range
    '''

    # try 구문으로 에러에 대한 예외처리 할수있다.
    try:
        print(a[9])
    except IndexError:
        print('존재하지 않는 인덱스')
```


### 리스트 요소값 삭제

    - 인덱스로 삭제하기
    - 값으로 삭제하기

del 키워드를 사용하면 **인덱스의 위치에 있는 요소**를 삭제할 수 있다.
```Python
    >>> a
    [1, 2, 3, 5, 4, '안녕', True]
    # 리스트 a의 인덱스 1에 해당하는 값 2를 삭제한다.
    >>> del a[1]
    >>> a
    [1, 3, 5, 4, '안녕', True]
```


remove()함수를 사용하면 **값에 해당하는 요소**를 삭제할 수 있다.
```Python
    >>> a
    [1, 3, 5, 4, '안녕', True]
    # 해당 값인 3인 정수형 객체를 삭제한다.
    >>> a.remove(3)
    >>> a
    [1, 5, 4, '안녕', True]
```

pop() 함수를 사용하면 스택의 팝(pop) 연산처럼 추출로 처리된다.<br> 즉 삭제될 값을 리턴하고 삭제가 진행된다.
```Python
    >>> a
    [1, 5, 4, '안녕', True]
    # 리스트a의 인덱스 3에 위치한 값 '안녕'이 스택의 pop 연산처럼 추출해 리턴하고 삭제가 진행된다.
    >>> a.pop(3)
    '안녕'
    >>> a
    [1, 5, 4, True]
```

### 리스트의 특징

![python_list](https://user-images.githubusercontent.com/62383573/105075433-1ad69c80-5acd-11eb-9aca-6e52ee15497d.png)

파이썬의 리스트는 객체에 대한 포인터 목록을 관리하는 형태로 구현되어 있다.<br>
사실상 연결 리스트에 대한 포인터 목록을 배열 형태로 관리하고 있으며, 덕분에 배열과 연결 리스트를 합친 듯한 기능을 보인다.<br>
따라서 정수, 문자, 불리언 등 다양한 타입을 동시에 단일 리스트에서 관리 가능하다.<br>

각 자료형의 크기는 저마다 다르기 때문에 이들을 연속된 메모리에 구현할 수 없기에, 인덱스를 조회하는 데에도 모든 포인터의 위치를 찾아가서
타입 코드를 확인하고 값을 일일이 살펴봐야 하는 등 추가적인 작업이 필요하여, 속도 면에서 불리하다.



### Python 과 C의 연산차이 예
-------------------------------------

Python은 인터프리터 언어이다. 
    (인터프리터 언어: 소스 코드를 인터프리터를 통해 직접 바로 번역하고 실행하는 컴퓨터 프로그램으로 실행파일 존재하지않는다.) <br>
    ex) 자바스크립트, HTML, 액션스크립트, SQL, python, ruby 등..

C는 컴파일 언어이다. 
    (컴파일 언어 : 소스코드에서 컴파일러를 통해 컴퓨터 하드웨어가 알아들을 수 있는 기계어로 번역한 바이너리 파일 실행한다.) <br>
    ex) C, C++, JAVA, C# 등

-----------------------------------------------

Python 연산과 C 연산의 속도 차이발생을 예시로 알아보자.


```C
    int a = 1;
    int b = 2;
    int c = a + b;
```
C 덧셈
1. 1을 a에 할당
2. 2을 b에 할당
3. binary_add<int, int>(a,b) 호출 
4. 결과를 c에 할당


```Python
    a = 1
    b = 1
    c = a + b
```
파이썬 덧셈
1. a에 1을 할당
    1) a -> PyObject_HEAD -> typecode 정수 설정
    2) a -> val = 1 설정
2. b에 2를 할당
    1) b -> PyObject_HEAD -> typecode 정수 설정
    2) b -> val = 2 설정
3. binary_add(a,b) 호출
    1) a -> PyObject_HEAD 에서 typecode 찾기
    2) a는 정수형; 값 a->val
    3) b->PyObject_HEAD 에서 typecode 찾기
    4) b는 정수형; 값 b->val
    5) binary_add<int, int>(a->val, b->val) 호출
    6) 정수형 결과 값 result
4. 파이썬 개체 c 생성
    1) c -> PyObject_HEAD -> typecode 정수 설정
    2) c -> val에 result 설정 동적 타이핑은 모든 작업에 더 많은 단계가 있다는 포함되어있다는것을 의미한다. 
    이것이 숫자데이터에 관한 연산에서 C언어와 비교했을때 파이썬이 느린 가장 큰 이유다.

-------------------------------------------------------------------

## 딕셔너리
: 파이썬의 딕셔너리는 키/값 구조로 이뤄진 딕셔너리를 말한다. <br>
파이썬 3.7+ 에서 입력 순서가 유지되며, 내부적으로는 해시 테이블(Hash Table)로 구현되어 있다.

|언어|해시테이블|
|:--|:--|
|Python|dict()|
|C++|std::unordered_map|
|Java|HashMap|

파이썬의 딕셔너리는 해시할 수만 있다면 숫자뿐만 아니라, 문자, 집합까지 불변객체를 모두키로 사용할 수 있다.<br>
이 과정을 **해싱** 이라 하며, 해시 테이블을 이용해 자료를 저장한다.<br>
해시 테이블은 다양한 타입을 키로 지원하면서도 입력과 조회 모두 O(1)에 가능하다.

|연산|시간복잡도|설명|
|:--|:--|:--|
|len(a)|O(1)|요소의 개수를 리턴한다.|
|a[key]|O(1)|키를 조회하여 값을 리턴한다.|
|a[key] = value|O(1)|키/값을 삽입한다.|
|key in a|O(1)|딕셔너리에 키가 존재하는지 확인한다. -> True 또는 False 반환|

- 파이썬 3.7+ : 딕셔너리 입력 순서 유지하도록 개선. (내부적으로 인덱스 이용하도록 개선됨.)
- 파이썬 3.6+ : 딕셔너리 메모리 사용량 20% 감소하도록 개선.

파이썬 3.6이하에서 항상 입력 순서가 유지되는 **collections.OrderedDict()**를 비롯해,<br>
조회시 항상 디폴트 값을 생성해 키 오류를 방지하는 **collections.defaultdict()**,
요소의 값을 키로 하고 개수를 값 형태로 만들어 카운팅하는 **collections.Counter()** 등이 있다. 

```Python
    # 선언방법1
    >>> a = dict()
    # 선언방법2
    >>> a = {}

    >>> a = {'key1':'value1', 'key2':'value2'}
    >>> a
    {'key1':'value1', 'key2':'value2'}
    # key 값 과 value 삽입
    >>> a['key3'] = 'value3'
    >>> a
    {'key1':'value1', 'key2':'value2', 'key3':'value3'}

    # 딕셔너리 key를 지정하여 값 조회한다.
    >>> a['key1']
    'value1'
    # 없는 key를 조회할시 KeyError 발생. 
    >>> a['key4']
    ''' 
    ---------------------------------------------------------------------------
    KeyError                                  Traceback (most recent call last)
    <ipython-input-47-91c1e5997b2c> in <module>
    ----> 1 a['key4']
    KeyError: 'key4'
    '''
    # 예외처리 방법. -> 나중에 삽입하는 등 별도로 추가작업을 할 수 있어 유용하게 쓰인다.
    try:
        print(a['key4'])
    except KeyError:
        print('존재하지 않는 키')

    
    # 없는 값을 삭제하려고 할 경우도 KeyError 발생한다.
    >>> del a['key4']
    '''
    ---------------------------------------------------------------------------
    KeyError                                  Traceback (most recent call last)
    <ipython-input-49-11c368e79f18> in <module>
    ----> 1 del a['key4']

    KeyError: 'key4'
    '''

    # 예외처리 외에도 미리 확인하고 차후 작업 진행하는 방법 가능하다. 
    >>> 'key4' in a
    False
    >>>  if 'key4' in a:
    ...     print('Exists Key')
    ...  else:
    ...     print('Not Exists Key')
    Not Exists Key
    
    # for 반복문으로도 조회가능하다. itms() 메소드를 사용하면 키와 값을 각각 꺼내올 수 있다. 
    >>> for k,v in items():
    ...     print(k,v)
    ...
    key1 value1
    key2 value2
    key3 value3

    # 딕셔너리 삭제
    >>> del a['key1']
    >>> a
    {'key2': 'value2', 'key3': 'value3'}
```


### 딕셔너리 모듈

#### defaultdict 객체
:defaultdict 객체는 존재하지 않는 키를 조회할 경우 , 에러 메시지를 출력하는 대신 디폴트 값을 기준으로 해당 키에 대한 딕셔너리 아이템을 생성해준다.<br>
마찬가지로 실제로는 collections.defaultdict 클래스를 갖는다.

```Python
    
    >>> a = collections.defaultdict(int)
    >>> a['A'] = 5
    >>> a['B'] = 4
    >>> a
    defaultdict(<class 'int'>, {'A': 5, 'B': 4})

    # C는 존재하지 않는 Key지만 , defaultdict 객체는 에러 없이 바로 +1 연산이 가능하여 default인 0을 기준으로 자동생성 후 1을 더해 최종적으로 1이 생성된다.
    >>> a['C'] += 1
    >>> a
    defaultdict(<class 'int'>, {'A': 5, 'B': 4, 'C': 1})
```

#### Counter 객체
: Counter 객체는 아이템에 대한 개수를 계산해 딕셔너리로 리턴하며, 다음과 같이 사용한다.

```Python
    >>> a = [1, 2, 3, 4, 5, 5, 5, 6]
    >>> b = collections.Counter(a)
    # Counter 객체는 이처럼 key에는 값이, 값에는 해당 아이템의 개수가 들어간 딕셔너리를 생성한다.
    # 실제로는 다음과 같이 딕셔너리를 한 번 더 래핑(Wrapping)한 collections.Counter클래스를 갖는다.
    >>> b
    Counter({1: 1, 2: 1, 3: 1, 4: 1, 5: 3, 6: 1})

    >>> type(b)
    collections.Counter

    # Counter 객체에서 가장 빈도 수가 높은 요소 추출 -> most_common()을 사용하면 된다.
    # b라는 Counter 객체를 참조하는 변수를 이용해서 가장 빈도가 높은 2개의 요소를 추출하도록 했다.
    >>> b.most_common(2)
    [(5, 3), (6, 2)]
```

#### OrderedDict객체

3.6 이하에서는 해시 테이블을 이용한 자료형인 dict에서 입력 순서가 유지되지 않았다. <br>
3.7+ 부터는 dict 자료형에서 내장인덱스를 통해서 입력순서가 유지된다.<br>
따라서 더 이상 필요없으나 하위 호환성을 위해서 남겨졌다. (**코딩테스트시 버전 주의하도록 하자.**)

```Python
    >>> a = collections.OrderedDict({'banana': 3, 'apple': 4, 'pear': 1, 'orange': 2})
    >>> a
    OrderedDict([('banana', 3), ('apple', 4), ('pear', 1), ('orange', 2)])
```

### 타입선언 문법
```Python
    # 타입의 이름을 지정하여 선언하는 예.
    >>> a = list()
    >>> type(a)
    <class 'list'>

    # 기호를 통한 선언 예.
    >>> type([])
    <class 'list'>
    >>> type(())
    <class 'tuple'>
    >>> type({})
    <class 'dict'>
    >>> type({1})
    <class 'set'>
```
