스택(stack)
======================

1.1 스택이란?
---------------------
-스택이란 데이터를 일시적으로 저장하기 위해 사용하는 자료구조이다.

-한 쪽 끝에서만 자료를 넣고, 뺼 수 있다.

-가장 마지막에 넣은 자료가 가장 먼저 빠진다.(FILO(First In Last Out)/LIFO(Last In First Out))

-데이터를 넣는 작입을 push, 빼는 작업을 pop이라 한다.

-쉽게 생각했을 때 한쪽이 막힌 원통이라고 생각할 수 있다.

1.2 스택의 연산
--------------------
스택은 **LIFO(Last In First Out)** 형태를 따르기 때문에 가장 최근에 추가한 데이터가 가장 먼저 제거된다.

**-push(item):** item 하나를 스택의 가장 윗부분에 넣는다.

**-pop():** 스택에서 가장 위에 있는 데이터를 제거한다.

![스택1](https://t1.daumcdn.net/cfile/tistory/2679DF3358881D3934)

출처 https://monsieursongsong.tistory.com/4

**-top():** 가장 마지막에 들어온(스택에서 가장 위에 있는) 데이터를 확인한다.

**-size():** 스택에 몇개의 자료가 들어가 있는지 확인한다.

**-empty():** 스택이 비어있는지, 아닌지 확인하다.(이 때 비어있으면 1을 반환, 비어있지 않으면 0을 반환)


1.3 스택의 구현
---------------------
스택을 기본적으로 구현하는데는 여러가지 방법이 존재한다.

그 중 가장 기본적인 구현 방법은 배열(array)을 이용하여 구현하는 방법이다.

위에 첨부된 사진을 보면 알겠지만 스택을 기울이면 배열과 비슷한 형태가 된다. 이를 이용하여 배열을 스택으로 만들 것이다.

구현할 때 필요한 것: 배열(+최대크기), top변수, 각종 함수

```
#include <stdio.h>
#include <string.h>

int idx = 0;
int stack[10002];

void push(int n) {
	stack[idx++] = n;
	return;
}

void pop() {
	if (idx != 0)
		printf("%d\n", stack[--idx]);// 그냥 idx를 --해도 무관하다! stack에 자료가 있거나 없거나 인덱스만 줄이면 인식을하지 않기때문 오히려 stack에서 자료를뺴면 그때 cost가 발생함
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
