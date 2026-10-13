# Unity / C# 개념 정리

## Unity 기본

Unity에서 스크립트를 `MonoBehaviour`로 만들면 자주 쓰는 기능들을 바로 사용할 수 있다.

```csharp
public class Creator : MonoBehaviour
{
}
```

`MonoBehaviour`를 상속하면 아래 요소들을 자주 사용하게 된다.

- `transform` : 자신의 위치, 회전, 크기 정보
- `gameObject` : 현재 스크립트가 붙어 있는 오브젝트
- `GetComponent<T>()` : 같은 오브젝트 안의 컴포넌트 가져오기

```csharp
public class Creator : MonoBehaviour
{
    void Start()
    {
        Transform tr = transform;
        GameObject obj = gameObject;
        Rigidbody2D rb = GetComponent<Rigidbody2D>();
    }
}
```
---
# C# 기초 용어 정리



---

## 1. 클래스(Class)

클래스는 **객체를 만들기 위한 설계도**다.  
클래스 안에는 데이터와 기능을 함께 넣을 수 있다.

```csharp
class Player
{
    public int hp;
    public string name;

    public void Attack()
    {
        Console.WriteLine("Attack!");
    }
}
```

위 코드에서 `Player`가 클래스다.  
이 클래스는 `hp`, `name`이라는 데이터를 가지고 있고, `Attack()`이라는 기능도 가진다.

---

## 2. 객체(Object)와 인스턴스(Instance)

객체와 인스턴스는 거의 같은 의미로 사용된다.  
보통은 **클래스를 실제로 만든 결과물**을 말한다.

```csharp
Player player1 = new Player();
```

여기서 `new Player()`로 만들어진 것이 객체이자 인스턴스다.  
`player1`은 그 인스턴스를 가리키는 변수다.

### 핵심
- 클래스: 틀
- 인스턴스: 그 틀로 만든 실제 대상
- 변수: 인스턴스를 가리키는 이름

---

## 3. 변수(Variable)

변수는 **값을 저장하거나 참조를 저장하는 이름**이다.

```csharp
int a = 10;
string text = "hello";
Player player = new Player();
```

여기서:
- `a`는 `10`이라는 값을 가진다.
- `text`는 문자열을 가리킨다.
- `player`는 `Player` 객체를 가리킨다.

변수는 타입에 따라 동작이 다르다.

---

## 4. 값 타입(Value Type)

값 타입은 **값 자체를 직접 저장하는 타입**이다.  
대표적으로 다음이 있다.

- `int`
- `float`
- `double`
- `bool`
- `char`
- `struct`

예:

```csharp
int num1 = 100;
int num2 = num1;
```

이 코드에서 `num2 = num1`은 **값 복사**다.  
즉 `num1`의 내용인 `100`이 그대로 `num2`에 복사된다.

```csharp
num2 = 200;

Console.WriteLine(num1); // 100
Console.WriteLine(num2); // 200
```

둘은 서로 독립적이다.

### 값 타입의 특징
- 변수 안에 값 자체가 들어간다.
- 대입하면 값이 복사된다.
- 하나를 바꿔도 다른 변수에는 영향이 없다.

---

## 5. 참조 타입(Reference Type)

참조 타입은 **객체 자체가 아니라 객체를 가리키는 참조를 저장**한다.  
대표적으로 다음이 있다.

- `string`
- `class`
- `array`

예:

```csharp
string str1 = "abc";
string str2 = str1;
```

이 경우 `str2`는 `str1`이 가리키던 참조를 그대로 복사한다.  
즉 두 변수는 같은 문자열 객체를 가리킬 수 있다.

```csharp
Console.WriteLine(Object.ReferenceEquals(str1, str2));
```

이런 비교가 가능한 이유는 `string`이 참조 타입이기 때문이다.

### 참조 타입의 특징
- 변수 안에 객체 자체가 들어가는 것이 아니라 참조가 들어간다.
- 대입하면 참조가 복사된다.
- 같은 객체를 여러 변수가 같이 가리킬 수 있다.

---

## 6. 레퍼런스(Reference)

레퍼런스는 **객체를 가리키는 정보**다.  
즉 “이 객체가 어디에 있는지”를 나타내는 개념이다.

```csharp
Player p1 = new Player();
Player p2 = p1;
```

여기서 `p1`과 `p2`는 서로 다른 변수가 아니라, **같은 객체를 가리키는 두 개의 이름**처럼 동작할 수 있다.

```csharp
p2.hp = 50;
Console.WriteLine(p1.hp); // 50
```

둘이 같은 객체를 보고 있기 때문이다.

---

## 7. 값 복사와 참조 복사

### 값 복사
값 자체가 복사된다.

```csharp
int a = 5;
int b = a;
```

### 참조 복사
객체를 가리키는 정보가 복사된다.

```csharp
Player a = new Player();
Player b = a;
```

### 차이점
값 복사는 완전히 독립적이지만, 참조 복사는 같은 객체를 공유할 수 있다.

---

## 8. 필드(Field)

필드는 클래스 안에 선언된 **직접적인 변수**다.

```csharp
class Player
{
    public int hp;
    public string name;
}
```

여기서 `hp`, `name`이 필드다.

### 특징
- 클래스 내부 데이터 저장용
- 보통 외부에서 직접 접근하지 않도록 설계하는 경우가 많음
- 객체의 상태를 표현할 때 사용

---

## 9. 프로퍼티(Property)

프로퍼티는 **필드처럼 보이지만, 값을 읽고 쓰는 방법을 제어하는 기능**이다.

```csharp
class Player
{
    public int Hp { get; set; }
}
```

이 코드는 겉보기엔 변수처럼 보이지만, 실제로는 `get`과 `set`을 통해 값을 처리한다.

### 자동 구현 프로퍼티
```csharp
public int Hp { get; set; }
```

이 형태는 C#이 알아서 내부 필드를 만든 것처럼 처리해준다.

### 직접 제어하는 프로퍼티
```csharp
private int hp;

public int Hp
{
    get { return hp; }
    set
    {
        if (value < 0)
            hp = 0;
        else
            hp = value;
    }
}
```

여기서는 값을 넣을 때 조건을 추가할 수 있다.

### 특징
- 외부에서는 변수처럼 보임
- 내부적으로는 함수처럼 동작할 수 있음
- 검증, 제한, 계산 등을 넣기 좋음

---

## 10. 메서드(Method)

메서드는 **동작을 실행하는 함수**다.

```csharp
class Player
{
    public void Attack()
    {
        Console.WriteLine("Attack!");
    }
}
```

호출할 때는 괄호 `()`를 사용한다.

```csharp
player.Attack();
```

### 특징
- 어떤 행동을 수행함
- 결과를 반환할 수도 있고, 안 할 수도 있음
- 괄호가 붙는다

```csharp
public int GetHp()
{
    return hp;
}
```

이것도 메서드다.

---

## 11. 생성자(Constructor)

생성자는 **객체가 만들어질 때 자동으로 실행되는 특별한 메서드**다.

```csharp
class Player
{
    public int hp;

    public Player()
    {
        hp = 100;
    }
}
```

### 특징
- 클래스 이름과 같다
- 반환형이 없다
- `new`로 객체를 만들 때 자동 실행된다

```csharp
Player p = new Player();
```

위 코드에서 `Player()` 생성자가 실행된다.

---

## 12. 문자열(String)

`string`은 참조 타입이다.  
하지만 **불변(immutable)** 이기 때문에 내용 자체를 수정할 수 없다.

```csharp
string s1 = "abc";
string s2 = s1;
```

여기서 `s2`는 `s1`의 참조를 복사한 것이다.

```csharp
s2 = "def";
```

이 코드는 기존 문자열 `"abc"`를 수정하는 것이 아니라, `s2`가 다른 문자열 `"def"`를 가리키게 하는 것이다.

### 중요
- `string`은 참조 타입
- 내용은 바꿀 수 없음
- 대입하면 참조가 복사됨

---

## 13. `ReferenceEquals`

`ReferenceEquals`는 **두 변수가 같은 객체를 가리키는지** 확인한다.

```csharp
string a = "hello";
string b = a;

Console.WriteLine(Object.ReferenceEquals(a, b));
```

이 경우 `true`가 나올 수 있다.

하지만 값 타입에는 보통 쓰지 않는다.

```csharp
int x = 10;
int y = x;
Console.WriteLine(Object.ReferenceEquals(x, y));
```

이 경우는 박싱(Boxing) 때문에 헷갈릴 수 있고, 값 비교 용도로는 적절하지 않다.

---

## 14. 박싱(Boxing)

박싱은 **값 타입을 object 타입으로 감싸는 과정**이다.

```csharp
int num = 10;
object obj = num;
```

여기서 `num`은 `object`로 바뀌면서 박싱된다.

### 왜 중요한가
`ReferenceEquals(num1, num2)`처럼 값 타입을 참조 비교에 넣으면, 내부적으로 박싱이 일어나서 별도 객체가 만들어질 수 있다.

---

## 15. 언박싱(Unboxing)

박싱된 값을 다시 원래 값 타입으로 꺼내는 과정이다.

```csharp
object obj = 10;
int num = (int)obj;
```

---

## 16. 메서드와 프로퍼티 구분법

### 메서드
- 동작을 한다
- 괄호 `()`가 있다

```csharp
str.Split(',');
str.Trim();
str.Replace(" ", "");
```

### 프로퍼티
- 상태나 값을 읽는다
- 괄호가 없다

```csharp
str.Length
array.Length
```

---


## 생명주기 함수

Unity는 특정 시점에 자동으로 호출되는 함수들이 있다.

### Awake()

오브젝트가 생성될 때 가장 먼저 실행된다.  
자기 자신 컴포넌트 초기화에 자주 사용한다.

```csharp
void Awake()
{
    rb = GetComponent<Rigidbody2D>();
}
```

### Start()

`Awake()`가 모두 끝난 뒤 실행된다.  
게임 시작 시 1번만 실행된다.

```csharp
void Start()
{
    speed = 5.0f;
}
```

### Update()

게임이 실행되는 동안 매 프레임 실행된다.  
입력 처리, 상태 체크 같은 실시간 로직에 자주 사용한다.

```csharp
void Update()
{
    if (Input.GetKeyDown(KeyCode.Space))
    {
        Debug.Log("점프");
    }
}
```

### FixedUpdate()

일정한 시간 간격으로 실행된다.  
물리 연산과 `Rigidbody` 관련 처리는 여기서 하는 것이 적합하다.

```csharp
void FixedUpdate()
{
    rigidbody2D.MovePosition(nextPos);
}
```

실행 흐름은 보통 아래처럼 이해하면 된다.

```text
Awake() -> Start() -> Update() -> Update() -> ...
```

