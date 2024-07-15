### loops

- `for` loops
- `while` and `do while` loops
- `break` and `continue`

### Manipulate control

- **Branching:** `if` and `switch`
- Exceptions: `try` , `catch` and `throw`

### For loop

`Closures`와 `For` loop

**클로저 (Closures)란?**

클로저는 함수가 정의된 위치에서의 변수들을 기억하고 그 변수들에 접근할 수 있는 함수. 클로저는 함수 내부에 정의된 다른 함수가 외부 함수의 변수에 접근할 수 있도록 함.

Dart에서 for 루프 안에서 클로저를 사용할 때, 클로저는 **반복 변수의 값을 캡처**합니다. 이는 JavaScript와의 중요한 차이점입니다. JavaScript에서는 클로저가 반복 변수의 마지막 값을 **캡처**하는 반면, Dart에서는 클로저가 각 반복에서의 변수를 캡처합니다.

예제:

```dart
var callbacks = [];
for (var i = 0; i < 2; i++) {
  callbacks.add(() => print(i));
}

for (final c in callbacks) {
  c();
}
```

위 코드는 다음과 같은 출력을 생성:

```
0
1
```

이 예제에서 `callbacks` 리스트에는 두 개의 클로저가 추가됩니다. 각 클로저는 `i`의 현재 값을 캡처합니다. 따라서 첫 번째 클로저는 0을 출력하고, 두 번째 클로저는 1을 출력합니다. 이는 Dart의 클로저가 반복 변수의 각 값을 개별적으로 캡처하기 때문에 가능합니다.

반면, JavaScript에서는 동일한 코드가 다음과 같은 출력을 생성할 수 있습니다:

```jsx
var callbacks = [];
for (var i = 0; i < 2; i++) {
  callbacks.push(function() { console.log(i); });
}

callbacks.forEach(function(callback) {
  callback();
});
```

이 경우, 출력은 다음과 같습니다:

```
2
2
```

JavaScript에서는 클로저가 반복 변수의 마지막 값을 캡처하기 때문에 이러한 결과가 나옵니다. 따라서 두 클로저 모두 마지막 값인 2를 출력합니다.

### while 및 do-while

while 루프는 루프 전에 조건을 평가합니다:

```dart
while (!isDone()) {
  doSomething();
}

```

do-while 루프는 루프 후에 조건을 평가합니다:

```dart
do {
  printLine();
} while (!atEndOfPage());

```

### Break 및 Continue

break를 사용하여 반복을 중지하십시오:

```dart
while (true) {
  if (shutDownRequested()) break;
  processIncomingRequests();
}

```

continue를 사용하여 다음 반복으로 건너뛰십시오:

```dart
for (int i = 0; i < candidates.length; i++) {
  var candidate = candidates[i];
  if (candidate.yearsExperience < 5) {
    continue;
  }
  candidate.interview();
}

```

Iterable(예: 리스트나 세트)을 사용하는 경우, 이전 예제를 다르게 작성할 수 있습니다:

```dart
candidates
    .where((c) => c.yearsExperience >= 5)
    .forEach((c) => c.interview());

```
