# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day8

## 이 코드는 C++ 언어의 std::vector와 std::list에 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 연습 예제 코드 : 벡터

자동 크기 조정 (push_back(), resize()), 안전한 메모리 관리, 다양한 함수 지원

```cpp
#include <iostream>
#include <vector> // 벡터 사용을 위해 추가
#include <algorithm> // 정렬을 위해 추가
using namespace std;

int main() {
	vector<int> vec1 = { 1,2,3,4 };
	vector<int> vec2(5, 10);

	for (int i = 0; i < size(vec1); i++) {
		cout << vec1[i] << " ";
	}
	cout << endl << endl;

	for (int i = 0; i < size(vec2); i++) {
		cout << vec2[i] << " ";
	}
	cout << endl << endl;

	// begin, end 사용
	for (int i = 0; i < vec1.end() - vec1.begin(); i++) {
		cout << vec1[i] << " ";
	}
	cout << endl << endl;

	// 반복자로 배열의 모든 요소에 접근하는 방법
	for (vector<int>::iterator it /*it는 일종의 포인터*/ = vec1.begin(); it < vec1.end(); it++) { // 반복자를 하나씩 불러냄
		cout << *it << " "; // it가 일종의 포인터이기 때문에 값에 접근하려면 역참조
	}
	cout << endl << endl;

	// auto는 자동으로 타입 추론
	for (auto it = vec1.begin(); it < vec1.end(); it++) {
		cout << *it << " ";
	}
	cout << endl << endl;

	// 값 추가
	vec1.push_back(5);
	for (int i = 0; i < size(vec1); i++) {
		cout << vec1[i] << " ";
	}
	cout << endl << endl;
	// 값 제거
	vec1.pop_back();
	for (int i = 0; i < size(vec1); i++) {
		cout << vec1[i] << " ";
	}
	cout << endl << endl;
	// 중간 값 추가
	vec1.insert(vec1.begin() + 2, 10);
	for (int i = 0; i < size(vec1); i++) {
		cout << vec1[i] << " ";
	}
	cout << endl << endl;
	// 중간 값 삭제
	vec1.erase(vec1.begin() + 2);
	for (int i = 0; i < size(vec1); i++) {
		cout << vec1[i] << " ";
	}
	cout << endl << endl;

	vector<int> vec3 = { 2,5,9,4,6,1,3,7,8 };
	// sort(처음 반복자, 마지막 반복자)
	sort(vec3.begin(), vec3.end());
	for (int i = 0; i < size(vec3); i++) {
		cout << vec3[i] << " ";
	}
	cout << endl << endl;
}

```

---

## 🔹 연습 예제 코드: 이차원 벡터

벡터를 요소로 가지는 행렬(Matrix)과 유사한 벡터

```cpp
#include <iostream>
#include <vector> // 벡터 사용을 위해 추가
#include <algorithm> // 정렬을 위해 추가
using namespace std;

int main() {

	// 이차원 벡터
	vector<vector<int>> vec4 = { {1,2,3},{4,5,6},{7,8,9} };

	for (int i = 0; i < size(vec4); i++) {
		for (int j = 0; j < size(vec4[i]); j++) {
			cout << vec4[i][j] << " ";
		}
		cout << endl;
	}
	cout << endl;
	// 이차원 벡터(3*3) 0으로 초기화
	vector<vector<int>> vec5(3, vector<int>(3, 0));
	for (int i = 0; i < size(vec5); i++) {
		for (int j = 0; j < size(vec5[i]); j++) {
			cout << vec5[i][j] << " ";
		}
		cout << endl;
	}
	cout << endl;
}
```

---

