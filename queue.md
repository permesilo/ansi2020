큐(Queue)
======================

1 큐란?
---------------------
-큐는 스택과 같이 데이터를 일시적으로 저장하기 위해 사용하는 자료구조이다.

-한 쪽 끝에서 자료를 넣으면,다른 한 쪽에서만 자료를 뺄 수 있다.

-가장 처음에 넣은 자료가 가장 먼저 빠진다.(FIFO(First In First Out))

-데이터를 넣는 작입을 push, 빼는 작업을 pop이라 한다.

-쉽게 생각했을 때 양쪽이 모두 뚫려있는 원통이라고 생각할 수 있다.

2 스택의 연산
--------------------
스택은 **FIFO(First In First Out)** 형태를 따르기 때문에 가장 처음에 추가한 데이터가 가장 먼저 제거된다.

**-push(item) / Enqueue(item):** item 하나를 큐의 가장 아랫부분에 넣는다.

**-pop() / Dequeue():** 큐에서 가장 위에 있는 데이터를 제거한다.

![큐1](https://upload.wikimedia.org/wikipedia/commons/d/d3/Fifo_queue.png)

출처 https://ko.wikipedia.org/wiki/선입_선출

**-front():** 큐에 존재하는 데이터 중 가장 처음에 들어온(큐에서 가장 위에 있는) 데이터를 확인한다.

**-back():** 큐에 존재하는 데이터 중 가장 마지막에 들어온(큐에서 가장 아래에 있는) 데이터를 확인한다.

**-size():** 큐에 몇개의 자료가 들어가 있는지 확인한다.

**-empty():** 큐가 비어있는지, 아닌지 확인하다.(이 때 비어있으면 1을 반환, 비어있지 않으면 0을 반환)


3 큐의 구현
---------------------
큐를 기본적으로 구현하는데는 여러가지 방법이 존재한다.

그 중 가장 기본적인 구현 방법은 스택과 마찬가지로 배열(array)을 이용하여 구현하는 방법이다.

위에 첨부된 사진을 보면 알겠지만 큐를 기울이면 배열과 비슷한 형태가 된다. 이를 이용하여 배열을 큐로 만들 것이다.

구현할 때 필요한 것: 배열(+최대크기), front변수, back변수(밑에 코드에서는 front, back함수가 있으므로 f, b라는 이름의 변수로 사용), 각종 함수

-front변수는 큐의 가장 앞부분을 의미하며, back변수는 큐의 가장 마지막 부분을 의미한다. 

-data하나가 들어오면 front는 변화하지 않고 back의 값이 하나 증가된다.

-data하나가 빠지면 front의 값이 하나 증가하고 back의 값은 변하지 않는다. (모든 데이터를 하나씩 당기지 않고 front만 증가 시키는 것이 시간적으로 이득이기 때문에 이런식으로 진행한다)

-배열의 최대 크기를 잡을 때 유의해야 할 것은 스택을 구현할 땐 들어갈 수 있는 데이터의 최대 용량이 들어갔다면 큐에서는 단순히 데이터의 최대 용량으로 잡으면 배열의 용량이 부족할 수 있으므로 push 횟수의 총 합으로 최대 크기를 잡아야한다.(왜 이렇게 해야 하는지는 "5 원형큐"에서 설명하도록 하겠다.)

아래 코드는 배열을 이용하여 큐를 구현한 것 이다.
```cpp
#include <stdio.h>
#include <string.h>

int q[10010]; //queue
char inp[10]; //명령어를 저장하는 배열
int num; //push ?형태로 들어오기 때문에 data를 저장하는 변수
int f = 0, b = 0; //front와 back변수

void push(int val) { //push함수
    q[b++] = val;
}
int pop() { //pop함수
    if (f == b)
        return -1;
    else
        return q[f++];
}
int front() { //front함수
    if (f == b)
        return -1;
    else
        return q[f];
}
int back() { //back함수
    if (f == b)
        return -1;
    else
        return q[b - 1];
}
int size() { //size함수
    return b - f;
}
int empty() { //empty함수
    if (f == b)
        return 1;
    else
        return 0;
}
int main() {
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%s", inp);
        if (strcmp(inp, "push") == 0) {//push일 때
            scanf("%d", &num);
            push(num);
        }
        else if (strcmp(inp, "pop") == 0) {
            printf("%d\n", pop());
        }
        else if (strcmp(inp, "front") == 0) {
            printf("%d\n", front());
        }
        else if (strcmp(inp, "back") == 0) {
            printf("%d\n", back());
        }
        else if (strcmp(inp, "size") == 0) //q의 size를 출력하기 위해 back-front의 값을 출력
            printf("%d\n", size());
        else if (strcmp(inp, "empty") == 0) {
            printf("%d\n", empty());
        }
    }
}
```
p.s. pop()함수에서 data를 뺄 때 굳이 배열에서 data를 제거할 필요가 없다. 그냥 front만 늘려주면 인식을 하지 않는다.

4 큐 활용(c++/stl사용)
-------------------------
c++에서는 queue를 일일히 구현하지 않아도 된다. stack과 같이 이미 라이브러리로 구현되어있기 때문이다.

헤더파일은 ```#include <queue>```코드를 추가하면된다.

또한 queue를 만드려면 int형 변수, char형 변수를 선언하는 것처럼 queue변수를 하나 선언해주어야한다.

방법은 간단하다. ```queue<원하는 자료형> 원하는 변수이름;```위와 같은 형태로 사용하면 된다.

마지막으로 queue헤더에 있는 push, pop등의 함수를 사용하려면 "queue 변수이름.원하는 함수"의 형태로 사용하면 된다.

아래 코드는 c++에 미리 구현되어있는 queue 라이브러리(stl) 사용해 구현한 것이다.
```cpp
#include <stdio.h>
#include <string.h>
#include <queue>
using namespace std;

char inp[10]; //명령어를 저장하는 배열
int num; //push ?형태로 들어오기 때문에 data를 저장하는 변수
queue<int> q;

int main() {
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%s", inp);
        if (strcmp(inp, "push") == 0) { //push일 때
            scanf("%d", &num);
            q.push(num);
        }
        else if (strcmp(inp, "pop") == 0) {
            if (q.empty())
                printf("-1\n");
            else {
                printf("%d\n", q.front());
                q.pop();
            }
        }
        else if (strcmp(inp, "front") == 0) {
            if (q.empty())
                printf("-1\n");
            else {
                printf("%d\n", q.front());
            }
        }
        else if (strcmp(inp, "back") == 0) {
            if (q.empty())
                printf("-1\n");
            else {
                printf("%d\n", q.back());
            }
        }
        else if (strcmp(inp, "size") == 0) //q의 size를 출력하기 위해 rear-front의 값을 출력
            printf("%d\n", q.size());
        else if (strcmp(inp, "empty") == 0) {
            printf("%d\n", q.empty());
        }
    }
}
```

5 원형큐(Circular Queue)
-----------------------------
원형큐는 배열에서 큐를 사용할 때 발생하는 불필요한 공간들을 절약하기 위해 고안된 자료구조이다.

예를들어 push와 pop이 번갈아가면서 1억번 일어났다고 생각했을 때 단순히 배열로 구현한 큐의 front와 rear의 값은 1억이 될 것이다.

이 말은 실제 배열에는 1개의 data도 없지만 배열의 크기는 1억개 이상이 필요하다는 것이다.

한마디로 front이전의 모든 배열의 공간은 의미가 없게 되는 것이다.

이렇게 낭비되는 공간을 효율적으로 관리하기 위해서 고안된 것이 원형큐이다.

![원형큐1](https://t1.daumcdn.net/cfile/tistory/244DFA41550C39DE1F)
출처: https://hellmath.tistory.com/8

원형큐의 구조는 큐의 front와 back을 이어붙인 구조이다.

이 원형큐를 구현할 때 필요한 배열의 크기는 스택과 같이 한번에 큐에 들어갈 수 있는 최대 데이터의 개수이다.

원형큐의 작동원리를 간단하게 설명하도록 하겠다.

front와 back변수의 역할은 기존 큐와 동일하다. 하지만 front와 back변수의 값이 배열의 크기를 넘어갈 때 다시 맨 앞으로 설정해주어야 한다는 점이 큰 차이점이다.

```cpp
#include <stdio.h>
#include <string.h>
#define MAX_SIZE 10000
int q[MAX_SIZE]; //queue
char inp[10]; //명령어를 저장하는 배열
int num; //push ?형태로 들어오기 때문에 data를 저장하는 변수
int f = 0, b = 0; //front와 back변수

void push(int val) { //push함수
    if((b + 1) % MAX_SIZE == f) //원형큐에 모든 데이터가 있어 더이상 데이터를 넣을 수 없을 때
        return -1;
    q[b++] = val;
    b %= MAX_SIZE; //b의값이 배열의 크기보다 더 클때 다시 처음으로 돌아가는 코드
}
int pop() { //pop함수
    if (f == b) //원형 큐가 비어있을때를 의미
        return -1;
    else{
        return q[f++];
        f %= MAX_SIZE; //f의 값이 배열의 크기보다 더 클때 다시 처음으로 돌아가는 코드
    }
}
int front() { //front함수
    if (f == b)
        return -1;
    else
        return q[f];
}
int back() { //back함수
    if (f == b)
        return -1;
    else
        return q[b - 1];
}
int size() { //size함수
    return b - f;
}
int empty() { //empty함수
    if (f == b)
        return 1;
    else
        return 0;
}
int main() {
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%s", inp);
        if (strcmp(inp, "push") == 0) {//push일 때
            scanf("%d", &num);
            push(num);
        }
        else if (strcmp(inp, "pop") == 0) {
            printf("%d\n", pop());
        }
        else if (strcmp(inp, "front") == 0) {
            printf("%d\n", front());
        }
        else if (strcmp(inp, "back") == 0) {
            printf("%d\n", back());
        }
        else if (strcmp(inp, "size") == 0) //q의 size를 출력하기 위해 back-front의 값을 출력
            printf("%d\n", size());
        else if (strcmp(inp, "empty") == 0) {
            printf("%d\n", empty());
        }
    }
}
```
