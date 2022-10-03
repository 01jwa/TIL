# **Iterator**

* Iterator, ListIterator, Enumeration은 모두 컬렉션에 저장된 요소를 접근하는데 사용되는 인터페이스이다.
* Enumeration은 Iterator의 구버젼이고, ListIterator는 Iterator의 기능을 향상 시킨 것이다.

---
<br>

## **Iterator**

* 컬렉션 프레임웍에서는 컬렉션에 저장된 각 요소에 접근하는 기능을 가진 Iterator 인터페이스를 정의하고, Collection 인터페이스에서 'Iterator'를 반환하는 `iterator()` 메서드를 정의하는 방식으로 컬렉션에 저장된 요소들을 읽어오는 방법을 표준화해 놓았다.
```java
public interface Iterator {
    boolean hasNext();
    Object next();
    void remove();
}

public interface Collection {
    ‥‥
    public Iterator iterator(); // Iterator를 구현한 클래스의 인스턴스를 반환하는 메서드
    ‥‥
}
```
* `iterator()` 메서드는 Collection 인터페이스에 정의되어 있으므로 Collection 인터페이스의 자손인 List와 Set에도 포함되어 있다.
* iterator 인터페이스의 메서드
    |메서드|설명|
    |---|---|
    |`boolean hasNext()`|읽어 올 요소가 남아있는지 확인한다. 있으면 true, 없으면 false 반환|
    |`Object next()`|다음 요소를 읽어 온다. `next()` 호출 전 `hasNext()`를 호출하여 요소가 있는지 확인하는 것이 안전하다.|
    |`void remove()`|`next()`로 읽어 온 요소를 삭제한다. `next()` 다음에 호출해야 한다.|

* Iterator 사용 예시
    - List 클래스들은 저장순서를 유지하므로 Iterator로 읽어도 저장 순서가 바뀌지 않지만 <br> Set 클래스들은 순서 유지가 안 되기 때문에 Iterator를 사용하여도 저장된 순서와 같지 않다.
    ```java
    import java.util.*;

    class IteratorTest {
        public static void main(String[] args) {
            ArrayList list = new ArrayList(); // ArrayList 생성

            list.add("1");
            list.add("2");
            list.add("3");

            Iterator it = list.iterator();

            while(it.hasNext()) {   // while문과 hasNext()를 통해 요소가 남아있을 때까지 출력
                Object obj = it.next();
                System.out.println(obj);
            }
        }
    }
    ```

---
<br>

## **ListIterator와 Enumeration**

* Enumeration은 컬렉션 프레임웍이 만들어지기 이전에 사용하던 것으로 가능하면 Iterator를 쓰는 것이 좋다.

* ListIterator는 Iterator를 상속받아 기능을 추가한 것으로 Iterator는 요소에 접근할 때 단방향으로만 이동하지만 <br> ListIterator는 양방향으로의 이동이 가능하다. 하지만 List 인터페이스를 구현한 컬렉션에서만(ArrayList, LinkedList) 사용할 수 있다.


* ListIterator의 메서드
    - Iterator 인터페이스에 있는 메서드는 생략하였다.

    |메서드|설명|
    |---|---|
    |`void add(Object o)`|컬렉션에 새로운 객체(o)를 추가한다.|
    |`boolean hasPrevious()`|읽어 올 이전 요소가 남아있는지 확인한다. 있으면 true, 없으면 false 반환|
    |`Object previous()`|이전 요소를 읽어 온다. `previous()` 호출 전 `hasNext()`를 호출하여 요소가 있는지 확인하는 것이 안전하다.|
    |`int nextIndex()`|다음 요소의 index를 반환한다.|
    |`int previousIndex()`|이전 요소의 index를 반환한다.|
    |`void set(Object o)`|`next()` 또는 `previous()`로 읽어 온 요소를 지정된 객체(o)로 변경한다. 반드시 `next()`, `previous()`를 먼저 호출한 후에 이 메서드를 호출해야 한다.|

* ListIterator 사용 예시
    ```java
    import java.util.*;

    class ListIteratorTest {
        public static void main(String[] args) {
            ArrayList list = new ArrayList();

            list.add("1");
            list.add("2");
            list.add("3");

            ListIterator it = list.listIterator();

            while (it.hasNext()) {
                System.out.print(it.next());  // 순방향으로 진행하면서 읽어온다.
            }
            System.out.println();             // 실행결과 --- 123

            while (it.hasPrevious()) {
                System.out.print(it.previous());  // 역방향으로 진행하면서 읽어온다.
            }
            System.out.println();                 // 실행결과 --- 321 
        }
    }
    ```
