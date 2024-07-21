# constructors

Generative constructors: Creates new instances and initializes instance variables.
Default constructors: Used to create a new instance when a constructor hasn't been specified. It doesn't take arguments and isn't named.
Named constructors: Clarifies the purpose of a constructor or allows the creation of multiple constructors for the same class.
Constant constructors: Creates instances as compile-type constants.
Factory constructors: Either creates a new instance of a subtype or returns an existing instance from cache.
Redirecting constructor: Forwards calls to another constructor in the same class.

- 생성자: 새로운 인스턴스를 생성하고 인스턴스 변수를 초기화합니다.
```dart
class Point {
  // Initializer list of variables and values
  double x = 2.0;
  double y = 2.0;

  // Generative constructor with initializing formal parameters:
  Point(this.x, this.y);
}
```


### 기본 생성자
생성자가 지정되지 않았을 때 새로운 인스턴스를 생성하는 데 사용됩니다. 인수를 받지 않으며 이름이 없습니다.


### 명명된 생성자
생성자의 목적을 명확히 하거나 동일한 클래스에 여러 생성자를 만들 수 있게 합니다.
```dart
const double xOrigin = 0;
const double yOrigin = 0;

class Point {
  final double x;
  final double y;

  // Sets the x and y instance variables
  // before the constructor body runs.
  Point(this.x, this.y);

  // Named constructor
  Point.origin()
      : x = xOrigin,
        y = yOrigin;
}

// 생성 예시
Point p1 = Point(5, 6);
Point p2 = Point.origin();
```


### 상수 생성자
컴파일 시 상수로 인스턴스를 생성합니다.
변경되지 않는 객체로 사용할때, 상수 생성자를 이용한다.
const 키워드를 생성자에 적용하며, 모든 인스턴스 변수들에 final을 붙인다.
```dart
class ImmutablePoint {
  static const ImmutablePoint origin = ImmutablePoint(0, 0);

  final double x, y;

  const ImmutablePoint(this.x, this.y);
}
```


### 리디렉팅 생성자
동일한 클래스 내의 다른 생성자에 호출을 전달합니다.
생성자는 동일한 클래스의 다른 생성자로 호출을 전달할 수 있습니다. 리디렉팅 생성자는 본문이 비어 있습니다. 생성자는 콜론 (:) 뒤에 클래스 이름 대신 this를 사용합니다.
```dart
class Point {
  double x, y;

  // The main constructor for this class.
  Point(this.x, this.y);

  // Delegates to the main constructor.
  Point.alongXAxis(double x) : this(x, 0);
}
```


### 팩토리 생성자
하위 유형의 새 인스턴스를 생성하거나 캐시에서 기존 인스턴스를 반환합니다.
다음 두 가지 경우에 생성자를 구현할 때는 factory 키워드를 사용합니다:

생성자가 항상 클래스의 새로운 인스턴스를 생성하지 않는 경우. 비록 팩토리 생성자가 null을 반환할 수는 없지만, 다음과 같은 경우에는 반환할 수 있습니다:

1. 새 인스턴스를 생성하는 대신 캐시에서 기존 인스턴스를 반환하는 경우
2. 하위 타입의 새 인스턴스를 반환하는 경우
3. 인스턴스를 생성하기 전에 복잡한 작업을 수행해야 하는 경우. 여기에는 인수 검사나 초기화 목록에서 처리할 수 없는 다른 처리가 포함될 수 있습니다.

팁: late final을 사용하여 final 변수의 초기화를 나중에 처리할 수 있습니다 (조심!).

다음 예시는 두 개의 팩토리 생성자를 포함하고 있습니다.

Logger 팩토리 생성자는 캐시에서 객체를 반환합니다.
Logger.fromJson 팩토리 생성자는 JSON 객체에서 final 변수를 초기화합니다.

```dart
class Logger {
  final String name;
  bool mute = false;

  // _cache는 이름 앞의 _ 덕분에 라이브러리-프라이빗입니다.
  static final Map<String, Logger> _cache = <String, Logger>{};

  // 1번경우
  factory Logger(String name) {
    return _cache.putIfAbsent(name, () => Logger._internal(name));
  }
  
  // 3번 경우
  factory Logger.fromJson(Map<String, Object> json) {
    return Logger(json['name'].toString());
  }

  Logger._internal(this.name);

  void log(String msg) {
    if (!mute) print(msg);
  }
}
```
경고: 팩토리 생성자는 this에 접근할 수 없습니다.

다른 생성자와 동일하게 팩토리 생성자를 사용하십시오:
```dart
var logger = Logger('UI');
logger.log('Button clicked');

var logMap = {'name': 'UI'};
var loggerJson = Logger.fromJson(logMap);
```

### 리디렉팅 팩토리 생성자

리디렉팅 팩토리 생성자는 리디렉팅 생성자가 호출될 때마다 다른 클래스의 생성자를 호출하도록 지정합니다.
```dart
factory Listenable.merge(List<Listenable> listenables) = _MergingListenable;
```

일반 팩토리 생성자가 다른 클래스의 인스턴스를 생성하고 반환할 수 있을 것처럼 보일 수 있습니다. 이는 리디렉팅 팩토리의 필요성을 없앨 수 있습니다. 그러나 리디렉팅 팩토리에는 몇 가지 장점이 있습니다:

추상 클래스는 다른 클래스의 상수 생성자를 사용하는 상수 생성자를 제공할 수 있습니다.
리디렉팅 팩토리 생성자는 전달자가 형식 매개변수와 기본값을 반복할 필요성을 없애줍니다.

