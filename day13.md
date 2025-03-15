# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day13

## 이 코드는 C++ 언어의 상속에 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 연습 예제 코드 : const

상수, 객체의 데이터를 변경하지 못하게 명시적으로 표시하는 키워드

```cpp
#include <iostream>
using namespace std;

class Car {
private:
	string brand;
public:
	int speed;
	void setBrand(string brand) {
		this->brand = brand;
	}

	// 브랜드를 출력해주는 함수
	void showBrand() const{
		// brand = "Hyundai"; => const 키워드로 인해 오류 발생
		cout << "브랜드는 " << brand << endl;
	}
};

int main() {
	Car c1;
	const Car c2;

	c1.setBrand("BMW");
	c1.speed = 100;
	c1.showBrand();
	// c2.setBrand("Benz"); => 특정 상황에서 객체를 보호하기 위한 장치
	// c2.speed = 200; => 특정 상황에서 객체를 보호하기 위한 장치
	c2.showBrand();
}

```

---

## 🔹 연습 예제 코드 : 상속

기존 클래스(부모 클래스)의 속성과 기능(메서드)을 새로운 클래스(자식 클래스)가 물려받아 확장하거나 변경하여 사용할 수 있도록 하는 개념 => 코드 재사용성과 확장성

```cpp
#include <iostream>
using namespace std;

class Parent {
public:
	string familyName;

	Parent() {
		cout << "부모 클래스 실행" << endl;
	}
	Parent(string fn) {
		familyName = fn;
		cout << "부모 클래스 실행" << endl;
	}

	void showFamilyName() {
		cout << "우리 집안의 성씨는 : " << familyName << endl;
	}
	~Parent() {
		cout << "부모 클래스 종료" << endl;
	}
};
// 접근 지정자를 설정을 하지 않으면 private으로 기본 설정됨
class Child :public Parent {
public:
	int age;
	Child() {
		// Parent() => 보이지 않지만 Parent의 생성자가 추가되어 있음
		cout << "자식 클래스 실행" << endl;
	}
	// 멤버 이니셜라이저 리스트(Member Initializer List)는 클래스의 생성자에서 멤버 변수를 초기화하는 방법
	Child() : Parent("박"), age(20) { // => 선언과 동시에 초기화
		cout << "자식 클래스 실행" << endl;
	}
	~Child() {
		cout << "자식 클래스 종료" << endl;
		// ~Parent() => 보이지 않지만 Parent의 소멸자가 추가되어 있음
	}
};

int main() {
	Child c1;
	c1.familyName = "이";
	c1.showFamilyName();
}
```

---

## 🔹 실습 1 : 상속 연습 - Shape

상속을 활용하여 삼각형과 사각형의 넓이를 출력하는 프로그램

