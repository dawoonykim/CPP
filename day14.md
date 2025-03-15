# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day14

## 이 코드는 C++ 언어의 상속(오버로딩, 오버라이딩)에 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 연습 예제 코드 : 함수 숨김(Name Hiding)

자식 클래스에서 부모 클래스와 동일한 이름의 함수를 정의했을때, 부모 클래스의 함수가 가려지는 현상

```cpp
#include <iostream>
using namespace std;

class Animal {
	void speak() {
		cout << "동물이 소리를 냅니다." << endl; // 함수가 가려짐
	}
};

class Dog :public Animal {
	void speak() {
		cout << "멍멍" << endl;
	}
};

int main() {

}

```

---

## 🔹 연습 예제 코드 : 상속 (오버라이드)

부모 클래스에서 virtual 키워드를 사용하고 자식 클래스에서 override 키워드를 사용해 해당 함수를 재정의

```cpp
#include <iostream>
using namespace std;

int add(int a, int b) {
	return a + b;
}

//class Animal {
//	virtual void speak() {
//		cout << "동물이 소리를 냅니다." << endl;
//	} // 기본 기능을 부여 => 부모 요소를 쓰게 되어있는데, 추상 메서드를 사용해서 사용할 수 없게 제한해야 함
//}; // 기본 값을 제공
//// => 순수 추상 메서드를 생성해야 함

class Animal {
	virtual void speak() = 0; // 순수 가상 함수 (a.k.a 추상 메서드)
	virtual void move() = 0;
};
// abstract // 자녀 요소의 인터페이스로만 사용 가능 => 객체 생성 불가

class Dog :public Animal {
public:
	void speak() override {
		cout << "멍멍" << endl;
	}

	void move() override {
		cout << "네 발로 걸어요" << endl;
	}
};

int main() {
	add(10, 2); // 컴파일 할 때 실체가 생김(정적 바인딩)
	Dog dog;
	dog.speak();
}
```

---

###### 코드 리팩토링

```cpp
#include <iostream>
using namespace std;

int add(int a, int b) {
	return a + b;
}

//class Animal {
//	virtual void speak() {
//		cout << "동물이 소리를 냅니다." << endl;
//	} // 기본 기능을 부여 => 부모 요소를 쓰게 되어있는데, 추상 메서드를 사용해서 사용할 수 없게 제한해야 함
//};
//// abstract => 순수 추상 메서드를 생성해야 함

class Animal {
public:
	virtual void speak() = 0; // 순수 가상 함수 (a.k.a 추상 메서드)
	virtual void move() = 0;
};
// abstract // 자녀 요소의 인터페이스로만 사용 가능 => 객체 생성 불가

class Dog :public Animal {
public:
	void speak() override {
		cout << "멍멍" << endl;
	}

	void move() override {
		cout << "네 발로 걸어요" << endl;
	}

	void tailSwing() {
		cout << "꼬리를 흔들어요" << endl;
	}
};

class Dinosaur :public Animal {
public:
	void speak() override {
		cout << "크롱크롱" << endl;
	}

	void move() override {
		cout << "쿵쾅쿵쾅" << endl;
	}
};

int main() {
	/*Animal*은 메모리를 해석하는 방식*/
	Animal* animal = nullptr; // Animal 클래스 포인터 변수 생성

	// Dog dog; // Dog 인스턴스 생성
	// Dinosaur dino; // 공룡 인스턴스 생성
	// animal = &dog; // Dog 인스턴스의 주소로 초기화
	//animal->speak();
	// virtual을 선언하면, 오버라이드를 하면 가상 테이블이 생성이 되어서
	// animal->tailSwing(); // Animal 포인터는 tailSwing을 해석할 근거가 없음 => 실행시 에러 발생

	string choise;
	cin >> choise;

	if (choise == "강아지") {
		animal = new Dog();
	}
	else {
		animal = new Dinosaur();
	}

	animal->speak(); // 특정 상황에서 기능이 동적으로 변경

	delete animal;
}

```

