# Stack 1

#### 스택(stack)의 특성

* 물건을 쌓아 올리듯 자료를 쌓아 올린 형태의 자료구조
* 스택에 저장된 자료는 선형 구조를 갖는다
  * 선형구조 : 자료 간의 관계가 1대1
  * 비선형구조 : 자료 간의 관계가 1대N
* 스택에 자료를 삽입하거나 스택에서 자료를 꺼낼 수 있다
* 마지막에 삽입한 자료를 가장 먼저 꺼낸다. 후입선출(LIFO)라고 부른다.



#### 스택을 프로그램에서 구현하기 위해 필요한 자료구조와 연산

* 자료구조 : 자료를 선형으로 저장할 저장소
  * C언어에서는 배열 사용
  * 저장소 자체를 스택이라 부르기도 한다
  * 스택에서 마지막 삽입된 원소의 위치를 top이라고 부른다
* 연산
  * 삽입: 저장소에 자료를 저장한다. `push`
  * 삭제: 저장소에서 자료를 꺼낸다. 꺼낸 자료는 삽입한 자료의 역순으로 꺼낸다. `pop`
  * 스택이 공백인지 아닌지 확인. `isEmpty`
  * 스택의 `top`에 있는 `item(원소)`을 반환하는 연산. `peek`



##### 스택의 push 알고리즘

> Append 메소드를 통해 리스트의 마지막에 데이터 삽입

```python
def push(item):
    s.append(item)
```



##### 스택의 pop 알고리즘

```python
def pop() :
    if len(s) == 0 :
        # underflow
        return
    else :
        return s.pop(-1);
```



#### 스택 구현 고려 사항

* 1차원 배열을 사용하여 구현할 경우 구현이 용이하다는 장점이 있지만 스택의 크기를 변경하기가 어렵다는 단점이 있다.
* 이를 해결하기 위한 방법으로 저장소를 동적으로 할당하여 스택을 구현하는 방법이 있다. 동적 연결리스트를 이용하여 구현하는 방법을 의미한다. 구현이 복잡하다는 단점이 있지만 메모리를 효율적으로 사용한다는 장점을 가진다. 스택의 동적 수현은 생략한다.





#### Function call

> 프로그램에서의 함수 호출과 복귀에 따른 수행 순서를 관리

* 가장 마지막에 호출된 함수가 가장 먼저 실행을 완료하고 복귀하는 후입선출 구조이므로 스택을 이용해 수행순서 관리
* 함수 호출이 발생하면 호출한 함수 수행에 필요한 지역변수, 매개변수 및 수행 후 복귀할 주소 등의 정보를 스택 프레임에 저장하여 시스템 스택에 삽입
* 함수의 실행이 끝나면 시스템 스택의 top원소를 삭제(pop)하면서 프레임에 저장되어 있던 복귀 주소를 확인하고 복귀
* 함수 호출과 복귀에 따라 이 과정을 반복하여 전체 프로그램 수행이 종료되면 시스템 스택은 공백 스택이 된다.



#### 재귀호출

> 자기 자신을 호출하여 순환 수행되는 것
>
> 함수에서 실행해야 하는 작업의 특성에 따라 일반적인 호출방식보다 재귀호출방식을 사용하여 함수를 만들면 프로그램의 크기를 줄이고 간단하게 작성

```python
# 대표적으로 Factorial 함수

def fact(n):
    if n == 1:
        return 1
    else :
        return n * fact(n-1)
```

> 0 과 1로 시작하고 이전의 두 수 합을 다음 항으로 하는 수열을 피보나치라고 한다.

```python
# 재귀함수

def fibo(n):
    if n < 2 :
        return n
    else :
        return fibo(n-1) + fibo(n-2)
```

--> 문제점 : __엄청난 중복 호출이 존재한다__

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fwx0Dp%2FbtqEODZ9Eip%2F5WMAkJeMWwEhPEOP3HOhjk%2Fimg.png">





