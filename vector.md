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

- 기본적인 vector 선언
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

-2차원 벡터 선언
```cpp
#include<stdio.h>
#include<vector>
using namespace std;

int main(){
  int n, m;
  n = 10; m = 20;
  vector<vector<int>> v1(n, vector<int>(m)); //첫번째 방법
  vector<int> v2[10]; //두번째 방법
  return 0;
}
```
-이 때 v1은 2차원 배열인 ```int v1[n][m]```과 같은 크기이다.

-v2는 세로(열)의 크기는 n과 같지만 가로(행)의 크기는 미리 지정할 수는 없다.

3 vector의 활용
---------------------------------
**- 벡터에 값 저장 및 삭제**
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


**- 벡터의 크기를 구하는 방법**
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

**- 벡터의 특정 원소에 접근하는 방법**
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

**- for문 사용**
```cpp
#include<stdio.h>
#include<vector>
using namespace std;
int main(){
  vector<int> a = { 1,2,3,4,5 };
  for (int i = 0; i < a.size(); i++){
    printf("%d ", a[i]);
  }
  printf("\n");
  for (int x : a)
    printf("%d ", x);
  printf("\n");
  return 0;
}
```
-위에서 사용된 for문 2개는 출력결과가 동일하다

-따라서 어떠한 형식의 for문을 사용해도 상관없지만, 앞으로는 기존의 for문 형식과 같은 첫번째 for문과 같은 형식으로 설명하도록 하겠다.

**- insert와 erase하는 법**
```cpp
#include<stdio.h>
#include<vector>
using namespace std;
int main(){
  vector<int> a = { 1,2,3,4,5 };
  for (int i = 0; i < a.size(); i++){
    printf("%d ", a[i]);
  printf("\n");
  a.insert(a.begin(), 4);
  for (int i = 0; i < a.size(); i++){
    printf("%d ", a[i]);
  printf("\n");
  a.insert(a.begin() + 3, 999);
  for (int i = 0; i < a.size(); i++){
    printf("%d ", a[i]);
  printf("\n");
  a.insert(a.begin() + 1, 5, 0);
  for (int i = 0; i < a.size(); i++){
    printf("%d ", a[i]);
  printf("\n");
  vector<int> b = { 10,20 };
  a.insert(a.begin() + 1, b.begin(), b.end());
  for (int i = 0; i < a.size(); i++){
    printf("%d ", a[i]);
  printf("\n");
  return 0;
}
```

-```insert```함수는 vector에서 원하는 곳에 값을 끼워넣을 수 있는 역할을 해주는 함수이다.

-하지만 vector에서 insert함수의 시간복잡도는 O(N)이다. 이유는 중간에 삽입을 하게되면, 그 위치 뒤에 있는 모든 원소를 한칸씩 뒤로 이동시켜야하기 때문이다.

-```erase(a, b)```는 vector에서 a번째부터 b번째 직전까지의 원소를 삭제한다는 의미이다.

-erase함수도 insert함수와 같은 원리로 시간복잡도는 O(N)이다.

-위 코드에서 ```begin()```함수는 다음 코드에서 좀더 다루도록 하겠다.

-따라서 위 코드의 실행결과는 다음과 같다
```
1 2 3 4 5
4 1 2 3 4 5
4 1 2 999 3 4 5
4 0 0 0 0 0 1 2 999 3 4 5
4 10 20 0 0 0 0 0 1 2 999 3 4 5
```

**- begin, end함수**
```cpp
#include<stdio.h>
#include<vector>
using namespace std;
int main(){
  vector<int> a = { 1,2,3,4,5 };
  a.insert(a.begin(), 4);
  for (int i = 0; i < a.size(); i++){
    printf("%d ", a[i]);
  printf("\n");
  a.erase(a.begin() + 1, a.begin() + 3);
  for (int i = 0; i < a.size(); i++){
    printf("%d ", a[i]);
  printf("\n");
  return 0;
}
```
-위 코드에서 ```begin()```함수는 vector의 가장 첫 위치를 뜻한다.(저장되어있는 값이 아닌 주솟값을 의미) 

-```end()```함수는 vector내에서 원소가 있는 가장 마지막 위치를 의미한다.(저장되어있는 값이 아닌 주솟값을 의미)

-위 코드에서 ```a.erase(a.begin() + 1, a.begin() + 3)```은 a의 맨 앞에서 첫번째 값부터 세번째 값 직전까지 지우겠다는 의미이다.

-따라서 위 코드의 결과는 다음과 같다
```
4 1 2 3 4 5
4 3 4 5
```
