# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day12

## 이 코드는 C++ 언어의 클래스에 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 연습 예제 코드 : 클래스

클래스란 객체를 생성하기 위한 설계도(빵틀)

```cpp
#include <iostream>
using namespace std;

class Car {
public:
	int speed;

	// default 생성자
	Car() {
		speed = 300;
	}
	// 생성자
	Car(int speed) {
		this->speed = speed;
	}


	void drive() {
		cout << speed << "km/s로 주행중입니다." << endl;
	}

	// 소멸자
	~Car(){
		cout << "자동차를 폐차했습니다." << endl;
	}
};

int main() {
	Car c1;
	c1.speed = 100;
	c1.drive();

	Car c2;
	c2.drive();

	Car c3(4000);
	c3.drive();
}

```

---

## 🔹 실습 3 : 클래스 사용해보기(3) - 계좌

은행 계좌(BankAccount)를 모델링한 클래스,

```cpp
#include <iostream>
using namespace std;
// 1. accountNumber(계좌번호), balance(잔액)를 멤버 변수로 가지는 BankAccount 클래스 작성
class BankAccount {
	string* accountNumber;
	int balance;

public:
	// 2. 생성자에서 계좌번호와 초기 잔액을 설정
	BankAccount() {
		accountNumber = new string;
		cout << "계좌번호를 입력하세요 : ";
		cin >> *accountNumber;
		cout << "초기 잔액을 입력하세요 : ";
		cin >> balance;
	}

	BankAccount(string accountNumber, int balance) {
		this->accountNumber = new string(accountNumber);
		this->balance = balance;
	}
	// 3. deposit(int amount), withdraw(int amount) 멤버 함수 추가
	void deposit(int amount) {
		balance += amount;
	}

	void withdraw(int amount) {
		balance -= amount;
	}

	void showInfo() {
		cout << *accountNumber << "의 잔액은 " << balance << "원 입니다." << endl;
	}
	// 4. 소멸자에서 "계좌 삭제됨: [계좌번호]" 출력
	~BankAccount() {
		cout << "계좌 삭제됨 : [" << *accountNumber << "]" << endl;
		delete accountNumber;
	}
};

int main() {
	BankAccount b1;
	b1.deposit(5000);
	b1.withdraw(2000);
	b1.showInfo();
}
```

---

## 🔹 연습 예제 코드 : 클래스

Method Chaining : 한 객체의 메서드를 연속적으로 호출하는 방식

```cpp
#include <iostream>
using namespace std;
class Person {
public:
	string name;

	// Method Chaining => 클래스 포인터를 사용하여 this를 반환함으로써 메서드 체이닝을 활용
	Person* setName(string name) {
		this->name = name;
		return this;
	}

	void showName() {
		cout << "내 이름은 " << name << endl;
	}
};

int main() {
	Person p1;
	p1.setName("jerry")->showName();
}
```

---

## 🔹 연습 예제 코드 : 클래스

동적 메모리 할당과 객체 삭제를 처리하는 예제

```cpp
#include <iostream>
using namespace std;
class Person {
public:
	string name;

	void setName(string name) {
		this->name = name;
	}

	void showName() {
		cout << "내 이름은 " << name << endl;
	}
};

int main() {
	// 동적으로 할당된 객체를 삭제할 때, 클래스 포인터를 사용하여 객체를 메모리에서 제거
	Person* p1 = new Person();
	// Person*/* 포인터 자료형*/ _this/*변수*/ = &클래스;
	p1->setName("jerry");
	// (*p1).setName("jerry"); => 기존 문법은 이렇게 작성해야 함
	delete p1;
}
```

---

## 🔹 실습 1 : 두 객체 비교 및 반환

Method Chaining을 활용한 두 객체 비교 및 반환 프로그램