---

### 초기화의 의미

초기화 = 처음 값을 정해주는 것

예:
```csharp
int a = 10;
```

- 변수 `a`를 만들고
- 처음 값으로 `10`을 넣은 것

---

## 오브젝트와 컴포넌트 찾기

Unity에서는 오브젝트나 컴포넌트를 찾아서 사용하는 일이 많다.

### 현재 오브젝트 기준

```csharp
transform
gameObject
GetComponent<BoxCollider2D>()
```

### 부모 / 자식 접근

```csharp
transform.parent
transform.GetChild(0)
```

### 이름으로 오브젝트 찾기

```csharp
GameObject.Find("Player")
```

`Find()`는 편하지만 자주 호출하면 비효율적일 수 있어서 보통 `Start()`에서 한 번만 저장해두는 경우가 많다.

---

## transform

`transform`은 오브젝트의 위치, 회전, 크기를 다루는 가장 기본적인 요소다.

### 위치 이동

`transform.Translate()`는 현재 위치를 기준으로 상대 이동한다.

```csharp
transform.Translate(-1.0f, 0.0f, 0.0f);
```

위 코드는 왼쪽으로 1만큼 이동한다.

### 프레임 보정 이동

컴퓨터 성능에 따라 프레임 수가 달라질 수 있어서 `Time.deltaTime`을 곱해서 속도를 일정하게 맞춘다.

```csharp
transform.Translate(-moveSpeed * Time.deltaTime, 0.0f, 0.0f);
```

---

## void와 반환형

메서드는 반환형을 가진다.

### void

`void`는 반환값이 없다는 뜻이다.

```csharp
void Start()
{
    Debug.Log("실행");
}
```

### 다른 반환형 예시

```csharp
int GetHP()
{
    return 10;
}

bool IsAlive()
{
    return true;
}
```

- `int` : 정수 반환
- `bool` : 참/거짓 반환
- `void` : 반환값 없음

---

## if 문

`if` 문은 조건이 참일 때 코드를 실행한다.

```csharp
if (조건식)
{
    // 실행
}
else if (다른조건식)
{
    // 실행
}
else
{
    // 위 조건이 모두 거짓일 때 실행
}
```

### 예시

```csharp
int score = 85;

if (score >= 90)
{
    Console.WriteLine("A");
}
else if (score >= 80)
{
    Console.WriteLine("B");
}
else if (score >= 70)
{
    Console.WriteLine("C");
}
else
{
    Console.WriteLine("F");
}
```

위에서부터 순서대로 검사하고, 처음 참이 되는 블록만 실행된다.

---

## switch 문

`switch` 문은 하나의 값을 여러 경우와 비교할 때 사용한다.

```csharp
switch (변수)
{
    case 값1:
        // 실행
        break;
    case 값2:
        // 실행
        break;
    default:
        // 모든 case에 해당하지 않을 때
        break;
}
```

### 예시

```csharp
string calc = "+";

switch (calc)
{
    case "+":
        Console.WriteLine("더하기");
        break;
    case "-":
        Console.WriteLine("빼기");
        break;
    case "*":
        Console.WriteLine("곱하기");
        break;
    default:
        Console.WriteLine("연산자 오류");
        break;
}
```

`case`에는 고정된 값이 들어가고, 각 case는 보통 `break`로 끝낸다.

---

## for 문

`for` 문은 반복 횟수가 비교적 분명할 때 많이 쓴다.

```csharp
for (초기식; 조건식; 증감식)
{
    // 반복할 코드
}
```

### 기본 예시

```csharp
for (int i = 1; i <= 5; i++)
{
    Console.WriteLine(i);
}
```

### 초기식 생략

```csharp
int i = 0;

for (; i < 5; i++)
{
    Console.WriteLine(i);
}
```

초기식, 조건식, 증감식은 일부 생략 가능하다.

---

## while 문

`while` 문은 조건이 참인 동안 계속 반복한다.

```csharp
while (조건식)
{
    // 반복할 코드
}
```

### 예시

```csharp
int count = 0;

while (count < 5)
{
    Console.WriteLine("count: " + count);
    count++;
}
```

조건을 먼저 검사하기 때문에 처음부터 거짓이면 한 번도 실행되지 않는다.

---

## 중첩 while

`while` 안에 또 다른 `while`을 넣을 수도 있다.

```csharp
while (바깥조건)
{
    while (안쪽조건)
    {
        // 반복 실행
    }
}
```

이 구조는 2중 반복이 필요할 때 사용한다.

---

## do-while 문

`do-while`은 먼저 실행하고 나중에 조건을 검사한다.

```csharp
do
{
    // 실행할 코드
}
while (조건식);
```

### 예시

```csharp
int count = 0;

do
{
    Console.WriteLine("count: " + count);
    count++;
}
while (count < 5);
```

조건과 상관없이 최소 1번은 실행된다.

---

## Instantiate

`Instantiate()`는 프리팹이나 오브젝트를 복제 생성하는 메서드다.

### 기본 형태

```csharp
Instantiate(prefab);
```

### 부모 지정

```csharp
Instantiate(prefab, parentTransform);
```

### 위치와 회전 지정

```csharp
Instantiate(prefab, spawnPos, Quaternion.identity);
```

### 반환값 받기

```csharp
GameObject obj = Instantiate(prefab, spawnPos, Quaternion.identity);
```

주로 적, 아이템, 총알, 이펙트 생성에 사용한다.

---

## Destroy

`Destroy()`는 오브젝트를 제거하는 메서드다.

### 즉시 제거 예약

```csharp
Destroy(gameObject);
```

### 일정 시간 뒤 제거

```csharp
Destroy(gameObject, 3f);
```

### 충돌한 상대 제거 예시

```csharp
private void OnTriggerEnter2D(Collider2D collision)
{
    if (collision.gameObject.CompareTag("Rain"))
    {
        Destroy(collision.gameObject);
    }
}
```

---

## Invoke

`Invoke()`는 함수를 일정 시간 뒤 한 번 실행한다.

```csharp
Invoke("SpawnEnemy", 3f);
```

위 코드는 3초 뒤 `SpawnEnemy()`를 1번 실행한다.

```csharp
void Start()
{
    Invoke("SpawnEnemy", 3f);
}

void SpawnEnemy()
{
    Debug.Log("적 생성");
}
```

---

## InvokeRepeating

`InvokeRepeating()`은 함수를 일정 간격으로 반복 실행한다.

```csharp
InvokeRepeating("SpawnRain", 0f, 1f);
```

- 첫 번째 값 : 함수 이름
- 두 번째 값 : 처음 시작 전 대기 시간
- 세 번째 값 : 반복 간격

```csharp
void Start()
{
    InvokeRepeating("SpawnRain", 0f, 1f);
}
```

반복 호출은 `CancelInvoke("SpawnRain")`으로 멈출 수 있다.

---

## 충돌 감지

Unity 2D에서 자주 쓰는 충돌 함수는 아래와 같다.

```csharp
void OnCollisionEnter2D(Collision2D col) { }
void OnCollisionExit2D(Collision2D col) { }
void OnTriggerEnter2D(Collider2D col) { }
void OnTriggerExit2D(Collider2D col) { }
```

### Collision

실제로 서로 막히는 물리 충돌이다.

### Trigger

서로 겹치지만 통과할 수 있고, 감지만 한다.

Trigger를 사용하려면 Collider의 `Is Trigger`를 체크해야 한다.

또한 충돌이 감지되려면 보통 둘 중 하나 이상에 `Rigidbody`가 필요하다.

---

## Rigidbody와 물리 이동

`Rigidbody2D`가 붙은 오브젝트는 물리 엔진 기준으로 움직이는 것이 더 안정적이다.

### 물리 오브젝트에 transform 이동을 바로 쓰는 경우

```csharp
transform.Translate(moveSpeed * Time.deltaTime, 0, 0);
```

이 방식은 충돌이나 물리 처리와 어긋날 수 있다.

### Rigidbody 방식

```csharp
rigidbody2D.MovePosition(next);
```

물리 오브젝트는 `FixedUpdate()` 안에서 `Rigidbody` 관련 메서드로 움직이는 방식이 일반적이다.

```csharp
void FixedUpdate()
{
    rigidbody2D.MovePosition(next);
}
```

---

## Update와 FixedUpdate 차이

### Update()

- 매 프레임 실행
- 입력 처리에 적합

### FixedUpdate()

- 일정 시간 간격으로 실행
- 물리 처리에 적합

보통은 아래처럼 나눠 쓴다.

```csharp
void Update()
{
    // 입력 받기
}

void FixedUpdate()
{
    // 물리 이동 처리
}
```

---

## 배열(Array)

같은 자료형의 값을 여러 개 저장할 수 있는 변수 묶음  
인덱스(index)는 0부터 시작함

예:
```csharp
int[] arrays = new int;
```

- `int[]` : int형 배열
- `arrays` : 배열 이름
- `new int[10]` : int 10개를 저장할 수 있는 배열 생성
- 인덱스 범위 : `[0] ~ [9]`

### 배열 기본값

배열을 만들기만 하고 값을 따로 넣지 않으면 기본값으로 초기화됨

```csharp
int[] arrays = new int;
```

위 코드는 실제로 아래처럼 들어 있다고 생각하면 됨

```csharp
int[] arrays = new int;
```

- `int` 배열 기본값 : `0`
- `float` 배열 기본값 : `0`
- `bool` 배열 기본값 : `false`
- `string` 배열 기본값 : `null`





---

## 배열 출력

배열은 보통 `for`문으로 순회하면서 출력함

```csharp
int[] arrays = new int;

for (int i = 0; i < arrays.Length; i++)
{
    Console.Write($"{i}:{arrays[i]} ");
}
```

### 해석

- `i = 0` 부터 시작
- `arrays.Length` 전까지 반복
- `arrays[i]` : i번째 배열 요소
- `$"{i}:{arrays[i]}"` : 인덱스와 값을 같이 출력

### `Length`

배열의 길이(칸 수)를 알려주는 프로퍼티

```csharp
arrays.Length
```

- 배열이 10칸이면 `Length`는 10
- 보통 `for`문 조건에서 많이 씀
- 직접 숫자 `10`을 쓰는 것보다 안전함

예:
```csharp
for (int i = 0; i < arrays.Length; i++)
```

---

## 배열 선언 방법

### 1. 선언과 동시에 초기화

```csharp
int[] array1 = { 0, 1, 2, 4 };
```

가장 간단한 방식  
배열을 만들면서 바로 값까지 넣음

### 2. new를 명시해서 초기화

```csharp
int[] array2 = new int[] { 0, 1, 2, 4 };
```

의미는 위와 같음  
조금 더 풀어서 쓴 형태