## 🔹 실습 1 : vector 조작하기

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
	// 1. Vector를 사용하여 정수를 저장하는 빈 벡터 선언
	vector<int> vec = {};

	int input1;
	// 2. 사용자로부터 5개의 정수를 입력받아 벡터에 추가
	cout << "정수 5개를 입력하세요 : ";
	for (int i = 0; i < 5; i++) {
		cin >> input1;
		vec.push_back(input1);
	}
	cout << endl;

	// 3. 벡터의 크기 출력
	cout << "벡터의 크기 출력 : " << vec.size() << endl << endl;

	// 4. 벡터의 모든 원소 출력
	cout << "벡터의 모든 원소 출력 : ";
	for (vector<int>::iterator it = vec.begin(); it < vec.end(); it++) {
		cout << *it << " ";
	}
	cout << endl << endl;

	// 5. 가장 큰 값을 찾아 출력
	int maxV = 0;
	for (int i = 0; i < vec.size(); i++) {
		if (maxV < vec[i]) maxV = vec[i];
	}

	vector<int> vec2 = vec;
	sort(vec2.begin(), vec2.end());
	cout << "가장 큰 값 출력 : " << vec2[4] << endl << endl;
	cout << "가장 큰 값 출력 : " << maxV << endl << endl;

	// 6. 벡터의 모든 원소를 두배로
	cout << "벡터의 모든 원소를 두배로 : ";
	for (int i = 0; i < vec.size(); i++) {
		vec[i] *= 2;
	}
	// for (int& num : vec) num *= 2;

	for (int i = 0; i < vec.size(); i++) {
		cout << vec[i] << " ";
	}
	cout << endl << endl;

	// 7. 인덱스를 입력받아 해당 인덱스에 있는 원소 제거
	int input2;
	cout << "지우고자 하는 인덱스를 입력하세요 (0~4) : ";
	while (true) {
		cin >> input2;
		if (input2 <= 4 && input2 >= 0){
			break;
		}
		else {
			cout << "값을 벗어났습니다. 다시 입력하세요 : ";
		}
	}

	vec.erase(vec.begin() + input2);

	for (int i = 0; i < vec.size(); i++) {
		cout << vec[i] << " ";
	}
	cout << endl << endl;

	// 8. 인덱스를 입력받아 해당 인덱스에 있는 새로운 원소 삽입
	int input3;
	int num3;
	cout << "추가 하고자 하는 인덱스를 입력하세요 (0~4) : ";
	while (true){
		cin >> input3;
		if (input3 <= 4 && input3 >= 0) {
			cout << "추가하고자 하는 값을 입력하세요 : ";
			cin >> num3;
			break;
		}
		else {
			cout << "값을 벗어났습니다. 다시 입력하세요 : ";
		}
	}

	vec.insert(vec.begin() + input3, num3);

	for (int i = 0; i < vec.size(); i++) {
		cout << vec[i] << " ";
	}
	cout << endl << endl;

}
```

---

## 🔹 실습 2 : 2차원 행렬 만들기

사용자가 입력한 행(rows)과 열(cols) 크기에 맞는 동적 2차원 배열을 생성하고, 각 요소를 (i + 1) \* (j + 1) 값으로 초기화한 후, 출력하는 프로그램

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
	int row, col;
	cout << "행과 열 입력 : ";
	cin >> row >> col;

	vector <vector<int>> vec2(row, vector<int>(col));

	for (int i = 0; i < row; i++) {
		for (int j = 0; j < col; j++) {
			vec2[i][j] = (i + 1) * (j + 1);
		}
	}

	for (int i = 0; i < row; i++) {
		for (int j = 0; j < col; j++) {
			cout << vec2[i][j] << " ";
		}
		cout << endl;
	}
}
```

---

## 🔹 실습 3 : 2차원 행렬 만들기