```cpp
#include <iostream>
using namespace std;

int add(int a, int b) {
	return a + b;
}

//class Animal {
//	virtual void speak() {
//		cout << "동물이 소리를 냅니다." << endl;
//	} // 기본 기능을 부여 => 부모 요소를 쓰게 되어있는데, 추상 메서드를 사용해서 사용할 수 없게 제한해야 함
//};
//// abstract => 순수 추상 메서드를 생성해야 함

class Animal {
public:
	virtual void speak() = 0; // 순수 가상 함수 (a.k.a 추상 메서드)
	virtual void move() = 0;
};
// abstract // 자녀 요소의 인터페이스로만 사용 가능 => 객체 생성 불가

class Dog :public Animal {
public:
	void speak() override {
		cout << "멍멍" << endl;
	}

	void move() override {
		cout << "네 발로 걸어요" << endl;
	}

	void tailSwing() {
		cout << "꼬리를 흔들어요" << endl;
	}
};

class Dinosaur :public Animal {
public:
	void speak() override {
		cout << "크롱크롱" << endl;
	}

	void move() override {
		cout << "쿵쾅쿵쾅" << endl;
	}
};

int main() {
	Animal* animal;
	Dog dog;
	animal = &dog;
	(*animal).speak();


	Animal* animal = new Dog();
	(*animal).speak();
	delete animal;
}
```

---

## 🔹 실습 3 : 오버라이딩 - 자동차 가속 기능 구현

Vehicle 클래스를 만들고, accelerate()라는 함수를 정의해서 다형성을 활용하는 프로그램

```cpp
#include <iostream>
using namespace std;

// 1. Vehicle 클래스를 만들고, accelerate()라는 함수를 정의하세요.
class Vehicle {
protected:
	int speed;
public:
	virtual int Accelate() = 0;
};

// 2. Car, SportsCar, Truck 클래스를 Vehicle 클래스로부터 상속받아 각각 accelerate()를 오버라이딩하세요.(가속도를 각각 다르게 설정)
class Car :public Vehicle {
	int Accelate() override {
		speed = 30;
		return speed;
	}
};

class Truck :public Vehicle {
	int Accelate() override {
		speed = 15;
		return speed;
	}
};

class SportsCar :public Vehicle {
	int Accelate() override {
		speed = 60;
		return speed;
	}
};

// 3. main()에서 각 차량의 accelerate()가 올바르게 실행되는지 확인하세요.
int main() {
	Vehicle* vehicle = nullptr;

	string type;
	int index;

	cout << "자동차 유형을 선택하세요" << endl << "1. Car (일반 자동차)" << endl << "2. SportsCar (스포츠카)" << endl << "3. Truck (트럭)" << endl << "입력 : ";
	cin >> index;

	if (index == 1) {
		vehicle = new Car();
		type = "일반 자동차가";
	}
	else if (index == 2) {
		vehicle = new SportsCar();
		type = "스포츠카가";
	}
	else if (index == 3) {
		vehicle = new Truck();
		type = "트럭이";
	}

	cout << type << " 시속 " << vehicle->Accelate() << "km 증가!" << endl;

	delete vehicle;
}
```

###### 리팩토링

