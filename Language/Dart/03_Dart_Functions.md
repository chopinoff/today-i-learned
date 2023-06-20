# Dart Functions
## Defining a Function
- void : 아무것도 return하지 않는 함수를 정의
- return 값에 따라 함수 앞의 Type을 지정
```dart
String sayHello(String name) {
    return "Hello $name nice to meet you!";
}

void main() {
    print(sayHello("horong"));
}
```
- 화살표 함수로 표현할 수 있음
```dart
String sayHello(String name) => "Hello $name nice to meet you!";
```
## Positional Parameters
- 함수에 사용되는 변수를 순서대로 입력해야 함
- 변수가 들어가는 순서를 기억해야한다는 단점이 있음
- 모든 변수는 필수로 값이 들어가야 함
```dart
String sayHello(String name, int age, String country) {
    return "Hello $name, you are $age, and you come from $country";
}

void main() {
    print(sayHello("horong", 20, "USA"));
}
```

## Named Parameters
- named parameters를 사용하면 변수의 이름과 값을 key-value 형태로 입력할 수 있음
- 하지만 map의 개념이 아니므로 주의
- 변수가 들어가는 순서를 기억하지 않아도 됨
- 함수에 인자를 적을 때, 
```dart
String sayHello({
    String name,
    int age,
    String country,
    }) {
    return "Hello $name, you are $age, and you come from $country";
}

void main() {
    print(sayHello(name : "horong", age : 20, country : "USA"));
    // key-value 형태지만 map이 아니므로 작성에 주의
    // "name" : "horong" (X)
    // name : "horong" (O)
}
```
**만약 유저가 이름을 적지 않는다면?**
1. default value 설정하기
- 값을 입력하지 않았을 때의 기본 값 설정
```dart
String sayHello({
    String name = "hy",
    int age = 20,
    String country = "Korea",
    }) {
    return "Hello $name, you are $age, and you come from $country";
}
```
2. required modifier 사용하기
- 필수 값으로 지정하기
- 필수로 지정된 변수에 값이 할당되지 않으면 해당 함수를 컴파일하지 않음
```dart
String sayHello({
    required String name,
    required int age,
    required String country,
    }) {
    return "Hello $name, you are $age, and you come from $country";
}
```
- 비교 : positional parameters는 기본값이 required임

## Optional Positional Parameters
- positional parameters에서 변수를 옵션으로 설정하기
- 자주 사용하는 방법은 아님
```dart
String sayHello(String name, int age,
    [String? country = "Korea"]) { // 대괄호와 ? 사용해서 옵션으로 설정할 수 있음
    return "Hello $name, you are $age, and you come from $country";
}

void main() {
    print(sayHello("horong", 20));
}
```

## QQ Operator
- **특정 값이 null일 때** 원하는 값을 return하거나 할당할 때 사용함
### QQ Operator : `??`
- `A ?? B`일 때, A가 null이 아니면 A를 return, null이면 B를 return
- ex) 내 이름을 대문자로 출력하는 함수
- 사용자가 null도 입력할 수 있게 만들고자 함
1. if문 작성하기
```dart
String capitalizeName(String? name) {
    if (name != null) {
        return name.toUpperCase()
    }
    return "ANON"
}

void main() {
    capitalizeName("horong"); // HORONG
    capitalizeName(null);
}
```
2. 삼항 연산자 사용하기
```dart
String capitalizeName(String? name) =>
    name != null ? name.toUpperCase() : "ANON";
```
3. QQ Operator 사용하기
```dart
    name?.toUpperCase() ?? "ANON"
    // name.toUpperCase()로 작성하는 경우
    // name이 null이면 toUpperCase()가 실행될수 없기 때문에
    // name이 null일 경우 null을 반환할 수 있도록 name?.toUpperCase()로 작성함
```
### QQ Equals (QQ Assignment Operator) : `??=`
- `x ??= A`일 때, x가 null일 때만 x에 A를 할당함
```dart
void main() {
    String? name;
    name ??= "horong"
    name = null
    name ??= "another"
    print(name) // another
}
```

## Typedef
- 자료형이 헷갈릴 때 도움이 되는 alias를 작성하는 방법
- ex 1) 리스트 요소 순서를 거꾸로 반환하는 함수
```dart
typedef ListOfInts = List<int>; // alias 생성

List<int> reverseListOfNumbers(ListOfInts list) {
    var reversed = list.reversed;
    return reversed.toList();
}

void main() {
    reverseListOfNumbers([1, 2, 3])
}
```
- ex 2) 맵의 name을 사용해 인사하는 함수
- 이렇게 써도 돌아가지만, 구조화된 data의 형태를 지정하고 싶다면 **class를 사용해야 함**
```dart
typedef UserInfo = Map<String, String>

String sayHi(UserInfo userInfo) {
    return "Hello ${userInfo['name']}";
}

void main() {
    sayHi({"name" : "horong"})
}
```