```cpp
#include <iostream>
using namespace std;

// 부모 클래스
// 1. Shape라는 클래스를 만들어주세요.
class Shape {
protected:
  // 조건 1. 변의 개수, 밑변의 길이를 저장하는 변수를 가지고 있어야 합니다
	int line, lineLength;
	// int sides, base;
public:

  // 조건 2. 변의 개수와 밑변의 길이를 출력하는 printInfo() 함수를 가지고 있어야 합니다.
	Shape(int line, int lineLength) {
		this->line = line;
		this->lineLength = lineLength;
	}
	// Shape(int s,int b):sides(s),base(b){}

	void printInfo() {
		cout << "변의 개수는 " << line << ", 밑변의 길이는 " << lineLength << "입니다." << endl;
	}
};

// 자식 클래스 : Rectangle
 // 2. Shape 클래스를 상속 받는 Rectangle, Triangle 클래스를 만들어주세요.
class Rectangle :public Shape {
  // 조건 1. Rectangle 클래스에는 세로 길이를 의미하는 변수를 가지고 있어야 합니다.
	int height_length;
public:
  // 조건 4. 두 클래스 모두 생성자에서 모든 변수에 값을 대입해주세요. (변, 밑변도 대입)
	Rectangle(int line, int lineLength, int height) :Shape(line, lineLength) {
		this->height_length = height;
	}
  // 조건 3. 두 클래스에는 각각 도형의 넓이를 구하고 출력하는 area() 함수를 가지고 있어야 합니다.
	void Area() {
		cout << "사각형의 넓이는 " << lineLength * height_length << "입니다." << endl;
	}
};

// 자식 클래스 : Triangle
 // 2. Shape 클래스를 상속 받는 Rectangle, Triangle 클래스를 만들어주세요.
class Triangle :public Shape {
  // 조건 2. Triangle 클래스에는 높이 길이를 의미하는 변수를 가지고 있어야 합니다.
	int height;
public:
  // 조건 4. 두 클래스 모두 생성자에서 모든 변수에 값을 대입해주세요. (변, 밑변도 대입)
	Triangle(int line, int lineLength, int height) :Shape(line, lineLength) {
		this->height = height;
	}
  // 조건 3. 두 클래스에는 각각 도형의 넓이를 구하고 출력하는 area() 함수를 가지고 있어야 합니다.
	void Area() {
		cout << "삼각형의 넓이는 " << (lineLength * height)/2 << "입니다." << endl;
	}
};

// 3. 메인 함수에서 Triangle과 Rectangle 클래스를 통해 각각 인스턴스를 만들고 area() 함수를 실행시키도록 만들어주세요.
int main() {
	int line, lineLength, height;
	cout << "변의 개수와 길이 그리고 높이를 입력하세요 : ";
	cin >> line >> lineLength >> height;

	Triangle t1(line, lineLength, height);
	Rectangle r1(line, lineLength, height);

	t1.printInfo();
	t1.Area();
	r1.printInfo();
	r1.Area();
}
```

---

## 🔹 실습 1 : 상속 연습 - Shape

상속을 활용하여 삼각형과 사각형의 넓이를 출력하는 프로그램 (문제 해결을 위해 수정한 프로그램)

```cpp
#include <iostream>
using namespace std;

// 부모 클래스
// 1. Shape라는 클래스를 만들어주세요.
class Shape {
protected:
  // 조건 1. 변의 개수, 밑변의 길이를 저장하는 변수를 가지고 있어야 합니다
	int line, lineLength;
	// int sides, base;
public:

  // 조건 2. 변의 개수와 밑변의 길이를 출력하는 printInfo() 함수를 가지고 있어야 합니다.
	Shape(int line, int lineLength) {
		this->line = line;
		this->lineLength = lineLength;
	}
	// Shape(int s,int b):sides(s),base(b){}

	void printInfo() {
		cout << "변의 개수는 " << line << ", 밑변의 길이는 " << lineLength << "입니다." << endl;
	}
};

// 자식 클래스 : Rectangle
class Rectangle :public Shape {
  // 조건 1. Rectangle 클래스에는 세로 길이를 의미하는 변수를 가지고 있어야 합니다.
	int height_length;
public:
  // 조건 4. 두 클래스 모두 생성자에서 모든 변수에 값을 대입해주세요. (변, 밑변도 대입)
	Rectangle(int lineLength, int height) :Shape(4, lineLength) {
		this->height_length = height;
	}
  // 조건 3. 두 클래스에는 각각 도형의 넓이를 구하고 출력하는 area() 함수를 가지고 있어야 합니다.
	void Area() {
		cout << "사각형의 넓이는 " << lineLength * height_length << "입니다." << endl;
	}
};

// 자식 클래스 : Triangle
// 2. Shape 클래스를 상속 받는 Rectangle, Triangle 클래스를 만들어주세요.
class Triangle :public Shape {
  // 조건 2. Triangle 클래스에는 높이 길이를 의미하는 변수를 가지고 있어야 합니다.
	int height;
public:
  // 조건 4. 두 클래스 모두 생성자에서 모든 변수에 값을 대입해주세요. (변, 밑변도 대입)
	Triangle(int lineLength, int height) :Shape(3, lineLength) {
		this->height = height;
	}
  // 조건 3. 두 클래스에는 각각 도형의 넓이를 구하고 출력하는 area() 함수를 가지고 있어야 합니다.
	void Area() {
		cout << "삼각형의 넓이는 " << (lineLength * height) * 0.5 << "입니다." << endl;
	}
};

// 3. 메인 함수에서 Triangle과 Rectangle 클래스를 통해 각각 인스턴스를 만들고 area() 함수를 실행시키도록 만들어주세요.
int main() {
	int lineLength, height;
	cout << "변의 길이 그리고 높이를 입력하세요 : ";
	cin >> lineLength >> height;

	Triangle t1(lineLength, height);
	Rectangle r1(lineLength, height);

	t1.printInfo();
	t1.Area();
	r1.printInfo();
	r1.Area();
}
```

