# **[JAVA] Comparator, Comparable**

## **`Comparator`, `Comparable` 는 왜 필요한가?**

<br>

```java
public class Test {
    public static void main(String[] args) {

        int a = 10;
        int b = 6;

        if (a > b) {
            System.out.println("a는 b보다 크다.");
        } else if (a == b) {
            System.out.println("a와 b는 같다.");
        } else if (a < b>) {
            System.out.println("a는 b보다 작다.");
        }
    }
}
```
* 위의 코드처럼 `java`에서 primitive type의 경우 부등호로 쉽게 비교가 가능하다. <br><br> 하지만 객체의 경우 기본 자료형처럼 부등호로 비교하기 어렵다.

```java
class Person {
    int age;
    String name;

    Person(int age, String name) {
        this.age = age;
        this.name = name;
    }
}

public class Main {
    public static void main(String[] args) {

        Person p1 = new Person(15, "김00");
        Person p2 = new Person(24, "이00");
    }
}
```

* 위의 코드에서 두 객체 p1, p2를 어떻게 구분할 수 있는가에 대한 문제가 발생한다. 만약 비교한다면 나이를 기준으로 구분하는지, 아니면 이름을 기준으로 구분하는지 와 같은 문제가 생기게 된다.
  
* 이 때, 두 객체를 비교하기 위해서 `Comparator`, `Comparable`이 쓰이게 되는 것이다.

---
<br>

## **`Comparator`, `Comparable`**

* `Comparator`와 `Comparable`은 모두 인터페이스로 컬렉션을 정렬하는데 필요한 메서드를 정의하고 있다.
  
* 즉, `Comparator`나 `Comparable`을 사용하려면 해당 인터페이스 내에 선언된 메서드를 반드시 **'구현'** 해야만 한다.
  
* `Comparable`은 `java.lang` 패키지에 있고, `Comparator`는 `java.util` 패키지에 있다.
    ```java
    public interface Comparator {
        int compare(Object o1, Object o2);
        boolean equals(Object obj);
    }

    public interface Comparable {
        public int compareTo(Object o);
    }
    ```
<div align=center>▲ Comparator와 Comparable의 실제 소스</div>

<br>

* `compareTo()`의 반환값은 실제로는 비교하는 두 객체가 같으면 0, 비교하는 값보다 작으면 음수, 크면 양수를 반환하도록 구현해야 한다.
  
* `compare()`도 마찬가지로 구현해야 함.

    > `Comparable` → 기본 정렬기준을 구현하는데 사용 <br>
    > `Comparator` → 기본 정렬기준 외에 다른 기준으로 정렬할 때 사용

---
<br>

## **`Comparable`**

* `compareTo(Object o)` 메서드는 매개변수가 1개로 **자기 자신과 매개변수 객체를 비교** 한다.

* 사용하려면 `compareTo` 메서드를 반드시 구현해야만 한다.

```java
class Person implements Comparable {
    int age;
    String name;

    Person(int age, String name) {
        this.age = age;
        this.name = name;
    }

    @override
    public int compareTo(Person o) {

        // 자기 자신의 age가 o의 age보다 크면 양수
        if (this.age > o.age) {
            return 1;
        }
        // 자기 자신의 age가 o의 age와 같다면 0
        else if (this.age == o.age) {
            return 0;
        }
        // 자기 자신의 age가 o의 age보다 작다면 음수
        else if (this.age < o.age>) {
            return -1;
        }
    }

    // 위의 compareTo() 메서드를 더 단순하게 쓸 수도 있다.

    @override
    public int compareTo(Person o) {

        return this.age - o.age;

        /* 자신의 age가 o의 age보다 크다면 양수, 같다면 0,
        *  작다면 음수를 반환할 것이다.
        *
        *  하지만, 위의 식을 이용할 때 자료형의 범위를 넘어가게 되는 경우가 생기면,
        *  (Underflow나 Overflow가 생기면) 비교값이 잘못될 수 있다.
        *  그렇기에 위와 같은 예외를 확인하기 어려운 경우, 부등호를 통한 대소비교를 해주는 것이 안전하다.
        */
    }
}
```
---
<br>

## **`Comparator`**

* `Compare(Object o1, Object 02)` 메서드는 매개변수가 2개로, **두 매개변수 객체를 비교** 한다.
  
* 사용하려면 `compare` 메서드를 반드시 구현해야만 한다.

```java
class Person implements Comparable {
    int age;
    String name;

    Person(int age, String name) {
        this.age = age;
        this.name = name;
    }

    @override
    public int compare(Person o1, Person o2) {

        // o1의 age가 o2의 age보다 크다면 양수
		if(o1.age > o2.age) {
			return 1;
		}
		// o1의 age가 o2의 age와 같다면 0
		else if(o1.age == o2.age) {
			return 0;
		}
		// o1의 age가 o2의 age보다 작다면 음수
		else {
			return -1;
		}
    }

    // ComparaTo()와 같이 단순하게 쓸 수도 있다.

    @override
    public int compare(Person 01, Person 02) {

        return o1.age - o2.age;

        /*
        * CompareTo()의 경우처럼 리턴값이 자료형의 범위를 넘어가게 되면
        * Overflow 또는 Underflow가 발생하여 잘못된 결과를 얻게 된다.
        */
    }
```

---
<br>

## **예시**

```java
import java.util.*;  // Comparator는 java.util. 패키지에 있어 import 해주어야 한다.

class ComparatorTest {
    public static void main(String[] args) {
        String[] strArr = {"melon", "apple", "pear", "Banana"};

        Arrays.sort(strArr); // String의 Comparable 구현에 의한 정렬
        System.out.println("strArr= " + Arrays.toString(strArr));
        // 결과 --- strArr= [Banana, apple, melon, pear]

        Arrays.sort(strArr, String.CASE_INSENSITIVE_ORDER); // 대소문자 구분 X
        System.out.println("strArr= " + Arrays.toString(strArr));
        // 결과 --- strArr = [apple, Banana, melon, pear]

        Arrays.sort(strArr, new Descending()); // 역순 정렬
        System.out.println("strArr= " + Arrays.toString(strArr));
    }
}

class Descending implements Comparator {
    public int compare(Object o1, Object o2) {
		if (o1 instanceof Comparable && o2 instanceof Comparable) {
			Comparable c1 = (Comparable)o1;
			Comparable c2 = (Comparable)o2;
			
			return c1.compareTo(c2) * -1; // -1을 곱해서 기본 정렬방식의 역으로 변경한다.
            // 또는 c2.compareTo(c1)과 같이 순서를 바꿔도 된다.
		}
		return -1;
	}

}
```

<br>

* `Arrays.sort()`는 배열을 정렬할 때, `Comparator`를 지정해주지 않으면 저장하는 객체에 구현된 내용에 따라 정렬된다.
    - `static void sort(Object[] a) // 객체 배열에 저장된 객체가 구현한 Comparable에 의한 정렬`
    - `static void sort(Object[] a, Comparator c) // 지정한 Comparator에 의한 정렬` 

<br>

* `String`의 `Comparable` 구현은 문자열이 사전 순으로 정렬되도록 작성되어 있다.
    - 정확히는 문자의 **유니코드**의 순서가 작은 값에서부터 큰 값으로 정렬된다.
* 또한 `String`은 대소문자를 구분하지 않고 비교하는 `Comparator`를 상수의 형태로 제공한다.
    ```java
    public static final Comparator CASE_INSENSITIVE_ORDER

    Arrays.sort(strArr, String.CASE_INSENSITIVE_ORDER); // 대소문자 구분없이 정렬
    ```

