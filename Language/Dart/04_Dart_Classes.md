# Dart Classes
## Class
### 의미
- 객체를 만들기 위한 template
- 데이터와 코드를 그룹화해 관련 코드를 함께 유지할 수 있음

### 구성 요소
- Field : class 내부에 선언된 데이터 (변수 / 상수 등)
- Method : class 내부에 선언된 기능 (함수)
- Constructor : class 인스턴스를 생성할 때 사용되는 코드

### 사용 방법
- type을 사용해 property를 선언함
- 함수 안 변수에서는 var로 대체할 수 있었던 것과는 다르게, 반드시 type을 지정해주어야 함
- method 작성 시, 같은 이름의 변수가 있어서 어쩔 수 없이 사용하는 경우가 아닌 이상, **this를 쓰지 않는 것을 권장**

### 코드 예시
```dart
class Player {
    final String name = "horong";  // name은 수정할 수 없음
    int xp = 1500;

    void sayHello() {
        print("Hello my name is $name");
    }
}

void main() {
    var player = Player(); // 앞에 new 작성하지 않아도 됨
    // player.name = "hahaha" : compile error
    print(player.xp) // 1500
    player.xp = 1200;
    print(player.name) // 1200
}
```

## Dart Constructors
### 1. Default constructors
- 기본 constructors
- constructors를 선언하지 않을 경우 제공되는 constructors
### 2. Named constructors
- 개발자가 필요에 의해 생성한 constructors
- 클래스에 대한 여러 constructors를 구현하거나 추가적인 클래스의 명확성을 제공
### 3. Redirecting constructors
- 목적이 동일한 constructors로 전달하기 위한 constructors
- constructors의 본문은 비어있지만 전달된 constructors에 대한 초기값 등을 구현할 때 사용
### 4. Const constructors
- 상수 constructors
- class가 불변의 객체를 생성하는 경우 활용
### 5. Factory constructors
- 매번 새로운 인스턴스를 만들지 않는 constructors를 활용할 때 사용
- 이미 존재하는 인스턴스를 반환하거나, 단순한 초기값 부여가 아닌 연산이 필요한 객체 생성 시 사용
<br><br>
기본적으로 가장 많이 사용되는 **Default constructors와 Named constructors에 대해서만 우선 공부**

## Default Constructors
### 의미
- 생성자를 선언하지 않을 경우 제공되는 기본 constructors
- class를 호출할 때마다 기본으로 호출됨

## Named Constructors
### 의미
- 개발자가 필요에 의해 생성한 constructors

### 사용 목적
1. 추가적인 클래스의 명확성을 제공
2. 클래스에 대한 여러 constructors를 구현

**목표 1 : 추가적인 클래스의 명확성을 제공**
### 사용 방법
- method 이름을 class의 이름과 동일하게 작성

### 코드 예시
- class 호출 시, 입력한 argument를 사용해 값을 할당함
- 따라서 나중에 할당되는 변수를 의미하는 `late`를 사용
```dart
class Player {
    late final String name;
    late int xp;

    Player({
        required String name,
        required int xp,
    }) {
        // late를 사용하지 않으면 좌항에 error 발생
        this.name = name; 
        this.xp = xp;
    }
}

void main() {
    var player1 = Player(
        name: "horong",
        xp: 1500
    );
    var player2 = Player(
        name: "chop",
        xp: 3000
    );
}
```
- 위 코드에서 반복되고 불필요한 부분을 생략할 수 있음 (type, 변수 이름, late 등)
- contructor method의 인자를 바로 this.name, this.xp로 할당
```dart
class Player {
    // 아래 Player에서 바로 할당하기 때문에 late가 필요하지 않음
    final String name;
    int xp;

    Player({
        required this.name,
        required this.xp
    });
}
```
**목표 2 : 클래스에 대한 여러 constructors를 구현**
### 사용 방법
1. `Player.createPlater`과 같이 method를 정의
2. colons(:)를 사용해 기본 constructor의 parameters를 초기화

### 코드 예시
```dart
class Player {
    final String name;
    int xp, age;
    String team;

    Player({
        required this.name,
        required this.xp,
        required this.team,
        required this.age,
    });

    Player.createBluePlayer({
        required String name,
        required int age,
    // parameters로 받은 name, age를 사용해 property 초기화
    // this를 사용하는 이유 : argument의 변수명과 중복되기 때문
    // semicolons(;)가 아닌 comma(,)를 사용함
    }): this.age = age,
        this.name = name,
        this.team = "blue",
        this.xp = 0;

    // positional parameters로 작성해보기
    Player.createRedPlayer(String name, int age) : 
        this.age = age,
        this.name = name,
        this.team = "red",
        this.xp = 0;
}

void main() {
    // named parameters
    var player1 = Player.createBluePlayer(
        name: "horong",
        age : 20,
    );

    // positional parameters
    var player2 = Player.createBluePlayer("chop", 20);
}
```

## with APIs (in Flutter)
### 사용 방법
- API로 플레이어 정보를 받으면 **Flutter Dart class**로 바꿔줘야 함
- 일반적으로 `fromJson`이라는 named constructor을 생성해 사용