---

## 🔹 연습 예제 코드 : 상속

상속과 접근 지정자 => 상속 방식과 멤버 접근 권한 변화를 시각적으로 표현한 프로그램

```cpp
#include <iostream>
using namespace std;

// 부모 클래스
class Parent {
private:
	string privateValue = "프라이빗";
protected:
	string protectedValue = "프로텍티드";
public:
	string publicValue = "퍼블릭";
};

class Child1 :public Parent {
public:
	void showValues() {
		cout << "public : " << publicValue << endl;
		cout << "protected : " << protectedValue << endl; // 자식 클래스 내에서는 접근 가능
		// cout << "private : " << privateValue << endl; // => 아무리 상속을 받았다 할지라도 접근 불가
	}
};

class Child2 :protected Parent {
public:
	void showValues() {
		cout << "public : " << publicValue << endl; // 상속 받아 protected으로 접근 권한 변경
		cout << "protected : " << protectedValue << endl;
		// cout << "private : " << privateValue << endl; // => 아무리 상속을 받았다 할지라도 접근 불가
	}
};

class Child3 :private Parent {
public:
	void showValues() {
		cout << "public : " << publicValue << endl; // 상속 받아 priavte으로 접근 권한 변경
		cout << "protected : " << protectedValue << endl; // 상속 받아 priavte으로 접근 권한 변경
		// cout << "private : " << privateValue << endl; // => 아무리 상속을 받았다 할지라도 접근 불가
	}
};

class GrandChild :protected Child3 {
	void showValues() {
		// cout << "public : " << publicValue << endl;
		// cout << "protected : " << protectedValue << endl;
		// cout << "private : " << privateValue << endl;
	}
};

int main() {
	Child1 c1;
	cout << "public : " << c1.publicValue << endl;
	// cout << "protected : " << c1.protectedValue << endl; // 자식 클래스로 상속을 받았다 할지라도 접근 지정자가 protected로 선언되어 접근 불가
	// cout << "private : " << c1.privateValue << endl; // => 아무리 상속을 받았다 할지라도 접근 불가

	Child2 c2;
	// cout << "public : " << c2.publicValue << endl; // 모든 접근 지정자가 protected로 변경되어 접근 불가
	// cout << "protected : " << c2.protectedValue << endl; // 모든 접근 지정자가 protected로 변경되어 접근 불가
	// cout << "private : " << c2.privateValue << endl; // => 아무리 상속을 받았다 할지라도 접근 불가

	Child3 c3;
	// cout << "public : " << c3.publicValue << endl; // 모든 접근 지정자가 private으로 변경되어 접근 불가
	// cout << "protected : " << c3.protectedValue << endl; // 모든 접근 지정자가 private으로 변경되어 접근 불가
	// cout << "private : " << c3.privateValue << endl; // => 아무리 상속을 받았다 할지라도 접근 불가
}
```

---

## 🔹 실습 2 : 상속과 접근 지정자

Vehicle 클래스를 상속받아 Car와 Truck클래스를 구현하는 프로그램

