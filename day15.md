# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day15

## 이 코드는 C++ 언어의 제네릭 템플릿과 스마트 포인터에 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 연습 예제 코드 : 제네릭 프로그래밍

다양한 타입 추론을 연습할 수 있는 프로그램

```cpp
#include <iostream>
using namespace std;

// 타입 추론을 위한 제네릭 템플릿 선언
template <typename T>
T add1(T a, T b) {
	return a + b;
}

template <typename T, typename D>
void add2(T a, D b) {
	cout << a << b << endl;
}

class Test {
public:
	T data;
	Test(T d) : data(d) {}

	void show() {
		cout << data << endl;
	}
};
template <typename T>
class Parent {
public:
	T data;
	Parent(T d) : data(d) {}

	void show() {
		cout << data << endl;
	}
};

//class Child :public Parent<int> {
//public:
//	Child(int d) :Parent(d) {}
//};

template <typename T>
class Child :public Parent<T> {
public:
	Child(T d) :Parent<T>(d) {}
};

int main() {
	vector<자료형> // 템플릿이 사용됨
	cout << add1(1, 3) << endl;
	cout << add1(1.1, 3.1) << endl;
	cout << add1<int>(1.1, 3.1) << endl; // 강제 형 변환
	cout << add1("가나다", "라마바") << endl;// 자료형이 같으면 에러는 없으나 컴파일 시 에러가 발생할 수 있음

	// ---------------------------------------------------------------------------------------------------

	Test<string> t1("테스트데이터");
	Test<int> t2(100);

	cout << t1.data << endl;
	cout << t2.data << endl;

	t1.show();
	t2.show();
}
```

---

## 🔹 실습 1 : 두 개의 값을 저장하는 클래스 구현

두 개의 값을 저장하는 Pair 클래스 구현

```cpp
#include <iostream>
using namespace std;

// 1. Pair<T1, T2> 클래스는 두 개의 서로 다른 타입을 저장할 수 있어야 합니다.
template <typename T1, typename T2>
class Pair {
	T1 first;
	T2 second;

public:
  // 2. 생성자를 통해 초기 값을 설정할 수 있어야 합니다.
  //Pair(T1 t1, T2 t2) {
  //	this->first = t1;
  //	this->second = t2;
  //}
  Pair(T1 t1, T2 t2) :first(t1), second(t2) {};

  // 3. show() 멤버 함수를 통해 저장된 값을 출력해야 합니다.
	void show() {
		cout << "first : " << first << ", second : " << second << endl;
	}


  // 4. getFirst(), getSecond() 함수를 구현하여 각 값을 반환해야 합니다.
	T1 getFirst() {
		return first;
	}
  T2 getSecond() {
		return second;
	}

  // 5. setFirst(), setSecond() 함수를 구현하여 값을 변경할 수 있어야 합니다
  void setFirst(T1 t1) {
		this->first = t1;
	}
	void setSecond(T2 t2) {
		this->second = t2;
	}
  // 직접 멤버 변수에 접근하는 것을 방지하여, 예상치 못한 값이 할당되는 것을 막고, 유효성 검사를 추가
};

int main() {
	Pair<int, int> p1(10, 20);
	p1.show();

	p1.setFirst(30);
	cout << p1.getFirst() << endl;
	p1.show();

	p1.setSecond(100);
	cout << p1.getSecond() << endl;
	p1.show();
}
```

---

## 🔹 연습 예제 코드 : 스마트 포인터

자동으로 메모리를 관리해주는 포인터

```cpp
#include <iostream>
#include <memory> // 스마트 포인터를 사용하기 위한 라이브러리
using namespace std;

class Car {
public:
	void show() {
		cout << "부릉부릉" << endl;
	}
};

unique_ptr<Car> createCar() {
	return make_unique<Car>();
	// make_unique<Car>()를 반환하기 때문에 반환 타입은 unique_ptr<Car>
}

class Parent {
public:
	virtual void show() {
		cout << "부모 클래스입니다." << endl;
	}
};

class Child :public Parent {
public:
	void show() override {
		cout << "자녀 클래스입니다." << endl;
	}

	void eat() {
		cout << "밥을 먹습니다." << endl;
	}
};

int main() {
	int a = 10;
	int* ptr1 = &a;

	int* ptr2 = new int(10);
	delete ptr2;

	unique_ptr<int> smartPtr = make_unique<int>(10); // 스마트 포인터는 동적 메모리(힙) 영역에 할당되지만 delete를 사용해서 해제를 할 필요가 없음
	cout << "smartPtr의 주소 : " << smartPtr << endl;
	cout << "smartPtr의 값   : " << *smartPtr << endl;

	unique_ptr<int> smartPtr2 = move(smartPtr); // move 함수를 사용해서 참조해야 함

	unique_ptr<Car> smartPtr3 = make_unique<Car>();
	smartPtr3->show();


	shared_ptr<Car> smartPtr4 = make_shared<Car>();
	shared_ptr<Car> smartPtr5 = smartPtr4; // 같은 타입의 포인터를 담아낼 수 있음

	// 스마트 포인터의 업캐스팅과 다운캐스팅 연습
	shared_ptr<Child> child = make_shared<Child>(); // child를 가리키는 포인터
	cout << "child show : ";
	child->show();
	cout << "child eat : ";
	child->eat();
	shared_ptr<Parent> parent = child; // 업 캐스팅
	cout << "parent show : ";
	parent->show();

	shared_ptr<Child> parentToChild = dynamic_pointer_cast<Child>(parent); // 다운 캐스팅
	cout << "parentToChild show : ";
	parentToChild->show();
	cout << "parentToChild eat : ";
	parentToChild->eat();
}
```
