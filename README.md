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