# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day6

## 이 코드는 C++ 언어의 함수 정의에 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 연습 코드: 함수 선언

add 함수를 구현했으나 main 함수 아래에 작성되어 있어, 함수 선언을 통해 에러를 해결

```cpp
#include <iostream>
using namespace std;

// 함수 선언
int add(int x, int y);

int main() {

    int a = 10, b = 20;
    int c = 10, d = 20;
    int e = 10, f = 20;

    cout << a + b << endl;
    cout << c + d << endl;
    cout << e + f << endl;

    cout << add(a, b) << endl;
    cout << add(c, d) << endl;
    cout << add(e, f) << endl;
}

int add(int x, int y) {
    return x + y;
}
```

---

## 🔹 연습 코드 : 헤더 파일과 외부 파일에 함수 선언

헤더 파일을 활용하여 코드를 분리하고, main 함수에서 작성되지 않은 코드를 실행할 수 있도록 연습

```cpp
#include <iostream>
#include "func.h" // => 함수 정의를 포함한 헤더 파일
using namespace std;


int main() {
    int x = 10, y = 20;
    cout << add(x, y) << endl;
    cout << sub(x, y) << endl;
    cout << mul(x, y) << endl;
    cout << divide(x, y) << endl;
}
```

```cpp
// 함수 구현 (func.cpp)
#include "func.h"

int add(int x, int y) {
	return x + y;
}

int sub(int x, int y) {
	return x - y;
}

float divide(int x, int y) {
	if (y == 0) return 0;
	return (float)x / y;
}

int mul(int x, int y) {
	return x * y;
}
```

```cpp
// 헤더 파일 (func.h)
# pragma once

int add(int x, int y);
int sub(int x, int y);
int mul(int x, int y);
float divide(int x, int y);
```

---

## 🔹 연습 코드 : 정적 변수와 일반 변수의 차이

입력받은 정수가 홀수인지 짝수인지 판별하는 프로그램

```cpp
#include <iostream>
using namespace std;

int staticFunc() {
    static int globalStatic = 0; // 정적 변수는 한 번만 초기화
    globalStatic++;
    return globalStatic;
}

int nomalFunc() {
    int normalVar = 0; // 일반 변수는 매번 초기화
    normalVar++;
    return normalVar;
}

int main() {
    staticFunc();
    staticFunc();
    cout << "static : " << staticFunc() << endl;

    nomalFunc();
    nomalFunc();
    cout << "normal : " << nomalFunc() << endl;

    realGlobalVar = 200;
    cout << "전역 변수 값 : " << realGlobalVar << endl;
}
```

```cpp
// 헤더 파일 (func.h)
# pragma once

extern int realGlobalVar;
```
