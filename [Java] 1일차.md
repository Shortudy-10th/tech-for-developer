# Java 1일차

<details>

<summary>❓ Java 소스 파일의 컴파일과 실행 과정에 대해 설명해주세요.</summary>

### ❓ Java 소스 파일의 컴파일과 실행 과정에 대해 설명해주세요.

<img src="https://github.com/seongeun42/cs-shortudy/assets/64778589/c0f4715d-1e34-4bdf-9ad7-7a57ea823d58" width="850"/>

1. 자바 컴파일러(Java Compiler)가 소스 파일(.java)을 컴파일해 바이트 코드 파일(.class)을 생성
2. 바이트 코드 파일을 JVM의 클래스 로더에게 전달
3. 클래스 로더는 동적 로딩을 통해 필요한 클래스들을 로딩 및 링크해 JVM의 메모리에 올림
4. 실행 엔진은 JVM 메모리에 올라온 바이트 코드를 명령어 단위로 하나씩 가져와 실행

</details>

<br>

---

<br>

<details>

<summary>❓ 클래스 로더의 세부 동작 방식에 대해 설명해주세요.</summary>

### ❓ 클래스 로더의 세부 동작 방식에 대해 설명해주세요.

<img src="https://github.com/seongeun42/cs-shortudy/assets/64778589/dfd07001-3e2f-43b1-99f7-581851feaf34" width="700"/>

- **Load**
    - 클래스 파일을 가져와 JVM의 메소드 영역에 로드
- **Link**
    - Verify : 자바 언어 명세 및 JVM 명세에 명시된 대로 구성되어 있는지 검증
    - Prepare : 클래스가 필요로 하는 메모리 할당(필드, 메소드, 인터페이스 등)
    - Resolve : 클래스 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레펀런스로 변경
- **Initalization**
    - 클래스 변수들을 적절한 값으로 초기화 함

</details>

<br>

---

<br>

<details>

<summary>❓ JVM의 메모리 구조에 대해 설명해주세요.</summary>

### ❓ JVM의 메모리 구조에 대해 설명해주세요.

<img src="https://github.com/seongeun42/cs-shortudy/assets/64778589/9fd0873f-6bc7-4a9f-8516-944977209976" width="700"/>

- **Method Area**
    - 모든 스레드가 공유함
    - 클래스의 멤버 변수의 이름, 데이터 타입, 접근 제어자 등의 각종 필드 정보와 메서드
    정보, 데이터 Type 정보, static 변수, final class, Runtime Constant Pool 등 프로그램
    실행할 때 필요한 데이터들이 저장되는 영역
    - Class Area나 Static Area로도 부름
- **Heap Area**
    - 모든 스레드가 공유함
    - new 키워드로 생성된 객체와 배열이 저장되는 영역
    - GC가 관리함
- **Stack Area**
    - 스레드 별로 생성됨
    - 함수 실행 시 지역 변수, 파라미터, 리턴 값 등 함수 내부에서 일시적으로 쓰이는 값들이
    저장되는 영역
    - 함수가 호출될 때마다 그 함수를 위한 스택 프레임이 쌓이고, 종료되면 삭제됨
- **PC Register**
    - 스레드 별로 생성
    - 스레드가 생성될 때마다 생기는 영역으로, 현재 수행 중인 JVM 명령어 주소를 저장함
    - JVM 명령어 주소는 스레드가 실행 중인 부분을 기록하고 있음
- **Native Method stack**
    - Java 이외의 언어 혹은 기계어로 작성된 네이티브 코드를 실행할 때 사용되는 메모리 영역

</details>

<br>

---

<br>

<details>

<summary>❓ Call By Value / Call By Reference에 대해 설명해주세요.</summary>

### ❓ Call By Value / Call By Reference에 대해 설명해주세요.

함수를 호출할 때 parameter로 값이 전달되는 방식의 차이를 말한다.

- **Call By Value**
    - parameter에 전달하는 인자 값을 복사해 새로운 data를 전달하는 방식
    - 값을 복사해 새로운 데이터를 만든 것이기 때문에 함수 내부에서 데이터를 변경하더라도 원본 값에는 영향을 주지 않음
- **Call By Reference**
    - parameter에 전달하는 인자 자체를 전달하는 방식
    - 주소 값을 넘김으로써 함수 내부에서 데이터를 변경하면 원본 값에도 영향을 미침

Java의 경우 Call By Value를 채택하고 있으며, 자료형에 따라 Call By Reference처럼 보일 수 있으나 실제로는 Call By Value로 동작한다.

</details>

<br>

---

<br>

<details>

<summary>❓ Java는 Call By Value로 동작함에도 불구하고 객체나 배열의 경우 함수 내부에서 변경 시 원본 값에도 영향을 줍니다. 이유가 무엇인가요?</summary>

### ❓ Java는 Call By Value로 동작함에도 불구하고 객체나 배열의 경우 함수 내부에서 변경 시 원본 값에도 영향을 줍니다. 이유가 무엇인가요?

객체나 배열의 경우 Reference Type인데, 참조 타입은 Heap Area에 생성된 객체의 주소 값을 참조하기 때문에 '참조 타입'이라고 불린다. 메모리에 저장된 값이 주소 참조 값이기 때문에 복사되어 파라미터로 넘겨주는 값 또한 같은 객체의 주소 참조 값이 된다. 동일한 주소 참조 값을 가지고 있으므로, 메소드 내에서 parameter를 이용해 상태를 수정하면 원본 값에도 영향을 주게 된다.

</details>

<br>

---

<br>

<details>

<summary>❓ 자바의 자료형에 대해 설명해주세요.</summary>

