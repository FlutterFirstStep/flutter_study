# 함수
- 다트는 객체 지향(object-oriented)언어로, 함수 또한 객체이며 Function이라는 타입을 가진다
- 함수를 변수에 할당할 수 있다
- 함수를 다른 함수의 인자로 전달할 수 있다

# 함수 선언 방식
일반 🔽
```
bool isNoble(int atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

타입 생략 🔽
```
isNoble(atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

one expression일때 짧게 가능 🔽
```
bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```

# Parameters
- 함수에는 required positional parameters가 온다.
- 그 다음 명명된 매개변수(named parameters) 또는 선택적 위치 매개변수(optional positional parameters) 둘중 하나만 사용가능

## named parameters
- required 가 없는 한 optional 하다

예시
```
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool? bold, bool? hidden}) {...}
```

호출시에는 paramName: value 형태로 사용한다
```
enableFlags(bold: true, hidden: false);
```

기본값은 =로 설정한다
```
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold = false, bool hidden = false}) {...}

// bold will be true; hidden will be false.
enableFlags(bold: true);
```

필수적으로 요구하기 위해서 required 어노테이션을 붙인다.
```
const Scrollbar({super.key, required Widget child});
```

## optional parameters
optional parameters는 []로 감싼다
```
String say(String from, String msg, [String? device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}
```

# Functions as first-class objects
함수도 다른 함수의 인자가 될 수 있다.
```dart
void printElement(int element) {
  print(element);
}

var list = [1, 2, 3];

// Pass printElement as a parameter.
list.forEach(printElement);
```

함수를 변수에 할당할 수 있다
```dart
//shorthand
var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
assert(loudify('hello') == '!!! HELLO !!!');
```

This example uses an anonymous function. More about those in the next section.

# Anonymous functions
이름없는 함수이다
- 비슷한 용어
  - anonymous functions
  - lambdas
  - closures

```
fun1(arg) {
  return 10;
}

// 익명함수
Function fun2 = (arg) {
  return 10;
}
```