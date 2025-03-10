# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day5

## 이 코드는 C++ 언어의 함수에 관련된 기본적인 문법을 포함하고 있습니다.

리팩토링을 위한 함수 문법 이해도를 높이기 위한 코드

---

## 🔹 연습 예제 코드: 간단한 코드로 만든 함수 리팩토링

add 함수로 더하기 구현하는 프로그램

```cpp
#include <iostream>
using namespace std;

int add(int x, int y) {
    return x + y;
}

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
```

---

## 🔹 실습 1: 기본적인 연산 함수

정수를 입력받아, 사칙 연산을 수행하는 프로그램

```cpp
#include <iostream>
using namespace std;

int add(int x, int y) {
    return x + y;
}

int sub(int x, int y) {
    return x - y;
}

int mul(int x, int y) {
    return x * y;
}

float divide(int x, int y) {
    if (y == 0) {
        cout << "0으로 나눌 수 없습니다." << endl;
    }
    else {
        return (float)x / y;
    }
}

int main() {
    cout << "두 수를 입력하세요.";

    int a, b;
    cin >> a >> b;

    cout << add(a, b) << endl;
    cout << sub(a, b) << endl;
    cout << mul(a, b) << endl;
    cout << divide(a, b) << endl;
}
```

---

## 🔹 실습 2: 홀짝 판별

입력받은 정수가 홀수인지 짝수인지 판별하는 프로그램

```cpp
#include <iostream>
using namespace std;

void oddOrEven(int x) {
    if (x % 2 == 0) {
        cout << "짝수입니다." << endl;
    }
    else {
        cout << "홀수입니다." << endl;
    }
}

int main() {
    int a;
    cin >> a;
    oddOrEven(a);
}
```

---

## 🔹 실습 3: 가장 큰 값 찾기

입력 받은 숫자 세 개 중에서 가장 큰 값을 출력하는 프로그램

```cpp
#include <iostream>
using namespace std;

int findMaxValue(int x, int y, int z) {
    if (x > y && x > z) {
        return x;
    }
    else if (y > x && y > z) {
        return y;
    }
    else {
        return z;
    }
}

int findMaxValue2(int array[3]) {
    int maxValue = 0;
    for (int i = 0; i < 3; i++) {
        if (array[i] > maxValue) {
            maxValue = array[i];
        }
    }
    return maxValue;
}

int main() {
    cout << "세 수를 입력하세요.";
    int x, y, z;
    cin >> x >> y >> z;
    cout << "가장 큰 값 " << findMaxValue(x, y, z) << endl;

    // 배열로 리팩토링
    int array[3] = { x,y,z };
    cout << "가장 큰 값 " << findMaxValue2(array) << endl;
}
```

---

## 🔹 연습 예제 코드 : 함수와 재귀함수 에 대한 문법 이해도를 높이기 위한 코드

```cpp
#include <iostream>
using namespace std;

void funcA(int x) {
    int localA = x + 1;
    cout << "Function A " << localA << endl;
}

void funcB(int x) {
    int localB = x * 2;
    funcA(localB);
    cout << "Function B " << localB << endl;
}

void RecursiveFunc(int n) {
    if (n == 0) return;
    cout << "재귀 호출 : " << n << endl;
    RecursiveFunc(n - 1); // 재귀 호출
}

int main() {
    int num = 5;
    funcB(num);
    cout << num << endl;

    // 재귀함수
    RecursiveFunc(5);
}
```

---

## 🔹 실습 4 : 팩토리얼

팩토리얼을 함수와 재귀함수로 구현하는 프로그램

```cpp
#include <iostream>
using namespace std;

int factorial(int n) {
    int result = 1;
    for (int i = n; i > 0; i--) {
        result *= i;
    }
    return result;
}

int RecursiveFactorial(int n) {
    if (n == 1) return 1;

    int facValue = RecursiveFactorial(n - 1);
    return n * facValue;
}

int main() {

    // 반복문
    cout << "팩토리얼로 계산할 숫자를 입력하세요 : ";
    int num4;
    cin >> num4;
    cout << "팩토리얼 : " << factorial(num4) << endl;
    // 재귀 호출
    cout << "팩토리얼 : " << RecursiveFactorial(num4) << endl;
}
```

---

## 🔹 실습 6 : 거듭 제곱

거듭 제곱을 재귀함수로 구현하는 프로그램

```cpp
#include <iostream>
using namespace std;

int powNumber(int x, int y) {
    if (y == 1) return x;

    int powValue = powNumber(x, y - 1);
    return x * powValue;
}

int main() {
    cout << "거듭제곱을 계산할 두 숫자를 입력하세요.";
    int a, b;
    cin >> a >> b;
    cout << a << "의 " << b << "승은 " << powNumber(a, b) << "입니다." << endl;
}
```

---

## 🔹 실습 5: 피보나치 수열

피보나치 수열을 for문과 재귀함수로 구현하는 프로그램

```cpp
#include <iostream>
using namespace std;

int fibo1(int num) {
    int result = 0;
    int x = 1, y = 1;
    cout << x << " " << y << " ";
    if (num <= 0) return 0;
    else if (num == 1 || num == 2) return 1;
    for (int i = 3; i <= num; i++) {
        result = x + y;
        x = y;
        y = result;
        cout << result << " ";
    }
    return result;
}

int fibo2(int num) {
    if (num <= 0) return 0;
    if (num <= 2) return 1;

    return fibo2(num - 2) + fibo2(num - 1);
}

int main() {
  int num5 = 20;
  cout << endl << fibo1(num5) << endl;
  cout << endl << fibo2(num5) << endl;
}
```
