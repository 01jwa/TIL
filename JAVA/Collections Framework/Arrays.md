# **Arrays**

* Arrays 클래스에는 배열을 다루는데 유용한 메서드가 정의되어 있다.

* Arrays에 정의된 메서드는 모두 **`static`** 메서드이다.
    > ✔ &nbsp;객체를 생성하지 않고도 사용할 수 있다. <br>
    > ✔ &nbsp;`java.util` 패키지에 포함되므로 반드시 `import`문으로 불러와야만 한다.

---
<br>

## Arrays 클래스 메서드
* [`copyOf()`, `copyOfRange()`](#copyof-copyofrange) <br>
* [`fill()`, `setAll()`](#fill-setall) <br>
* [`sort()`, `binarySearch()`](#sort-binarysearch) <br>
* [`equals()`, `toString()`](#equals-tostring) <br>
* [`asList(Object... a)`](#aslistobject-a)

---
<br>
## **`copyOf()`, `copyOfRange()`**

* `copyOf()`는 배열 전체를, `copyOfRange()`는 배열의 일부를 복사해서 새로운 배열을 만들어 반환한다.
```java
int[] arr = {0,1,2,3,4};
int[] arr2 = Arrays.copyOf(arr, arr.length);  // arr2 = [0,1,2,3,4]
int[] arr3 = Arrays.copyOf(arr, 7);           // arr3 = [0,1,2,3,4,0,0]
int[] arr4 = Arrays.copyOfRange(arr, 2, 4);   // arr4 = [2,3]
int[] arr5 - Arrays.copyOfRange(arr, 0, 7);   // arr5 = [0,1,2,3,4,0,0]
```
---
<br>

## **`fill()`, `setAll()`**

* `fill()`은 배열의 모든 요소를 지정된 값으로 채운다. `setAll()`은 배열을 채우는데 사용할 함수형 인터페이스를 매개변수로 받는다.
* `setAll()`을 호출할 때는 함수형 인터페이스를 구현한 객체를 매개변수로 지정하던가 람다식을 지정해야한다.

```java
int[] arr = new int[5];
Arrays.fill(arr, 9);    // arr = [9,9,9,9,9]

Arrays.setAll(arr, () -> (int)(Math.random() * 5) + 1);
```
---
<br>

## **`sort()`, `binarySearch()`**

* `sort()`는 배열을 정렬할 때, `binarySearch()`는 배열에 저장된 요소를 검색할 때 사용한다.
* `binarySearch()`는 배열에서 지정된 값이 저장된 위치(index)를 찾아서 반환하는데, 반드시 배열이 **정렬된** 상태이어야 올바른 결과를 얻을 수 있다. 그리고 만약 검색한 값과 같은 요소가 여러 개 있다면, 어떤 것의 위치가 반환될지는 알 수 없다.

```java
int[] arr = {2, 3, 0, 4, 1};
int idx = Arrays.binarySearch(arr, 2); // 잘못된 결과를 얻는다.

Arrays.sort(arr); // 배열 arr을 정렬한다.
System.out.println(Arrays.toString(arr)); // [0, 1, 2, 3, 4]
int idx = Arrays.binarySearch(arr, 2); // idx = 2 / 올바른 결과
```

---
<br>

## **`equals()`, `toString()`**

* `toString()` 메서드는 배열의 모든 요소를 문자열로 출력해준다.
* `toString()`은 일차원 배열에만 사용할 수 있으며, 다차원 배열의 경우 `deepToString()` 메서드를 사용해야 한다.

```java
int[] arr = {0, 1, 2, 3};
int[][] arr2 = {{11,12}, {21,22}};

System.out.println(Arrays.toString(arr));       // [0, 1, 2, 3]
System.out.println(Arrays.deepToString(arr2));  // [[11,12], [21,22]] 
```

* `equals()`는 두 배열에 저장된 모든 요소를 비교하여 같으면 `true`, 다르면 `false`를 반환한다.
* `equals()` 또한 일차원 배열에만 사용할 수 있으며, 다차원 배열의 비교에는 `deepEquals()`를 사용해야한다.

```java
String [][] str1 = new String[][] {{"aa", "bb"}, {"cc", "dd"}};
String [][] str2 = new String[][] {{"aa", "bb"}, {"cc", "dd"}};

System.out.println(Arrays.equals(str1, str2)); // false
System.out.println(Arrays.deepEquals(str1, str2)); // true
```

---
<br>

## **`asList(Object... a)`**

* `asList()`는 배열을 `List`에 담아서 반환한다.
* 매개변수의 타입이 가변인수라서 배열 생성 없이 저장할 요소들만 나열하는 것도 가능하다.
* `asList()`가 반환한 `List`의 크기는 변경할 수 없다. 즉 추가와 삭제가 불가능하며, 저장된 내용은 변경가능하다.

```java
List list = Arrays.asList(new Integer[] {1,2,3,4}); // list = [1, 2, 3, 4]
List list = Arrays.asList(1,2,3,4);                 // list = [1, 2, 3, 4]

list.add(6); // UnsupportedOperationException 예외 발생
```