```cpp
#include <iostream>
using namespace std;

// 1. Rectangle 클래스를 만든다.
class Rectangle {
	// 2. width(가로)와 height(세로)를 멤버 변수로 포함한다.
	int width, height;

public:

	Rectangle(int width, int height) {
		this->width = width;
		this->height = height;
	}

	// 3. getArea() 멤버 함수를 작성하여 넓이를 반환한다.
	int getArea() {
		return width * height;
	}

	// 4. compareArea(Rectangle& other) 멤버 함수를 추가하여 현재 객체와 다른 객체의 넓이를 비교
	Rectangle* compareArea(Rectangle& other/*메모리에 접근하여 값을 가져옴*/) {
		// 5. 더 넓은 객체를 반환하도록 한다.
		// 6. this 포인터를 활용하여 this->getArea() vs other.getArea() 비교 후 더 큰 객체 반환
		if (this->getArea() >= other.getArea()) return this;
		else return &other;
	}

	void print() {
		cout << "사각형의 넓이 출력 : " << getArea() << endl;
	}
};
// 7. main()에서 두 개의 Rectangle 객체를 생성하고, 넓이가 더 큰 객체의 정보를 출력
int main() {
	int width, height;
	cout << "첫 번째 width와 height의 값을 입력하세요 : ";
	cin >> width >> height;
	Rectangle r1(width, height);

	cout << "두 번째 width와 height의 값을 입력하세요 : ";
	cin >> width >> height;
	Rectangle r2(width, height);

	Rectangle* larger = r1.compareArea(r2);

	larger->print(); // 메서드 체이닝
	return 0;
}
```

---

## 🔹 연습 예제 코드 : 포인터 복습

```cpp
#include <iostream>
using namespace std;

int main() {
	int a = 10;
	int* p = &a;
	*p = 100;
	/*
	int* p = &a;
	*p = 100;
	이 과정을 아래와 같이 축약함
	int* const p = &a; 이것과 같기 때문에 주소 변경이 불가
	*/
	int v = a; // 값을 복사
	int& r = a; // A의 메모리에 접근
	r = 200;

	return 0;
}
```

---

## 🔹 연습 예제 코드 : static(정적) 변수

static 멤버 함수를 설명하기 위해 static(정적)변수 설명

```cpp
#include <iostream>
using namespace std;
void countStatic() {
	static int i = 0;
	i++;
	cout << i << endl;
}

void count() {
	int i = 0;
	i++;
	cout << i << endl;
}

int main() {
	countStatic();
	countStatic();
	countStatic();

	count();
	count();
	count();
}
```

---

## 🔹 연습 예제 코드 : static 멤버 함수

static 멤버 변수는 클래스의 인스턴스가 아니라 클래스 자체에 속하므로, this 포인터를 사용하여 접근할 수 없습니다. this는 객체에 대한 포인터로, static 멤버 변수는 객체의 인스턴스와 관계없이 클래스 자체에 속하기 때문에, 객체를 통해 접근할 수 없습니다.

```cpp
#include <iostream>
using namespace std;

class Counter {
private:
	static int count; // static 멤버 변수
public:
	Counter() {
		count++; // 객체가 생성될 때마다 count 증가
	}

	static int getCount() {
		return count; // static 변수는 클래스 이름을 통해 접근
	}
};

int Counter::count = 0; // Counter의 count에 접근

int main() {
	Counter c1, c2, c3;
	cout << "객체 수 : " << Counter::getCount() << endl;
}
```

---

## 🔹 실습 2 : 유일한 ID 할당

사용자 정보를 입력받고, 각 객체에 유일한 ID를 부여하며, 생성된 객체 수를 추적하여 출력하는 프로그램

```cpp
#include <iostream>
using namespace std;

// 1. User 클래스를 만든다.
class User {

	// 2. static 멤버 변수 nextID를 선언하여 각 객체가 생성될 때마다 유일한 ID를 부여(1부터 시작)
	static int nextID;

	//3. id(고유 ID), name(이름) 멤버 변수를 포함한다.
	string ID;
	string name;

public:
	User() {
		cout << "ID와 이름을 입력하세요 : ";
		cin >> this->ID >> this->name;
		nextID++;
	}

	// 4. static 멤버 함수 getTotalUsers()를 작성하여 생성된 사용자 수를 반환
	static int getTotalUsers() {
		return nextID;
	}

	string showInfo() {
		return ID + " " + name;
	}

};

int User::nextID = 0;

// 5. main()에서 여러 개의 User 객체를 생성한 후 각 사용자 ID를 출력
int main() {
	User u1, u2, u3;
	u1.showInfo();
	u2.showInfo();
	u3.showInfo();

	// 6. getTotalUsers()를 호출하여 총 사용자 수를 출력
	cout << "총 사용자 수 : " << User::getTotalUsers() << endl;
}
```

---

## 🔹 실습 2 : 유일한 ID 할당 (에러 수정)

사용자 정보를 입력받고, 각 객체에 유일한 ID를 부여하며, 생성된 객체 수를 추적하여 출력하는 프로그램

