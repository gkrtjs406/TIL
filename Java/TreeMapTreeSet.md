# TreeSet / TreeMap

컬렉션 프레임 워크는 검색 기능을 강화시킨 TreeSet과 TreeMap을 제공하고 있다. 이 컬렉션들은 이진 트리(binary tree)를 이용해서 계층적 구조(Tree 구조)를 가지면서 객체를 저장한다.

------------------------

### 이진 트리 구조

여러개의 노드가 트리 형태로 연결된 구조로, 루트 노드라고 불리는 하나의 노드에서부터 시작해 각 노드에 최대 2개의 노드를 연결할 수 있는 구조를 가지고 있다.첫번째로 저장되는 값은 루트 노드가 되고, 두번째 부터는 값의 크기를 비교해 트리를 만들며 내려간다. 작은 값은 왼쪽에, 큰 값은 오른쪽에 저장한다.

-> 이진 트리가 범위 검색을 쉽게 할 수 있는 이유는 값들이 정렬되어 있어 그룹핑이 쉽기 때문이다

![이진트리구조](C:\Users\COM\Desktop\이진트리구조.PNG)



## TreeSet

이진 트리를 기반으로한 Set 컬렉션이다. 객체를 저장하면 자동으로 정렬되는데 부모값과 비교해서 낮은 것은 왼쪽 자식 노드에, 높은 것은 오른쪽 자식 노드에 저장한다.

```java
//생성시 저장할 객체 타입을 파라미터로 표기하고,
// 기본 생성자를 호출하면 된다
TreeSet<E> treeset = new TreeSet<E>();
```

![treeset 검색 관련 메소드](C:\Users\COM\Desktop\treeset 검색 관련 메소드.PNG)

```java
TreeSet<Integer> num = new TreeSet<Integer>();
		
// set 값 넣기
num.add(10);
num.add(8);
num.add(9);
num.add(20);
num.add(45);
num.add(0);
		
int number = num.first();
System.out.println("제일 낮은 객체(숫자)를 리턴 : " + number); // 결과 0
System.out.println("---------------------------");
		
number = num.last();
System.out.println("제일 높은 객체(숫자)를 리턴 : " + number); // 결과 45
System.out.println("---------------------------");
		
number = num.lower(30);
System.out.println("30점보다 작은 점수 중 가장 가까운 수를 리턴 : " + number); // 결과 20
// 만약 가장 작은수를 lower로 넣으면? = 에러

System.out.println("----------------------------");
		
number = num.higher(20);
System.out.println("20점보다 높은 점수 : " + number); // 결과 45
// 만약에 가장 높은 수를 higher에 넣으면? = 에러남

System.out.println("----------------------------");
		
number = num.floor(20);
System.out.println("20이랑 똑같은 수가 있으면 그거 가져오고, 아니면 바로 아래의 값 리턴 : " + number); // 결과 20
System.out.println("----------------------------");
		
number = num.ceiling(0);
System.out.println("0이랑 똑같은 수 있으면 그거 가져오고, 아니면 바로 위 값 리턴 : " + number); // 결과 0
System.out.println("----------------------------");
		
System.out.println("현재 num의 사이즈 : " + num.size()); // 결과 6
number = num.pollFirst(); // 제거한 값 0
System.out.println("가장 높은 값을 읽고 제거.제거한 값 : " + number); // 결과 0
System.out.println("제거하고 난 뒤 num 사이즈 : " + num.size()); // 결과 5
```

#### 정렬관련 메소드

![treeset 검색 관련 메소드2](C:\Users\COM\Desktop\treeset 검색 관련 메소드2.PNG)

1. descendingIterator()
2. descendingSet()
   - descendingSet()은 두번하면 올림차순이 된다 