```cpp
#include <iostream>
using namespace std;

// 1. Vehicle 클래스를 만들고, accelerate()라는 함수를 정의하세요.
class Vehicle {
protected:
	int speed;
public:
	virtual int Accelate() = 0;
};

// 2. Car, SportsCar, Truck 클래스를 Vehicle 클래스로부터 상속받아 각각 accelerate()를 오버라이딩하세요.(가속도를 각각 다르게 설정)
class Car :public Vehicle {
	int Accelate() override {
		speed = 30;
		return speed;
	}
};

class Truck :public Vehicle {
	int Accelate() override {
		speed = 15;
		return speed;
	}
};

class SportsCar :public Vehicle {
	int Accelate() override {
		speed = 60;
		return speed;
	}
};

// 3. main()에서 각 차량의 accelerate()가 올바르게 실행되는지 확인하세요.
int main() {
	Vehicle* vehicle = nullptr;

	string type;
	int index;

	cout << "자동차 유형을 선택하세요" << endl
		 << "1. Car (일반 자동차)" << endl
		 << "2. SportsCar (스포츠카)" << endl
		 << "3. Truck (트럭)" << endl
		 << "입력 : ";
	cin >> index;


	switch (index) {
	case 1:
		vehicle = new Car();
		type = "일반 자동차가";
		break;
	case 2:
		vehicle = new SportsCar();
		type = "스포츠카가";
		break;
	case 3:
		vehicle = new Truck();
		type = "트럭이";
		break;
	default:
		cout << "잘못된 입력입니다." << endl;
		return 1;
	}
	if (vehicle) {
		cout << type << " 시속 " << vehicle->Accelate() << "km 증가!" << endl;
	}

	delete vehicle;
}
```

---

## 🔹 연습 예제 코드 : 순수 가상 소멸자

순수 가상 소멸자를 선언하여 메모리 누수를 방지

```cpp
#include <iostream>
using namespace std;

class Vehicle {
protected:
	int speed;
public:
	virtual int Accelate() = 0;

	virtual ~Vehicle() {}; // 순수 가상 소멸자
	// 자식 클래스의 소멸자가 제대로 호출되도록 보장하여 메모리 누수를 방지하는 역할
};

class Car :public Vehicle {
	int Accelate() override {
		speed = 30;
		return speed;
	}
};

class Truck :public Vehicle {
	int Accelate() override {
		speed = 15;
		return speed;
	}
};

class SportsCar :public Vehicle {
	int Accelate() override {
		speed = 60;
		return speed;
	}
};

int main() {
	Vehicle* vehicle = nullptr;

	string type;
	int index;

	cout << "자동차 유형을 선택하세요" << endl
		 << "1. Car (일반 자동차)" << endl
		 << "2. SportsCar (스포츠카)" << endl
		 << "3. Truck (트럭)" << endl
		 << "입력 : ";
	cin >> index;


	switch (index) {
	case 1:
		vehicle = new Car();
		type = "일반 자동차가";
		break;
	case 2:
		vehicle = new SportsCar();
		type = "스포츠카가";
		break;
	case 3:
		vehicle = new Truck();
		type = "트럭이";
		break;
	default:
		cout << "잘못된 입력입니다." << endl;
		return 1;
	}
	if (vehicle) {
		cout << type << " 시속 " << vehicle->Accelate() << "km 증가!" << endl;
	}

	delete vehicle;
}
```

---

## 🔹 실습 4 : 과자, 사탕, 초콜릿

추상 클래스와 다형성을 활용하여 Snack 클래스를 기반으로 한 다양한 간식 클래스(Candy, Chocolate)에서 printInfo() 메서드를 오버라이드하여 각각의 정보를 출력하는 프로그램