```python
'''
재귀 함수 : 자기자신을 호출하는 함수
'''
# def func():         #함수를 정의
#     print("hello")
#     func()
#
# func()

#위의 코드를 그대로 실행하면 무한 반복 발생

'''
무한 반복에 빠지지 않게 하려면 어떻게 해야할까?
    매개변수를 하나 받음
    재귀 호출이 발생할때마다 매개변수의 값이 변하도록 설정
    재귀 함수에서 매개변수의 값을 이용해서 조건을 설정하고 일정조건을 만족하면 
    리턴하도록 설정
'''
# def func(k):         #함수를 정의
#     if k < 0 :
#         return
#     else:
#         print("hello")      #조건식 : 변수 < 0
#         func(k-1)
# func(4)     #hello를 다섯번만 출력하도록 설정해 봅시다

'''
재귀함수의 구조
- 기본파트
    : 적어도 하나의 재귀에 빠지지 않는 경우가 존재해야 함.
- 유도파트
    : 재귀를 반복하다보면 결국 기본파트에 수렴해야 함.
'''

#1~10까지의 합을 구하는 재귀 함수를 만들어보세요.
#답 : 55

# def sum(k,total):
#     if k <= 0:
#         print(total)
#         return
#     # print(k)
#     sum(k-1,total+k)
# sum(10,0) #10을 줌

def sum2(k):
    if k == 0:
        return 0
    # print(k)
    return k + sum2(k-1)

print(sum2(5))
```



#### Memoization

* 메모이제이션은 컴퓨터 프로그램을 실행할 때 이전에 계산한 값을 메모리에 저장해서 매번 다시 계산하지 않도록 하여 전체적인 실행속도를 빠르게 하는 기술이다. 동적계획법의 핵심이 되는 기술.
* 글자 그대로 해석하면 `메모리에 넣기` 라는 의미이며 `기억되어야 할 것` 이라는 뜻의 라틴어에서 파생되었다. 흔히 `기억하기` `암기하기` 라는 뜻의 memorization과 혼동하지만, 정확한 단어는 memoization이다. 동사형은 memoize이다.
* 앞의 예에서 피보나치 수를 구하는 알고리즘에서 fibo(n)의 값을 계산하자마자 저장하면(memoize), 실행시간을 줄일 수 있다.

```python
# memo를 위한 배열을 할당하고, 모두 0으로 초기화한다.
# memo[0]을 0으로 memo[1]는 1로 초기화한다.

def fibo1(n):
    global memo
    if n >= 2 and len(memo) <= n :
        memo.append(fibo1(n-1) + fibo1(n-2))
    return memo[n]

memo = [0, 1]
```



#### DP (Dynamic Programming)

* 동적 계획 알고리즘은 그리디 알고리즘과 같이 `최적화 문제`를 해결하는 알고리즘이다.

* 동적 계획 알고리즘은 먼저 입력 크기가 작은 부분 문제들을 모두 해결한 후에 그 해들을 이용하여 보다 큰 크기의 부분 문제들을 해결하여, 최종적으로 원래 주어진 입력의 문제를 해결하는 알고리즘이다.

* 피보나치 수 DP 적용

  * 피보나치 수는 부분 문제의 답으로부터 본 문제의 답을 얻을 수 있으므로 최적 부분 구조로 이뤄져있다.

    * 문제를 부분 문제로 분할한다.
      * Fib(n)함수는 Fib(n-1)과 Fib(n-2)의 합
      * Fib(n-1)함수는 Fib(n-2)과 Fib(n-3)의 합
      * Fib(2)함수는 Fib(1)과 Fib(0)의 합
      * Fib(n)함수는 Fib(n-1)과 Fib(n-2), ..... Fib(2), Fib(1), Fib(0)의 부분집합으로 나뉜다.
    * 부분 문제로 나누는 일을 끝냈으면 가장 작은 부분 문제부터 해를 구한다.
    * 그 결과는 테이블에 저장하고, 테이블에 저장된 부분 문제의 해를 이용하여 상위 문제의 해를 구한다.

  * ```python
    def fibo2(n):
        f = [0, 1]
        
        for i in range(2, n+1):
            f.append(f[i-1] + f[i-2])
            
        return f[n]
    ```



* DP의 구현 방식
  * recursive 방식 : fibo1()
  * iterative 방식 : fibo2()
  * memoization을 재귀적 구조에 사용하는 것보다 반복적 구조로 DP를 구현하는 것이 성능 면에서 보다 효율적이다.
  * 재귀적 구조는 내부에 시스템 호출 스택을 사용하는 오버헤드가 발생하기 때문이다.




