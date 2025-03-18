# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 mini_project

## 이 코드는 C++ 언어의 클래스 종합 실습에 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 Character.h

```cpp
#pragma once
#include <iostream>
#include <string>
#include <memory>
using namespace std;

class Character {
protected:
	// 1. 멤버 변수:
	string name; // name: 캐릭터 이름
	// int level; // level: 캐릭터 레벨
	int health; // health: 체력
	int maxHealth;
	int attackPower; // attackPower: 공격력

public:
	Character();

	// 2. 멤버 함수:
	Character(string name, int health, int attackPower);
	// attack(Character& target): 기본 공격 (순수 가상 함수)
	virtual void attack(Character& target) = 0;

	// specialAttack(Character& target): 특수 공격 (순수 가상 함수)
	virtual void specialAttack(Character& target) = 0;

	// takeDamage(int damage): 피해를 입으면 체력이 감소
	void takeDamage(int damage) {
		health -= damage;
		if (health < 0) health = 0;
	}

	// isAlive() : 체력이 0 이하이면 false 반환
	bool isAlive();

	// showStatus(): 캐릭터 정보를 출력
	void showStatus();

	// void resetHealth(): 캐릭터의 체력을 초기화
	void resetHealth();

	string getName();
};

```

## 🔹 Character.cpp

```cpp
#include "Character.h"

Character::Character() {};

Character::Character(string name, int health, int attackPower) :
	name(name), health(health), maxHealth(health), attackPower(attackPower) {
	;
}

// isAlive() : 체력이 0 이하이면 false 반환
bool Character::isAlive() {
	return health > 0;
}

// showStatus(): 캐릭터 정보를 출력
void Character::showStatus() {
	cout << "Name: " << name << endl;
	//cout << "Level: " << level << endl;
	cout << "Health: " << health << endl;
	cout << "Attack Power: " << attackPower << endl;
}

// void resetHealth(): 캐릭터의 체력을 초기화
void Character::resetHealth() {
	health = maxHealth;
}

string Character::getName() {
	return name;
}
```

###### 일부 수정

```cpp
#include "Character.h"

Character::Character() {};

Character::Character(string name, int health, int attackPower) :
	name(name), health(health), maxHealth(health), attackPower(attackPower) {
	;
}

// isAlive() : 체력이 0 이하이면 false 반환
bool Character::isAlive() {
	return health > 0;
}

// showStatus(): 캐릭터 정보를 출력
void Character::showStatus() {
	cout << "Name: " << name << endl;
	cout << "Health: " << health << endl;
}

// void resetHealth(): 캐릭터의 체력을 초기화
void Character::resetHealth() {
	health = maxHealth;
}

string Character::getName() {
	return name;
}
```

---

## 🔹 Warrior.h

```cpp
#pragma once
#include <iostream>
#include <string>
#include "Character.h"
using namespace std;

class Warrior :public Character {
public:
	Warrior();

	Warrior(string name);

	void attack(Character& target) override;

	void specialAttack(Character& target) override;
};
```

## 🔹 Warrior.cpp

```cpp
#include "Warrior.h"

Warrior::Warrior() : Character("전사", 100, 15) {};

Warrior::Warrior(string name) : Character(name, 100, 15) {}

void Warrior::attack(Character& target) {
	cout << name << "이(가)" << target.getName() << "을 공격합니다." << endl;
	target.takeDamage(attackPower);
}

// powerStrike
void Warrior::specialAttack(Character& target) {
	cout << name << "이(가)" << target.getName() << "을 쎄게 공격합니다." << endl;
	target.takeDamage(attackPower * 2);
	takeDamage(5);
}
```

###### 일부 수정

```cpp
#include "Warrior.h"

Warrior::Warrior() : Character("전사", 100, 15) {};

Warrior::Warrior(string name) : Character(name, 100, 15) {}

void Warrior::attack(Character& target) {
	cout << name << "이(가) 헤비 슬래시를 " << target.getName() << "에게 사용했습니다." << endl;
	target.takeDamage(attackPower);
}

// powerStrike
void Warrior::specialAttack(Character& target) {
	cout << name << "이(가) (특수)powerStrike를 " << target.getName() << "에게 사용했습니다." << endl;
	target.takeDamage(attackPower * 2);
	takeDamage(5);
}
```

---

## 🔹 Mage.h

```cpp
#pragma once
#include <iostream>
#include <string>
#include "Character.h"
using namespace std;

class Mage :public Character {
protected:
	int mana;
public:
	Mage();

	Mage(string name);

	void attack(Character& target) override;

	void specialAttack(Character& target) override;

	// isAlive() : 체력이 0 이하이면 false 반환
	bool isAlive();

	// showStatus(): 캐릭터 정보를 출력
	void showStatus();

	// void resetHealth(): 캐릭터의 체력을 초기화
	void resetHealth();

	string getName();
};
```

## 🔹 Mage.cpp