사용자가 입력한 행(rows)과 열(cols), 행렬의 원소를 직접 입력하도록 구현하고 각 행과 열의 합을 구하는 프로그램

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {

	// 사용자가 입력한 행(rows)과 열(cols), 행렬의 원소를 직접 입력하도록 구현하고 각 행과 열의 합을 구하도록 구현해보세요.
	int row, col;
	cout << "행과 열 입력 : ";
	cin >> row >> col;

	vector <vector<int>> vec3(row, vector<int>(col));
	cout << "행렬 원소를 입력하세요 : " << endl;
	for (int i = 0; i < row; i++) {
		int inputNum;
		for (int j = 0; j < col; j++) {
			cin >> inputNum;
			vec3[i][j] = inputNum;
		}
	}
	cout << "각 행의 합 : " << endl;
	for (int i = 0; i < row; i++) {
		int rowSum = 0;
		for (int j = 0; j < col; j++) {
			rowSum += vec3[i][j];
		}
		cout << "행 " << i + 1 << ": " << rowSum << endl;
	}

	cout << endl << "각 열의 합 : " << endl;
	for (int i = 0; i < col; i++) {
		int colSum = 0;
		for (int j = 0; j < row ; j++) {
			colSum += vec3[j][i];
		}
		cout << "열 " << i + 1 << ": " << colSum << endl;
	}

}
```

---

## 🔹 연습 예제 코드 : 리스트

연속적으로 저장하는 자료구조 (연결 리스트(Linked List) 기반으로 동작)

```cpp
#include <iostream>
#include <vector>
#include <list>
using namespace std;

int main() {
	list<int> myList = { 10,20,30,40,50,60 };
	myList.push_back(60);
	myList.push_front(0);

	for (int num : myList) {
		cout << num << " ";
	}
	cout << endl << endl;

	myList.pop_back();
	myList.pop_front();
	for (int num : myList) {
		cout << num << " ";
	}
	cout << endl << endl;

	auto it = myList.begin();
	advance(it, 2);
	myList.insert(it, 60);
	for (int num : myList) {
		cout << num << " ";
	}
	cout << endl << endl;

	advance(it, 1);
	myList.erase(it);
	for (int num : myList) {
		cout << num << " ";
	}
	cout << endl << endl;

	myList.remove_if([](int n) {return n % 2 == 0; }); // 임시로 만든 람다 함수

	list<int> myList2 = { 70,80,90,100,110 };
	myList.merge(myList2);
	for (int num : myList) {
		cout << "여기" << num << " ";
	}
	cout << endl << endl;
	myList.unique(); // 연속된 중복값 제거
	for (int num : myList) {
		cout << num << " ";
	}
	cout << endl << endl;
	myList.splice(++myList.begin(),myList2);
	for (int num : myList) {
		cout << num << " ";
	}
	cout << endl << endl;


	for (auto it = myList.begin(); it != myList.end(); it++) {
		cout << *it << endl;
	}
}
```

---

## 🔹 실습 1 :

list 사용해보기

```cpp
#include <iostream>
#include <list>
#include <algorithm>
using namespace std;

int main() {
  // 1. std::list<int> myList = {5, 4, 3, 4, 2, 1, 1};
	list<int> myList = { 5,4,3,4,2,1,1 };

  // 2. 4가 몇 개인지 출력
	int count4=count(myList.begin(), myList.end(), 4);
	cout << "count 4 : " << count4 << endl << endl;

  // 3. {1, 1, 2, 3, 4, 4, 5} 가 나오도록 리스트 변경
	list<int> myList2 = myList;
	myList2.sort();
	cout << "sort : ";
	for (int num : myList2) {
		cout << num << " ";
	}
	cout << endl << endl;

  // 4. {1, 2, 3, 4, 5} 가 나오도록 리스트 변경
	cout << "unique : ";
	myList2.unique();
	for (int num : myList2) {
		cout << num << " ";
	}
	cout << endl << endl;

  // 5. {1, 2, 3, 4, 5, 6, 7} 이 나오도록 리스트 변경
	cout << "merge : ";
	list<int> myList3 = { 6,7 };
	myList2.merge(myList3);
	for (int num : myList2) {
		cout << num << " ";
	}
	cout << endl << endl;

  // 6. {0, 1, 2, 3, 4, 5, 6, 7} 이 나오도록 리스트 변경
	myList2.push_front(0);
	cout << "push_front : ";
	for (int num : myList2) {
		cout << num << " ";
	}
	cout << endl << endl;

  // 7. 3~6은 리스트에만 존재하는 함수 사용
}
```
