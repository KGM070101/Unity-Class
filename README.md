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