```java
TreeSet<Integer> num = new TreeSet<Integer>();
		
// set 값 넣기
num.add(10);
num.add(8);
num.add(9);
num.add(20);
num.add(45);
num.add(0);
		
// 내림차순으로 출력합시다 1
Iterator<Integer> it = num.descendingIterator();
while(it.hasNext()) {
	Integer ss = it.next();
	System.out.println(ss); // 결과: 45 20 10 9 8 0
}
System.out.println("-----------");
		
	
// 내림차순으로 출력합시다 2
NavigableSet<Integer> ds = num.descendingSet();
it = ds.iterator();
while(it.hasNext()) {
	Integer ss = it.next();
	System.out.println(ss); //결과: 45 20 10 9 8 0
}
System.out.println("-----------");
	
// 올림차순은 내림차순을 두번 
ds = ds.descendingSet();
it = ds.iterator();
while(it.hasNext()) {
	Integer ss = it.next();
	System.out.println(ss); //결과: 0 8 9 10 20 45
}
System.out.println("-----------");
```

#### 범위관련 메소드

![treeset 검색 관련 메소드3](C:\Users\COM\Desktop\treeset 검색 관련 메소드3.PNG)

```java
TreeSet<Integer> ts = new TreeSet<Integer>();

ts.add(100);
ts.add(95);
ts.add(85);
ts.add(90);
ts.add(80);

// x < 90
// 90보다 작은객체 출력
SortedSet<Integer> a90 = ts.headSet(90);
Iterator<Integer> it = a90.iterator();
while (it.hasNext()) {
	System.out.print(it.next() + " "); //결과 80 85
}
System.out.println("\n--------------------------");
		
	
// x <= 90
// 90 도 포함해서 90보다 작은 객체들 모두
SortedSet<Integer> b90 = ts.headSet(90, true);
it = b90.iterator();
while(it.hasNext()) {
	System.out.print(it.next() + " "); //결과 80 85 90
}
System.out.println("\n--------------------------");
		
		
// 85 < x
SortedSet<Integer> a85 = ts.tailSet(85);
it = a85.iterator();
while(it.hasNext()) {
	System.out.print(it.next() + " "); //결과 85 90 95 100
}
System.out.println("\n--------------------------");
		
		
// 85 <= x
SortedSet<Integer> b85 = ts.tailSet(85,true);
it = b85.iterator();
while(it.hasNext()) {
	System.out.print(it.next() + " "); //결과 85 90 95 100
}
System.out.println("\n--------------------------");
		
		
// 85 < x < 95
SortedSet<Integer> a8595 = ts.subSet(85, false, 95, false);
it = a8595.iterator();
while(it.hasNext()) {
	System.out.print(it.next() + " "); //결과 90
}
System.out.println("\n--------------------------");
		
		
// 85 <= x <= 95
SortedSet<Integer> b8595 = ts.subSet(85, true, 95, true);
it = b8595.iterator();
while(it.hasNext()) {
	System.out.print(it.next() + " "); //결과 85 90 95
}
System.out.println("\n--------------------------");
```



## TreeMap

TreeSet과의 차이점은 키와 값이 저장된 Map.Entry를 저장한다는 점이다.

TreeMap에 객체 저장하면 자동으로 정렬되는데, 기본적으로 부모 키값과 비교해서 키 값이 낮은 것은 왼쪽 자식 노드에, 키 값이 높은 것은 오른쪽 자식 노드에 Map.Entry 객체를 저장한다.

다음은 TreeMap이 가지고 있는 검색 관련 메소드들이다

![treemap 검색 관련 메소드](C:\Users\COM\Desktop\treemap 검색 관련 메소드.PNG)

