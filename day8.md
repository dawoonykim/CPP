# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day8

## 이 코드는 C++ 언어의 포인터와 함수 포인터에 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 연습 예제 코드: 포인터

포인터의 타입 캐스트

```cpp
#include <iostream>
using namespace std;

int main() {
    // void
    int i = 0;
    char c = 'a';
    short s = 10;
    double d = 3.14;

    void* ptr = nullptr;

    ptr = &i;
    int* iTemp = (int*)ptr; // 타입캐스트
    cout << *iTemp << endl;
    ptr = &c;
    char* cTemp = (char*)ptr; // 타입캐스트
    cout << *cTemp << endl;
    ptr = &s;
    short* sTemp = (short*)ptr; // 타입캐스트
    cout << *sTemp << endl;
    ptr = &d;
    double* dTemp = (double*)ptr; // 타입캐스트
    cout << *dTemp << endl;
}

```

---

## 🔹 연습 예제 코드: 포인터

동적 메모리 할당과 동적 배열

```cpp
#include <iostream>
using namespace std;


int main() {
    // 힙에 정수 공간 할당
    int* iPtr = new int(10); // 포인터는 해당 메모리 주소를 담기 때문에 동적 메모리를 할당할 수 있음
    cout << *iPtr << endl;

    // 메모리 해제
    delete iPtr;

    // 동적 배열 생성
    int idx;
    cout << "배열의 크기는? ";
    cin >> idx;
    int* iArr = new int[idx]; // 동적 배열 할당

    for (int i = 0; i < idx; i++) {
        cout << "iArr[" << i << "]에 입력할 수는? ";
        cin >> iArr[i];
    }

    for (int i = 0; i < idx; i++) {
        cout << "출력 : " << iArr[i] << endl;
    }

    cout << iArr << endl;
    delete[] iArr; // 메모리 해제
}
```

---

## 🔹 연습 예제 코드: 포인터

이중 포인터와 2차원 배열

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 100;
    int* ptr = &a;
    int** dPtr = &ptr;

    cout << **dPtr << endl;

    cout << "포인터     : " << ptr << endl;
    cout << "이중포인터 : " << *dPtr << endl;

    // 3*3 배열
    int row = 3;
    int col = 3;

    int** matrix = new int* [row]; // 이중포인터에는 포인터를 담아줘야 함 => row를 생성
    for (int i = 0; i < row; i++) {
        matrix[i] = new int[col];
    }

    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col; j++) {
                matrix[i][j] = i + j;
        }
    }

    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col; j++) {
            cout << matrix[i][j] << " ";
        }
        cout << endl;
    }

    for (int i = 0; i < row; i++) {
        delete[] matrix[i];
    }
    delete[] matrix;
}
```

---

## 🔹 실습1 : 동적 2차원 배열 생성 및 해제

포인터로 동적 2차원 배열 생성 및 자원 해제 프로그램

```cpp
#include <iostream>
using namespace std;

int main() {
    int rows, cols;
    cout << "행과 열을 입력하세요. ";
    cin >> rows >> cols;

    int** matrix = new int* [rows];

    for (int i = 0; i < rows; i++) {
    	matrix[i] = new int[cols];
    }

    for (int i = 0; i < rows; i++) {
    	for (int j = 0; j < cols; j++) {
    		matrix[i][j] = (i + 1) * (j + 1);
    	}
    }

    for (int i = 0; i < rows; i++) {
    	for (int j = 0; j < cols; j++) {
    		cout << matrix[i][j] << " ";
    	}
    	cout << endl;
    }

    for (int i = 0; i < rows; i++) {
    	delete[] matrix[i];
    }

    delete[] matrix;
}
```

---

## 🔹 연습 예제 코드 : 함수 포인터

포인터를 반환하는 함수

```cpp
#include <iostream>
using namespace std;

void coutFunc() {
	cout << "출력" << endl;
}

void myCallback() {
	cout << "콜백입니다." << endl;
}

// 인자에 함수를 전달할 수 있는 함수 => 고차함수
void coutFunc1(void (*myCallback)()) {
	cout << "함수를 실행합니다." << endl;
	myCallback();
}

int add(int a, int b) {
	return a + b;
}

int main() {

    //cout << coutFunc << endl; // => 함수의 메모리 주소 출력
    void (*funcPtr)() = nullptr;
    funcPtr = coutFunc;
    funcPtr();

    int (*addPtr)(int, int) = nullptr;
    addPtr = add;
    cout << addPtr(3, 5) << endl;

    coutFunc1(myCallback);
}
```

---

## 🔹 실습 2 :

함수 포인터를 사용한 계산기

```cpp
#include <iostream>
using namespace std;

int add(int a, int b) {
	return a + b;
}

int sub(int a, int b) {
	return a - b;
}

int mul(int a, int b) {
	return a * b;
}

float divide(int a, int b) {
	return 	b != 0 ? float(a) / b : 0;
}

int main() {
    int a, b;
    char c;

    cout << "계산하려고 하는 두 정수를 입력하세요. ";
    cin >> a >> b;
    cout << "연산자(+, -, *, /)를 입력하세요.";
    cin >> c;

    int (*addPtr)(int, int) = nullptr;
    int (*subPtr)(int, int) = nullptr;
    int (*mulPtr)(int, int) = nullptr;
    float(*divPtr)(int, int) = nullptr;

    int(*ASMPtr)(int, int) = nullptr;
    float(*DPtr)(int, int) = nullptr;

    switch (c) {
        case '+':
            addPtr = add;
            ASMPtr = add;
            cout << addPtr(a, b) << endl;
            break;
        case '-':
            subPtr = sub;
            ASMPtr = sub;
            cout << subPtr(a, b) << endl;
            break;
        case '*':
            mulPtr = mul;
            ASMPtr = mul;
            cout << mulPtr(a, b) << endl;
            break;
        case '/':
            divPtr = divide;
            DPtr = divide;
            if (b != 0) cout << divPtr(a, b) << endl;
            else cout << "계산할 수 없습니다." << endl;

            break;
        default:
            cout << "잘못입력했습니다." << endl;
    }

    if (c == '+' || c == '-' || c == '*') cout << ASMPtr(a, b) << endl;
    else if (c == '/') {
        if (b != 0) {
            cout << DPtr(a, b) << endl;
        }else {
            cout << "계산할 수 없습니다." << endl;
        }

    }else cout << "잘못입력했습니다." << endl;
}
```
