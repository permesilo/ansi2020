스택(stack)
======================

1 스택이란?
---------------------
-스택이란 데이터를 일시적으로 저장하기 위해 사용하는 자료구조이다.

-한 쪽 끝에서만 자료를 넣고, 뺼 수 있다.

-가장 마지막에 넣은 자료가 가장 먼저 빠진다.(FILO(First In Last Out)/LIFO(Last In First Out))

-데이터를 넣는 작입을 push, 빼는 작업을 pop이라 한다.

-쉽게 생각했을 때 한쪽이 막힌 원통이라고 생각할 수 있다.

2 스택의 연산
--------------------
스택은 **LIFO(Last In First Out)** 형태를 따르기 때문에 가장 최근에 추가한 데이터가 가장 먼저 제거된다.

**-push(item):** item 하나를 스택의 가장 윗부분에 넣는다.

**-pop():** 스택에서 가장 위에 있는 데이터를 제거한다.

![스택1](https://t1.daumcdn.net/cfile/tistory/2679DF3358881D3934)

출처 https://monsieursongsong.tistory.com/4

**-top():** 가장 마지막에 들어온(스택에서 가장 위에 있는) 데이터를 확인한다.

**-size():** 스택에 몇개의 자료가 들어가 있는지 확인한다.

**-empty():** 스택이 비어있는지, 아닌지 확인하다.(이 때 비어있으면 1을 반환, 비어있지 않으면 0을 반환)


3 스택의 구현
---------------------
스택을 기본적으로 구현하는데는 여러가지 방법이 존재한다.

그 중 가장 기본적인 구현 방법은 배열(array)을 이용하여 구현하는 방법이다.

위에 첨부된 사진을 보면 알겠지만 스택을 기울이면 배열과 비슷한 형태가 된다. 이를 이용하여 배열을 스택으로 만들 것이다.

구현할 때 필요한 것: 배열(+최대크기), top변수(밑에 코드에서는 top함수가 있으므로 idx라는 이름의 변수로 사용), 각종 함수

아래 코드는 배열을 이용하여 스택을 구현한 이다.
```cpp
#include <stdio.h>
#include <string.h>

int idx = 0; //앞에서 말한 top변수
int stack[10002]; //배열의 크기는 스택의 최대 용량만큼 잡아줘야한다.

void push(int n) {
	stack[idx++] = n;
	return;
}

void pop() {
	if (idx != 0)
		printf("%d\n", stack[--idx]);
	else
		printf("-1\n");
	return;
}

void top() {
	if (idx != 0)
		printf("%d\n", stack[idx - 1]);
	else
		printf("-1\n");
}
void empty() {
	if (idx == 0)
		printf("1\n");
	else
		printf("0\n");
}

int main() {
	int N, data;
	char order[8];
	scanf("%d", &N);

	while (N--) {
		scanf("%s", order);
		if (strcmp(order, "push") == 0) {
			scanf("%d", &data);
			push(data);
		}
		else if (strcmp(order, "pop") == 0) {
			pop();
		}
		else if (strcmp(order, "size") == 0)
			printf("%d\n", idx);
		else if (strcmp(order, "top") == 0)
			top();
		else if (strcmp(order, "empty") == 0)
			empty();
	}
}
```
p.s. pop()함수에서 data를 뺄 때 굳이 배열에서 data를 제거할 필요가 없다. 그냥 idx만 줄여주면 인식을 하지 않는다.

4 스택 활용(c++/stl사용)
-------------------------
c++에서는 stack을 일일히 구현하지 않아도 된다. stdio처럼 이미 라이브러리로 구현되어있기 때문이다.

헤더파일은 ```cpp #include <stack>```코드를 추가하면된다.

이 때 c++헤더를 사용하기 위해서는 한 줄을 더 추가해주어야 하는데 이는 밑에 전체 코드에서 설명하도록 하겠다.

또한 stack을 만드려면 int형 변수, char형 변수를 선언하는 것처럼 stack이라는 변수를 하나 선언해주어야한다.

방법은 간단하다. ```cpp
stack<원하는 자료형> 원하는 변수이름;
```위와 같은 형태로 사용하면 되는데

하나의 예시를 들자면 stack안에 int형 자료만 들어갈 경우, stack변수 이름을 s로 지정하고 싶을 때 ```cpp
stack<int> s;
```이런 방식으로 사용하면 된다.

마지막으로 stack헤더에 있는 push, pop등의 함수를 사용하려면 "stack변수이름.원하는 함수"의 형태로 사용하면 된다.

아래 코드는 stl을 사용해 스택을 구현한 것이다.
```cpp
#include<stdio.h>
#include<string.h>
#include<stack>
using namespace std; //이 부분이 c++헤더를 사용할 때 꼭 추가해주어야하는 줄이다

stack<int> s;

int main() {
	int N, data;
	char order[8];
	scanf("%d", &N);

	while (N--) {
		scanf("%s", order);
		if (strcmp(order, "push") == 0) {
			scanf("%d", &data);
			s.push(data);
		}
		else if (strcmp(order, "pop") == 0) {
			if(s.empty())
				printf("-1\n");
			else{
				printf("%d\n", s.top());
				s.pop();
			}
		}
		else if (strcmp(order, "size") == 0)
			printf("%d\n", s.size());
		else if (strcmp(order, "top") == 0){
			if(s.empty())
				printf("-1\n");
			else{
				printf("%d\n", s.top());
			}
		}
		else if (strcmp(order, "empty") == 0)
			printf("%d\n", s.empty());
	}
	return 0;
}
```
