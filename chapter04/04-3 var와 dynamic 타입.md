### Dart의 `dynamic`

Dart에서 `dynamic`은 모든 타입의 값을 가질 수 있는 변수에 사용. `dynamic`은 Dart의 타입 시스템의 유연성을 제공, 타입 안전성을 희생.

### `dynamic`의 특징

- **유연성**: 모든 타입의 값을 할당 가능.
- **타입 체크 없음**: 컴파일 타임에 타입 체크가 수행되지 않으므로 런타임 오류가 발생 가능성.
- **사용 예시**: 변수의 타입이 런타임에 결정되거나, 여러 타입을 처리해야 하는 경우에 유용.

### `dynamic` 변수 선언

- **예시**:
    
    ```dart
    dart코드 복사
    dynamic anything = 'Hello';
    print(anything); // 출력: Hello
    
    anything = 42;
    print(anything); // 출력: 42
    
    anything = [1, 2, 3];
    print(anything); // 출력: [1, 2, 3]
    
    ```
    

### `dynamic`과 `var`의 차이점

- **타입 추론 vs 유연성**:
    - `var`로 선언된 변수는 초기 값에 따라 타입이 고정.
    - `dynamic`으로 선언된 변수는 언제든지 다른 타입의 값을 가질 수 있음.
- **예시**:
    
    ```dart
    dart코드 복사
    var inferredType = 'Hello';
    inferredType = 42; // 오류: String 타입에서 int 타입으로 변경 불가
    
    dynamic flexibleType = 'Hello';
    flexibleType = 42; // 가능: 타입이 런타임에 결정됨
    
    ```