### ❓ 자바의 자료형에 대해 설명해주세요.

![type](https://github.com/seongeun42/cs-shortudy/assets/64778589/4969a549-3655-4317-a402-d4700b251af1)

크게 Primitive Type과 Reference Type으로 나뉜다. Primitive는 실제 값을 저장하고, Reference는 값이 저장된 메모리 주소를 가리키는 값을 저장한다. Primitive에는 boolean, char, byte, short, int, long, float, double 8가지가 있으며 범위가 작은 타입은 큰 타입으로 묵시적 형변환이 가능하다. 반대의 경우 명시적 형변환이 가능하며 값의 손실이 일어날 수 있다. Reference는 크게 객체형과 배열형으로 나눌 수 있는데, 객체형은 클래스를 인스턴스화한 것을 가리키고, 배열형은 같은 타입을 값을 연속적인 공간에 여러 개를 모아둔 자료구조를 가리킨다.

Primitive에는 boolean, char, byte, short, int, long, float, double 8가지가 있으며 범위가 작은 타입은 큰 타입으로 묵시적 형변환이 가능하다. 반대의 경우 명시적 형변환이 가능하나 값의 손실이 일어날 수 있다. 또한 Primitive를 Reference형으로 바꾸는 Wrapper 객체가 있는데, 이들 간에는 오토박싱과 오토언박싱이 일어날 수 있다.

Reference는 크게 객체형과 배열형으로 나뉘는데, 객체형은 클래스를 실제 값을 가지는 객체 인스턴스화 했을 때 힙 영역에 생기는 실제 값을 가리키는 주소 참조값을 가진다. 배열형은 배열이 실제로 생긴 메모리 주소의 참조값을 가진다. 객체형의 경우 상속 관계에 있다면 형변환이 가능하다.

</details>

<br>

---

<br>

<details>

<summary>❓ Primitive Type과 Reference Type의 자료들은 선언 및 정의할 때 어떤 차이가 있나요?</summary>

### ❓ Primitive Type과 Reference Type의 자료들은 선언 및 정의할 때 어떤 차이가 있나요?

선언의 가장 큰 차이점은 `new` 키워드 사용 여부이다.

- Primitive Type은 대입 연산자만을 사용해서 선언할 수 있다.
    - e.g. `int a = 10;`
- Reference Type은 `new` 키워드와 생성자를 사용해야 한다.
    - e.g. `StringBuilder builder = new StringBuilder();`
    - `null`로 초기화할 수도 있다.
        - e.g. `StringBuilder builder = null;`
    - 배열 역시 Reference Type이므로 new를 사용한다.
        - e.g. `int[] arr = new int[10];`
    - `String`은 예외적으로 대입 연산자로도 초기화할 수 있다.
        - e.g. `String str = "string"`

</details>

<br>

---

<br>

<details>

<summary>❓ JAVA의 접근 제어자에 대해 설명해주세요.</summary>

### ❓ JAVA의 접근 제어자에 대해 설명해주세요.

접근 제어자를 통해 변수나 메소드의 사용 권한을 설정할 수 있기 때문에 정보 은닉의 목적으로 사용한다.

| private | 같은 클래스 내에서만 사용 가능 |
| --- | --- |
| 생략(default) | private + 같은 패키지 내에서만 사용 가능 |
| protected | default + 두 클래스가 상속 관계일 때 패키지가 달라도 사용 가능 |
| public | 접근 제한 없이 모든 클래스에서 사용 가능 |

공개 범위: public > protected > default > private

</details>

<br>

---

<br>

<details>

<summary>❓ Java Collection에 대해서 설명해주세요.</summary>

### ❓ Java Collection에 대해서 설명해주세요.

<img src="https://github.com/seongeun42/cs-shortudy/assets/64778589/f3564424-2c6b-449a-80e4-5a13e7a5f96d" width="600"/>

<img src="https://github.com/seongeun42/cs-shortudy/assets/64778589/d71a39ec-5bf3-421a-8305-fcbd2c37b7f5" width="800"/>

Java Collection이란 데이터의 집합, 그룹을 의미하며 여러 자료구조를 구현해 놓은 클래스를 정의해둔 인터페이스를 포함하는 개념이다. 크게 List와 Set이 있는 Collection과 키와 값으로 이뤄진 HashMap을 가진 Map이 있다.

- **List**
    - 순서가 있는 데이터의 집합으로, 중복을 허용함
    - ArrayList, LinkedList, ...
- **Set**
    - 순서를 유지하지 않고 중복을 허용하지 않는 집합 개념의 자료구조
    - SortedSet, HashSet, TreeSet, ...
- **Map**
    - Key와 Value 쌍으로 이루어진 데이터의 집합으로, 순서는 유지되지 않고, 키의 중복은 허용되지 않으나 값의 중복은 허용
    - HashMap, TreeMap, ...

</details>

<br>

---

<br>

<details>

<summary>❓ Collection에서 사용되는 제네릭에 대해서 설명해주세요.</summary>

### ❓ Collection에서 사용되는 제네릭에 대해서 설명해주세요.

제네릭(Generic)은 자바에서 데이터 타입을 파라미터화하여 클래스나 메서드를 일반화하는 기능을 말한다. 타입에 대한 정의를 외부로 미룸으로써 타입에 대한 유연성을 확보할 수 있다. 또한 제네릭을 사용하면 컬렉션에 저장되는 요소들의 타입을 컴파일 시점에 체크할 수 있으므로, 타입 안정성을 보장할 수 있다. 이를 통해 런타임 시점에서 발생할 수 있는 타입 관련 예외를 컴파일 시점에 미리 방지할 수 있다.

</details>

<br>