#### DFS(깊이우선탐색)

* 비선형구조인 그래프 구조는 그래프로 표현된 모든 자료를 빠짐없이 검색하는 것이 중요.
* 두 가지 방법
  * 깊이 우선 탐색(Depth First Search, DFS)
  * 너비 우선 탐색(Breadth First Search, BFS)
* 시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 방문하는 순회방법
* 가장 마지막에 만났던 갈림길의 정점으로 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 후입선출 구조의 스택 사용



#### DFS 알고리즘

* 시작 정점 v를 결정하여 방문한다.
* 정점 v에 인접한 정점 중에서
  * 방문하지 않은 정점 w가 있으면, 정점 v를 스택에 push하고 정점 w를 방문한다. 그리고 w를 v로 하여 다시 반복한다.
  * 방문하지 않은 정점이 없으면, 탐색의 방향을 바꾸기 위해서 스택을 pop하여 받은 가장 마지막 방문 정점을 v로 하여 다시 반복한다.
* 스택이 공백이 될 때까지 반복한다.



> DFS 알고리즘 - 재귀

```python
DFS_Recursive(G, v)
	visited[v]  <-- TRUE	// v 방문 설정
    
    for each all w in adjacency(G, v)
    	IF visited[w] != TRUE
        	DFS_Recursive(G, w)
```



> DFS 알고리즘 - 반복

```python
STACK s
visited[]
DFS(v)
	push(s, v)
    WHILE NOT isEmpty(s)
    	v <-- pop(s)
        IF NOT visited[v]
        	visit(v)
            FOR each w in adjancency(v)
            	IF NOT visited[w]
                	push(s, w)
```



```python
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''

def dfs(n,V):   #n :현재 정점
    stack = [0] * V     #스택
    visited = [0]* (V+1)    #방문배열
    top = -1

    top +=1
    stack[top] = n  #시작정점을 스택에 넣기
    visited[n] = 1  #시작정점을 방문했다고 표시

    while (top >= 0):   #스택이 비어있지 않는 동안 반복
        n = stack[top]  #스택에서 하나 꺼내오기
        top-=1
        print(n,end=' ')
        for i in range(1,V+1):
            #n에 인접하고 아직 방문하지 않은 정점 i라면
            if adj[n][i] == 1 and visited[i] == 0:
                top+=1
                stack[top] = i
                visited[i] = 1  #방문여부 체크

V,E = map(int,input().split())
#인접행렬을 생성
adj = [[0] * (V+1) for _ in range(V+1)]
# for row in adj:
#     print(row)
edges = list(map(int,input().split()))  #간선정보 가져오기
for i in range(E):
    n1,n2 = edges[i*2],edges[i*2+1]
    adj[n1][n2] = 1
    adj[n2][n1] = 1     #무방향그래프

dfs(1,V)        #1번 정점을 시작으로 순회할래
```



> 그래프 기초

```python
'''
그래프
그래프 G는 (V,E)의 집합이다.
    V : 정점의 집합
    E : 간선들의 집합

인접
    (u,v)라는 간선이 있다면
    정점u와 정점v는 "인접하다"라고 함


그래프의 표현
    - 인접 행렬
        V*V 크기의 행렬
        두 정점 i,j 잇는 간선이 있다면(인접하면) 행렬의 (i,j)를 1로 하고 아니면 0
    - 인접 리스트 : 추후 설명

- 무방향 그래프
    양방향으로 간선이 있다고 생각해서 인접행렬을 만듬 => 대칭행렬
- 방향 그래프
    대칭이 아님
'''
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''
V,E = map(int,input().split())
#인접행렬을 생성
adj = [[0] * (V+1) for _ in range(V+1)]
# for row in adj:
#     print(row)
edges = list(map(int,input().split()))  #간선정보 가져오기
for i in range(E):
    n1,n2 = edges[i*2],edges[i*2+1]
    adj[n1][n2] = 1
    adj[n2][n1] = 1     #무방향그래프
for row in adj:
    print(row)
```









