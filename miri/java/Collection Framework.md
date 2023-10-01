## Collection Framework

컬렉션 프레임워크란?

```
다수의 데이터 그룹을 저장하는 자료 구조와, 데이터를 처리하는 알고리즘을 클래스로 구현해 놓은 것
```

> List와 Set 인터페이스는 공통적으로 Collection 인터페이스를 상속받는다

> 클래스 내에서 사용할 데이터 타입을 미리 지정하여 사용한다

`List<E>`

- 순서가 있는 데이터의 집합을 처리할 때 사용하는 인터페이스

- 데이터들의 중복을 허용

`Set<E>`

- 순서가 없는 데이터의 집합을 처리할 때 사용하는 인터페이스

- 데이터들의 중복을 허용하지 않음

`Map<K, V>`

- 키와 값(Key, value) 의 한 쌍으로 이루어진 데이터의 집합을 처리할 때 사용하는 인터페이스

- 키를 바탕으로 데이터 값을 검색하기 때문에, 키는 중복을 허용하지 않지만 값은 중복될 수 있음

- 순서가 없음

---

#### List 와 Array 의 차이

List

- 데이터를 빈틈없이 적재한다
- 원시데이터 타입을 저장할 수 없다
- 추가, 검색, 수정 및 삭제등 다양한 기능을 하는 메서드를 제공한다

Array

- 배열의 크기가 고정되어있기 때문에 배열의 빈 공간만큼 메모리가 낭비되는 경우가 생긴다
- 원시데이터 타입과, 객체 등을 모두 저장할 수 있다

---

#### List 와 ArrayList 의 차이

List(배열)

- 초기화시 배열의 크기가 정해지고, 변경될 수 없다
- 인덱스가 존재하여 인덱스값으로 값을 꺼낸다
- 데이터의 삽입/삭제시 매번 메모리를 재할당 하기때문에 속도가 느리다
- 다차원 배열로 사용이 가능하다
- 크기 값을 length로 식별

ArrayList(리스트)

- 초기화시 리스트의 크기를 선언하지 않고, 필요에 따라 변한다
- 식별자가 없다(인덱스)
- 크기 값을 size로 식별

##### 사용 예제

```java
//ArrayList
ArrayList<Integer> arryList = new ArrayList<>();

//List
int[] array = new int[3];
```

---

컬렉션 클래스란?

```
컬렉션 프레임워크의 3가지의 핵심 인터페이스를 기반으로
각 인터페이스를 상속받아 기능을 구현해놓은 것
```

각 클래스마다 정렬, 섞기, 검색등의 기능을 하는 메서드들을 가진다

### List

- null 값을 저장할 수 있다
- 값을 넣는 순서대로 저장한다
- 값을 꺼낼 때 숫자 인덱스를 사용하여 꺼낸다

> 아래 기능을 사용하면 List에 저장된 값들에 대해 특정 기준에 따라 순차적으로 정렬해줄 수 있다
>
> > Collections.sort(list name);

        오름차순으로 정렬, 대문자가 우선순위가 높음

> > Collections.sort(list name, Collections.reverseOrder());

        내림차순으로 정렬

> > Collections.sort(list name, String.CASE_INSENSITIVE_ORDER);

        대소문자 구분 없이 오름차순으로 정렬

> > Collections.sort(list name, Collections.reverseOrder(String.CASE_INSENSITIVE_ORDER));

        대소문자 구분 없이 내림차순으로 정렬

예)

`ArrayList`, `LinkedList`

### Set

- 인스턴스의 해시값을 기준으로 저장되기때문에 순서가 없다
- 순서가 없는 집합이기 때문에 값을 중복 저장할 수 없고, 숫자 인덱스로 값을 꺼낼수도 없다

예)

`HashSet`, `TreeSet`

### Map

- 중복되지 않은 키를 바탕으로 값을 저장한다 (키와 값이 한 쌍으로 저장)
- 키값을 바탕으로 value 값을 꺼낸다

예)

`HashMap`, `TreeMap`, `Hashtable`

---

#### Stack

```
List의 Vector 클래스를 상속받는, LIFO(Last In First Out, 후입선출) 구조의 자료구조 클래스
```

- top의 위치에 따라 데이터를 쌓는다

`push` 값을 넣는 순서대로 쌓는 것

`pop` 최근에 push한 순서대로 값을 빼는 것

#### Queue

```
FIFO(First In First Out, 선입선출) 형식의 자료구조로, 인터페이스 형식이다
```

- 한 쪽(rear)에서만 삽입이 이루어지고, 반대쪽(front)에서는 삭제만 이루어진다

`enqueue` 큐에 자료를 넣는 것

`dequeue` 넣어둔 자료부터 순서대로 꺼내는 것
