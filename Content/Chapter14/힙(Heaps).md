14장 힙 (Heaps)

a. 데이터 구조
 - 힙은 항목의 모음을 표현하는 데이터 구조

이진 트리
순서 : 모든 노드의 값은 그 자식 노드의 값보다 작거나 같다
모양 : 종단 노드가 최대 두 레벨 (마지막 두 레벨)에 걸쳐 존재할 수 있고, 최종 레벨의 노드들은 모두 왼쪽으로 치우쳐 있다.

위 이진 트리는 배열로 사용할 수 있으며, 아래는 전형적인 이진 트리에 대한 함수들이다.
 

root = 1
value(i) = x[i]
leftchild(i) = 2*i
rightchild(i) = 2*i+1
parent(i) = i/2
null(i) = (i < 1) or (i > n)

b. 두 가지 중요한 함수
 - 힙 속성이 무너진 배열을 바로잡는 두 가지 함수에 대해 설명하는 절

 - 배열 x가 힙이고, 임의 요소(힙이 성립되지 않는)를 x[i]에 넣었을 때, 새로운 요소를 적당한 위치까지 위로 올리면서 힙이 성립할 때까지 만들어줌

//sudo code
loop
/* invariant: heap(i, n) except perhaps
between I and its parent */

//implement code
void siftup(n)
pre n > 0 && heap(i, n-1)
post heap(i, n)
i = n
loop
/* invariant: heap(i, n) except perhaps
between i and its parent */
if i == 1
break
p = i / 2
if x[p] <= x[i]
break
swap(p, I)
i = p

 - 배열 x가 힙이고, 임의 요소(힙이 성립되지 않는)를 x[i]에 넣었을 때, 새로운 요소를 적당한 위치까지 밑으로 내리면서 힙이 성립할 때까지 만들어줌

// sudo code
loop
/* invariant: heap(i, n) except perhaps between
i and its (0, 1 or 2) children */

// implements
void siftdown(n)
pre heap(2, n) && n >= 0
post heap(1, n)
i = 1
loop
/* invariant: heap(i, n) except perhaps between
i and its (0, 1 or 2) children */
c = 2*i
if c > n
break
/* c is the left child of i */
if c+1 <= n
/* c+1 is the right child or i */
if x[c+1] < x[c]
c++
/*c is the lesser child of i */
if x[i] <= x[c]
break
swap(c, i)
i = c

c. 우선순위 큐

template<class T>
class priqueue {
private:
int n, maxsize;
T *x;

void swap(int I, int j)
{ T t = x[i]; x[i] = x[j]; x[j] = t }

public:
priqueue(int m)
{
maxsize = m;
x = new T[maxsize+1]
n = 0;
}

void insert(T t)
{
int I, p;
x[++n] = t;
for (i = n; I > 1 && x[p=i/2] > x[i]; I = p)
swap(p, I);
}

T extractmain()
{
int I, c;
T t = x[i];
x[i] = x[n--];
for (i = i; (c = 2*i) <= n; I = c)
{
if (c+1 <= n && x[c+1] < x[c])
c++;
if (x[i] <= x[c]) break;
swap(c, I);
}
return t;
}
};

d. 원리

 1. 효율성
  - 모양 속성은 힙의 모든 노드가 루트로부터 logn레벨 내에 있음을 보장함
  - 트리의 균형이 유지되기에 siftup / siftdown 함수가 효율적인 실행시간을 가짐

 2. 정확성
  - 루프에 대한 코드를 작성하기 위해 먼저 불변식을 정확하게 기술하고, 그 불변식을 보존하면서 루프가 종료될 때까지 진행함.

 3. 추상화
  - 어떤 컴포넌트가 무슨 일을 하는지(사용자 입장에서의 추상화)와 어떻게 그 일을 수행하는지(블랙 박스 내부 구현)를 구별함.

 4. 절차 추상화
  - 정렬 함수가 어떻게 구현되어 있는지 알 필요 없이 배열을 정렬하기 위해 그 함수를 사용할 수 있음
  - 이와 같이 블랙 박스 컴포넌트 정의는 한번만 하고, 서로 다른 두 종류의 도구들을 결합하기 위해 컴포넌트를 사용할 수 있도록 함

 5. 추상 데이터 타입
  - 1데이터 타입이 하는 일은 그 데이터 타입의 메소드와 각 메소드의 명세로 알 수 있음