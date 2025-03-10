# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day7

## 이 코드는 C++ 언어의 비트연산자 연습문제를 포함하고 있습니다.

---

## 🔹 실습 1 : 특정 비트 설정

num = 0b00010010(10진수 18)에서 5번째 비트를 1로 설정한 결과를 출력하세요.

```cpp
#include <iostream>
#include <bitset>
using namespace std;

int main() {
   int num1 = 0b00010010;
   cout << "1번 : " << bitset<8>(0b00100000 | num1) << endl << endl;
}
```

---

## 🔹 실습 2 : 특정 비트 제거

▪ num = 0b10101111(10진수 175)에서 2번째 비트를 0으로 변경한 결과를 출력하세요.

```cpp
#include <iostream>
#include <bitset>
using namespace std;


int main() {
    int num2 = 0b10101111;
    cout << "2번 : " << bitset<8>(0b00000100 ^ num2) << endl << endl;
}
```

---

## 🔹 실습 3 : 특정 비트 반전

num = 0b11011010(10진수 218)에서 4번째 비트를 반전시킨 결과를 출력하세요.

```cpp
#include <iostream>
#include <bitset>
using namespace std;

int main() {
   int num3 = 0b11011010;
   cout << "3번 : " << bitset<8>(0b00010000 ^ num3) << endl << endl;
}
```

---

## 🔹 실습 4 : 특정 비트 값 추출

▪ 임의의 num이 주어졌을 때 4번째 비트를 추출하여 출력하세요.

```cpp
#include <iostream>
#include <bitset>
using namespace std;

int main() {
    int num4;
    cout << "4번 : 정수를 입력하세요.";
    cin >> num4;
    if ((num4 & 0b00010000) == 16)
        cout << "4번 : 1" << endl << endl;
    else
        cout << "4번 : 0" << endl << endl;
}
```

---

## 🔹 실습 5 : 짝수 / 홀수 판별

임의의 num이 주어졌을 때, 홀수인지 짝수인지 비트 연산자로 판별하세요.
• 홀수/짝수 2진수 표현의 특징을 생각해봅시다.

```cpp
#include <iostream>
#include <bitset>
using namespace std;

int main() {
    int num5;
    cout << "5번 : 정수를 입력하세요.";
    cin >> num5;
    if ((num5 & 0b00000001) == 1)
        cout << "5번 : 참입니다." << endl << endl;
    else
        cout << "5번 : 거짓입니다." << endl << endl;
}
```

---

## 🔹 실습 6 : 2의 거듭 제곱 판별

▪ 임의의 num이 주어졌을 때, 2의 거듭제곱인지 확인하세요.
• 2의 거듭제곱의 2진수 표현의 특징을 생각해봅시다.

```cpp
#include <iostream>
#include <bitset>
using namespace std;

int main() {
    int num6;
    cout << "6번 : 정수를 입력하세요.";
    cin >> num6;
    int compare6 = 0b00000001;
    int switchNum6 = 0;
    for (int i = 0; i < 8; i++) {
        if (num6 == compare6)
            switchNum6 = 1;
        compare6 <<= 1;
    }
    cout << "6번 : " << (switchNum6 == 1 ? "2진수로 1이 존재합니다" : "2진수로 1이 존재하지 않습니다") << endl << endl;
    if (switchNum6 == 1)
        cout << "6번 : 2진수로 1이 존재합니다." << endl << endl;
    else
        cout << "6번 : 2진수로 1이 존재하지 않습니다." << endl << endl;

    bool compare6_1 = num6 & (num6 - 1);
    cout << "6번 : 2진수로 1이 존재" << (compare6_1 ? "하지 않습니다" : "합니다") << endl << endl;
```

---

## 🔹 실습 7: 가장 왼쪽에 있는 1비트의 위치 찾기

▪ 임의의 num이 주어졌을 때 가장 왼쪽의 1이 위치한 비트 자리를 출력하세요.
• num은 char로 선언해주세요
• 4번 문제를 참고해주세요
• 반복문을 활용합니다

```cpp
#include <iostream>
using namespace std;

int main() {
    int num7;
    cout << "7번 : 정수를 입력하세요.";
    cin >> num7;
    int compare7 = 0b10000000;
    int compareNum7 = 128;
    int switchNum7 = 7;

    1이 처음 나오는 위치 찾기
    while ((num7 & compare7) != compareNum7) {
        compare7 >>= 1;
        compareNum7 /= 2;
        switchNum7 -= 1;
    }

    int position = 0;
    for (int i = 7; i >= 0; i--) {
        if (num7&(1 << i)) {
            position = i;
            break;
        }
    }

    cout << "7번 : 1이 처음 나오는 위치: " << switchNum7 << "번 위치입니다." << endl << endl;
}
```

---

## 🔹 실습 8: 가장 오른쪽에 있는 1비트의 위치 찾기

임의의 num이 주어졌을 때, 가장 오른쪽의 1비트가 위치한 자리수를 출력하세요.
• 2의 보수법을 활용합니다
• while과 >>을 활용해서 자리수를 계산합니다

```cpp
#include <iostream>
using namespace std;

int main() {
    int num8;
    cout << "8번 : 정수를 입력하세요.";
    cin >> num8;
    int compare8 = 0b00000001;
    int compareNum8 = 1;
    int switchNum8 = 1;

    if (num8 == 0) {
        cout << "입력된 값은 0입니다." << endl;
    }
    else {
        while ((num8 & compare8) != compareNum8) {
            compare8 <<= 1;
            compareNum8 *= 2;
            switchNum8 += 1;
        }
        cout << "8번 : 1이 처음 나오는 위치: " << switchNum8 << "번째 입니다." << endl << endl;
    }
}
```