### 코드 예시
- 기본 constructor를 작성하지 않아도 named constructor을 생성할 수 있음
```dart
class Player {
    final String name;
    int xp;
    String team;

    // json object의 key에 해당하는 value로 property 초기환
    // this 사용하지 않는 이유 : 변수명이 중복되지 않음
    Player.fromJson(Map<String, dynamic> playerJson) :
        name = plyerJson["name"],
        xp = plyerJson["xp"],
        team = playerJson["team"];

    void sayHello() {
        print("Hello my name is $name");
    }
}

void main() {
    var apiData = [
        {
            "name" : "horong",
            "team" : "red",
            "xp" : 0,
        }, 
        {
            "name" : "chop",
            "team" : "blue",
            "xp" : 0,
        }, 
        {
            "name" : "kim",
            "team" : "red",
            "xp" : 0,
        }, 
    ];

    apiData.forEach((playerJson) {
        var player = Player.fromJson(playerJson);
        player.sayHello();
    })
    // Hello my name is horong
    // Hello my name is chop
    // Hello my name is kim
}
```

## Cascade Notation
### 의미
- 직전 class를 불러와서 사용하는 것

### 사용 방법
1. semicolons를 삭제
2. 직전 class 대신 cascade operater(.)을 사용

### 코드 예시
- 사용 전
```dart
class Player() {
    final String name;
    int xp;
    String team;

    Player({
        required name,
        required xp,
        required team,
    })

    void sayHello() {
        print("Hello my name is $name");
    }
}

void main() {
    var player = Player(name : "horong", xp: 1200, team: "red");
    player.name = "chop";
    player.xp = 2000;
    player.team = "blue";
}
```
- 사용 후
```dart
void main() {
    var player = Player(name : "horong", xp: 1200, team: "red")
    ..name = "chop"
    ..xp = 2000
    ..team = "blue";

    // 꼭 선언 직후가 아니더라도 다음과 같이 사용할 수 있음
    var chop = player
    ..xp = 3000
    ..sayHello();
}
```

## Enums
### 의미
- value의 선택지를 미리 지정하는 것
- 오타로 인한 실수를 줄일 수 있음 ex) `team : "bule"`

### 코드 예시
```dart
enum Team { red , blue } // red, blue로 지정
enum XPLevel { beginner, medium, pro } // beginner, medium, pro로 지정

class Player() {
    final String name;
    XPLevel xp;
    Team team;

    Player({
        required name,
        required xp,
        required team,
    })

    void sayHello() {
        print("Hello my name is $name");
    }
}

void main() {
    var player = Player(
        name : "horong",
        xp: XPLevel.medium,
        team: Team.red
        )
    ..name = "chop"
    ..xp = XPLevel.pro
    ..team = Team.blue
    ...sayHello();
}
```

## Abstract Classes
### 의미
- 다른 클래스가 직접 구현해야하는 method를 모아놓은 class
- 다른 클래스가 어떤 blueprint를 가지고 있어야하는지 정의, 강제함
- 객체를 생성하지 않음
- Flutter에서 많이 사용하지는 않지만 유용함

### 사용 방법
1. abstract class 안에 method 작성
2. 다른 클래스에 `extends`를 사용해 확장 후 해당 method 재작성

### 코드 예시
```dart
abstract class Human {
    void walk();
}

enum Team { red , blue }
enum XPLevel { beginner, medium, pro }

class Player() extends Human {
    final String name;
    XPLevel xp;
    Team team;

    Player({
        required name,
        required xp,
        required team,
    })

    void walk() {
        print("I'm walking")
    }

    void sayHello() {
        print("Hello my name is $name");
    }
}

void main() {
    var player = Player(
        name : "horong",
        xp: XPLevel.medium,
        team: Team.red
        )
    ..name = "chop"
    ..xp = XPLevel.pro
    ..team = Team.blue
    ...sayHello();
}
```

## Inheritance
### 의미
- Inheritance : 상속

### 사용 방법
- `extends` : 상속받을 부모 class를 지정하는 키워드
- `super` : 부모 class의 constructor method 및 property를 호출하는 키워드
    - `super`은 확장한 부모 class를 의미함
- `@override` :  부모 class의 method를 대체하는 키워드

### 코드 예시
```dart
class Human {
    final String name;
    Human({required this.name});
    void sayHello() {
        print("Hello my name is $name");
    }
}

enum Team { blue, red }

// Human의 모든 것을 Player에서 사용하는 경우 ()
// Human의 생성자 함수에 name이라는 변수를 넣어야 하기 때문에
// Human의 생성자 함수를 Player에서도 호출해야 함
class Player extends Human {
    final Team team;

    // named argument를 사용하는 Player의 생성자 함수
    Player({
        required this.team,
        required String name
        // name을 Human의 생성자 함수에 전달
    }) : super(name: name);

    // Human이 abstract class가 아니기 때문에 sayHello() method를 따로 작성해주지 않아도 문제 없음

    // Human으로부터 상속받은 sayHello()를 직접 만든 method로 대체
    @override
    void sayHello() {
        super.sayHello();
        print("and I play for $team")
    }
}

void main() {
    var player = Player(
        team: Team.red,
        name: "horong",
    )
    ..sayHello();
    // Hello my name is horong
    // and I play for red
}
```

## Mixins
### 의미
- 생성자가 없는 class
- class에 property를 추가할 때 사용
- 다른 class의 method와 property를 가져오는 개념 (상속 X)
- Dart에만 존재함

### 사용 방법
- `extends` : method, property를 가져올 Mixin class를 지정하는 키워드
    - Flutter나 Flutter 플러그인을 사용할 때 많이 사용
### 코드 예시
```dart
class Strong {
    final double strengthLevel = 1500.99;
}

class QuickRunner {
    void runQuick() {
        print("Ruuuun!");
    }
}

class Tall {
    final double height = 198.5;
}

enum Team { blue, red }

class Player with Strong, QuickRunner, Tall {
    final Team team;

    Player({
        required this.team,
    })
}

void main() {
    var player = Player(team: Team.blue)
    ..runQuick(); // Ruuuun!
}
```



