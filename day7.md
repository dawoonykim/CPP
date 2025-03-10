# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day7

## 이 코드는 C++ 언어의 포인터에 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 연습 코드: 포인터

다른 변수의 메모리 주소를 저장하는 변수 활용

```cpp
#include <iostream>
using namespace std;

int main() {

    int i = 0;
    cout << "i 주소   : " << &i << endl;

    int* ptr = &i;
    cout << "ptr 주소 : " << ptr << endl;
    cout << "ptr 값   : " << *ptr << endl;

    int* iPtr = nullptr;
    int* iPtr = &i;

    float f = 3.14f;
    short s = 100;

    short* sPtr = &s;

    cout << "포인터 크기 : " << sizeof(iPtr) << endl;
    cout << "포인터 크기 : " << sizeof(sPtr) << endl;


    cout << "ptr 주소 : " << iPtr << endl;
    cout << "ptr 값   : " << *iPtr << endl; // 역참조 => 그 주소에 담긴 값 출력


    int i = 0;
    int* iPtr = &i;
    cout << "int 주소 계산" << endl;
    cout << iPtr << endl;
    cout << iPtr + 1 << endl;
    *iPtr = 100; // 역참조로 값 바꿔주기
    cout << i << endl << endl;

    short s = 100;
    short* sPtr = &s;
    cout << "short 주소 계산" << endl;
    cout << sPtr << endl;
    cout << sPtr + 1 << endl << endl;

    int iArr[4] = { 10,20,30,40 };
    cout << "배열의 주소 표현" << endl;
    cout << iArr << endl;
    cout << *iArr << endl; // 역참조
    cout << iArr + 1 << endl;
    cout << *(iArr + 1) << endl; // 역참조

    cout << "배열의 인덱스로 접근" << endl;
    cout << *(iArr + 0) << " (*(iArr + 0))==(iArr[0]) " << iArr[0] << endl; // 역참조
    cout << *(iArr + 1) << " (*(iArr + 1))==(iArr[1]) " << iArr[1] << endl; // 역참조
    cout << *(iArr + 2) << " (*(iArr + 2))==(iArr[2]) " << iArr[2] << endl; // 역참조
    cout << *(iArr + 3) << " (*(iArr + 3))==(iArr[3]) " << iArr[3] << endl; // 역참조
    cout << sizeof(iArr) << endl << endl;
}
```

---

## 🔹 실습 1 :

포인터 주소로 실행한 코드의 결과 값

```cpp
#include <iostream>
using namespace std;


int main() {
    char cArr[4] = { 1,1,1,1 };
    short* shortPtr = (short*)cArr;
    short sData = *(shortPtr + 1);
    cout << "실습 1번 정답 : " << (int)sData << endl;
    // 00000001 1
    // 00000001 1
    // 00000001 1
    // 00000001 1

    // (00000001 00000001) (v 00000001 00000001 == (int)257)
}
```

---

## 🔹 실습 2 :

포인터 주소로 실행한 코드의 결과 값

```cpp
#include <iostream>
using namespace std;

int main() {
    short sArr[6] = { 256,257,258,259,260,261 };
    char* pC = (char*)sArr;
    char cData = *(pC + 3);
    cout << "실습 2번 정답 : " << (int)cData << endl;
    // 00000001 00000000 256
    // 00000001 00000001 257
    // 00000001 00000010 258
    // 00000001 00000011 259
    // 00000001 00000100 260
    // 00000001 00000101 261

    // (00000001) (00000000) (00000001) (v 00000001 == (int)1) (00000001) (00000010) (00000001) (00000011) (00000001) (00000100) (00000001) (00000101)
}
```

---

## 🔹 연습 예제 코드 : const 포인터

값을 변경할 수 없는 포인터와 포인터가 가리키는 주소를 변경할 수 없는 포인터

```cpp
#include <iostream>
using namespace std;

// 주소로 값을 전달 => 효율적
void coutFunc(const int* x) {
	cout << "출력 : " << *x << endl;
}

int main() {
    const int iVar = 0; // read-only

    int myVar = 100;

    int i = 100;
    int* iPtr = &i;
    // *iPtr = 100; // 값 변경
    int j = 200;

    // 1. 바라보는 주소의 값을 바꾸는 걸 방지
    const int* iPtr1 = &i;
    // *iPtr1 = 200; // 값 수정 불가
    iPtr1 = &j; // 주소 변경 가능
    i = 400;

    // 2. 바라보는 주소를 바꾸는 걸 방지
    int* const iPtr2 = &i;
    *iPtr2 = 200; // 값 변경 가능
    // iPtr2 = &j; // 주소 수정 불가

    // 3. 바라보는 주소와 값을 모두 바꾸는 걸 방지
    const int* const iPtr3 = &i;
    int a = 100;
    coutFunc(&a);
}
```
