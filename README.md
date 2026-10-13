# Unity / C# 개념 정리

## 목차

### 용어 정리
- [용어](Unity_Class.md#c-기초-용어-정리)
  - [클래스(Class)](Unity_Class.md#1-클래스class)
  - [객체(Object)와 인스턴스(Instance)](Unity_Class.md#2-객체object와-인스턴스instance)
  - [변수(Variable)](Unity_Class.md#3-변수variable)

- [타입](Unity_Class.md#2-타입)
  - [값 타입(Value Type)](Unity_Class.md#4-값-타입value-type)
  - [참조 타입(Reference Type)](Unity_Class.md#5-참조-타입reference-type)
  - [문자열(String)](Unity_Class.md#12-문자열string)

- [참조와 복사](Unity_Class.md#7-값-복사와-참조-복사)
  - [레퍼런스(Reference)](Unity_Class.md#6-레퍼런스reference)
  - [값 복사와 참조 복사](Unity_Class.md#7-값-복사와-참조-복사)
  - [ReferenceEquals](Unity_Class.md#13-referenceequals)
  - [박싱(Boxing)](Unity_Class.md#14-박싱boxing)
  - [언박싱(Unboxing)](Unity_Class.md#15-언박싱unboxing)

- [클래스 구성 요소](Unity_Class.md#4-클래스-구성-요소)
  - [필드(Field)](Unity_Class.md#8-필드field)
  - [프로퍼티(Property)](Unity_Class.md#9-프로퍼티property)
  - [메서드(Method)](Unity_Class.md#10-메서드method)
  - [생성자(Constructor)](Unity_Class.md#11-생성자constructor)

### Unity 기본
- [Unity 기본 / MonoBehaviour](./Unity_Class.md#unity-기본)
- [생명주기 함수 (Awake / Start / Update / FixedUpdate)](./Unity_Class.md#생명주기-함수)
- [오브젝트와 컴포넌트 찾기](./Unity_Class.md#오브젝트와-컴포넌트-찾기)
- [transform과 이동](./Unity_Class.md#transform)
- [Rigidbody와 물리 이동](./Unity_Class.md#rigidbody와-물리-이동)
- [충돌 감지 (Collision / Trigger)](./Unity_Class.md#충돌-감지)
- [Instantiate / Destroy / Invoke / InvokeRepeating](./Unity_Class.md#instantiate)
- [Update와 FixedUpdate 차이](./Unity_Class.md#update와-fixedupdate-차이)
- [Coroutine 기본 개념 및 사용](./Unity_Class.md#coroutine)

### C# 기본 문법
- [void와 반환형](./Unity_Class.md#void와-반환형)
- [if 문](./Unity_Class.md#if-문)
- [switch 문](./Unity_Class.md#switch-문)
- [for 문](./Unity_Class.md#for-문)
- [while 문](./Unity_Class.md#while-문)
- [중첩 while](./Unity_Class.md#중첩-while)
- [do-while 문](./Unity_Class.md#do-while-문)
- [배열 기본 개념](./Unity_Class.md#배열array)
- [배열 출력 / Length](./Unity_Class.md#배열-출력)
- [배열 선언 방법](./Unity_Class.md#배열-선언-방법)
- [배열 복사 / Clone / Sort / CopyTo / Clear](./Unity_Class.md#배열-복사)
- [배열 관련 표현 정리](./Unity_Class.md#배열-관련-자주-쓰는-표현-정리)
- [Partial](./Unity_Class.md#partial)


### 클래스와 객체지향
- [캡슐화(접근제한)](./Unity_Class.md#캡슐화접근제한)
    - [private](./Unity_Class.md#private)
    - [protected](./Unity_Class.md#protected)
    - [public](./Unity_Class.md#public)
- [상속](./Unity_Class.md#상속)
- [다형성](./Unity_Class.md#다형성)
    -  [abstract](./Unity_Class.md#abstract)
    - [virtual](./Unity_Class.md#virtual)
    - [override](./Unity_Class.md#override)

    



### 람다 / 델리게이트 / 제네릭
- [람다, 델리게이트, 캡처, 클로저](./Unity_Class.md#람다-델리게이트-캡처-클로저)
  - [델리게이트에 메서드 넣기](./Unity_Class.md#1-델리게이트에-메서드-넣기)
  - [메서드 대신 람다 넣기](./Unity_Class.md#2-메서드-대신-람다-넣기)
  - [인자 없는 람다와 인자 있는 람다](./Unity_Class.md#3-인자-없는-람다와-인자-있는-람다)
  - [Func와 반환값 있는 람다](./Unity_Class.md#4-func와-반환값-있는-람다)
  - [내부 함수와 델리게이트](./Unity_Class.md#5-내부-함수와-델리게이트)
  - [캡처와 클로저](./Unity_Class.md#6-캡처와-클로저)
  - [for문에서 캡처할 때 주의할 점](./Unity_Class.md#7-for문에서-캡처할-때-주의할-점)
  - [람다식과 람다문](./Unity_Class.md#8-람다식과-람다문)
  - [Predicate](./Unity_Class.md#9-predicate)
  - [람다 특성](./Unity_Class.md#10-람다-특성)
- [제네릭과 일반 클래스](./Unity_Class.md#제네릭과-일반-클래스)
  - [일반 클래스 A](./Unity_Class.md#1-일반-클래스-a)
  - [제네릭 메서드 `Print<T>`](./Unity_Class.md#2-제네릭-메서드-printt)
  - [제네릭 클래스 `B<T>`](./Unity_Class.md#3-제네릭-클래스-bt)
  - [제네릭 없이 `object`를 쓰는 클래스 `C`](./Unity_Class.md#4-제네릭-없이-object를-쓰는-클래스-c)
  - [`B<T>`와 `C` 비교](./Unity_Class.md#5-bt와-c-비교)

### 정규화 · 법선 벡터 · 내적
- [정규화 · 법선 벡터 · 내적](./Unity_Class.md#정규화--법선-벡터--내적)
    - [개념 연결](./Unity_Class.md#1-개념-연결)
    - [벡터(Vector2)](./Unity_Class.md#2-벡터vector2)
    - [벡터의 길이: magnitude와 sqrMagnitude](./Unity_Class.md#3-벡터의-길이-magnitude와-sqrmagnitude)
    - [기준값도 제곱해서 비교](./Unity_Class.md#기준값도-제곱해서-비교)
    - [정규화(Normalization)](./Unity_Class.md#4-정규화normalization)
    - [법선 벡터(Normal Vector)](./Unity_Class.md#5-법선-벡터normal-vector)
    - [Unity에서 법선 가져오기](./Unity_Class.md#6-unity에서-법선-가져오기)
    - [내적(Dot Product)](./Unity_Class.md#7-내적dot-product)
    - [내적 전에 정규화하는 이유](./Unity_Class.md#8-내적-전에-정규화하는-이유)
    - [입력 크기를 먼저 검사하는 이유](./Unity_Class.md#9-입력-크기를-먼저-검사하는-이유)
    - [벽 상태 진입에 적용](./Unity_Class.md#10-벽-상태-진입에-적용)
    - [벽 상태 종료에 적용](./Unity_Class.md#11-벽-상태-종료에-적용)
    - [방향 기준값 0.9의 주의점](./Unity_Class.md#12-방향-기준값-09의-주의점)
    
### FSM
- [FSM](./Unity_Class.md#1-fsm의-개념)
  - [FSM의 개념](./Unity_Class.md#1-fsm의-개념)
  - [FSM의 구성 요소](./Unity_Class.md#2-fsm의-구성-요소)
  - [FSM과 상태 패턴의 관계](./Unity_Class.md#3-fsm과-상태-패턴의-관계)
  - [상태의 기본 함수](./Unity_Class.md#4-상태의-기본-함수)
  - [상태 클래스의 공통 틀](./Unity_Class.md#5-상태-클래스의-공통-틀)
  - [FSM의 기본 구현](./Unity_Class.md#6-fsm의-기본-구현)
  - [상태 객체 준비와 제어 대상 연결](./Unity_Class.md#7-상태-객체-준비와-제어-대상-연결)
  - [최초 상태 등록](./Unity_Class.md#8-최초-상태-등록)
  - [상태 전환의 실행 순서](./Unity_Class.md#9-상태-전환의-실행-순서)
  - [같은 상태로 반복 전환하지 않는 이유](./Unity_Class.md#10-같은-상태로-반복-전환하지-않는-이유)
  - [Tick(dt)와 시간 전달](./Unity_Class.md#11-tickdt와-시간-전달)
  - [상태 선택과 상태 실행 분리](./Unity_Class.md#12-상태-선택과-상태-실행-분리)
  - [상태 진입 조건](./Unity_Class.md#13-상태-진입-조건)
  - [Enter와 Exit의 데이터 처리](./Unity_Class.md#14-enter와-exit의-데이터-처리)
  - [상태 종료 이유 구분](./Unity_Class.md#15-상태-종료-이유-구분)
  - [FSM과 실제 이동 처리의 차이](./Unity_Class.md#16-fsm과-실제-이동-처리의-차이)
  - [테스트 시 확인할 항목](./Unity_Class.md#17-테스트-시-확인할-항목)

