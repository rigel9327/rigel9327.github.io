---
layout: single
title: "<자바의 정석 Chap12> Generics, enums, annotation"
categories: JAVA
tag: [java, blog, jekyll]
toc: true
toc_sticky: true
toc_label: 목차
author_profile: false
sidebar:
    nav: "counts"
---

**[공지사항]** [Rigel 신규 업데이트](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)
{: .notice--warning}

<div class="notice--success">
<h4>공지사항입니다.</h4>
<ul>
    <li>공지사항 순서 1</li>
    <li>공지사항 순서 2</li>
    <li>공지사항 순서 3</li>
</ul>
</div>

***
<h2>1. 지네릭스(Generics)</h2>
***
  - Java5부터 추가된 지네릭스(Generics);
  - 다양한 타입의 객체를 다루는 메서드나 컬렉션 클래스에 
  - **컴파일 시의 타입체크(compile-time type check)를 해주는 기능**

  <h3>1. 지네릭스란?</h3>
  - 런타임시 발생할 에러를 컴파일 타임으로 끌어온다 -> 미리 알고 고침
  - 컴파일시 타입을 체크해주는 기능
  - 객체의 타입 안정성을 높이고, 형변환의 번거로움을 줄여줌

  <h3>2. 지네릭스 클래스 선언</h3>       
  - 일반 컬렉션 클래스의 경우     
  - 'list'에는 'String' 타입의 요소가 저장되어 있지만 
    - 'list'는 'List'타입으로 선언되어 있어서 'Object'타입의 객체를 저장할 수 있다.
    - 'get'메서드로 요소를 꺼낼 경우, 반환되는 객체는 'Object'타입이므로,  다시 'String'타입으로 형변환 필요하다.

  ```java
  list list = new ArrayList();
  list.add("hello");
  String str = (String) list.get(0);
  ```

  - 지네릭스를 이용하는 경우
  - 'List'에 저장된 객체의 타입이 'String'으로 제한되기 때문에, 
    - 'get'메서드로 요소를 꺼내면 바로 'String'타입으로 반환할 수 있다.

  ```java
  List<String> list = new ArrayList<String>();
  list.add("hello");
  String str = list.get(0);
  ```
   
  <h3>3. 와일드카드</h3>
  - 지네릭스에서 매개변수 타입으로 사용되는 특별한 기호
  - 다양한 유연성과 지네릭 타입의 호환성을 지원하기 위해 사용된다.
  - 크게 세 가지 형태로 사용
    1. '<?>' : 비한정 와일드카드(Unbounded Wildcard)
    - 모든 타입을 나타내는 와일드카드
    - 실제 타입을 알 수 없는 경우 사용된다.
    - ex. 'List<?>'는 어떤 타입의 리스크라도 받을 수 있다.
    - but. 'List<'Object'>'와는 다르다, 'Object'와 그 하위 타입만 받을 수 있음
<br>
    2. '<? extend 상위타입>' : 상한 경계 와일드카드(Upper Bounded Wildcard)
    - 특정 상위 타입의 서브타입들을 나타내는 와일드카드
    - 상위 타입과 그 하위 타입만 받을 수 있다.
    - ex. 'List<? extend Number>'는 Number 타입과 Number의 하위 타입들을 받을 수 있다.
    - 즉, 'List<"Integer">'나 'List<"Double">'과 같은 타입을 받을 수 있다.
<br>
    3. '<? super 하위타입>' : 하한 경계 와일드카드(Lower Bounded Wildcard)
    - 특정 하위 타입의 상위 타입들을 나타내는 와일드 카드
    - 하위 타입과 그 상위 타입만 받을 수 있다.
    - ex. 'List<? super Integer>'는 'Integer' 타입과 'Integer'의 상위 타입들을 받을 수 있다.
    - 즉, 'List<"Integer">'나 'List<"Object">'와 같은 타입을 받을 수 있다.
<br>

***
<h2>2. 열거형(Enum)</h2>
***

  <h3>1. 열거형(Enum)이란?</h3>
  - 서로 연관된 상수들의 집합을 정의하는 기능
  - **Java는 타입에 안전한(값 & 타입 체크) 열거형을 제공**

  <h3>2. 열거형의 정의와 사용</h3>
  - 'enum' 키워드를 사용
  - 열거형의 각 상수들은 열거형의 타입으로 간주된다.
    - ('Weekday'타입의 변수에는 'MONDAY', 'TUESDAY' 등의 상수 대입 가능)

  ```java
  enum Weekday {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
  }
  ```

***
<h2>3. 애너테이션(Annotation)</h2>
***

  <h3>1. 에너테이션이란?</h3>
    - 주석처럼 프로그래밍언어에 영향을 미치지 않으며, 유용한 정보를 제공
    - 에너테이션은 '@' 기로를 이용하여 표기한다.

  <h3>2. 표준 애너테이션</h3>
    - 자바에서 기본적으로 제공해주는 애너테이션들

```java
    @Deprecated
    public void oldMethod() {
      // 이전 버전에서 사용되던 메서드나 클래스가 더 이상 사용되지 않는 것을 나타냄
    }    
```

 ```java
    @Override
    public void someMethod() {
      // 오버라이딩된 메서드가 부모 클래스에 있는 메서드를 오버라이딩하는지 검사
    }
```

    - 에너테이션은 개발자가 직접 정의할 수도 있다.

```java
    @Test
    public void testMethod() {
      // 테스트 메서드임을 나타낼 수 있다.
    }
```

    - 리플렉션(Reflection)을 이용하여 실행 중에도 정보를 추출할 수 있다.

```java
    @SuppressWarnings("deprecation")
    public void someMethod() {
      oldMethod(); // 경고 메세지 출력
      // 더 이상 사용되지 않는 메서드를 실행할 때 경고 메세지를 출력할 수 있다,
    }
```
