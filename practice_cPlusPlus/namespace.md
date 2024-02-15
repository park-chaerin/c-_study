#  이름공간 (namespace)

std : c++ 표준 라이브러리의 모든 함수, 객체 등이 정의된 namespace.
namespace : 말 그대로 어떤 정의된 객체에 대해 어디 소속인지 지정해주는 것과 같음.
``` c++
std::cout
//std라는 namespace에 정의되어 있는 cout를 의미.
// 만약 그냥 cout라고 하면, 컴파일러가 cout를 찾지 못함.
```
## namespace를 정의하는 방법
ex) 
두개의 헤더파일이 있다고 했을때,

```c++
namespace header1 {
int foo();
void bar();
}

namespace header2{
int foo();
void bar();
}
```
-> 각각 header1에 있는 foo와 header2에 있는 foo가 다름.

```c++
//자기 자신이 포함되어 있는 namespace에서는 자유롭게 사용 가능.

# include "header1.h"
namespace header1{
int func(){
  foo();    
}
}
```
-> 알아서 header1::foo()가 실행됨.

다만, 어떠한 namespace에도 소속되지 않은 경우라면 아래와 같이 명시적으로 namespace 지정해야함.
```c++
#include "header1.h"
#include "header2.h"

int func() {
  header1::foo();   // header1이란 namespace에 있는 foo호출.
}
```

여기서! 만약 foo를 반복적으로 호출해야 하는 경우 매번 header1::을 붙이기 귀찮을 때는!
```c++
#include "header1.h"
#include "header2.h"

using header1::foo;     // header1의 namespace에 있는 foo만 사용할거라는 선언.
int main(){
  foo();
}
```

또한, 기본적으로 header1의 namespace에 정의된 모든 것들을 header:: 없이 사용하고 싶을 경우,

```c++
#include "header1.h"
#include "header2.h"

using namespace header1;    //이렇게 명시하면 됨.
int main() {
  foo();
  bar();
}
```

### 주의!
- 여기서 using namespace std;를 사용하는 것은 권장 X.
- std에 이름이 겹치는 함수를 만들게 된다면 오류가 발생하기 때문.
- std에는 매번 많은 함수들이 새롭게 추가되고 있기 때문에, 권장하지 않음.
- using namespace std;는 사용하지 말고, std:: 를 사용하자.

# cout
- ostream 클래스의 객체로, 표준 출력을 담당.
```c++
std::cout << /* 출력할 것 */ << /* 출력할 것 */ << ... << /* 출력할 것 */;
```

# endl 
- 화면에 출력해주는 함수.
```c++
std::cout << std:endl;

//이렇게 사용하면, 화면에 엔터를 하나 출력해줌.
```

# 이름없는 namespace
- c++에서는 namespace에 굳이 이름을 설정하지 않아도 됨.
- 이 경우 해당 namespace에 정의된 것들은 해당 파일 안에서만 접근할 수 있게 됨. => 마치 static 키워드를 사용한 것과 같은 효과!

```c++
#include <iostream>

namespace{
//이 함수는 이 파일 안에서만 사용 가능함.
//마치 static int OnlyInThisFile()과 동일.
int OnlyInThisFile() {}

//이 변수도 static int x와 동일.
int only_in_this_file = 0;
}   //namespace

int main() {
OnlyInThisFile();
only_in_this_file = 3;
}
```
-> 예를 들어 위 OnlyInThisFile 함수나 only_in_this_file 변수는 해당 파일 안에서만 접근 가능!

# 생각 해보기
아래 문장은 화면에 어떻게 출력될까?

```c++
std::cout << "hi" <<std::endl
          << "my name is "
          << "Chaerin" << std::endl;
```

요렇게 출력됩니다~
```c++
hi
my name is Chaerin
```
