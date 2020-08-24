# Python String

### 컴퓨터에서의 문자표현

* 메모리는 숫자만을 저장할 수 있다.
  * 각 문자에 대응되는 숫자를 정해 놓고 이것을 메모리에 저장하는 방법 사용

* 영어가 대소문자 합쳐 52이므로 6비트(64가지)면 모두 표현할 수 있다. => 코드체계
  * 표준안 ASCII -> 7bit 인코딩으로 128문자를 표현하며 33개의 출력 불가능한 제어 문자들과 공백을 비롯한 95개의 출력 가능한 문자들로 이루어져 있다.

![ASCII](https://mblogthumb-phinf.pstatic.net/20150122_214/ouwukwfy_14218983802750XhtH_JPEG/%BE%C6%BD%BA%C5%B0%C4%DA%B5%E5%C7%A5_01.jpg?type=w2)



![ASCII](https://mblogthumb-phinf.pstatic.net/20150122_206/ouwukwfy_1421898380619oE3vf_JPEG/%BE%C6%BD%BA%C5%B0%C4%DA%B5%E5%C7%A5_02.jpg?type=w2)





* python의 문자열 처리

  * char 타입이 없다.

  * 텍스트 데이터의 취급방법이 통일되어 있다.

  * ' ' , " ", ''' ''', """ """

  * +연결 = 문자열 + 문자열을 이어 붙여준다

  * *반복 = 문자열\*수 만큼 문자열이 반복된다.

  * 문자열은 시퀀스 자료형이다. --> 인덱싱, 슬라이싱 연산 가능

  * replace(), split(), isalpha(), find()

  * immutable --> 튜플과 같이 요소값을 변경할 수 없다.

    

    

* 비교 함수
  * C : strcmp() 함수 제공
  * Java : equals() 메소드 제공
    * 문자열 비교에서 == 연산은 메모리 참조가 같은지를 묻는 것이다
  * Python : == 연산자와 is 연산자를 제공
    * == 연산자는 내부적으로 특수 메서드 \__eq__()를 호출한다.



* 문자열을 정수로 변환
  * C : atoi() 함수 제공. 역 함수 => itoa()
  * Java : 숫자 클래스의 parse 메소드를 제공
    * ex) Integer.parseInt(String)
    * 역함수 => toString() 메소드 제공
  * Python : 숫자와 문자변환 함수를 제공
    * int("123"), float("3.14") , str(123), repr(123)

```python
str = "123"
str2 = "12.3"

print(int(str), type(str))
print(float(str2), type(float(str2)))

test = "1 + 2"
print(test)
print(repr(test))
print(eval(test))
print(eval(repr(test)))
print(eval(eval(repr(test))))

# 123 <class 'str'>
# 12.3 <class 'float'>
# 1 + 2
# '1 + 2'
# 3
# 1 + 2
# 3
```



Q. 파이썬과 자바의 유니코드 기본 인코딩 방법은??

​	파이썬: UTF-8, 자바: UTF-16



#### 패턴 매칭

* 고지식한 알고리즘(Brute Force)
  * 본문 문자열을 처음부터 끝까지 차례대로 순회하면서 패턴 내의 문자들을 일일이 비교하는 방식으로 동작



* KMP 알고리즘
  * 불일치가 발생한 텍스트 스트링의 앞 부분에 어떤 문자가 왔는지 미리 알고 있으므로, 불일치가 발생한 앞 부분에 대하여 다시 비교하지 않고 매칭 수행
  * 패턴을 전처리하여 배열 next[M]을 구해 잘못된 시작을 최소화
  * 시간 복잡도: O(M+N)
  * 매칭이 실패했을 때 돌아갈 곳을 계산한다



* 보이어-무어 알고리즘

  * 오른쪽에서 왼쪽으로 비교한다. [발상의 전환!]
* 대부분의 상용 SW에서 채택하고 있는 알고리즘
  * 보이어-무어 알고리즘은 패턴에 오른쪽 끝에 있는 문자가 불일치 하고 이 문자가 패턴 내에 존재하지 않는 경우, 이동 거리는 무려 패턴의 길이 만큼이 된다.



### Brute Force

```python
p = "is"                   # 찾을 패턴
t = "This is a book~!"     # 전체 텍스트
M = len(p)                 # 찾을 패턴의 길이
N = len(t)                 # 전체 텍스트의 길이

def BruteForce(p, t):
    i = 0                  # t의 인덱스
    j = 0                  # p의 인덱스
    while j < M and i < N:
        if t[i] != p[j]:
            i = i - j
            j = -1
            
        i = i + 1
        j = j + 1
        
    if j == M:
        return i - M        # 검색 성공
    else:
        return -1           # 검색 실패
```



#### 연습

고지식한 방법을 이용하여 패턴을 찾아봅시다 

임의의 본문 문자열과 찾을 패턴 문자열을 만듭니다 

결과 값으로 찾은 위치 값을 결과로 출력합니다

```python
def brute(t, p):
    i, j = 0, 0
    while j < len(p) and i < len(t):
        if t[i] != p[j]:
            i = i - j
            j = -1
        i += 1
        j += 1

    if j == len(p):
        return i - len(p)
    else:
        return -1

text = "(TEXT)"
pattern = "(pattern)"
print(brute(text, pattern))
```