```cpp
#include "Mage.h"

Mage::Mage() :Character("마법사", 80, 18), mana(100) {};

Mage::Mage(string name) :Character(name, 80, 18), mana(100) {};

void Mage::attack(Character& target) {
	cout << name << "이(가)" << target.getName() << "을(를) 마법으로 공격합니다." << endl;
	target.takeDamage(attackPower);
}

// fireball
void Mage::specialAttack(Character& target) {
	if (mana < 20) throw runtime_error("마나가 부족합니다!");
	cout << name << "이(가)" << target.getName() << "을(를) 마법으로 쎄게 공격합니다." << endl;
	target.takeDamage(attackPower * 1.5);
}
```

###### 일부 수정

```cpp
#include "Mage.h"

Mage::Mage() :Character("마법사", 80, 18), mana(100) {};

Mage::Mage(string name) :Character(name, 80, 18), mana(100) {};

void Mage::attack(Character& target) {
	cout << name << "이(가) 에테르 스파크를 " << target.getName() << "에게 사용했습니다." << endl;
	target.takeDamage(attackPower);
}

// fireball
void Mage::specialAttack(Character& target) {
	if (mana < 20) throw runtime_error("마나가 부족합니다!");
	cout << name << "이(가) (특수)fireball을 " << target.getName() << "에게 사용했습니다." << endl;
	target.takeDamage(attackPower * 1.5);
	Mage::setMana();
}
```

---

## 🔹 Rogue.h

```cpp
#pragma once
#include <iostream>
#include <string>
#include "Character.h"
using namespace std;

class Rouge :public Character {
public:
	Rouge();

	Rouge(string name);

	void attack(Character& target) override;

	void specialAttack(Character& target) override;
};
```

## 🔹 Rogue.cpp

```cpp
#include<random>
#include "Rouge.h"

Rouge::Rouge() :Character("도적", 90, 12) {};

Rouge::Rouge(string name) :Character(name, 90, 12) {};

void Rouge::attack(Character& target) {
	cout << name << "이(가) 겁나 빠르게" << target.getName() << "을(를) 마법으로 공격합니다." << endl;
	target.takeDamage(attackPower);
}

void Rouge::specialAttack(Character& target) {
	random_device rd; // 하드웨어 기반 난수 생성기 (시드 제공)
	mt19937 gen(rd()); // Mersenne Twister 19937 엔진
	uniform_int_distribution<int> dist(0, 100);

	int chance = dist(gen);

	if (chance < 70) {
		cout << name << "이(가) 급습에 성공해서" << target.getName() << "을(를) 쎄게 공격합니다." << endl;
		target.takeDamage(attackPower * 3);
	}
	else {
		cout << name << "이가 급습에 실패했습니다." << endl;
	}
}
```

###### 일부 수정

```cpp
#include<random>
#include "Rouge.h"

Rouge::Rouge() :Character("도적", 90, 12) {};

Rouge::Rouge(string name) :Character(name, 90, 12) {};

void Rouge::attack(Character& target) {
	cout << name << "이(가) 더블 펑처를 " << target.getName() << "에게 사용했습니다." << endl;
	target.takeDamage(attackPower);
}

void Rouge::specialAttack(Character& target) {
	random_device rd; // 하드웨어 기반 난수 생성기 (시드 제공)
	mt19937 gen(rd()); // Mersenne Twister 19937 엔진
	uniform_int_distribution<int> dist(0, 100);

	int chance = dist(gen);

	if (chance < 70) {
		cout << name << "이(가) (특수)섀도우 팬텀을 " << target.getName() << "에게  사용했습니다." << endl;
		target.takeDamage(attackPower * 3);
	}
	else {
		cout << name << "이가 급습에 실패했습니다." << endl;
	}
}
```

---

## 🔹 BattleManager.h

```cpp
#pragma once
#include <iostream>
#include <memory>
#include <string>
#include<random>
#include "Character.h"
using namespace std;

class BattleManager {
public:

	static void startBattle(unique_ptr<Character>& char1, unique_ptr<Character>& char2);
	// void startBattle(shared_ptr<Character> char1, shared_ptr<Character> char2);

	static void choiceTheAttack(unique_ptr<Character>& char1, unique_ptr<Character>& char2);


	static int R() {
		random_device rd; // 하드웨어 기반 난수 생성기 (시드 제공)
		mt19937 gen(rd()); // Mersenne Twister 19937 엔진
		uniform_int_distribution<int> dist(0, 100);
		int random_number = dist(gen);
		return random_number;
	}
};
```

## 🔹 BattleManager.cpp