```cpp
#include <iostream>
using namespace std;
// 1. Vehicle 클래스를 만들고, 이를 상속받아 Car와 Truck클래스를 작성하세요.

// 2. Vehicle 클래스(부모 클래스)
class Vehicle {
protected:
	// 조건1. 브랜드 이름과 속도를 저장하는 변수를 가지고 있어야 합니다.
	string brand;
  // 조건2. 속도의 경우 외부에서 접근은 불가능하되, 자식 클래스에서는 사용할 수 있어야 합니다.
	int speed;

public:
	Vehicle(string brand, int speed) :brand(brand), speed(speed) {};

	// 조건3. 브랜드와 속도를 출력하는 함수가 있어야 합니다.
	void showInfo() {
		cout << "브랜드는 " << brand << ", 속도는 " << speed << "입니다." << endl;
	}
};

// Car 클래스(자식 클래스)
class Car :public Vehicle {
	// 조건1. 승객수를 저장하는 변수를 가지고 있어야 하며, 외부·자식 클래스에서 접근할 수 없어야 합니다.
	int passengerCapacity;
public:
	Car(string brand, int speed, int passengerCapacity) :Vehicle(brand, speed) {
		this->passengerCapacity = passengerCapacity;
	}
  // Car(string brand, int speed, int passengerCapacity) :Vehicle(brand, speed), passengerCapacity(passengerCapacity) {}; => 같은 코드

	// 조건2. 승객수를 출력하는 함수를 가지고 있어야 합니다.
	void print() {
		cout << "승객 수는 " << passengerCapacity << "명 입니다." << endl;
	}
};

// 4. Truck 클래스 (자식 클래스)
class Truck : public Vehicle {
	// 조건1. 적재 용량을 저장하는 변수를 가지고 있어야 하며, 외부·자식 클래스에서 접근할 수 없어야 합니다.
	int loadCapacity;
public:
	Truck(string brand, int speed, int loadCapacity) :Vehicle(brand, speed) {
		this->loadCapacity = loadCapacity;
	}
  // Truck(string brand, int speed, int loadCapacity) :Vehicle(brand, speed), loadCapacity(loadCapacity) {}; => 같은 코드

	// 조건2. 적재 용량을 출력하는 함수를 가지고 있어야 합니다.
	void print() {
		cout << "적재 용량은 " << loadCapacity << "개 입니다." << endl;
	}

};

int main() {
  Car c1("Benz", 10, 20);
  Truck t1("BMW", 20, 10);

  c1.showInfo();
  c1.printCar();

  t1.showInfo();
  t1.printTruck();
}
```

---

## 🔹 연습 예제 코드 : overloading

같은 이름의 함수를 매개변수의 개수나 타입을 다르게 하여 여러 개 정의하는 기능

```cpp
#include <iostream>
using namespace std;

int add(int a, int b) {
	cout << "두 개 더하기 : ";
	return a + b;
} // add 1번

int add(int a, int b, int c) {
	cout << "세 개 더하기 : ";
	return a + b + c;
} // add 2번

int main() {
	cout << add(30, 50) << endl; // 매개변수가 2개이기 때문에 add 1번을 선택
	cout << add(30, 50, 20) << endl; // 매개변수가 3개이기 때문에 add 2번을 선택
}
```

```cpp
#include <iostream>
using namespace std;

class Calc {
public:
	int add(int a, int b) {
		cout << "두 개 더하기 : ";
		return a + b;
	} // add 1번

	int add(int a, int b, int c) {
		cout << "세 개 더하기 : ";
		return a + b + c;
	} // add 2번
};

int main() {
	Calc c1;
	cout << c1.add(30, 50) << endl; // 매개변수가 2개이기 때문에 add 1번을 선택
	cout << c1.add(30, 50, 20) << endl; // 매개변수가 3개이기 때문에 add 2번을 선택
}
```

```cpp
#include <iostream>
using namespace std;

class CalcParent {
public:
	int add(int a, int b) {
		cout << "두 개 더하기 : ";
		return a + b;
	}
};

class CalcChild: public CalcParent {
public:
	int add(int a, int b, int c) {
		cout << "세 개 더하기 : ";
		return a + b + c;
	}
};

int main() {
	CalcChild c1;
	cout << c1.add(30, 50) << endl; // 매개변수의 개수가 상속 받은 것과 다르기 때문에 실행 불가
	cout << c1.add(30, 50, 20) << endl;
}
```

---

## 🔹 실습 1 : 함수 오버로딩 - 면적 계산하기

Shape 클래스를 만들고, 함수 오버로딩을 활용하여 정사각형, 직사각형, 원의 면적을 계산하는 프로그램