```java
// 키로 점수를 넣고
// 값으로 이름을 넣음
TreeMap<Integer, String> scores = new TreeMap<Integer, String>();
	
// TreeMap은 값 넣어줄때 put 사용
// 값은 중복될 수 있지만, 키는 중복 xxx
scores.put(new Integer(87), "홍길동");
scores.put(new Integer(98), "이동수");
scores.put(new Integer(75), "박길순");
scores.put(new Integer(95), "신용권");
scores.put(new Integer(80), "김자바");
		
// firstEntry 해보기
// 제일 낮은 Map.Entry를 리턴
Entry<Integer, String> result1 = scores.firstEntry();
System.out.println("가장 낮은 점수 : " + result1.getKey() + "점\t\t학생명 : " + result1.getValue()); //결과 75점 박길순
	
		
// lastEntry()
// 제일 높은 Map.Entry를 리턴
Entry<Integer, String> result2 = scores.lastEntry();
System.out.println("가장 높은 점수 : " + result2.getKey() + "점\t\t학생명 : " + result2.getValue()); //결과 98점 이동수
		
		
// lowerEntry(K Key)
// 주어진 키보다 바로 아래 Map.Entry를 리턴
// x < 90
Entry<Integer, String> result3 = scores.lowerEntry(90);
System.out.println("90 보다 바로 아래 점수 : " + result3.getKey() + "점\t학생명 : " + result3.getValue()); //결과 87점 홍길동
		
		
// higherEntry(K Key)
// 주어진 키보다 바로 위 Map.Entry를 리턴
// x > 80
Entry<Integer, String> result4 = scores.higherEntry(80);
System.out.println("80보다 바로 위 점수 : " + result4.getKey() + "점\t학생명 : " + result4.getValue()); //결과 87점 홍길동
		
		
// floorEntry(K Key)
// 주어진 키와 동등한 키 있으면 해당 Map.Entry를 리턴, 없다면 바로 아래의 Map.Entry리턴
// x <= 90
Entry<Integer, String> result5 = scores.floorEntry(90);
System.out.println("x <= 90 : " + result5.getKey() + "점\t\t학생명 : " + result5.getValue()); //결과 87점 홍길동
		
		
// ceilingEntry(K Key)
// 주어진 키와 동등한 키 있으면 해당 Map.Entry리턴 없다면 바로 위 Map.Entry 리턴
// x >= 80
Entry<Integer, String> result6 = scores.ceilingEntry(90);
System.out.println("x >= 90 : " + result6.getKey() + "점\t\t학생명 : " + result6.getValue()); //결과 95점 신용권
```

#### 정렬관련 메소드

![treemap 검색 관련 메소드2](C:\Users\COM\Desktop\treemap 검색 관련 메소드2.PNG)

```java
TreeMap<Integer, String> scores = new TreeMap<Integer, String>();
		
scores.put(new Integer(87), "홍길동");
scores.put(new Integer(98), "이동수");
scores.put(new Integer(75), "박길순");
scores.put(new Integer(95), "신용권");
scores.put(new Integer(80), "김자바");

// 키값으로 내림차순해서 출력하는 코드 1
NavigableMap<Integer, String> deMap = scores.descendingMap();
Set<Map.Entry<Integer, String>> des = deMap.entrySet();
for (Entry<Integer, String> entry : des) {
	System.out.println("학생 : " + entry.getValue() + "\t" + entry.getKey() + "점"); 
}
System.out.println(); 

		
// 키값으로 내림차순해서 출력하는 코드 2
NavigableSet<Integer> keyset = scores.descendingKeySet();
Iterator<Integer> it = keyset.iterator();
while (it.hasNext()) {
	Integer key = it.next();
	String value = scores.get(key);
	System.out.println("학생 : " + value + "\t" + key + "점");
		}
System.out.println();
		
		
// 키값으로 올림차순해서 출력하는 코드 1
// descendingMap() 을 두 번 사용하면 올림차순이 된다
deMap = deMap.descendingMap();
des = deMap.entrySet();
for (Entry<Integer, String> entry : des) {
	System.out.println("학생 : " + entry.getValue() + "\t" + entry.getKey() + "점");
}
System.out.println();
```

#### 범위관련 메소드 사용

```java
TreeMap<String, Integer> treeMap = new TreeMap<String, Integer>();
		
treeMap.put("apple", new Integer(10));
treeMap.put("forever", new Integer(60));		
treeMap.put("description", new Integer(40));
treeMap.put("ever", new Integer(50));
treeMap.put("zoo", new Integer(10));
treeMap.put("base", new Integer(20));
treeMap.put("guess", new Integer(70));
treeMap.put("cherry", new Integer(30));
		
System.out.println("[c~f 사이의 단어 검색]");
// c부터 f까지라서
// 시작이 f로 된 거 까지만 (뒤에 덧붙여진 내용이 있는 forever는 출력되지 x
NavigableMap<String, Integer> reangeMap = treeMap.subMap("c", true, "f", true);
for(Map.Entry<String, Integer> entry : reangeMap.entrySet()) {
	System.out.println(entry.getKey() + "-" + entry.getValue() + "페이지"); //결과 cherry, description, ever
}
```