```cpp
#include <memory>
#include <chrono>
#include <thread>
#include "BattleManager.h"
using namespace std;


void BattleManager::startBattle(unique_ptr<Character>& char1, unique_ptr<Character>& char2) {
	try {
		if (BattleManager::R() > BattleManager::R()) {
			BattleManager::choiceTheAttack(char1, char2);
			this_thread::sleep_for(chrono::milliseconds(1000));
			if (char2->isAlive()) {
				BattleManager::choiceTheAttack(char2, char1);
				this_thread::sleep_for(chrono::milliseconds(1000));
			}
			else {
				cout << char2->getName() << "이(가) 사망했습니다." << endl;
				this_thread::sleep_for(chrono::milliseconds(1000));
			}
		}
		else {
			BattleManager::choiceTheAttack(char2, char1);
			this_thread::sleep_for(chrono::milliseconds(1000));
			if (char1->isAlive()) {
				BattleManager::choiceTheAttack(char1, char2);
				this_thread::sleep_for(chrono::milliseconds(1000));
			}
			else {
				cout << char1->getName() << "이(가) 사망했습니다." << endl;
				this_thread::sleep_for(chrono::milliseconds(1000));
			}
		}
	}catch (const exception& e) {
		cout << e.what() << endl;
	}
}

void BattleManager::choiceTheAttack(unique_ptr<Character>& attacker, unique_ptr<Character>& defender) {

	if (BattleManager::R() < 70) attacker->attack(*defender);
	else attacker->specialAttack(*defender);
}
```

###### 수정

```cpp
#include <memory>
#include <chrono>
#include <thread>
#include "BattleManager.h"
using namespace std;

random_device rd; // 하드웨어 기반 난수 생성기 (시드 제공)
mt19937 gen(rd()); // Mersenne Twister 19937 엔진
uniform_int_distribution<int> attackTurn(0, 1);
// uniform_int_distribution<int> attackType(0, 1);

void BattleManager::startBattle(unique_ptr<Character>& char1, unique_ptr<Character>& char2) {
	cout << "전투 시작! " << char1->getName() << " vs " << char2->getName() << endl;

	bool playerAttackTurn = attackTurn(gen);

	while (char1->isAlive() && (*char2).isAlive()) {
		char1->showStatus();
		(*char2).showStatus();

		try {
			if (playerAttackTurn) {
				BattleManager::choiceTheAttack(char1, char2);
				this_thread::sleep_for(chrono::milliseconds(1000));
				if (char2->isAlive()) {
					BattleManager::choiceTheAttack(char2, char1);
					this_thread::sleep_for(chrono::milliseconds(1000));
				}
				else {
					cout << char2->getName() << "이(가) 사망했습니다." << endl;
					this_thread::sleep_for(chrono::milliseconds(1000));
					break;
				}
			}
			else {
				BattleManager::choiceTheAttack(char2, char1);
				this_thread::sleep_for(chrono::milliseconds(1000));
				if (char1->isAlive()) {
					BattleManager::choiceTheAttack(char1, char2);
					this_thread::sleep_for(chrono::milliseconds(1000));
				}
				else {
					cout << char1->getName() << "이(가) 사망했습니다." << endl;
					this_thread::sleep_for(chrono::milliseconds(1000));
					break;
				}
			}
		}
		catch (const exception& e) {
			cout << e.what() << endl;
		}

		cout << "-------------------------------------------------------------" << endl;
	}

	cout << (char1->isAlive() ? char1->getName() : (*char2).getName()) << "이(가) 전투에서 승리했습니다." << endl;

	cout << "-------------------------------------------------------------" << endl;
}

void BattleManager::choiceTheAttack(unique_ptr<Character>& attacker, unique_ptr<Character>& defender) {

	if (BattleManager::R() < 70) attacker->attack(*defender);
	else attacker->specialAttack(*defender);
}
```

## 🔹 main.cpp

```cpp
#include <iostream>
#include<random>
#include <memory> // 스마트 포인터를 사용하기 위한 라이브러리
#include "BattleManager.h"
#include "Warrior.h"
#include "Rouge.h"
#include "Mage.h"
#include "Character.h"
using namespace std;

unique_ptr<Character> chooseCharacter(const string& prompt) {
	int input;
	cout << prompt << endl
		 << "1. 전사" << endl
		 << "2. 마법사" << endl
		 << "3. 도적" << endl
		 << "입력 : ";
	cin >> input;
	switch (input) {
		case 1:
			return make_unique<Warrior>();
		case 2:
			return make_unique<Mage>();
		case 3:
			return make_unique<Rouge>();
		default:
			cout << "잘못된 입력입니다. 기본값으로 전사 선택" << endl;
			return make_unique<Warrior>();
	}
}

int main() {
	unique_ptr<Character> player1 = chooseCharacter("자신의 캐릭터를 선택하세요.");
	while (true) {
		unique_ptr<Character> player2 = chooseCharacter("상대 캐릭터를 선택하세요.");
		BattleManager::startBattle(player1, player2);

		if (!player1->isAlive()){
      cout << "패배하였습니다. 전투를 종료합니다.";
      break;
    }
		else player1->resetHealth();

		char choice;

		cout << "승리하였습니다. 전투를 계속 진행하겠습니까? (y/n) : ";
		cin >> choice;

		if (choice == 'n') {
			cout << "게임을 종료합니다." << endl;
			break;
		}
	}
}
```