### 3. 선언 후 나중에 초기화

```csharp
int[] array3;
array3 = new int[] { 0, 1, 2, 4 };
```

처음엔 선언만 하고  
나중에 실제 배열을 만들어 대입하는 방식

### 주의

```csharp
int[] array3;
array3 = { 0, 1, 2, 4 }; // 에러
```

이렇게는 안 됨  
중괄호 초기화는 선언과 동시에 쓸 때만 가능  
선언 후 대입할 때는 반드시 `new int[]`를 붙여야 함

---

## 배열 인덱스

배열은 0번부터 시작함

```csharp
int[] arr = { 10, 20, 30 };
```

- `arr[0]` : 10
- `arr[1]` : 20
- `arr[2]` : 30

즉, `arr[i]`는 배열의 i번째 값을 뜻함

---

## 배열 복사

### Clone()

배열을 똑같이 복사한 새 배열을 만들 때 사용

```csharp
int[] numbers = { 50, 36, 99, 87 };
int[] copyNumbers = (int[])numbers.Clone();
```

- `numbers.Clone()` : numbers 배열을 복사
- 반환형이 `object`라서 `(int[])` 캐스팅 필요

복사 후에는 `copyNumbers`가 별도의 배열이 됨

---

## 배열에서 지원되는 유틸 메서드

유틸(utility) = 자주 쓰는 작업을 편하게 해주는 도구 기능

즉, 유틸 메서드는  
직접 복잡하게 구현하지 않아도 되게 도와주는 편의 함수라고 생각하면 됨

---

## Array.Sort()

배열을 오름차순으로 정렬

```csharp
int[] numbers = { 50, 36, 99, 87 };
Array.Sort(numbers);
```

정렬 후:
```csharp
[0]:36 , [1]:50 , [2]:87 , [3]:99
```

- 작은 값부터 큰 값 순서로 정렬
- 원본 배열 자체가 바뀜

---

## CopyTo()

배열 내용을 다른 배열로 복사

```csharp
int[] numbers      = { 36, 50, 87, 99 };
int[] copyNumbers3 = new int[7];

numbers.CopyTo(copyNumbers3, 3);
```

### 해석

- `numbers`의 내용을
- `copyNumbers3` 배열의 `3`번 인덱스부터 복사

복사 후 예시:
```csharp
// copyNumbers3 내용:
// [0] 0
// [1] 0
// [2] 0
// [3] 36
// [4] 50
// [5] 87
// [6] 99
```

형식:
```csharp
원본배열.CopyTo(대상배열, 시작인덱스);
```

---

## Array.Clear()

배열의 특정 구간을 기본값으로 초기화

```csharp
Array.Clear(numbers, 0, numbers.Length);
```

### 해석

- `numbers` 배열의
- `0`번 인덱스부터
- `numbers.Length` 개수만큼
- 기본값으로 초기화

`int` 배열이면 결과적으로 전부 `0`이 됨

예:
```csharp
int[] numbers = { 36, 50, 87, 99 };   // 초기 상태

Array.Clear(numbers, 0, numbers.Length);
```

초기화 후:
```csharp
numbers = [0, 0, 0, 0];
```

형식:
```csharp
Array.Clear(배열, 시작인덱스, 개수);
```

---

## 배열 관련 자주 쓰는 표현 정리

- `arr.Length` : 배열 길이
- `arr[i]` : i번째 요소
- `Array.Sort(arr)` : 배열 정렬
- `arr.CopyTo(dest, index)` : 다른 배열에 복사
- `Array.Clear(arr, index, count)` : 배열 값 초기화
- `arr.Clone()` : 배열 복사본 생성

---
## Partial

`partial`은 **하나의 클래스를 여러 파일로 나눠서 작성할 수 있게 해주는 문법**이다.  
컴파일할 때는 여러 파일에 **나눠진 조각들이 전부 합쳐져서 하나의 클래스가 된다**.

### 쓸 때 규칙

1. 모든 써야하는 클래스 코드에 **`partial`키워드가 있어야함**
```csharp
public partial class Player // O
public class Player         // 다른 파일에 이렇게 쓰면 에러
```
2. 클래스 **이름이 완전히 같아야 함** (이름이 다르면 서로 다른 클래스로 인식이 돼서 합쳐지지 않는다.)
```csharp
public partial class Player  // 파일 A
public partial class Player  // 파일 B
```
3. **같은 네임스페이스, 같은 어셈블리(프로젝트) 안에 있어야 함**
    - 유니티 기준 서로 다른 어셈블리로 나뉜 프로젝트 끼리는 `partial`로 하나로 합칠 수 없다.
4. **접근 제한자**가 같아야 함
```csharp
public partial class Player  // 파일 A
internal partial class Player // 파일 B → 에러
```
5. 상속은 **한 곳에서만 명시해도 전체에 적용**됨
```csharp
public partial class Player : Character // 상속은 한 번만 써도 됨
{
}

public partial class Player // 여기선 다시 안 써도 Character 상속 유지
{
}
```

partial 예시
```csharp
public partial class Player : Character
{
    protected override void Awake()
    {
        base.Awake();
        AwakeBindInput();
    }
}
```
```csharp
public partial class Player
{
    private void AwakeBindInput()
    {
        // 입력 연결 코드
    }
}
```
- 두 클래스가 `partial`키워드로 선언 돼서 컴파일 후 하나의 완성된 `Player`클래스가 된다.

---

## Coroutine

코루틴(Coroutine)은  
함수를 한 번에 끝까지 실행하지 않고,  
중간에 잠깐 멈췄다가 다음 프레임이나 일정 시간이 지난 뒤 다시 이어서 실행할 수 있는 기능

일반 함수는 호출되면 한 번에 끝까지 실행됨  
코루틴은 `yield return`을 만나면 실행을 잠깐 멈추고,  
조건이 만족되면 다시 이어서 실행함

즉, 여러 프레임에 걸쳐 순서대로 처리해야 하는 로직에 자주 사용함

---

## Coroutine 특징

- 반환형이 `IEnumerator`
- 함수 안에 `yield return` 구문이 들어감
- `StartCoroutine()`으로 실행
- `yield return`을 기준으로 실행이 잠깐 멈춤
- 다시 조건이 만족되면 다음 부분부터 이어서 실행
- 멀티스레드가 아니라, 프레임 단위로 나눠 실행하는 흐름 제어 방식

---

## 기본 형식

```csharp
IEnumerator Co_Example()
{
    Debug.Log("시작");

    yield return new WaitForSeconds(1f);

    Debug.Log("1초 후 실행");
}
```

### 해석

- 코루틴 함수 이름은 `Co_Example`
- 실행되다가 `yield return new WaitForSeconds(1f);` 에서 멈춤
- 1초가 지나면 그 다음 줄부터 다시 실행

---

## 실행 방법

코루틴은 일반 함수처럼 그냥 호출하는 것이 아니라  
`StartCoroutine()`으로 실행함

```csharp
StartCoroutine(Co_Example());
```

### 해석

- `Co_Example()` 코루틴 시작
- 실행되다가 첫 번째 `yield return`에서 멈춤
- 이후 Unity가 다시 이어서 실행해 줌

---

## IEnumerator

코루틴 함수의 반환형

```csharp
IEnumerator Co_Example()
{
    yield return null;
}
```

### 의미

- 코루틴은 반드시 `IEnumerator` 반환형을 사용
- 일반 `void` 함수와 다르게 중간에 멈췄다가 다시 실행 가능
- `yield return`과 함께 사용됨

---

## yield return

코루틴 실행을 잠깐 멈추는 구문

```csharp
yield return null;
```

### 의미

- 현재 프레임에서 실행을 멈춤
- 다음 프레임에 다시 이어서 실행

코루틴에서 가장 중요한 문법이라고 보면 됨

---

## yield return null

다음 프레임까지 기다렸다가 다시 실행

```csharp
IEnumerator Co_Move()
{
    while (true)
    {
        transform.Translate(1f * Time.deltaTime, 0, 0);
        yield return null;
    }
}
```

### 해석

- 한 프레임 이동
- `yield return null`에서 멈춤
- 다음 프레임에 다시 실행
- 반복하면 매 프레임 조금씩 이동

`yield return null`이 없으면 반복문이 한 프레임 안에서 전부 돌아버려서  
오브젝트가 순간이동하듯 처리될 수 있음

---

## WaitForSeconds()

지정한 초만큼 기다렸다가 다시 실행

```csharp
yield return new WaitForSeconds(2f);
```

### 의미

- 2초 대기 후 다음 코드 실행
- 게임 시간 기준으로 대기
- `Time.timeScale` 영향을 받음

예:
```csharp
IEnumerator Co_Wait()
{
    Debug.Log("시작");
    yield return new WaitForSeconds(2f);
    Debug.Log("2초 후");
}
```

---

## WaitForSecondsRealtime()

실제 시간 기준으로 기다렸다가 다시 실행

```csharp
yield return new WaitForSecondsRealtime(2f);
```

### 의미

- 실제 시간 2초 대기
- `Time.timeScale` 영향을 받지 않음
- 일시정지 중에도 흐르는 시간을 기준으로 처리할 때 사용

예:
```csharp
IEnumerator Co_RealTimeWait()
{
    yield return new WaitForSecondsRealtime(2f);
}
```

---

## StartCoroutine()

코루틴 실행 함수

```csharp
StartCoroutine(Co_Example());
```

### 특징

- `MonoBehaviour`에서 사용
- 코루틴 실행 시작
- 첫 번째 `yield return` 전까지는 바로 실행됨
- 이후 `yield` 조건에 따라 다시 이어서 실행됨

코루틴은 여러 개를 동시에 실행할 수도 있음

---

## StopCoroutine()

특정 코루틴 하나를 멈출 때 사용

```csharp
Coroutine co;

void Start()
{
    co = StartCoroutine(Co_Example());
}

void StopIt()
{
    StopCoroutine(co);
}
```

### 의미

- 실행 중인 특정 코루틴 정지
- 보통 `Coroutine` 변수에 저장해 두고 멈춤
- 문자열, `IEnumerator`, `Coroutine` 방식으로 중지 가능

---

## StopAllCoroutines()

현재 스크립트에서 실행 중인 모든 코루틴 정지

```csharp
StopAllCoroutines();
```

### 의미

- 해당 `MonoBehaviour`에서 돌고 있는 코루틴 전체 정지
- 게임 오버, 씬 전환, 상태 초기화할 때 자주 사용

---

## Coroutine 객체

`StartCoroutine()`의 반환값

```csharp
Coroutine co = StartCoroutine(Co_Example());
```

### 의미

- 실행 중인 코루틴을 가리키는 참조값
- 나중에 `StopCoroutine(co)`로 멈출 때 사용

---

