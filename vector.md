벡터(vector)
======================

1 벡터란?
---------------------
-벡터는 거의 배열과 동일하게 사용가능한 자료구조이다.

-단, 배열과 가장 큰 차이점은 중간에 크기를 변경할 수 있다는 점이다.

-또한 프로그래밍 대회에서 가장 많이 사용하는 자료구조이다.

2 벡터의 선언
--------------------
벡터는 ```#include <vector>```헤더파일을 선언해야 사용이 가능한 자료구조이며

c++에서 사용하기 때문에 stack과 queue처럼 ```using namespace std;```를 필수적으로 작성해야한다.

```cpp
#include<stdio.h>
#include<vector>
using namespace std;
int main(){
  vector<int> v1;
  vector<int> v2(10);
  vector<int> v3(15, 1);
  vector<int> v4 = { 1,2,3,4,5 };
  return 0;
}
```
-v1은 vector의 가장 기본적인 선언 형태이다.

-v2는 vector의 크기를 정하는 방법으로 기본적인 배열처럼 사용할 수 있다.

-v3은 vector의 크기와 초기값을 정해주는 방법이다. 이 때 초기값을 정해주지 않을 경우에는 0으로 초기화된다.
따라서 v2에는 0이 10개, v3은 1이 15개 저장이 되어있다고 볼 수 있다.

-v4는 초기화 리스트를 이용하여 vector에 미리 값을 넣어 만든 방법으로 v4[0]부터 v4[4]까지 각각 1~5의 수가
저장되어있는 형태이다.

```cpp
#include<stdio.h>
#include<vector>
using namespace std;

int main(){
  int n, m;
  n = 10; m = 20;
  vector<vector<int>> v(n, vector<int>(m));
  return 0;
}
```
이 때 v은 2차원 배열인 ```int v[n][m]```과 같은 크기이다.

3 vector의 활용
---------------------------------
- 벡터에 값 저장 및 
```cpp
#include<stdio.h>
#include<vector>
using namespace std;

int main(){
  vector<int> a = { 1,2,3,4,5 };
  a.push_back(6); // [1,2,3,4,5,6]
  a.push_back(7); // [1,2,3,4,5,6,7]
  a.pop_back(); // [1,2,3,4,5,6]
  a.pop_back(); // [1,2,3,4,5]
  a.pop_back(); // [1,2,3,4]
  a.clear(); // []
  a.resize(5); // [0,0,0,0,0]
  a.clear(); // []
  return 0;
}
```
-vector에 값을 추가하는 방법은 ```push_back(추가할 data)```힘수를 사용하는 것이며, 
```push_back()```함수는 queue에서의 push함수처럼 vector의 뒤에 값을 추가하는 역할을 한다.

-vector에서 값을 제거하는 방법은 ```pop_back()```함수를 사용하는 것으로, pop_back()함수를 사용할 경우
가장 뒤에있는 값을 삭제한다.

-```clear()```함수는 vector내에 있는 값을 한꺼번에 삭제하는 역할을 한다.

-```resize()```함수는 벡터의 사이즈를 미리 정해주는 역할을 하며, 초기값을 설정해주지 않을 경우 기본적으로 
0이 저장된다.


- 벡터의 크기를 구하는 방법
```cpp
#include<stdio.h>
#include<vector>
using namespace std;

int main(){
  vector<int> a = { 1,2,3,4 };
  printf("size = %d\n", a.size());
  a.push_back(5);
  printf("size = %d\n", a.size());
  printf("empty = %d\n", a.empty());
  a.clear();
  printf("size = %d\n", a.size());
  printf("empty = %d\n", a.empty());
  return 0;
}
```

-```size()```함수는 벡터의 크기를 반환해주는 함수로 벡터의 크기를 알고싶을 때 사용한다.

-```empty()```함수는 해당 벡터가 비어있는지, 아닌지 알려주는 함수로서 비어있을 때는 1(true)을 반환해주고
비어있지 않을 경우에는 0(false)을 반환해준다.

따라서 위 코드의 실행결과는 다음과 같다.
```
size = 4
size = 5
empty = 0
size = 0
empty = 1
```

벡터를 배열처럼 사용하기 위해서는 한번에 특정 원소에 접근을 할 수 있어야한다.(이를 random access라고도 부름)

실제로 벡터의 특정 원소에 접근하는 방법은 배열과 같다.

- 벡터의 특정 원소에 접근하는 
```cpp
#include<stdio.h>
#include<vector>
using namespace std;

int main(){
  vector<int> a = { 1,2,3 };
  printf("front = %d\n", a.front());
  printf("a[1] = %d\n", a[1]);
  printf("back = %d\n", a.back());
  a.push_back(4);
  for (int i = 0; i < a.size(); i++)
    printf("%d ", a[i]);
  printf("\n");
  return 0;
}
```

-```front()```함수는 vector의 가장 앞에 저장되어있는 값을 반환한다.

-```back()```함수는 vector의 가장 뒤에 저장되어있는 값을 반환한다.

-```a[i]```와 같은 값은 i번째에 저장되어있는 값을 반환한다.

저장할때에도 특정 위치에 접근하여 저장할 수 있는데 이 때는 vector의 크기를 **미리** 지정해두어야한다.
(resize 혹은 초기 vector를 선언할 때 크기 지정하는 방법을 사용)

벡터의 모든 값을을 순서대로 접근할 수 있는 방법은 반복문을 사용하는 방법인데 이를 간단하게 2가지로 나눌 수 있다.


4 벡터를 이용한 그래프 저장(가중치 O)
--------------------