```cpp
#include <iostream>
#include <vector>
using namespace std;

// 1. 추상 클래스 Snack
// • productName, company, price 변수를 포함 (모든 간식 공통 속성)
// • printInfo()를 순수 가상 함수로 선언 → 자식 클래스에서 오버라이딩
class Snack {
protected:
	string productName;
	string company;
	int price;
public:
	Snack(string productName, string company, int price) :productName(productName), company(company), price(price) {};
	virtual void printInfo() = 0;

	virtual ~Snack() {};
};

// 2. Candy 클래스
// • taste 변수 추가 (맛을 저장)
// • printInfo() 오버라이딩하여 출력
class Candy :public Snack {
	string taste;
public:
	Candy(string productName, string company, int price, string taste) :Snack(productName, company, price), taste(taste) {};

	void printInfo() override {
		cout << company << " 회사의 " << productName << "의 맛은 " << taste << "이고, 가격은 " << price << "원 입니다." << endl;
	}

};

// 3. Chocolate 클래스
// • shape 변수 추가 (모양을 저장)
// • printInfo() 오버라이딩하여 출력
class Chocolate : public Snack {
	string shape;
public:
	Chocolate(string productName, string company, int price, string shape) :Snack(productName, company, price), shape(shape) {};
	void printInfo() {
		cout << company << " 회사의 " << productName << "의 모양은" << shape << "이고, 가격은 " << price << "원 입니다." << endl;
	}
};

// 4. 메인 함수에서 snackBasket 배열 생성
// • Candy와 Chocolate 객체 각각 2개씩 생성 후 배열에 저장
// • 다형성 활용하여 Snack* 배열을 통해 모든 간식 정보 출력
int main() {
	vector<Snack*> snackBasket;
	string productName1, productName2, company1, company2, taste, shape;
	int price1, price2;
	cout << "사탕의 제품명, 제조사명, 맛, 가격을 입력하세요 : ";
	cin >> productName1 >> company1 >> taste >> price1;

	cout << "초콜릿의 제품명, 제조사명, 모양, 가격을 입력하세요 : ";
	cin >> productName2 >> company2 >> shape >> price2;

	Snack* snack[] = { new Candy(productName1,company1,price1,taste),new Chocolate(productName2,company2,price2,shape) };
	snackBasket.push_back(new Candy(productName1, company1, price1, taste));
	snackBasket.push_back(new Chocolate(productName2, company2, price2, shape));

	for (Snack* s : snack) {
		s->printInfo();
	}

	for (Snack* s : snackBasket) {
		s->printInfo();
	}
}
```

---

## 🔹 실습 5 : AI 챗봇 시스템 설계

Vehicle 클래스를 상속받아 Car와 Truck클래스를 구현하는 프로그램

```cpp
#include <iostream>
#include <string>
using namespace std;
// 1. Chatbot이라는 추상 클래스를 만들고, respond(string message)라는 순수 가상 함수를 선언
class Chatbot {
protected:
	string message;
public:
	Chatbot(string message) :message(message) {};
	virtual void respond(string message) = 0;
};
// 2. CustomerSupportBot(고객 지원 봇)과 WeatherBot(날씨 봇)을 만들어 respond()를 다르게 구현
class CustomerSupportBot :public Chatbot {
public:
	CustomerSupportBot(string message) :Chatbot(message) {};

	void respond(string message) override {
		// CustomerSupportBot 클래스는 "고객 지원 문의를 처리합니다: [사용자 입력]" 출력.
		cout << "고객 지원 문의를 처리합니다: [" << message << "]" << endl;
	}
};

class WeatherBot :public Chatbot {
public:
	WeatherBot(string message) :Chatbot(message) {};
	void respond(string message) override {
		// WeatherBot 클래스는 "현재 날씨 정보를 제공합니다: [사용자 입력]" 출력.
		cout << "현재 날씨 정보를 제공합니다: [" << message << "]" << endl;
	}
};

// 3. main()에서 Chatbot* 포인터를 사용하여 두 챗봇을 실행.
int main() {
	int input;

	cout << "원하는 동작을 선택하세요." << endl
		 << "1. 고객 지원 봇" << endl
		 << "2. 날씨 봇" << endl
		 << "입력 : ";

	cin >> input;

	// 입력 버퍼에 남아 있는 개행 문자를 처리
	cin.ignore();  // 이 줄을 추가하여 문제를 해결합니다.

	string message;
	Chatbot* chat = nullptr;
	switch (input) {
		case 1:
			cout << "고객 문의 사항을 입력하세요 : ";
			getline(cin, message);
			chat = new CustomerSupportBot(message);
			break;
		case 2:
			cout << "현재 날씨 정보를 입력하세요 : ";
			getline(cin, message);
			chat = new WeatherBot(message);
			break;
		default:
			cout << "정보를 잘못 입력했습니다." << endl;
	}

	if (chat) {
		chat->respond(message);
	}
}
```

