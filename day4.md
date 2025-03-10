# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day4

## 이 코드는 C++ 언어의 반복문과 배열에 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 연습 코드 : for, while, do-while, break에 대한 문법 이해도를 높이기 위한 코드

```cpp
#include <iostream>
using namespace std;

int main() {

    for (int i = 0; i < 10; i++) {
        cout << i << endl;
    }

    int count = 0;
    while (count < 5) {
        cin >> count;
        cout << count << "-번째" << endl;
    }

    int i = 5;
    do {
        i++;
    } while (i < 5);
    cout << i << endl;

    for (int i = 0; i < 5; i++) {
        if (i == 3)
            break;
        cout << "반복 : " << i << endl;
    }
    cout << "반복 종료" << endl;
```

---

## 🔹 실습 1: for문을 활용한 별 출력

정수를 입력받아, 각 줄마다 별을 하나씩 증가시켜 출력하는 프로그램

```cpp
#include <iostream>
using namespace std;

int main() {
      // 왼쪽 정렬 별 찍기 코드
      int num;
      cout << "input : ";
      cin >> num;
      cout << "output : ";
      for (int i = 0; i <= num; i++) {
          for (int j = 0; j < i; j++) {
              cout << "*";
          }
          cout << endl;
      }
      // 위의 for문의 코드의 리팩토링
      for (int i = 0; i <= num; i++) {
          cout << string(i, '*') << endl;
      }
      // 오른쪽 정렬 별 찍기 코드
      for (int i = 0; i <= num; i++) {
          for (int j = num; j > i; j--) {
              cout << " ";
          }
          for (int k = 0; k < i; k++) {
              cout << "*";
          }
          cout << endl;
      }
      // 위의 for문의 코드의 리팩토링
      for (int i = 0; i <= num; i++) {
          cout << string(num - i, ' ') << string(i, '*') << endl;
      }
}
```

---

## 🔹 실습 2: 구구단 출력

구구단 출력 프로그램

```cpp
#include <iostream>
using namespace std;

int main() {
    // 입력 받은 정수에 해당하는 구구단 출력
    int dan;
    cout << "몇 단? : ";
    cin >> dan;
    cout << dan << "단 출력" << endl;
    for (int i = 1; i < 10; i++) {
        cout << dan << " * " << i << " = " << dan * i << endl;
    }

    // 1~9단의 모든 구구단 출력
    for (int i = 1; i <= 9; i++) {
        cout << "-----" << i << "단-----" << endl;
        for (int j = 1; j <= 9; j++) {
            cout << i << " * " << j << " = " << i * j << endl;
        }
    }
}
```

---

## 🔹 실습 3: do-while문을 활용한 입력한 수만큼 합계 계산

0을 제외한 숫자를 더하는 프로그램 (0은 프로그램 종료)

```cpp
#include <iostream>
using namespace std;

int main() {
      int num = 0;
      int input;
      cout << "숫자 입력 후 합계 계산" << endl;

      do {
          cout << "숫자 입력 (0 : exit) : ";
          cin >> input;
          num += input;
      } while (input != 0);

      cout << "입력된 숫자들의 합 : " << num << endl;
}
```

---

## 🔹 연습 예제 코드 : 배열에 대한 문법 이해도를 높이기 위한 코드

## 🔹 배열 예제 1

```cpp
#include <iostream>
using namespace std;

int main() {
    int numbers[5] = { 10, 20, 30, 40, 50 };
    // 배열 출력 : 배열명[인덱스]
    for (int i = 0; i < 5; i++) {
        cout << numbers[i] << endl;
    }
    // 배열 출력 : for-each
    for (int num : numbers) {
        cout << num << endl;
    }

    // input으로 배열에 동적으로 값 할당
    int input;
    for (int i = 0; i < 5; i++) {
        cout << "numbers[" << i << "] : ";
        cin >> input;
        numbers[i] = input;
    }

    for (int i = 0; i < 5; i++) {
        cout << numbers[i] << endl;
    }

    for (int num : numbers) {
        cout << num << endl;
    }
}
```

---

## 🔹 배열 예제 2

input으로 배열에 동적으로 요소를 할당하고, 각 요소를 for문과 for-each문으로 출력하는 프로그램

```cpp
#include <iostream>
using namespace std;

int main() {
    string city2[5] = {};
    for (int i = 0; i < 5; i++) {
        cout << "city2[" << i << "] : ";
        cin >> city2[i];
    }
    for (int i = 0; i < sizeof(city2) / sizeof(city2[0]); i++) {
        cout << " city2[" << i << "] : " << city2[i] << endl;
    }
    for (string city : city2) {
        cout << city << endl;
    }
}
```

---

## 🔹 배열 예제 3

input으로 배열에 동적으로 요소를 할당하고, 평균을 구하는 프로그램

```cpp
#include <iostream>
using namespace std;

int main() {
    int grade[5] = {};
    int sum = 0;
    for (int i = 0; i < 5; i++) {
        cout << i + 1 << "번째 학생의 점수는? : ";
        cin >> grade[i];
        sum += grade[i];
    }

    float avg = sum / 5.0;
    float average = (float)sum / 5;
    cout << "첫 번째 평균 : " << avg << endl;
    cout << "두 번째 평균 : " << average << endl;
}
```
