# Dart Data Types
## Basic Dart Types
- Dart의 모든 자료형은 Object, class로 이루어져 있음
```dart
void main() {
    String name = "horong";
    bool alive = true;
    int age = 12;
    double money = 70.05;
    num x = 12;
    x = 1.1; // int, double의 부모 class
}
```

## String Interpolation
- text에 변수를 추가하는 방법
- 단순히 변수를 담고 싶으면 $ 뒤에 변수 입력
- 변수에 계산을 추가하고 싶으면 ${} 안에 변수 입력
```dart
void main() {
    var name = "horong";
    var age = 10;
    var greeting = "Hello, my name is $name and I\'m ${age + 2}";
}
```

## Lists
```dart
void main() {
    var giveMeFive = true;
    var numbers = [
        1,
        2,
        3,
        4,
    ];
    numbers.first // 첫번째 요소
    numbers.last // 마지막 요소
    numbers.add() // 요소 추가
    numbers.clear() // 요소 전체 삭제
    // 이 외 다양한 메서드 사용할 수 있음
}
```
### Collection if
- if의 bool 값에 따라서 원소를 추가할 수 있음
```dart
void main() {
    var giveMeFive = true;
    var numbers = [
        1,
        2,
        3,
        4,
        if (giveMeFive) 5,  // giveMeFive가 true일 때 numbers에 5를 추가
    ];
}
```

### Collection for
- for을 사용해 리스트에 원소를 추가할 수 있음
```dart
void main() {
    var oldFriends = ["horong", "jungu"];
    var newFriends = [
        "lyn",
        "json",
        "bell",
        for (var friend in oldFriends) "❤️ $friend"
    ];
}
```

## Maps
- JavaScript의 Object, Python의 Dict와 같음

```dart
void main() {
    var player = {
        "name" : "horong",
        "xp" : 19.99,
        "superpower" : false,
    };
}
```
- 위 코드에서 player의 자료형 : Map<String, Object>
- key가 String, value가 Object인 Map
- Object는 기본적으로 어떤 자료형이든 될 수 있음 (TypeScript의 any와 같은 역할)
- 다른 타입처럼 자료형을 직접 지정할 수 있음
```dart
void main() {
    Map<List<int>, bool> player = {
        [1, 2, 3] : true,
    };
}
```
```dart
void main() {
    List<Map<String, Object>> players = [
        {name: "A", age : 20},
        {name: "B", age : 21},
    ];
}
```
- key-value가 특정 구조로 된 Object를 생성할 때는 위 코드와 같이 Map을 사용하기 보다는 **class를 사용하는 것을 추천함**
- ex) API에서 data를 불러올 때

## Sets
- JavaScript의 Set, Python의 Tuple과 같음
- List와의 차이점 : 모든 요소가 유니크함
```dart
void main() {
    var numbers = {1, 2, 3, 4};
    numbers.add(1);
    print(numbers) // {1, 2, 3, 4}
}
```