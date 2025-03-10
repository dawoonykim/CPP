# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day3

## 이 코드는 C++ 언어의 연산과 관련된 기본적인 문법을 포함하고 있습니다.

```cpp
#include <iostream>
#include <bitset>
using namespace std;

int main() {

    // 사칙 연산자 +, -, *, /, %

    int a = 10;
    int b = 4;

    cout << a + b << endl;
    cout << a * b << endl;
    cout << a / b << endl;
    cout << a - b << endl;
    cout << a % b << endl;

    a += 5;
    cout << a << endl;

    // % 연산자는 실수에서 사용 불가
     //cout << 10. % 3.;

    // 논리 연산자
    int b = 0;

    // 비트 연산자
    // & (and)
    int a = 0b0101;
    int b = 0b1001;

    cout << bitset<4>(a & b); // 1 출력

    // 시프트 연산
    int c = 0b0011;
    cout << bitset<5>(c << 3);

    // 특정 비트 추가 및 삭제
    int f = 0b1000;

    // 비트 추가
    cout << bitset<4>(f |= 0b0010) << endl;
    cout << f << endl;
    // 비트 삭제
    cout << bitset<4>(f & ~(1 << 1)) << endl;

    int myInput;
    cin >> myInput;

    switch (myInput) {
        case 1:
            cout << "1111111111111111";
            break;
    }
```

---

## 🔹 실습 1: 나이에 따른 분류

나이를 입력받아 해당 연령대에 맞는 그룹을 출력하는 프로그램

```cpp
#include <iostream>
#include <bitset>
using namespace std;
int main() {
    cout << "------실습 1------" << endl << "나이를 입력하세요 : ";
    int age;
    cin >> age;
    if (1 <= age && age <= 7) {
        cout << "유아" << endl << endl;
    }
    else if (8 <= age && age <= 13) {
        cout << "초등학생" << endl << endl;
    }
    else if (14 <= age && age <= 16) {
        cout << "중학생" << endl << endl;
    }
    else if (17 <= age && age <= 19) {
        cout << "고등학생" << endl << endl;
    }
    else if (20 <= age) {
        cout << "성인" << endl << endl;
    }
    else if (200 <= age) {
        cout << "나이가 너무 많습니다...!" << endl << endl;
    }
    else {
        cout << "오류";
    }
}
```

---

## 🔹 실습 2: 이름에 따른 성별 판별

특정 이름에 대해서 성별을 출력하는 프로그램

```cpp
#include <iostream>
#include <bitset>
using namespace std;
int main() {
    cout << "------실습 2------" << endl << "이름을 입력하세요 : ";
    string name;
    cin >> name;
    if (name == "홍길동") {
        cout << "남자" << endl << endl;
    }
    else if (name == "김영희") {
        cout << "여자" << endl << endl;
    }
    else {
        cout << "모르겠어요." << endl << endl;
    }
}
```

---

## 🔹 실습 3: 5의 배수 판별

+5의 배수인지 여부를 판단하는 프로그램

```cpp
#include <iostream>
#include <bitset>
using namespace std;
int main() {
    cout << "------실습 3------" << endl << "숫자를 입력하세요 : ";
    int num;
    cin >> num;
    cout << num << "은 5의 배수" << (num % 5 == 0 ? "입니다." : "가 아닙니다.") << endl << endl;
}
```

---

## 🔹 실습 4: 기본 사칙연산 계산기

두 개의 정수와 연산자를 입력받아 사칙연산을 수행하는 프로그램

```cpp
#include <iostream>
#include <bitset>
using namespace std;
int main() {
    cout << "------실습 4------" << endl << "두 개의 숫자를 입력해 주세요 : ";
    int a, b;
    char op;
    cin >> a >> b;
    cout << "연산자를 입력하세요 (+, -, *, /, %) : ";
    cin >> op;

    switch (op) {
    case '*':
        cout << "**** 연산 결과 ----> 곱하기 : " << a * b << "입니다.";
        break;
    case '/':
        if (b != 0)
            cout << "**** 연산 결과 ----> 나누기 : " << a / b << "입니다.";
        else
            cout << "b가 0이므로 나눌 수 없습니다.";
        break;
    case '+':
        cout << "**** 연산 결과 ----> 더하기 : " << a + b << "입니다.";
        break;
    case '-':
        cout << "**** 연산 결과 ----> 빼기 : " << a - b << "입니다.";
        break;
    case '%':
        cout << "**** 연산 결과 ----> 나머지 : " << a % b << "입니다.";
        break;
    default:
        cout << "잘못 입력하셨습니다.";
    }
}
```
