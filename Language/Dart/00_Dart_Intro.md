# Dart Intro

## Why Dart?
### 1. Compile
- Dart는 두 개의 컴파일러를 가짐
    -  Dart Web : Dart로 작성한 코드를 JavaScript로 변환
    - Dart Native : Dart로 작성한 코드를 여러 CPU의 아키텍처에 맞게 변환

- 컴파일 방식 : JIT, AOT
    - 개발중 피드백과 배포 시 성능을 고려해 두 가지 컴파일 방식을 모두 사용함
    1. 개발중일 떄 : JIT(just-in-time) (Dart VM 사용)
        - 내가 쓴 코드의 결과를 화면에 바로 보여줌 (디버깅에 좋음)
        - 가상 머신에서 실행됨
    2. 배포할 때 : AOT(ahead-of-time)
    -   앱이 빠르게 실행됨

### 2. Null Safety
- Java나 C++ 등 많은 언어가 문제를 가지고있음
- null을 참조했을 때 발생하는 문제를 방지해줌

### 3. Google, Dart, Flutter
- Dart를 최적화 하기 위해서 Flutter을 수정할 수 있다는 큰 장점이 있음
    - ex) 초기에는 AOT를 사용하지 않았으나 이후에 추가됨

## How To Learn
- 설치 없이 코드 작성하기
    - DartPad : https://dartpad.dev/
- VSCode 사용하기
    - Flutter, Dart 설치 후 사용
    - Flutter Extension 설치 추천 (DEBUG CONSOLE)
- Android Studio나 IntelliJ에서도 사용할 수 있음