###### do-while문 활용한 리팩토링

```cpp
#include <iostream>
#include <string>
using namespace std;

class Chatbot {
protected:
	string message;
public:
	Chatbot(string message) :message(message) {};
	virtual void respond(string message) = 0;
};

class CustomerSupportBot :public Chatbot {
public:
	CustomerSupportBot(string message) :Chatbot(message) {};
	void respond(string message) override {
		cout << "고객 지원 문의를 처리합니다: [" << message << "]" << endl;
	}
};

class WeatherBot :public Chatbot {
public:
	WeatherBot(string message) :Chatbot(message) {};
	void respond(string message) override {
		cout << "현재 날씨 정보를 제공합니다: [" << message << "]" << endl;
	}
};

int main() {
	int input;
	Chatbot* chat = nullptr;

	do {
		cout << "원하는 동작을 선택하세요." << endl
			 << "0. 프로그램 종료" << endl
			 << "1. 고객 지원 봇" << endl
			 << "2. 날씨 봇" << endl
			 << "입력 : ";

		cin >> input;

		// 입력 버퍼에 남아 있는 개행 문자를 처리
		cin.ignore();  // 이 줄을 추가하여 문제를 해결합니다.

		string message;

		switch (input) {
		case 1:
			cout << "고객 문의 사항을 입력하세요 : ";
			getline(cin, message);
			chat = new CustomerSupportBot(message);
			break;
		case 2:
			cout << "현재 날씨 정보를 입력하세요 : ";
			getline(cin, message);
			chat = new WeatherBot(message);
			break;
		case 0:
			cout << "프로그램을 종료합니다." << endl;
			break;
		default:
			cout << "정보를 잘못 입력했습니다." << endl;
		}

		if (chat) {
			chat->respond(message);
		}

	} while (input!=0);

	delete chat;
}
```

---

###### 가상 소멸자

가상 소멸자를 사용하여 부모 클래스의 포인터로 자식 클래스 객체를 삭제할 때, 자식 클래스의 소멸자도 제대로 호출되도록 보장

```cpp
#include <iostream>
using namespace std;

class Parent {
public:
	Parent() {
		cout << "부모 생성자" << endl;
	}
	virtual ~Parent() {
		cout << "부모 소멸자" << endl;
	}
};

class Child:public Parent {
public:
	Child() {
		cout << "자녀 생성자" << endl;
	}
	~Child() {
		cout << "자녀 소멸자" << endl;
	}
};

int main() {
	Parent* parent = new Child();

	delete parent;
}
```

---

## 🔹 연습 예제 코드 : up-casting, down-casting

Upcasting: 자식 클래스의 객체를 부모 클래스의 타입으로 변환, Downcasting : 부모 클래스의 객체를 자식 클래스의 타입으로 변환

```cpp
#include <iostream>
#include <string>
using namespace std;

class Chatbot {
protected:
	string message;
public:
	Chatbot(string message) :message(message) {};
	virtual void respond(string message) = 0;
};

class CustomerSupportBot :public Chatbot {
public:
	CustomerSupportBot(string message) :Chatbot(message) {};
	void respond(string message) override {
		cout << "고객 지원 문의를 처리합니다: [" << message << "]" << endl;
	}
};

class WeatherBot :public Chatbot {
public:
	WeatherBot(string message) :Chatbot(message) {};
	void respond(string message) override {
		cout << "현재 날씨 정보를 제공합니다: [" << message << "]" << endl;
	}
	void notice() {
		cout << "오늘 날시는 맑음" << endl;
	}
};

int main() {
	string input = "string";
	Chatbot* chat = nullptr;

	// 업 캐스팅 : 자녀 -> 부모
	chat = new WeatherBot(input);
	chat->respond("string");

	// 다운 캐스팅 : 부모 -> 자녀
	WeatherBot* weatherBot = (WeatherBot*)chat;
	weatherBot->notice();
	weatherBot->respond(input);

	delete chat;
}
```
