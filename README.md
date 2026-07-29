# Unity / C# 개념 정리

## 목차

### Unity 기본
- [Unity 기본 / MonoBehaviour](#unity-기본)
- [생명주기 함수 (Awake / Start / Update / FixedUpdate)](#생명주기-함수)
- [오브젝트와 컴포넌트 찾기](#오브젝트와-컴포넌트-찾기)
- [transform과 이동](#transform)
- [Rigidbody와 물리 이동](#rigidbody와-물리-이동)
- [충돌 감지 (Collision / Trigger)](#충돌-감지)
- [Instantiate / Destroy / Invoke / InvokeRepeating](#instantiate)
- [Update와 FixedUpdate 차이](#update와-fixedupdate-차이)
- [Coroutine 기본 개념 및 사용](#coroutine)

### C# 기본 문법
- [void와 반환형](#void와-반환형)
- [if 문](#if-문)
- [switch 문](#switch-문)
- [for 문](#for-문)
- [while 문](#while-문)
- [중첩 while](#중첩-while)
- [do-while 문](#do-while-문)
- [배열 기본 개념](#배열array)
- [배열 출력 / Length](#배열-출력)
- [배열 선언 방법](#배열-선언-방법)
- [배열 복사 / Clone / Sort / CopyTo / Clear](#배열-복사)
- [배열 관련 표현 정리](#배열-관련-자주-쓰는-표현-정리)

### 람다 / 델리게이트 / 제네릭
- [람다, 델리게이트, 캡처, 클로저](#람다-델리게이트-캡처-클로저)
  - [델리게이트에 메서드 넣기](#1-델리게이트에-메서드-넣기)
  - [메서드 대신 람다 넣기](#2-메서드-대신-람다-넣기)
  - [인자 없는 람다와 인자 있는 람다](#3-인자-없는-람다와-인자-있는-람다)
  - [Func와 반환값 있는 람다](#4-func와-반환값-있는-람다)
  - [내부 함수와 델리게이트](#5-내부-함수와-델리게이트)
  - [캡처와 클로저](#6-캡처와-클로저)
  - [for문에서 캡처할 때 주의할 점](#7-for문에서-캡처할-때-주의할-점)
  - [람다식과 람다문](#8-람다식과-람다문)
  - [Predicate](#9-predicate)
- [제네릭과 일반 클래스](#제네릭과-일반-클래스)
  - [일반 클래스 A](#1-일반-클래스-a)
  - [제네릭 메서드-printt](#2-제네릭-메서드-printt)
  - [제네릭 클래스-bt](#3-제네릭-클래스-bt)
  - [제네릭 없이-object를-쓰는-클래스-c](#4-제네릭-없이-object를-쓰는-클래스-c)
  - [bT와-c-비교](#5-bt와-c-비교)

---

## Unity 기본