```cpp
#include <iostream>
using namespace std;

// 1. User 클래스를 만든다.
class User {

	// 2. static 멤버 변수 nextID를 선언하여 각 객체가 생성될 때마다 유일한 ID를 부여(1부터 시작)
	static int nextID;

	//3. id(고유 ID), name(이름) 멤버 변수를 포함한다.
	int ID;
	string name;

public:
	User() {
		this->ID = ++nextID;
		cout << "이름을 입력하세요 : ";
		cin >> this->name;

	}

	// 4. static 멤버 함수 getTotalUsers()를 작성하여 생성된 사용자 수를 반환
	static int getTotalUsers() {
		return nextID;
	}

	/*string showInfo() {
		return ID + " " + name;
	}*/

	void showInfo() {
		cout << "ID : " << ID << ", name : " << name << endl;
	}

};

int User::nextID = 0;

// 5. main()에서 여러 개의 User 객체를 생성한 후 각 사용자 ID를 출력
int main() {
	User u1, u2, u3;
	//cout << u1.showInfo() << endl;
	//cout << u2.showInfo() << endl;
	//cout << u3.showInfo() << endl;

	u1.showInfo();
	u2.showInfo();
	u3.showInfo();

	// 6. getTotalUsers()를 호출하여 총 사용자 수를 출력
	cout << "총 사용자 수 : " << User::getTotalUsers() << endl;
}
```

---

## 🔹 실습 2 : 유일한 ID 할당 (에러 수정)

사용자 정보를 입력받고, 각 객체에 유일한 ID를 부여하며, 생성된 객체 수를 추적하여 출력하는 프로그램

```cpp
#include <iostream>
using namespace std;

// 1. User 클래스를 만든다.
class User {

	// 2. static 멤버 변수 nextID를 선언하여 각 객체가 생성될 때마다 유일한 ID를 부여(1부터 시작)
	static int nextID;

	//3. id(고유 ID), name(이름) 멤버 변수를 포함한다.
	int ID;
	string name;

public:
	User() {
		this->ID = ++nextID;
		cout << "이름을 입력하세요 : ";
		cin >> this->name;

	}

	// 4. static 멤버 함수 getTotalUsers()를 작성하여 생성된 사용자 수를 반환
	static int getTotalUsers() {
		return nextID;
	}

	/*string showInfo() {
		return ID + " " + name;
	}*/

	void showInfo() {
		cout << "ID : " << ID << ", name : " << name << endl;
	}

};

int User::nextID = 0;

// 5. main()에서 여러 개의 User 객체를 생성한 후 각 사용자 ID를 출력
int main() {
	User u1, u2, u3;
	//cout << u1.showInfo() << endl;
	//cout << u2.showInfo() << endl;
	//cout << u3.showInfo() << endl;

	u1.showInfo();
	u2.showInfo();
	u3.showInfo();

	// 6. getTotalUsers()를 호출하여 총 사용자 수를 출력
	cout << "총 사용자 수 : " << User::getTotalUsers() << endl;
}
```

---

## 🔹 연습 예제 코드 : 상속

기존 클래스의 특성과 행동(속성 및 메서드)을 재사용하고, 새로운 기능을 추가하거나 기존 기능을 변경

```cpp
#include <iostream>
using namespace std;

class Parent {
public:
	string familyName;
	string address;
	string asset;

	Parent() {
		familyName = "kim";
		address = "dowha";
		asset = "부동산";
		cout << "부모 클래스 실행" << endl;
	}

	Parent(string fn) {
		familyName = fn;
		cout << "부모 클래스 실행" << endl;
	}

	void eat() {
		cout << "과자를 먹습니다" << endl;
	}

	~Parent(){
		cout << "부모 클래스 종료" << endl;
	}
};

//class Child {
//public:
//	string familyName;
//	string address;
//	string asset;
//}; // => 코드가 비효율 => 상속 개념 등장

class Child :public Parent {
	int age;
public:
	Child(){
		cout << "자식 클래스 실행;" << endl;
	}

	Child(string fn) :Parent(fn) /*멤버 이니셜라이저 리스트*/ {
		cout << "자식 클래스 실행;" << endl;
	}
	Child(string fn, int myAge) :Parent(fn), age(myAge) /*변수의 선언과 초기화가 함께 발생*/ {
		cout << "자식 클래스 실행;" << endl;
	}

	void showFamilyName() {
		cout << "우리 가족의 성은 " << familyName << endl;
	}

	void eat() {
		cout << "초콜릿을 먹습니다." << endl;
	}

	~Child() {
		cout << "자식 클래스 종료" << endl;
	}
};


int main() {
	Child c1;
	c1.showFamilyName();
	c1.eat();
}
```
