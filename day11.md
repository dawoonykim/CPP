# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day11

## 이 코드는 C++ 언어의 구조체와 클래스에 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 연습 예제 코드 : 구조체

여러 개의 서로 다른 데이터 타입을 하나로 묶어서 새로운 데이터 타입을 만들 수 있게 해주는 C++의 사용자 정의 데이터 구조

```cpp
#include <iostream>
using namespace std;

//// C스타일
//typedef struct Person {
//	string name;
//	string address;
//	int age;
//} MyPerson; // Alias(별칭)

// C++ 스타일
struct Person {
	string name;
	string address;
	int age;

	void study() {
		cout << name << "학생이 공부합니다." << endl;
	}
};

struct Address {
	string city;
	string street;
};

struct TestPerson {
	string name;
	Address address; // 구조체를 멤버로 포함
	int age;

	void study() {
		cout << name << "학생이 공부합니다." << endl;
	}
};

using P = Person; // 별칭 지정 => 구조체의 이름이 너무 길 경우 간단하게 사용하기 위해 사용

int main() {
	Person p1; 						// 인스턴스 생성
	p1.name = "jerry"; 		// p1.name 초기화
	p1.address = "mapo"; 	// p1.address 초기화
	p1.age = 29; 					// p1.age 초기화

	cout << "이름 : " << p1.name << endl;
	cout << "주소 : " << p1.address << endl;
	cout << "나이 : " << p1.age << endl << endl;

	// -------------------------------------------------------------------------------

	Person p2 = { "jerry","mapo",29 }; // 인스턴스 생성 후 초기화

	cout << "이름 : " << p2.name << endl;
	cout << "주소 : " << p2.address << endl;
	cout << "나이 : " << p2.age << endl;
	p2.study();
	cout << endl;

	// -------------------------------------------------------------------------------

	TestPerson p3 = { "tom",{"Seoul","도화2길"},20 };
	cout << "이름 : " << p3.name << endl;
	cout << "주소 : " << p3.address.city << endl;
	cout << "주소 : " << p3.address.street << endl;
	cout << "나이 : " << p3.age << endl << endl;

	// -------------------------------------------------------------------------------
	// 포인터를 사용하여 구조체의 멤버에 접근하는 방법
	Person* ptr = &p1;
	cout << (*ptr).name << endl;
	cout << ptr->name << endl;
	cout << (*ptr).address << endl;
	cout << ptr->address << endl;
	cout << (*ptr).age << endl;
	cout << ptr->age << endl;
	ptr->study();
	cout << endl;

	TestPerson* ptr2 = &p3;
	cout << (*ptr2).name << endl;
	cout << ptr2->name << endl;
	cout << (*ptr2).address.city << endl;
	cout << ptr2->address.city << endl;
	cout << (*ptr2).address.street << endl;
	cout << ptr2->address.street << endl;
	cout << (*ptr2).age << endl;
	cout << ptr2->age << endl;
}

```

---

## 🔹 실습 1 : 구조체 사용해보기

구조체를 정의하고, 이를 이용해 사각형의 넓이를 계산하는 프로그램

```cpp
#include <iostream>
using namespace std;

// 1. Rectangle 구조체 만들기
// 2. 사각형의 가로 세로 길이를 저장하는 구조체
struct Rectangle {
	// 3. 변수 width, height
	int width;
	int height;

	void Area() {
		cout << "사각형의 넓이는 " << width * height << "입니다." << endl;
	}
};

int main() {
	// 4. 구조체를 이용하여 변수를 생성하고, width와 height 값을 콘솔로 입력 받아서 할당
	Rectangle r1;

	cout << "가로와 세로 길이를 입력하세요 : ";
	cin >> r1.width >> r1.height;

	// 5. width와 height 값을 이용해 넓이를 계산하여 출력
	cout << "사각형의 넓이는 " << r1.width * r1.height << "입니다." << endl;
	// 멤버 함수로 구현
	r1.Area();
}
```

---

## 🔹 실습 2 : 좌표(Point) 연산

구조체에 멤버 함수를 정의하여 좌표 연산 수행

```cpp
#include <iostream>
using namespace std;

// 1. Point 구조체를 정의하고, x, y 좌표를 멤버 변수로 포함
struct Point {
	int x, y;

	// 2. 좌표 값을 더하는 멤버 함수 add(const Point&)를 구현
	// 매개 변수에 자기 자신을 넣는다 -> Point struct의 자료형을 넣어줘라 => other의 접근 제한을 위해 const 사용
	// &는 참조자(Reference)로, 객체의 실제 메모리 주소를 참조하는 방식 => 값을 복사하지 않고 원본 객체를 그대로 참조, 메모리 복사가 발생하지 않아 성능상 이점이 있음
	void add(const Point& other) {
		x += other.x;
		y += other.y;
		cout << "x : " << x << ", y : " << y << endl;
	}
};
// 3. 두 개의 Point를 생성하여 값을 입력 받고, add함수를 이용해 좌표의 합을 출력
int main() {
	Point p1;
	Point p2;

	cout << "첫 번째 좌표를 입력하세요 : ";
	cin >> p1.x >> p1.y;

	cout << "두 번째 좌표를 입력하세요 : ";
	cin >> p2.x >> p2.y;

	p1.add(p2);
}
```

---

## 🔹 연습 예제 코드 : 클래스

클래스란 객체를 생성하기 위한 설계도(빵틀)

