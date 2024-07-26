# data-science

파이썬 데이터 사이언스 핸드북을 보고 따라하기

# 1장

## ?의 사용법

- `?`는 객체에 대한 도움말을 제공한다

```python
def square(a):
    """a의 제곱을 반환"""
    return a ** 2

```

- 이 함수에 대한 독스트링을 ipython shell에서 확인하면 다음과 같이 나온다.

```bash
 In [5]: square?
Signature: square(a)
Docstring: a의 제곱을 반환
File:      c:\users\dlwhd\pycharmprojects\data-science\<ipython-input-4-f16edf4dd406>
Type:      function


# 객체 자체에 대해서도 객체 타입에 대한 문서를 제공한다.
In [8]: L = [1, 2, 3]

In [9]: L.insert?
Signature: L.insert(index, object, /)
Docstring: Insert object before index.
Type:      builtin_function_or_method

In [10]: L?
Type:        list
String form: [1, 2, 3]
Length:      3
Docstring:
Built-in mutable sequence.


```

## ??로 소스코드에 접근하기

- 간단한 함수의 경우 `??`를 통해 소스코드에 접근하여 구현 세부사항을 살펴 볼 수 있다.

```bash
 In [11]: square??
Signature: square(a)
Source:
def square(a):
    """a의 제곱을 반환"""
    return a**2
File:      c:\users\dlwhd\pycharmprojects\data-science\<ipython-input-4-f16edf4dd406>
Type:      function


In [12]: len??
Signature: len(obj, /)
Docstring: Return the number of items in a container.
Type:      builtin_function_or_method

```

- 가끔 ?? 접미사가 떄때로 소스코드를 보여주지 않는 것은 객체가 파이썬에서 구현된 것이 아니라 C나 다른 확장 언어로 구현됐기 때문이다.

## 탭을 통한 자동 완성

### 와일드 카드 매칭

- 단어의 중간이나 마지막 글자로 매칭하고 싶다면 `*` 문자를 이용해 와일드 카드 먀칭 방법이 있다.

```bash
# Warning으로 끝나는 모든 객체를 나열하기

In [13]: *Warning?
BytesWarning
DeprecationWarning
EncodingWarning
FutureWarning
ImportWarning
PendingDeprecationWarning
ResourceWarning
RuntimeWarning
SyntaxWarning
UnicodeWarning

# find가 포함된 문자열 메서드를 찾을 때

In [14]: str.*find*?
str.find
str.rfind

```

## 텍스트 입력 단축키

| 키 입력     | 동작                                |
|----------|-----------------------------------|
| 백스페이스 키  | 그 줄의 이전 문자 삭제                     |
| ctrl + d | 그 줄의 다음 문자 삭제                     |
| ctrl + k | 현재 커서 위치에서 그 줄 마지막까지 텍스트를 잘라냄(유용) |
| ctrl + u | 그 줄의 처음부터 현재 커서 위치까지 텍스트를 잘라냄     |
| ctrl + y | 이전에 잘라낸 텍스트를 끌어당김(yank, 즉 붙여넣기함)  |
| ctrl + t | 앞의 두 글자의 위치를 바꿈                   |

## 명령어 이력 단축키

| 키 입력     | 동작              |
|----------|-----------------|
| ctrl + p | 이력에서 이전 명령어에 접근 |
| ctrl + n | 이력에서 다음 명령어에 접근 |
| ctrl + r | 명령어 이력을 역탐색     |

## 외부 파일 실행하기

### %run

- ipython shell에서 외부 스크립트 파일을 실행할 수 있다.

```python
# ch/01/ex_myscript.py

def square(x):
    """숫자의 제곱을 반환"""
    return x ** 2


for N in range(1, 4):
    print(N, "의 제곱은 ", square(N))
```

```bash

In [17]: %run ch/01/ex_myscript.py  # dir 위치를 지정함
1 의 제곱은  1
2 의 제곱은  4
3 의 제곱은  9


```

### 코드 실행 시간 측정 %timeit

- `%timeit` 함수는 그 뒤에 나오는 한 줄의 파이썬 문장 실행 시간을 자동으로 측정한다

```bash
In [18]: %timeit L = [n**2 for n in range(1000)]
103 μs ± 2.02 μs per loop (mean ± std. dev. of 7 runs, 10,000 loops each)
```

- 여러 줄로 된 문장의 실행 시간을 측정하려면 %을 하나 더 붙여서 여러 줄의 입력값을 처리할 수 있는 셸 매직으로 전환할 수 있다.

```bash
In [19]: %%timeit
    ...: L = []
    ...: for n in range(1000):
    ...:     L.append(n ** 2)
    ...:
112 μs ± 15.2 μs per loop (mean ± std. dev. of 7 runs, 10,000 loops each)

```

### 매직 함수에 관한 도움말: ?, %magic, %lsmagic

- 일반 파이썬 함수와 마찬가지로 IPython 매직 함수도 독스트링을 가지고 있으며, 이 유용한 문서는 표준 방식으로 접근할 수 있다.

```bash
In [20]: %timeit?
Docstring:
Time execution of a Python statement or expression

Usage, in line mode:
  %timeit [-n<N> -r<R> [-t|-c] -q -p<P> -o] statement
or in cell mode:
  %%timeit [-n<N> -r<R> [-t|-c] -q -p<P> -o] setup_code
...

```

## 입력/출력 이력