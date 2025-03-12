# 🖥️ C++ 기초 코드 모음

## 📌 개요

이 저장소는 C++ 기본 문법을 익히기 위한 다양한 코드를 포함하고 있습니다.

---

## 🔹 day9

## 이 코드는 C++ 언어의 이중 포인터와 C++ 표준 라이브러리에 관련된 기본적인 문법을 포함하고 있습니다.

---

## 🔹 연습 예제 코드: 이중 포인터 및 C++ 표준 라이브러리

포인터를 가리키는 포인터 (포인터의 주소를 저장하는 변수), C++ 표준 라이브러리

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    int** p = new int* [2];
    p[0] = new int(10);
    p[1] = new int(20);
    cout << *p[0] << " " << *p[1] << endl;


    int x = 5;
    int* ptr1 = &x;
    int** ptr2 = &ptr1;
    cout << **ptr2 << endl;
    **ptr2 = 10;
    cout << "x : " << x << endl;
    cout << "*ptr1 : " << *ptr1 << endl;
    cout << "**ptr2 : " << **ptr2 << endl;


    char c[] = "문자열";
    string str = "문자열";
    cout << c << " " << str << endl;


    string s1 = "Hello";
    string s2 = ("World!");
    string s3(5, '!');
    cout << s1 << " " << s2 << " " << s3 << endl;


    string s4;
    string s5;
    cin >> s4>>s5;
    cout << s4 << " " << s5 << endl;


    string s6;
    getline(cin, s6); // getline => 공백을 포함한 입력 받기
    cout << s6 << endl;


    string s7 = "Hello ";
    string s8 = "World!";
    cout << s7 + s8 << endl;
    cout << (s7 < s8) << endl; // 1순위 : 사전 순, 2순위 : 길이

    string s9 = "codingOn";
    cout << s9.at(3) << endl; // 특정 요소를 불러올 수도 있음
    cout << s9[3] << endl;

    cout << s9.front() << endl;
    cout << s9.back() << endl;

    cout << size(s9) << endl;
    cout << s9.append(" fighting!") << endl;

    cout << s9.insert(8, " not") << endl;

    cout << s9.replace(9, 3, "") << endl;

    cout << s9.find("g") << endl;


    string s10 = "apple";
    cout << s10.find("p") << endl;

    string s11 = "impossible";
    cout << s11.substr(2) << endl;

    int i1 = 1004;
    string s12 = "impossible";
    string s13 = to_string(i1);

    int i2 = stoi(s13);


    string s14 = "impossible";
    cout << s14 << endl;
    for (char &c : s14) {
    	c = toupper(c);
    }
    cout << s14 << endl;
}

```

---

## 🔹 실습 1 :

string 사용해보기

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    string s = "Police say two people are suspected of trying to create a shortcut for their construction work.The two have been detained and the case is under further investigation.The 38-year-old man and 55-year-old woman were working near the affected area, the 32nd Great Wall.";

    // 1. s 문자열의 길이 출력
    cout << "string s의 길이 : " << s.length() << endl;
    cout << "string s의 길이 : " << s.size() << endl;

    // 2. 100번째 문자 출력(index는 0부터 시작)
    cout << "string s의 100번째 문자 : " << s.at(99) << endl;
    cout << "string s의 100번째 문자 : " << s[99] << endl;

    // 3. “two” 라는 문자가 처음 나오는 index 출력
    cout << "string s에서 two가 먼저 나오는 index : " << s.find("two") << endl;

    // 4. “two” 라는 문자가 두번째 나오는 index 출력
    cout << "string s에서 two가 두 번째로 나오는 index : " << s.find("two", s.find("two")+1) << endl;
}
```

---

## 🔹 실습 2 :

string 사용해보기

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

bool isValidNumber(string& str) {
	for (char c : str) {
		if (!isdigit(c)) {
			return false;
		}
	}
	return true;
}

void checkStr(string &str, const string prompt) {
	while (!isValidNumber(str)) {
		cout << prompt;
		cin >> str;
	}
}

int main() {
    // 리팩토링 전

    string test21;
    string test22;
    bool test21Bool = true;
    bool test22Bool = true;
    bool flag = true;
    cout << "두 문자열을 입력하세요 : ";
    cin >> test21 >> test22;

    while (flag) {
        // 1. 두 문자열을 입력 받아서 둘 모두 숫자인지 검사, 아니면 다시 입력 받기
    	for (char c21 : test21) {
    		if (!isdigit(c21)) {
    			test21Bool = true;
    			break;
    		}
    		test21Bool = false;
    	}
    	if (test21Bool) {
    		cout << "test21의 문자열을 다시 입력하세요 : ";
    		cin >> test21;
    	}

    	for (char c22 : test22) {
    		if (!isdigit(c22)) {
    			test22Bool = true;
    			break;
    		}
    		test22Bool = false;
    	}
    	if (test22Bool) {
    		cout << "test22의 문자열을 다시 입력하세요 : ";
    		cin >> test22;
    	}

    	if (!test21Bool && !test22Bool) {
    		flag = false;
    	}

    }



    string test21;
    string test22;
    bool flag = true;
    cout << "두 문자열을 입력하세요 : ";
    cin >> test21 >> test22;

    // 리팩토링 후(1)

    while (flag) {
        // 1. 두 문자열을 입력 받아서 둘 모두 숫자인지 검사, 아니면 다시 입력 받기
    	if (!isValidNumber(test21)) {
    		cout << "test21의 문자열을 다시 입력하세요 : ";
    		cin >> test21;
    	}
    	if (!isValidNumber(test22)) {
    		cout << "test22의 문자열을 다시 입력하세요 : ";
    		cin >> test22;
    	}
    	if (isValidNumber(test21) && isValidNumber(test22)) {
    		flag = false;
    	}
    }

    // 리팩토링 후(2)

    // 1. 두 문자열을 입력 받아서 둘 모두 숫자인지 검사, 아니면 다시 입력 받기
    checkStr(test21, "test21의 문자열을 다시 입력하세요 : ");
    checkStr(test22, "test22의 문자열을 다시 입력하세요 : ");

    // 2.앞에서 입력 받은 두 숫자를 이어 붙여서 출력
    cout << test21 + test22 << endl;

    // 3.앞에서 입력 받은 두 숫자의 합을 출력
    cout << stoi(test21) + stoi(test22) << endl;
}
```

---

## 🔹 실습 3 :

string 사용해보기

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    // 1. string s = “Codingon”
    string s = "Codingon";
      cout << s << endl;

    // 2.첫번째 문자 소문자로 변경 → “codingon”
    s[0] = tolower(s[0]);
    cout << s << endl;

    // 3.“ding” 이라는 부분문자열 반환
    cout << s.substr(s.find("ding"), size("ding")-1) << endl;

    // 4.“coooooon” 이 되도록 변경
    cout << s.replace(2, s.find("on") - 1, string(size("ding"), 'o')) << endl;

    // 5.“con” 이 되도록 변경
    cout << s.erase(1, size("ding")) << endl;
}
```
