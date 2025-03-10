# 🖥️ C++ 기초 코드 모음

## 📌 개요

## 이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

## 🔹 day1

C++ 언어를 처음 접할 때 기초적인 문법이 포함되어 있습니다.

```cpp
// # => 전처리기 (# 프로그램 시작 전에 복사)
#include <iostream> // input, output stream
using namespace std;

int add(int a, int b) {
	return a + b;
}

int main() {

	cout << "hello world!" << endl;

	for (int i = 1; i <= 10; i++) {
		cout << i << " ";
	}

	cout << "\n";
	int result = add(3, 5);
	cout << result;

	// return 0;
}
```