```cpp
#include <iostream>
using namespace std;

class Car {
public:
	string brand;
	int speed;

	void drive() {
		cout << brand << "가 " << speed << "km/h로 주행합니다.";
	}

	void drive2();
};
// 클래스 외부에서 멤버 함수 구현
void Car::drive2() {
	cout << brand << "가 " << speed << "km/h로 주행합니다.";
}

int main() {
	Car c1;
	c1.brand = "Benz";
	c1.speed = 300;
	c1.drive();
	cout << endl << endl;

	Car c2;
	Car c3;

	c2.brand = "BMW";
	c2.speed = 300;
	c2.drive();
	cout << endl << endl;

	c3.brand = "Hyundai";
	c3.speed = 250;
	c3.drive();
	cout << endl << endl;
}
```

---

## 🔹 실습 1 : 클래스 사용해보기(1) - 사람

사람 클래스 생성 후 출력하는 프로그램 (리팩토링 전)

```cpp
#include <iostream>
using namespace std;

// 1. name(이름)과 age(나이)를 멤버 변수로 가지는 Person 클래스를 작성
class Person {
	string name;
	int age;

// 2. setName()과 setAge() 멤버 함수를 추가하여 값을 설정할 수 있도록 만들기
public:
	void setName(string n) {
		name = n;
		// (*this).name = n;
	}

	void setAge(int a) {
		age = a;
		// this->age = a;
	}
	// 3. showInfo() 멤버 함수를 만들어 이름과 나이를 출력하도록 만들기
	void showInfo() {
		cout << "이름 : " << name << ", 나이 : " << age << endl;
	}

};

int main() {
	Person p1;
	string name;
	cout << "이름을 입력하세요 : ";
	cin >> name;
	p1.setName(name);
	int age;
	cout << "나이를 입력하세요 : ";
	cin >> age;
	p1.setAge(age);

	p1.showInfo();
}
```

```cpp
#include <iostream>
using namespace std;

class Person {
	string name;
	int age;

public:
	void setName(string name) {
		(*this).name = name;
	}

	void setAge(int age) {
		this->age = age;
	}

	void showInfo() {
		cout << "이름 : " << name << ", 나이 : " << age << endl;
	}

};

int main() {
	Person p1;
	string name;
	cout << "이름을 입력하세요 : ";
	cin >> name;
	p1.setName(name);
	int age;
	cout << "나이를 입력하세요 : ";
	cin >> age;
	p1.setAge(age);

	p1.showInfo();
}
```

---

## 🔹 실습 1 : 클래스 사용해보기(1) - 사람

사람 클래스 생성 후 출력하는 프로그램 (리팩토링 후)

```cpp
#include <iostream>
using namespace std;

class Person {
	string name;
	int age;

public:
	void setName() {
		cout << "이름을 입력하세요 : ";
		cin >> name;
	}

	void setAge() {
		cout << "나이를 입력하세요 : ";
		cin >> age;
	}

	void showInfo() {
		cout << "이름 : " << name << ", 나이 : " << age << endl;
	}

};

int main() {
	Person p1;
	Person p2;

	p1.setName();
	p1.setAge();
	p1.showInfo();


	p2.setName();
	p2.setAge();
	p2.showInfo();
}
```

---

## 🔹 연습 예제 코드 : 생성자

객체가 생성될 때 자동으로 호출되는 특별한 메서드 (객체의 초기화 작업을 수행하는 역할)

```cpp
#include <iostream>
using namespace std;

class Person {
	string name;
	int age;

public:

	Person() {
		name = "jerry";
		age = 30;
	}

	void setName() {
		cout << "이름을 입력하세요 : ";
		cin >> name;
	}

	void setAge() {
		cout << "나이를 입력하세요 : ";
		cin >> age;
	}

	void showInfo() {
		cout << "이름 : " << name << ", 나이 : " << age << endl;
	}

};

int main() {
	Person p1;
	Person p2;
	Person p3;

	p1.setName();
	p1.setAge();
	p1.showInfo();


	p2.setName();
	p2.setAge();
	p2.showInfo();

	p3.showInfo();
}
```

```cpp
#include <iostream>
using namespace std;

class Person {
	string name;
	int age;

public:

	Person(string name, int age) {
		this->name = name;
		this->age = age;
	}

	void setName() {
		cout << "이름을 입력하세요 : ";
		cin >> name;
	}

	void setAge() {
		cout << "나이를 입력하세요 : ";
		cin >> age;
	}

	void showInfo() {
		cout << "이름 : " << name << ", 나이 : " << age << endl;
	}

};

int main() {
	Person p4("홍길동", 30);
	p4.showInfo();
}
```

---

## 🔹 연습 예제 코드 : 복사 생성자

"이미 존재하는 객체(인스턴스)"를 이용하여 "새로운 객체"를 초기화하는 생성자

```cpp
#include <iostream>
using namespace std;
// 포인터를 사용하는 경우 동적 메모리를 공유하기 때문에, 같은 주소로 인해 값이 같이 수정됨
class Person {
public:
	string* name;
	int* age;



	Person(string name, int age) {
		this->name = new string(name);
		this->age = new int(age);
	}

	// 복사 생성자, other => 다른 인스턴스
	Person(Person& other) {
		this->name = new string(*other.name);
		this->age = other.age;
	}

	void setName() {
		cout << "이름을 입력하세요 : ";
		cin >> *name;
	}

	void setAge() {
		cout << "나이를 입력하세요 : ";
		cin >> *age;
	}

	void showInfo() {
		cout << "이름 : " << *name << ", 나이 : " << *age << endl;
	}

	~Person() {
		delete name;
		cout << "Person 클래스 소멸" << endl;
	}
};

int main() {
	Person p1("홍길동", 30);
	p1.showInfo();

	Person p2 = p1;
	p2.setName();
	p2.setAge();
	p1.showInfo();
	p2.showInfo();

	Person p3=p1;
	*p3.name = "김연아";
	*p3.age = 33;
	p3.showInfo();
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