## 코루틴과 일반 함수 차이
### 일반 함수

```csharp
void Test()
{
    Debug.Log("A");
    Debug.Log("B");
    Debug.Log("C");
}
```

- 호출하면 한 번에 A, B, C가 모두 실행됨

### 코루틴

```csharp
IEnumerator Co_Test()
{
    Debug.Log("A");
    yield return new WaitForSeconds(1f);
    Debug.Log("B");
    yield return new WaitForSeconds(1f);
    Debug.Log("C");
}
```

- A 실행
- 1초 대기
- B 실행
- 1초 대기
- C 실행

즉, 시간 순서대로 나눠서 실행 가능

---

## Coroutine이 자주 쓰이는 상황

### 1. 시간차 실행

몇 초 뒤 어떤 동작을 실행할 때

```csharp
IEnumerator Co_Spawn()
{
    yield return new WaitForSeconds(3f);
    SpawnEnemy();
}
```

### 2. 반복 실행

일정 시간마다 반복 동작할 때

```csharp
IEnumerator Co_Repeat()
{
    while (true)
    {
        SpawnEnemy();
        yield return new WaitForSeconds(1f);
    }
}
```

### 3. UI 게이지 / 쿨타임 처리

대쉬 쿨타임, 스킬 쿨타임 UI처럼  
시간이 지나면서 게이지를 채우는 처리에 사용

```csharp
IEnumerator Co_Cooldown()
{
    float current = 0f;

    while (current < 3f)
    {
        current += Time.deltaTime;
        yield return null;
    }
}
```

### 4. 순차 연출

텍스트 출력 → 대기 → 효과음 → 대기 → 씬 전환  
이런 순서형 연출에 자주 사용

---

## Coroutine과 Update 차이

### Update

- 매 프레임 실행
- 입력 처리, 실시간 검사에 적합

### Coroutine

- 특정 시간 대기
- 순차 처리
- 일정 간격 반복
- 여러 프레임에 나눠서 처리하는 로직에 적합

즉,  
매 프레임 계속 확인해야 하는 건 `Update()`  
중간에 기다리거나 순서대로 실행해야 하는 건 `Coroutine`이 더 잘 맞음

---



## 자주 같이 쓰는 시간 관련 요소

### Time.deltaTime

이전 프레임과 현재 프레임 사이의 시간  
코루틴 안에서도 자주 사용

```csharp
current += Time.deltaTime;
```

### Time.timeScale

게임 시간 속도  
`WaitForSeconds()`는 이 값의 영향을 받음

- `timeScale = 1` : 정상 속도
- `timeScale = 0` : 멈춤

### WaitForSecondsRealtime

`timeScale` 영향을 받지 않는 실제 시간 대기

---

## 형식 정리

### 기본 코루틴 선언

```csharp
IEnumerator Co_Name()
{
    yield return null;
}
```

### 실행

```csharp
StartCoroutine(Co_Name());
```

### 특정 코루틴 정지

```csharp
StopCoroutine(co);
```

### 모든 코루틴 정지

```csharp
StopAllCoroutines();
```
---

## 람다, 델리게이트, 캡처, 클로저

### 1. 델리게이트에 메서드 넣기

```csharp
Action<int, string> action;
action = Test;
action.Invoke(1, "Hello");
action(1, "Hello");
```

- `Action<int, string>`은 `int`, `string`을 인자로 받고 반환값은 없는 함수 타입이다.
- `action = Test;`는 `Test(int a, string b)` 메서드를 델리게이트 변수에 넣은 것이다.
- `action.Invoke(1, "Hello")`와 `action(1, "Hello")`는 같은 호출이다.

---

### 2. 메서드 대신 람다 넣기

```csharp
action = (a, b) => print($"Lambda : {a}, {b}");
action(2, "World");
```

- `(a, b) => ...`는 이름 없는 함수를 만드는 람다식이다.
- 델리게이트 변수에 기존 메서드 대신 람다를 다시 대입할 수 있다.
- `action(2, "World")`를 호출하면 람다가 실행된다.

---

### 3. 인자 없는 람다와 인자 있는 람다

```csharp
Action action1 = () => print("Hello Lambda");
action1();

Action<int> action2 = (a) => print($"Lambda : {a}");
action2(3);
```

- `action1`은 인자 0개, 반환값 없음.
- `action2`는 `int` 인자 1개, 반환값 없음.
- 인자가 1개일 때는 `a => ...`처럼 괄호를 생략할 수 있다.

---

### 4. Func와 반환값 있는 람다

```csharp
Func<int> lambda2 = () => 5 * 5;
print($"lambda2 : {lambda2()}");

Func<int, int> lambda3 = (x) => x * x;
print($"lambda3 : {lambda3(5)}");

Func<int, int> lambda4 = (int x) => x * outer;
print($"lambda4 : {lambda4(5)}");
```

- `Func<int>`는 인자 없이 `int`를 반환하는 함수 타입이다.
- `Func<int, int>`는 `int` 하나를 입력받아 `int`를 반환하는 함수 타입이다.
- `Func`에서 마지막 제네릭 타입은 반환 타입, 앞의 타입들은 입력 타입이다.
- `lambda4`는 바깥 변수 `outer`를 함께 사용한다(캡처).

---

### 5. 내부 함수와 델리게이트

```csharp
int Square(int x)
{
    return x * x;
}

Func<int, int> square = Square;
int result = square(4);
print($"Square : {result}");
```

- `Square`는 `Start()` 안에 정의한 지역 함수다.
- `Func<int, int>`에 `Square`를 넣으면 함수도 변수처럼 다룰 수 있다.
- `square(4)`는 `Square(4)`와 같은 결과를 낸다.

---

### 6. 캡처와 클로저

```csharp
int outer = 15;

int Add(int x)
{
    return x + outer;
}

Func<int, int> add = Add;
print($"add = {add(5)}");

Func<int, int> add2 = Add;
print($"add = {add2(15)}");
```

- `outer`는 바깥에 있는 지역 변수다.
- `Add`가 `outer`를 사용하면 외부 변수를 캡처한 것이다.
- 함수가 외부 변수까지 같이 기억하고 사용하는 상태를 클로저라고 부른다.
- `add(5)`는 `20`, `add2(15)`는 `30`을 출력한다.

---

### 7. for문에서 캡처할 때 주의할 점

```csharp
List<Action> actions = new List<Action>();

for (int i = 0; i < 3; i++)
{
    int temp = i;
    // actions.Add(() => print(i));   // 3, 3, 3
    actions.Add(() => print(temp));   // 0, 1, 2
}

foreach (Action act in actions)
    act();
```

- `() => print(i)`처럼 `i`를 직접 캡처하면 모든 람다가 같은 `i` 변수를 본다.
- for문이 끝난 뒤 `i` 값은 3이라 나중에 실행하면 `3, 3, 3`이 찍힌다.
- `temp`를 반복마다 새로 만들고 `temp`를 캡처하면 `0, 1, 2`가 제대로 출력된다.

---

### 8. 람다식과 람다문

#### 람다식 (expression body)

```csharp
Action lambda1 = () => print("Hello Lambda");
lambda1();

Func<int> lambda2 = () => 5 * 5;
print($"lambda2 : {lambda2()}");

Func<int, int> lambda3 = (x) => x * x;
print($"lambda3 : {lambda3(5)}");

Func<int, int> lambda4 = (int x) => x * outer;
print($"lambda4 : {lambda4(5)}");

Action<string> append = (x) => print($"Append : {x}");
append("Test");
```

- 한 줄 표현식으로 동작이나 반환값을 바로 표현하는 형태다.
- 짧은 계산이나 간단한 동작에 쓰기 좋다.

#### 람다문 (statement body)

```csharp
Action<string> lambda5 = name =>
{
    string hello = $"Hello {name}";
    print("Lambda5 : " + hello);
};
lambda5("Unit");

Func<string, int, bool> lambda6 = (x, y) =>
{
    return x.Length > y;
};
print($"Lambda6 : {lambda6("Unity", 3)}");
```

- 중괄호를 써서 여러 줄 코드를 작성하는 형태다.
- `return`이 필요한 경우 직접 써야 한다.

---

### 9. Predicate

```csharp
Predicate<int> lambda7 = (x) =>
{
    string str = "Unity";
    return str.Length > x;
};
print($"Lambda7 : {lambda7(3)}");
```

- `Predicate<int>`는 `int` 하나를 입력받고 `bool`을 반환하는 델리게이트 타입이다.
- `Predicate<T>`는 입력 타입 `T`만 바꿀 수 있고, 반환 타입은 항상 `bool`이다.
- 리스트 검색, 조건 필터링 같은 곳에서 많이 쓰인다.

---

### 10. 람다 특성


#### 델리게이트에 의해 타입이 결정됨

- 람다는 단독으로 타입이 있는 게 아님.
- 반드시 `Func`, `Action`, `Comparison` 같은 델리게이트 타입에 들어가야 함.
- 델리게이트가 파라미터 타입과 리턴 타입을 정함.

```csharp
Func<int, string> lambda = (x) => x.ToString();
```

#### 타입 자체가 없어서 object 멤버 접근 불가

- 람다 자체는 `object`처럼 다룰 수 없음.
- 람다식 결과에 `ToString()` 같은 object 멤버를 바로 붙이는 건 안 됨.

```csharp
// Func<int, string> lambda = ((int x) => x).ToString(); // 불가능
```

#### 타입 자체가 없어서 캐스팅 불가

- 람다는 독립된 타입이 아니므로 직접 캐스팅할 수 없음.
- 델리게이트 형식으로 받아서 써야 함.

---

#### 델리게이트 형식과 반드시 일치해야 함

- 람다의 파라미터 개수, 파라미터 타입, 리턴 타입이 델리게이트와 맞아야 함.

```csharp
Func<int, bool> lambda = (int x) => x; // x 그 자체를 반환하기 때문에 오류
```
```csharp
Func<int, bool> lambda = (int x) =>
{
    return x>10; //반환형이 bool이라 정상작동
};
```
---

#### var로 형식 추론 불가

- `var`는 오른쪽 식을 보고 타입을 추론하지만 람다는 그 자체만으로는 타입이 정해지지 않음.
- 그래서 람다는 `var`로 선언할 수 없음.

```csharp
// var lambda = (int x) => x; // 불가능
```
---
#### out, ref 파라미터 사용 불가

- 일반 메서드처럼 `out`, `ref`를 람다 파라미터에 직접 쓰는 건 안 됨.

```csharp
// Action<int> lambda = (out int x) => x = 10; // 불가능
// Action<int> lambda = (ref int x) => x = 10; // 불가능
```
---
#### 클로저는 레퍼런스로 캡처됨