```cpp
#include <iostream>
#include <cmath>
using namespace std;

class Shape {
public:
	void Area() {};
};

class Circle :public Shape {
	double radius;
public:
	Circle(double radius) :radius(radius) {};
	void Area() {
		cout << "원의 넓이는 " << 3.14 * radius * radius << "입니다." << endl;
	}

};

class Rectangle :public Shape {
	int width, height;
public:
	Rectangle(int width, int height) :width(width), height(height) {};
	void Area() {
		cout << "직사각형의 넓이는 " << width * height << "입니다." << endl;
	}
};

class Square :public Shape {
	int side;
public:
	Square(int side) :side(side) {};
	void Area() {
		cout << "정사각형의 넓이는 " << side * side << "입니다." << endl;
	}
};

int main() {
	Circle c1(10);
	Rectangle r1(10, 20);
	Square s1(30);

	c1.Area();
	r1.Area();
	s1.Area();
}
```

###### 오버로딩을 구현하려고 했으나, 다형성을 사용하게 되어 코드를 오버로딩 방식으로 수정

```cpp
#include <iostream>
using namespace std;
// Shape 클래스를 만들고, 함수 오버로딩을 활용하여 정사각형, 직사각형, 원의 면적을 계산하는 프로그램을 작성하세요.
class Shape {

public:
  // 1. 정사각형의 면적: area(int side)
	void getArea(int side) {
		cout << "정사각형의 넓이는 " << side * side << "입니다." << endl;
	}

  // 2. 직사각형의 면적: area(int width, int height)
	void getArea(int width, int height) {
		cout << "직사각형의 넓이는 " << width * height << "입니다." << endl;
	}

  // 3. 원의 면적: area(double radius) 원의 면적을 계산할 때는 π = 3.14159를 사용
	void getArea(double radius) {
		cout << "원의 넓이는 " << 3.14159 * radius * radius << "입니다." << endl;
	}
};

// 4. main 함수에서 각각의 면적을 계산하여 출력
int main() {
	Shape c1;
	Shape r1;
	Shape s1;

	c1.getArea(10.0);
	r1.getArea(10, 20);
	s1.getArea(30);
}
```

---

## 🔹 연습 예제 코드 : 연산자 overloading

연산자(+, -, \*, /, == 등)를 재정의

```cpp
#include <iostream>
using namespace std;

class Weight {
public:
	int kg;

	Weight(int w) :kg(w) {};

	// 연산자 재정의 : +
	Weight* operator+(Weight& other) {
		this->kg += other.kg;
		return this;
	}

	void showWeight() {
		cout << "몸무게는 " << kg << "kg 입니다." << endl;
	}
};

int main() {
	Weight w1(100), w2(200);
	(w1 + w2)->showWeight();
}
```

---

## 🔹 실습 2 : 연산자 오버로딩 - 좌표 연산

연산자 오버로딩을 이용하여 좌표 간 덧셈 연산이 가능하도록 하는 프로그램

```cpp
#include <iostream>
using namespace std;

class Point {
	int x, y;

// 1. Point 클래스를 만들고, x, y 좌표를 저장하는 멤버 변수를 포함하세요
public:
	Point(int x, int y) :x(x), y(y) {};

  // 2. operator+ 연산자를 오버로딩하여 두 Point 객체를 더할 수 있도록 하세요.
	Point* operator+(Point& other) {
		this->x += other.x;
		this->y += other.y;
		return this;
	}

	void show() {
		cout << "x :" << x << ", y : " << y << endl;
	}
};

// 3. main 함수에서 두 개의 Point 객체를 더한 결과를 출력하세요.
int main() {
	Point p1(10, 20), p2(70, 80);

	(p1 + p2)->show();
}
```

---

## 🔹 실습 2 : 유일한 ID 할당 (에러 수정)

사용자 정보를 입력받고, 각 객체에 유일한 ID를 부여하며, 생성된 객체 수를 추적하여 출력하는 프로그램

```cpp

```

---

## 🔹 연습 예제 코드 : 상속

기존 클래스의 특성과 행동(속성 및 메서드)을 재사용하고, 새로운 기능을 추가하거나 기존 기능을 변경

```cpp

```
