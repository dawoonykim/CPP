# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day2

이 코드는 C++ 언어의 데이터 타입과 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 코드 연습: 기초적인 문법 연습

```cpp
#include <iostream>
using namespace std;

int main() {

    cout << "안녕하세요! 만나서 반갑습니다." << endl << "1부터 시작하는 숫자를 입력하세요.";

    int i; // 변수 선언
    i = 100; // 변수 초기화

    int i = 100; // 변수 선언과 동시에 초기화

    return 0;
}
```

---

## 🔹 코드 연습: 데이터 타입

데이터 타입에 대한 이해도를 높이는 코드

```cpp
#include <iostream>
#include <stdio.h>
using namespace std;

 int main() {
     // 정수형
     // char(1) short(2) int(4) long(4) long long(8)
     // unsigned 부호 없는(음수가 없는) 정수
     // char : 256개의 값 표현 가능 (-128 ~ 127)
     // unsigned char : 0 ~ 255
     unsigned char a = 257;
     unsigned char b = -1;
     cout << a;
     cout << b;

     // 실수형
     float c = 0.1;
     float d = 0.2;
     if ((c + d) == 0.3)
         cout << "0.3입니다!";
 }
```

---

## 🔹 실습: 데이터 타입

입력 받은 값을 저장해서 프롬프트에 출력하는 프로그램

```cpp
#include <iostream>
#include <string>

using namespace std;

int main() {
    char c = 'c';
    char d = 'd';
    string s = "hello world";
    cout << s << endl;

    cout << d;

    int myInput;
    cout << "input을 입력하세요 : ";
    cin >> myInput;
    cout << "myInput = " << myInput;

    cout << "이름을 입력하세요: ";
    string name;
    cin >> name;
    cout << "나이를 입력하세요: ";
    int age;
    cin >> age;
    cout << "안녕하세요! " << name << "님 (" << age << "세)";

     char name;
     int age;
     scanf_s("%d", &age); => string 타입을 받을 수 없음
     printf("%d", age);
}
```