- 람다는 바깥 변수를 캡처할 수 있음.
- 캡처된 변수는 람다 내부에서 사용할 수 있음.

```csharp
List<string> names = new List<string>() { "이순신", "강감찬" };

List<Action> actions = new List<Action>();
foreach (string name in names)
{
    actions.Add(() => print($"name : {name}"));
}
```
---
#### 람다는 델리게이트를 통해서만 사용됨

- `ForEach`, `Sort`, 이벤트 등록 같은 곳에서 람다를 많이 사용함.
- 람다의 실제 사용처는 결국 델리게이트가 필요한 자리임.

```csharp
items.ForEach((x) => print(x));
numbers.Sort((x, y) => y.CompareTo(x));
```
---
## 제네릭과 일반 클래스

### 1. 일반 클래스 A

```csharp
private class A { }
```

- 내용 없는 간단한 클래스다.
- 제네릭 메서드가 사용자 정의 타입도 받을 수 있다는 예시로 사용된다.

---

### 2. 제네릭 메서드 `Print<T>`

```csharp
private void Print<T>(T value)
{
    print($"print : {value}");
}
```

- `<T>`는 타입 매개변수다.
- `T`에 `int`, `string`, `A` 등 다양한 타입을 넣을 수 있다.

```csharp
Print<int>(5);
Print<string>("Unity");
Print(new A());
```

- 하나의 메서드로 여러 타입 값을 출력할 수 있다.

---

### 3. 제네릭 클래스 `B<T>`

```csharp
private class B<T>
{
    List<T> datas = new List<T>();

    public void Add(T data)
    {
        datas.Add(data);
    }

    public void PrintAll()
    {
        foreach (T data in datas)
            print($"data : {data}");
    }
}
```

```csharp
B<int> datas = new B<int>();
datas.Add(1);
datas.Add(3);
datas.Add(2);
datas.Add(5);
datas.PrintAll();
```

- `B<T>`는 특정 타입만 저장하는 제네릭 컨테이너다.
- `T`를 `int`로 정하면 `List<int>`처럼 동작하고, 컴파일 단계에서 타입 검사를 받을 수 있다.

---

### 4. 제네릭 없이 `object`를 쓰는 클래스 `C`

```csharp
private class C
{
    List<object> datas = new List<object>();

    public void Add(object data)
    {
        datas.Add(data);
    }

    public void PrintAll()
    {
        foreach (object data in datas)
            print($"data : {data}");
    }
}
```

```csharp
C datas2 = new C();
datas2.Add(1);
datas2.Add(3);
datas2.Add(2);
datas2.Add(5);
datas2.PrintAll();
```

- `C`는 모든 값을 `object`로 받아서 저장한다.
- 어떤 타입이든 넣을 수 있지만, 나중에 실제 타입으로 사용할 때 형변환이 필요할 수 있다.

---

### 5. `B<T>`와 `C` 비교

| 항목           | `B<T>`                | `C`                        |
|----------------|-----------------------|----------------------------|
| 저장 방식      | 같은 타입만 저장     | `object`로 모든 타입 저장 |
| 타입 검사      | 컴파일 단계에서 강함 | 런타임까지 미뤄짐          |
| 형변환 필요성  | 적음                  | 많을 수 있음              |
| 안정성         | 더 높음               | 더 낮음                    |

---

## 캡슐화(접근제한)
**캡슐화**는 데이터와 그 데이터를 다루는 기능을 하나로 묶고, **외부에서 함부로 접근할 수 없게 하는 것**이다.

---

## 상속
상속은 **기존 클래스의 기능을 재사용, 확장, 수정**하면서 새로운 클래스를 만드는 것을 뜻한다.  
**상속받는 클래스를 자식 클래스(derived class), 물려주는 클래스를 부모 클래스(base class)라고 부른다.**

---

## 다형성
다형성은 **실행 시점에 자식 클래스의 객체를 부모 클래스 타입으로 다룰 수 있다**.  

---
### private
**같은 클래스 내부에서만** 접근이 가능하게 하는 제한자

#### 예시
```csharp
public class Player
{
    private int hp = 100;

    private void Heal()
    {
        hp += 10;
    }
}
```
```csharp
Player player = new Player();

// player.hp = 999;   // 컴파일 에러, private이라 외부 접근 불가
// player.Heal();      // 컴파일 에러, private이라 외부 접근 불가
```
- `hp`,`Heal()` 은 오직 `Player` 클래스 내부 코드에서만 사용할 수 있다.

---

### protected
**같은 클래스 + 상속받은 자식 클래스에서** 접근이 가능하게 하는 제한자

#### 예시
```csharp
public class Character
{
    protected bool bMove;

    protected void Flip()
    {
    }
}
```
```csharp
public class Player : Character
{
    public void Test()
    {
        bMove = true; // 가능, 자식 클래스라서
        Flip();       // 가능
    }
}
```
```csharp
Player player = new Player();
// player.bMove = true; // 에러, 외부 코드에서는 protected 접근 불가
```
- `Player`는 `Character`클래스를 상속한 자식 클래스 이기 때문에 `bMove`와 `Flip()`을 사용할 수 있다.
- `protected`멤버는 자기 클래스 내부와 파생 클래스 내부에서만 접근할 수 있다.

---

### public
**어디서든** 접근이 가능하게 하는 제한자

#### 예시
```csharp
public class Character
{
    public void Move()
    {
        bMove = true;
    }
}
```
```csharp
public class GameManager : MonoBehaviour
{
    public Player player;

    private void Start()
    {
        player.Move(); // 가능, public이니까 어디서든 호출 가능
    }
}
```
- `Move()`의 접근 제한자가 `public`이기 때문에, 다른 스크립트에서도 자유롭게 `Move()`를 호출할 수 있다.

---



---
## abstract
**부모가 뼈대를 제공**하고 **자식이 세부동작을 반드시 구현**하는 키워드이다.

### abstract 규칙
1. `abstract` 클래스는 **`new`로 만들 수 없다**.
1. `abstract` 메서드는 **몸통`{}`이 없어야 한다**.
1. `abstract` 메서드는 가진 클래스를 반드시 **`abstract class`여야 한다**. (`abstract` 키워드를 써야 함)
1. `abstract` 메서드는 자식에게 반드시 **`override` 해야 한다**.
[override](./Unity_Class.md#override)

### abstract 클래스
```csharp
public abstract class Character : MonoBehaviour
{
}
```
- `abstract class`는 직접 인스턴스를 만들 수 없는 클래스이다.
```csharp
// Character character = new Character(); // 컴파일 에러
```
- 이 클래스는 **공통 기능을 담은 부모 틀**로만 존재하고, 실제로 게임에 등장하는건 이걸 **상속하는 구체적인 클래스**이다.

### abstract 메서드
```csharp
protected abstract void Update();
protected abstract void FixedUpdate();
```
- `{}`와 안의 코드가 존재하지 않는다.
- 부모가 상속받는 자식에게 세부구현을 하라고 강제한다.
```csharp
public class Player : Character
{
    protected override void Update()
    {
        // Player만의 이동 로직
    }

    protected override void FixedUpdate()
    {
        // Player만의 물리 이동 로직
    }
}
```
- 자식이 `Update()`와 `FixedUpdate()`를 구현하지 않으면 컴파일 에러가 일어난다.
- `override`를 통해 부모 클래스에 있던 메서드를 자식 클래스에서 구현한다.

---

## virtual
부모가 **기본 동작을 이미 구현해두지만, 자식이 그대로 써도 되고 원하면 재정의(override)해도 되는 키워드**이다.

### virtual 예시
```csharp
protected virtual void Awake()
{
    animator = GetComponentInChildren<Animator>();
    rigidbody2D = GetComponent<Rigidbody2D>();
}
```
- 부모가 기본동작을 미리 구현 한다.
- 자식은 이걸 그대로 써도 되고 재정의(`override`)해도 된다.

```csharp
public class Player : Character
{
    // Awake를 override 안 해도 됨 → 부모의 Awake 그대로 사용
}
```
- 재정의(`override`)를 안하면 부모의 기본동작 `Awake()`을 그대로 사용한다.
```csharp
public class Player : Character
{
    protected override void Awake()
    {
        base.Awake(); // 부모 기능 유지
        AwakeBindInput(); // 추가 기능
    }
}
```
- 재정의(`override`)를 해서 `AwakeBindInput()`을 넣고 부모의 기능도 `base.Awake()`로 그대로 사용 가능하다.

---

## override
`override`는 부모의 `virtual` 또는 `abstract` 메서드를 **자식 클래스에서 실제로 재구현한다는 표시**이다.  
`override`를 쓰려면 반드시 **부모 쪽 메서드가 `virtual`이거나 `abstract`여야 한다.** 일반 메서드는 불가능하다.

### override 규칙
1. **메서드 이름, 파라미터, 반환형이 부모와 정확히 같아야 한다.**
1. 부모가 **`virtual`/`abstract`가 아니면 `override`가 불가능** 하다.
1. `override`한 메서드는 다시 **그 자식의 자식이 `override`할 수도 있다.**(연쇄 가능)

### base.메서드()
`override`는 **새로 만드는게 아닌 다시 구현** 하는 의미라서,   
부모가 만든 메서드를 완전히 없애고 싶지 않으면 **`base.메서드()`로 부모 기능을 먼저 실행해야 한다**  
`base.메서드()`를 빼면 부모의 코드가 실행이 안된다.


### override 예시
```csharp
protected virtual void Awake()
{
    animator = GetComponentInChildren<Animator>();
    rigidbody2D = GetComponent<Rigidbody2D>();
}
```
```csharp
protected override void Awake()  //부모 메서드를 재구현 하므로 override 사용
{
    base.Awake();
    AwakeBindInput();
}
```
- 부모 메서드인 `Awake()`를 재정의 해야하므로 자식 메서드에서는 `override`를 사용 하였다.
- `base.Awake()`를 빼면 부모의 코드가 실행이 안된다.
---

## 정규화 · 법선 벡터 · 내적

### 1. 개념 연결

**법선 벡터는 표면에 수직인 방향을 나타내고, 정규화는 벡터 길이를 1로 맞추며, 내적은 두 벡터의 방향과 크기 관계를 숫자로 계산함.**

게임에서는 다음 순서로 연결해서 사용함.

```text
벽의 법선 벡터와 플레이어 입력 벡터 준비
    ↓
입력이 충분한지 확인
    ↓
두 벡터 정규화
    ↓
Dot으로 내적 계산
    ↓
결과를 기준값과 비교
    ↓
벽 상태 진입·종료 등의 행동 결정
```

---

### 2. 벡터(Vector2)

벡터는 방향과 크기를 가진 값임.

Unity의 `Vector2`는 X와 Y 두 성분으로 구성됨.

```csharp
Vector2 direction = new Vector2(1f, 0f);
```

| 벡터 | 방향 | 길이 |
|---|---|---:|
| `(1, 0)` | 오른쪽 | 1 |
| `(-1, 0)` | 왼쪽 | 1 |
| `(0, 1)` | 위쪽 | 1 |
| `(0, -1)` | 아래쪽 | 1 |
| `(1, 1)` | 오른쪽 위 | 약 1.414 |
| `(0, 0)` | 방향 없음 | 0 |

`Vector2`가 항상 방향만 의미하는 것은 아님.

사용 목적에 따라 위치, 방향, 속도 등을 표현함.

```csharp
Vector2 position;  // 위치
Vector2 moveDir;   // 입력 방향
Vector2 velocity; // 속도
```

---

## 3. 벡터의 길이: magnitude와 sqrMagnitude

벡터가 `(x, y)`일 때 피타고라스 정리를 이용해 길이를 계산함.

### magnitude

벡터의 실제 길이를 반환함.

```text
magnitude = √(x² + y²)
```

```csharp
Vector2 vector = new Vector2(3f, 4f);

Debug.Log(vector.magnitude); // 5
```

### sqrMagnitude

벡터 길이의 제곱을 반환함.

```text
sqrMagnitude = x² + y²
```

```csharp
Vector2 vector = new Vector2(3f, 4f);

Debug.Log(vector.sqrMagnitude); // 25
```

길이의 크기만 비교할 때는 제곱근 계산을 생략할 수 있는 `sqrMagnitude`를 사용함.

### 기준값도 제곱해서 비교

다음 두 조건은 같은 의미임.

```csharp
moveDir.magnitude > 0.1f
```

```csharp
moveDir.sqrMagnitude > 0.1f * 0.1f
```

즉 다음 조건은 입력 벡터의 길이가 `0.1`보다 큰지 검사함.

```csharp
moveDir.sqrMagnitude > 0.01f
```

> `sqrMagnitude > 0.1f`는 길이가 0.1보다 크다는 의미가 아님.
> 실제 길이가 약 0.316보다 큰지 검사하는 조건임.

---

## 4. 정규화(Normalization)

정규화는 벡터의 방향을 유지하면서 길이를 1로 맞추는 작업임.

길이가 1인 벡터를 단위 벡터라고 부름.

```text
정규화 전:
방향과 원래 크기를 가짐.

정규화 후:
방향은 유지하고 길이를 1로 맞춤.
```

### 정규화 예시

```csharp
Vector2 vector = new Vector2(3f, 4f);
Vector2 direction = vector.normalized;
```

```text
vector:
(3, 4)
길이 = 5

direction:
(0.6, 0.8)
길이 = 1
```

각 성분을 원래 벡터의 길이로 나누어 계산함.

```text
(3 ÷ 5, 4 ÷ 5)
= (0.6, 0.8)
```

### normalized와 Normalize()의 차이

```csharp
Vector2 vector = new Vector2(3f, 4f);

Vector2 direction = vector.normalized;
```

`.normalized`는 정규화된 값을 반환함. 원본 `vector`는 변경하지 않음.

```csharp
vector.Normalize();
```

`.Normalize()`는 원본 `vector` 자체를 정규화함.

| 사용 방식 | 원본 변경 여부 |
|---|---|
| `vector.normalized` | 변경하지 않음 |
| `vector.Normalize()` | 변경함 |

### 영벡터 정규화

```csharp
Vector2 vector = Vector2.zero;
Vector2 direction = vector.normalized;
```

영벡터 `(0, 0)`에는 방향이 없음.

Unity에서는 정규화하기에 너무 작은 벡터에 대해 영벡터를 반환함.

### 정규화 사용 목적

벡터의 원래 길이 영향을 제거하고 방향만 비교하기 위해 사용함.

```text
(1, 0)
(5, 0)

둘 다 오른쪽이지만 길이는 다름.
정규화하면 둘 다 (1, 0)이 됨.
```

---

## 5. 법선 벡터(Normal Vector)

법선 벡터는 표면에 수직인 벡터임.

표면에 화살표를 직각으로 꽂은 모습으로 이해할 수 있음.

### 바닥 위쪽 면의 법선

```text
        ↑ 법선
        │
──────────────── 바닥
```

```csharp
Vector2 normal = new Vector2(0f, 1f);
```

### 플레이어 오른쪽 벽의 플레이어 쪽 면

```text
플레이어          벽
   [P]      ←────│
             법선│
```

```csharp
Vector2 normal = new Vector2(-1f, 0f);
```

### 플레이어 왼쪽 벽의 플레이어 쪽 면

```text
벽          플레이어
│────→         [P]
│ 법선
```

```csharp
Vector2 normal = new Vector2(1f, 0f);
```

> 표면에 수직인 방향은 서로 반대인 두 방향이 존재함.
> 법선의 부호는 어느 면과 접촉 정보를 기준으로 보는지에 따라 확인해야 함.

### 경사면의 법선

법선이 항상 위·아래·좌·우 중 하나인 것은 아님.

경사면에서는 법선도 비스듬한 방향을 가짐.

```text
경사면을 따라가는 방향: (1, 1)
여기에 수직인 한 방향: (-1, 1)
```

두 벡터의 내적을 계산하면 다음과 같음.

```text
1 × (-1) + 1 × 1 = 0
```

두 벡터가 모두 영벡터가 아닌 상태에서 내적이 0이므로 서로 수직임.

### 법선과 정규화의 차이

| 개념 | 의미 |
|---|---|
| 법선 | 표면에 수직인 벡터 |
| 정규화 | 벡터 길이를 1로 맞추는 작업 |
| 단위 법선 | 길이가 1인 법선 벡터 |

수학적으로 법선이라는 이유만으로 길이가 반드시 1인 것은 아님.

```text
(0, 1)
(0, 3)

둘 다 평평한 바닥에 수직인 위쪽 방향임.
길이는 각각 1과 3으로 다름.
```

---

## 6. Unity에서 법선 가져오기

### 실제 충돌의 접촉 법선

```csharp
private void OnCollisionEnter2D(Collision2D collision)
{
    Vector2 normal = collision.GetContact(0).normal;
}
```

```text
GetContact(0):
첫 번째 접촉점 정보를 가져옴.

.normal:
해당 접촉점의 법선 벡터를 가져옴.
```

접촉점이 여러 개라면 첫 번째 접촉점만으로 전체 충돌을 판단하기에 부족할 수 있음.

### Cast 검사의 법선

```csharp
Vector2 normal = hit.normal;
```

`hit`이 `RaycastHit2D` 검사 결과라면 감지한 표면의 법선을 사용할 수 있음.

실제 접촉이 없어도 Cast 결과를 이용해 벽 방향을 판단할 수 있음.

---

## 7. 내적(Dot Product)

내적은 두 벡터를 받아 숫자 하나를 계산하는 연산임.

Unity에서는 `Vector2.Dot()`을 사용함.

```csharp
float result = Vector2.Dot(a, b);
```

반환값은 `Vector2`가 아니라 `float`임.

### 내적 계산

```text
a · b = a.x × b.x + a.y × b.y
```

다음 두 코드는 같은 계산을 수행함.

```csharp
float result = Vector2.Dot(a, b);
```

```csharp
float result = a.x * b.x + a.y * b.y;
```

### 길이가 1인 벡터끼리 비교

| 방향 관계 | 예시 | 내적 |
|---|---|---:|
| 완전히 같은 방향 | →와 → | 1 |
| 45도 차이 | →와 ↗ | 약 0.707 |
| 수직 | →와 ↑ | 0 |
| 완전히 반대 방향 | →와 ← | -1 |

```csharp
Vector2.Dot(Vector2.right, Vector2.right); //  1
Vector2.Dot(Vector2.right, Vector2.up);    //  0
Vector2.Dot(Vector2.right, Vector2.left);  // -1
```

### 내적과 각도의 관계

내적은 각도 자체를 반환하지 않음.

```csharp
float result = Vector2.Dot(a, b);
```

`result`를 도 단위 각도로 해석하면 안 됨.

내적과 각도의 관계는 다음과 같음.

```text
a · b = |a| × |b| × cos(θ)

|a|, |b|:
각 벡터의 길이.

θ:
두 벡터 사이 각도.
```

두 벡터의 길이가 모두 1이면 다음과 같이 단순해짐.

```text
a · b = cos(θ)
```

정규화된 두 벡터의 내적이 `0.9`보다 크면 사이 각도가 약 25.8도보다 작다는 의미임.

---

## 8. 내적 전에 정규화하는 이유

내적은 방향뿐 아니라 벡터 길이에도 영향을 받음.

### 정규화하지 않은 예시

```csharp
Vector2 normal = new Vector2(-1f, 0f);
Vector2 input = new Vector2(-0.5f, 0f);

float result = Vector2.Dot(normal, input);
```

```text
(-1 × -0.5) + (0 × 0)
= 0.5
```

두 벡터 모두 왼쪽을 향하지만 길이가 달라 내적 결과가 1이 나오지 않음.

### 정규화한 예시

```csharp
float result = Vector2.Dot(
    normal.normalized,
    input.normalized
);
```

```text
normal.normalized = (-1, 0)
input.normalized  = (-1, 0)

내적 = 1
```

두 벡터의 길이를 1로 맞춰 원래 크기의 영향을 제거함.

### 올바른 처리 순서

```text
두 벡터 정규화
    ↓
내적 계산
    ↓
결과 숫자를 기준값과 비교
```

### 잘못된 사용

```csharp
float result = Vector2.Dot(a, b);

result.normalized; // 사용 불가
```

`result`는 `float`이므로 `.normalized`를 사용할 수 없음.

정규화할 대상은 내적 결과가 아니라 내적에 전달할 벡터임.

---

## 9. 입력 크기를 먼저 검사하는 이유

```csharp
if (moveDir.sqrMagnitude > 0.01f)
{
    // 방향 비교
}
```

입력이 없거나 너무 약한 경우를 제외하기 위한 조건임.

정규화하면 원래 입력 크기가 사라지므로 먼저 검사함.

```text
약한 입력: (0.05, 0)
    ↓ 정규화
방향: (1, 0)
```

위 입력은 매우 약하지만 정규화 후에는 길이가 1이 됨.

따라서 다음 순서로 처리함.

```text
sqrMagnitude:
입력이 충분한지 검사.

normalized:
입력 방향만 남김.

Dot:
다른 방향과 얼마나 일치하는지 계산.
```

`0.01f`는 예시 기준이며 입력 설정에 맞춰 조절함.

---

## 10. 벽 상태 진입에 적용

오른쪽 벽을 향해 오른쪽으로 입력하는 상황을 가정함.

```text
벽 법선 normal: 왼쪽 (-1, 0)
입력 moveDir:   오른쪽 (1, 0)
```

벽 법선과 입력이 반대 방향임.

```csharp
float result = Vector2.Dot(
    normal.normalized,
    moveDir.normalized
);
```

```text
result = -1
```

다음 조건으로 벽을 향하는 입력을 검사할 수 있음.

```csharp
result < -0.9f
```

### 입력을 반전해서 비교

```csharp
Vector2.Dot(
    normal.normalized,
    -moveDir.normalized
) > 0.9f
```

벡터 앞의 `-`는 방향을 반전함.

```text
moveDir  = (1, 0)  → 오른쪽
-moveDir = (-1, 0) → 왼쪽
```

다음 두 조건은 같은 의미임.

```text
Dot(normal, input) < -0.9
→ 법선과 입력이 거의 반대 방향인지 검사.

Dot(normal, -input) > 0.9
→ 법선과 반전한 입력이 거의 같은 방향인지 검사.
```

입력이 충분하고 가까운 벽을 감지했다는 조건까지 만족할 때 벽 상태 진입을 처리함.

---

## 11. 벽 상태 종료에 적용

오른쪽 벽에서 왼쪽으로 입력하는 상황을 가정함.

```text
벽 법선: 왼쪽
입력:    왼쪽

내적 = 1
```

벽에서 떨어지는 입력을 확인하는 코드임.

```csharp
if (moveDir.sqrMagnitude > 0.01f)
{
    Vector2 normalDirection = wall.wallNormal.normalized;
    Vector2 inputDirection = moveDir.normalized;

    float result = Vector2.Dot(
        normalDirection,
        inputDirection
    );

    if (result > 0.9f)
    {
        fsm.ChangeStateNoExit(move);
    }
}
```

각 단계의 역할은 다음과 같음.

| 코드 | 역할 |
|---|---|
| `sqrMagnitude > 0.01f` | 입력 크기가 충분한지 검사 |
| `.normalized` | 벡터 길이를 1로 맞춤 |
| `Vector2.Dot()` | 두 방향의 관계를 계산 |
| `result > 0.9f` | 거의 같은 방향인지 판단 |
| `ChangeStateNoExit(move)` | 기존 FSM에서 이동 상태로 전환 |

이 조건은 벽에서 멀어지는 입력을 검사함.

벽이 사라지거나 캐릭터가 벽 끝을 지난 상황은 별도의 벽 감지 검사로 처리해야 함.

---

## 12. 방향 기준값 0.9의 주의점

`0.9f`는 필수값이 아니라 방향 일치 범위를 정하는 기준임.

```text
기준값이 높음:
거의 같은 방향만 인정함.

기준값이 낮음:
더 비스듬한 방향도 인정함.
```

정규화된 두 벡터의 각도 차이가 45도이면 내적은 약 0.707임.

```text
오른쪽과 오른쪽 위 비교
→ 내적 약 0.707
```

따라서 다음 조건은 45도 대각선을 인정하지 않음.

```csharp
result > 0.9f
```

대각선 입력도 벽 방향 입력으로 인정하려면 다음 방법을 고려함.

- 내적 기준값을 낮춤.
- 가로 입력 성분만 비교함.
- 벽 부착에 필요한 입력 조건을 별도로 정의함.

정규화는 길이 영향을 제거하는 작업이며, 대각선 입력을 자동으로 인정하게 만드는 작업은 아님.

---

## 1. FSM의 개념

**FSM은 정해진 상태 중 현재 상태를 선택하고, 조건에 따라 상태를 전환하며, 현재 상태의 행동을 실행하는 체계임.**

FSM은 `Finite State Machine`의 약자이며 유한 상태 머신이라고 부름.

| 단어 | 의미 |
|---|---|
| Finite | 정해진 수의 상태가 존재함 |
| State | 현재 행동 모드 |
| Machine | 상태를 관리하고 실행하는 체계 |

캐릭터 행동을 다음과 같은 상태로 구분할 수 있음.

```text
대기
이동
점프
공격
피격
사망
```

기본적인 단일 FSM에서는 현재 상태 하나를 선택해 실행함.

```text
현재 상태: 대기
    ↓ 이동 입력
다음 상태: 이동
    ↓ 입력 종료 + 움직임이 멈춤
다음 상태: 대기
```

---

## 2. FSM의 구성 요소

| 구성 요소 | 역할 |
|---|---|
| 상태(State) | 특정 상황에서 수행할 행동 정의 |
| 전환(Transition) | 현재 상태에서 다른 상태로 변경 |
| 전환 조건 | 상태를 변경할 조건 |
| 상태 머신 | 현재 상태 보관·전환·실행 |

### 상태

캐릭터가 현재 어떤 행동 모드인지 나타냄.

```text
대기 상태:
대기 애니메이션 재생

이동 상태:
입력에 따라 이동

공격 상태:
공격 동작 실행

사망 상태:
조작 차단 및 사망 처리
```

### 전환 조건

입력이나 상황에 따라 상태 전환 여부를 판단함.

```text
대기 → 이동:
이동 입력이 들어옴.

이동 → 대기:
입력이 종료되고 움직임이 멈춤.

이동 → 공격:
공격 입력이 들어오고 공격이 가능한 상태임.

공격 → 대기:
공격 동작이 종료됨.
```

상태 전환은 상태 이름을 선언하는 것만으로 자동 발생하지 않음.

조건을 검사하고 상태 변경 함수를 호출하는 코드가 필요함.

---

## 3. FSM과 상태 패턴의 관계

FSM은 상태와 전환을 이용해 행동을 관리하는 모델임.

상태 패턴은 상태별 행동을 별도 클래스로 분리하는 설계 방식임.

FSM을 반드시 상태 클래스로 구현해야 하는 것은 아님.

### enum과 switch를 사용하는 방식

```csharp
public enum CharacterState
{
    Idle,
    Move,
    Attack
}
```

```csharp
switch (currentState)
{
    case CharacterState.Idle:
        // 대기 행동
        break;

    case CharacterState.Move:
        // 이동 행동
        break;

    case CharacterState.Attack:
        // 공격 행동
        break;
}
```

상태를 열거형으로 구분하고 조건문에서 행동을 처리함.

### 상태 클래스를 사용하는 방식

```text
IdleState:
대기 행동

MoveState:
이동 행동

AttackState:
공격 행동
```

상태마다 클래스를 만들고 행동을 분리함.

```text
FSM:
현재 상태와 전환 흐름 관리

상태 클래스:
각 상태의 실제 행동 구현
```

상태와 행동이 복잡해질 때 관련 코드를 상태별로 나누어 관리할 수 있음.

---

## 4. 상태의 기본 함수

상태마다 다음 함수를 두어 실행 시점을 구분할 수 있음.

| 함수 | 역할 | 실행 시점 |
|---|---|---|
| `Enter()` | 초기 설정 | 상태에 들어갈 때 |
| `Tick(dt)` | 반복 행동 | 현재 상태인 동안 |
| `Exit()` | 종료 정리 | 상태에서 나갈 때 |

### Enter()

상태에 들어가는 순간 실행함.

```text
공격 애니메이션 시작
공격 타이머 초기화
이동 입력 제한
```

같은 상태를 유지하는 동안 매 프레임 실행하는 함수가 아님.

### Tick(dt)

현재 상태인 동안 반복 실행함.

```text
이동 속도 계산
공격 진행 시간 갱신
동작 종료 여부 확인
```

`Tick`은 임의로 정한 함수 이름임.

Unity가 `Update()`처럼 자동 호출하는 함수가 아니므로 별도의 호출 코드가 필요함.

### Exit()

상태에서 나가는 순간 실행함.

```text
공격 판정 비활성화
입력 제한 해제
임시 데이터 정리
```

---

## 5. 상태 클래스의 공통 틀

```csharp
public abstract class State
{
    public virtual void Enter()
    {
    }

    public virtual void Tick(float dt)
    {
    }

    public virtual void Exit()
    {
    }
}
```

각 상태가 같은 형태의 함수를 사용하도록 공통 틀을 정의함.

FSM은 구체적인 상태의 세부 내용을 몰라도 다음 형태로 실행할 수 있음.

```csharp
currentState.Enter();
currentState.Tick(dt);
currentState.Exit();
```

현재 상태 객체가 무엇인지에 따라 해당 상태의 행동이 실행됨.

```text
현재 상태가 IdleState
→ 대기 행동 실행

현재 상태가 MoveState
→ 이동 행동 실행

현재 상태가 AttackState
→ 공격 행동 실행
```

---

## 6. FSM의 기본 구현

```csharp
public class FSM
{
    public State CurrentState { get; private set; }

    public void ChangeState(State nextState)
    {
        if (nextState == null)
            return;

        if (CurrentState == nextState)
            return;

        CurrentState?.Exit();

        CurrentState = nextState;

        CurrentState.Enter();
    }

    public void Tick(float dt)
    {
        CurrentState?.Tick(dt);
    }
}
```

### 현재 상태 보관

```csharp
public State CurrentState { get; private set; }
```

현재 상태 객체의 참조를 저장함.

외부에서 상태를 확인할 수 있지만 직접 변경하지 못하도록 설정함.

상태 변경은 `ChangeState()`를 통해 처리함.

### 유효한 상태인지 검사

```csharp
if (nextState == null)
    return;
```

새 상태가 전달되지 않은 경우 전환을 생략함.

이 예제에서는 `null`을 현재 상태 해제 용도로 사용하지 않음.

### 같은 상태인지 검사

```csharp
if (CurrentState == nextState)
    return;
```

이미 같은 상태 객체를 사용 중이면 종료·재진입을 생략함.

### 이전 상태 종료

```csharp
CurrentState?.Exit();
```

현재 상태가 존재할 때만 종료 함수를 호출함.

최초 상태 등록처럼 현재 상태가 없으면 호출을 생략함.

### 새 상태 지정과 진입

```csharp
CurrentState = nextState;
CurrentState.Enter();
```

현재 상태가 가리키는 객체를 변경한 뒤 새 상태의 진입 행동을 실행함.

---

## 7. 상태 객체 준비와 제어 대상 연결

상태 머신을 사용하려면 실행할 상태 객체를 준비해야 함.

캐릭터가 자기 FSM과 상태 객체를 보관하는 예시임.

```csharp
private FSM fsm;

private IdleState idle;
private MoveState move;

private void Awake()
{
    fsm = new FSM();

    idle = new IdleState();
    move = new MoveState(this);
}

private void Start()
{
    fsm.ChangeState(idle);
}
```

실행 흐름은 다음과 같음.

```text
FSM 생성
    ↓
사용할 상태 객체 준비
    ↓
필요한 상태에 제어 대상 전달
    ↓
최초 상태 등록
```

### 상태가 캐릭터를 제어하는 방법

이동 상태는 어떤 캐릭터를 움직일지 알아야 함.

```csharp
move = new MoveState(this);
```

캐릭터 코드 안의 `this`를 전달하여 이동 상태가 해당 캐릭터를 사용할 수 있도록 연결함.

상태에서는 전달받은 참조를 보관함.

```csharp
public class MoveState : State
{
    private Player player;

    public MoveState(Player player)
    {
        this.player = player;
    }

    public override void Tick(float dt)
    {
        // player를 통해 이동 행동 처리
    }
}
```

```text
move 변수
    ↓
MoveState 객체
    ↓ player 참조
실제 Player 컴포넌트
```

새로운 Player를 복제하는 것이 아님.

상태가 기존 Player에 접근할 수 있도록 참조를 전달하는 과정임.

여러 상태에 같은 Player를 전달하면 각 상태가 같은 캐릭터를 제어할 수 있음.

```text
MoveState.player ──┐
                  ├──→ 같은 Player
AttackState.player┘
```

상태 객체를 한 번 준비한 뒤 재사용하는 구조에서는 상태 전환 때마다 객체를 새로 만들 필요가 없음.

---

## 8. 최초 상태 등록

```csharp
fsm.ChangeState(idle);
```

최초 상태를 대기로 지정함.

현재 상태가 없으므로 이전 상태의 종료 처리는 생략함.

```text
CurrentState = null
    ↓
이전 Exit() 호출 생략
    ↓
CurrentState = idle
    ↓
IdleState.Enter() 실행
```

상태 객체를 만들어 두는 것과 현재 상태로 지정하는 것은 다른 작업임.

```csharp
idle = new IdleState(); // 사용할 상태 객체 준비
fsm.ChangeState(idle);  // 현재 실행할 상태로 지정
```

---

## 9. 상태 전환의 실행 순서

대기 상태에서 이동 상태로 전환하는 경우임.

```csharp
fsm.ChangeState(move);
```

```text
1. 현재 상태와 목표 상태 비교
2. IdleState.Exit() 실행
3. CurrentState가 move 객체를 가리키도록 변경
4. MoveState.Enter() 실행
5. 이후 업데이트에서 MoveState.Tick(dt) 실행
```

전환 시 상태 객체를 복제하는 것이 아님.

현재 상태를 저장한 변수의 참조를 변경함.

```text
전환 전:
CurrentState → idle 객체

전환 후:
CurrentState → move 객체
```

`idle` 변수가 기존 대기 상태 객체를 계속 보관하고 있다면 이후 다시 사용할 수 있음.

```csharp
fsm.ChangeState(idle);
```

---

## 10. 같은 상태로 반복 전환하지 않는 이유

상태 전환 조건을 매 프레임 검사하면 같은 상태로 전환을 반복 요청할 수 있음.

```csharp
fsm.ChangeState(move);
```

동일 상태 검사가 없으면 다음 과정이 반복됨.

```text
Move.Exit()
Move.Enter()

다음 프레임:
Move.Exit()
Move.Enter()
```

진입 시 초기화하는 값도 반복 초기화될 수 있음.

```text
타이머 초기화
애니메이션 재시작
속도 초기화
임시 데이터 초기화
```

다음 검사는 불필요한 종료·재진입을 방지함.

```csharp
if (CurrentState == nextState)
    return;
```

### 같은 클래스와 같은 객체 구분

다음처럼 매번 새 상태 객체를 만들면 같은 클래스라도 서로 다른 객체임.

```csharp
fsm.ChangeState(new MoveState(this));
```

기본 예제의 동일 상태 검사는 객체 참조를 비교하므로 새 객체를 전달하면 재진입할 수 있음.

상태를 재사용하려면 보관해 둔 객체를 전달함.

```csharp
fsm.ChangeState(move);
```

---

## 11. Tick(dt)와 시간 전달

```csharp
public void Tick(float dt)
{
    CurrentState?.Tick(dt);
}
```

FSM이 전달받은 시간값을 현재 상태에 넘김.

호출하는 쪽에서는 다음처럼 사용할 수 있음.

```csharp
private void Update()
{
    fsm.Tick(Time.deltaTime);
}
```

```text
캐릭터 Update()
    ↓
FSM.Tick(Time.deltaTime)
    ↓
현재 상태.Tick(dt)
```

### 시간값을 전달하는 이유

상태 내부에서 직접 `Time.deltaTime`을 사용할 수도 있음.

매개변수로 받으면 시간값 선택과 행동 계산을 분리할 수 있음.

```text
호출하는 코드:
시간값 선택

FSM:
현재 상태에 시간값 전달

State:
전달받은 시간값으로 계산
```

시간 기반 계산 예시임.

```csharp
elapsedTime += dt;
```

```csharp
velocityY -= gravity * dt;
```

테스트에서는 원하는 시간값을 직접 전달할 수 있음.

```csharp
fsm.Tick(0.1f);
```

실제로 0.1초를 기다리는 명령이 아님.

0.1초만큼 시간이 흘렀다고 보고 상태 계산을 수행함.

---

## 12. 상태 선택과 상태 실행 분리

상태 선택과 상태 실행은 다른 작업임.

```text
상태 선택:
지금 어떤 행동을 해야 하는지 판단

상태 실행:
선택된 상태의 행동 수행
```

```csharp
private void Update()
{
    float dt = Time.deltaTime;

    SelectState();

    fsm.Tick(dt);
}
```

`SelectState()`는 예시로 정한 상태 선택 함수임.

입력과 상황을 검사하여 `ChangeState()`를 호출하는 역할로 사용할 수 있음.

상태 전환 판단 위치는 설계에 따라 달라질 수 있음.

- 캐릭터의 총괄 코드에서 판단함.
- 각 상태 내부에서 다음 상태를 결정함.
- 별도의 전환 규칙 관리 코드에서 판단함.

전환 규칙이 여러 곳에 중복되거나 충돌하지 않도록 관리해야 함.

---

## 13. 상태 진입 조건

특정 상태는 조건을 만족할 때만 진입하도록 제한할 수 있음.

```text
공격:
재사용 대기 시간이 끝나야 함.

점프:
지면에 있어야 함.

벽 상태:
가까운 벽을 감지해야 함.

사망:
체력이 0 이하이어야 함.
```

조건을 상태 선택 코드에서 검사하거나 `CanEnter()` 같은 함수로 분리할 수 있음.

함수를 선언하는 것만으로 자동 검사되지 않음.

상태 전환 과정에서 실제로 호출해야 함.

진입 조건을 설계할 때 다음 내용을 정해야 함.

- 어느 상태의 진입 조건을 검사할지
- 이전 상태 정보를 사용할지
- 입력·체력·접지 정보 등을 사용할지
- 진입 불가 시 현재 상태를 유지할지

---

## 14. Enter와 Exit의 데이터 처리

상태 전환 시 초기화할 값과 유지할 값을 구분해야 함.

### 진입 시 무조건 초기화하는 경우

```csharp
public override void Enter()
{
    // 속도 초기화
}
```

이동 상태로 들어갈 때 기존 점프 속도나 낙하 속도까지 사라질 수 있음.

상태마다 어떤 데이터가 초기화되어야 하는지 정해야 함.

### 전환 순서에 따른 덮어쓰기

```text
이전 상태 Exit:
점프 속도 설정
    ↓
새 상태 Enter:
속도 초기화
    ↓
방금 설정한 점프 속도가 사라짐
```

이전 상태의 종료 처리와 새 상태의 진입 처리가 서로 충돌하지 않도록 설계해야 함.

### 상태 객체 재사용 시 초기화

상태 객체를 재사용하면 내부 필드도 유지될 수 있음.

```text
공격 상태에서 타이머 사용
    ↓
다른 상태로 전환
    ↓
같은 공격 상태 객체에 재진입
```

새 공격을 시작할 때 타이머를 다시 초기화해야 한다면 `Enter()`에서 처리함.

객체를 한 번 생성해 두는 작업과 매번 상태에 들어갈 때 준비하는 작업을 구분해야 함.

---

## 15. 상태 종료 이유 구분

같은 상태에서 나가더라도 종료 이유가 다를 수 있음.

```text
공격 완료
피격으로 공격 중단
사망으로 강제 종료
```

모든 종료를 정상 완료처럼 처리하면 의도하지 않은 행동이 생길 수 있음.

공통 정리와 특정 전환 행동을 구분하는 방향을 고려함.

```text
공통 종료 정리:
공격 판정 비활성화
임시 효과 제거

특정 전환 행동:
다음 공격 연결
피격 반응 실행
사망 처리 시작
```

`Exit()`를 생략하는 전환을 추가할 수도 있지만, 필요한 정리까지 누락되지 않도록 주의해야 함.

---

## 16. FSM과 실제 이동 처리의 차이

FSM은 행동 상태를 관리하는 구조임.

물리 엔진이나 이동 컨트롤러 자체를 대체하는 기능은 아님.

```text
FSM:
대기·이동·점프 등의 현재 상태 관리

상태:
행동 규칙과 원하는 움직임 결정

이동 담당:
결정된 움직임을 실제 위치 변화로 적용
```

상태가 직접 이동을 처리하거나 별도 이동 컴포넌트에 요청할 수 있음.

```text
이동 상태
    ↓ 원하는 움직임 결정
이동 컴포넌트
    ↓ 이동 요청 적용
Rigidbody2D 또는 커스텀 컨트롤러
    ↓
실제 이동
```

이동 방식을 변경하더라도 상태 관리 구조는 유지할 수 있음.

---

## 17. 테스트 시 확인할 항목

### 최초 상태

- 최초 상태가 정상 등록되는지 확인함.
- 최초 상태의 `Enter()`가 실행되는지 확인함.
- 현재 상태가 없는 상황에서 오류가 발생하지 않는지 확인함.

### 상태 전환

- 이전 상태의 `Exit()`가 실행되는지 확인함.
- 새 상태의 `Enter()`가 실행되는지 확인함.
- 동일 상태 요청 시 불필요한 재진입이 발생하지 않는지 확인함.

### 반복 행동

- 현재 상태의 `Tick()`이 실행되는지 확인함.
- 비활성 상태의 반복 행동이 별도로 실행되지 않는지 확인함.
- 전달한 시간값이 계산에 사용되는지 확인함.

### 조건과 데이터

- 진입 조건을 만족하지 않으면 전환이 막히는지 확인함.
- 재진입 시 필요한 데이터가 초기화되는지 확인함.
- 유지해야 할 속도나 진행 정보가 전환 중 사라지지 않는지 확인함.
- 정상 종료와 강제 중단이 각각 올바르게 처리되는지 확인함.