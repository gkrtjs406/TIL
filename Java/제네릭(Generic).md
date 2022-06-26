# 제네릭(Generic)



## 왜 제네릭을 사용하는가?

1. 컴파일 시 강한 타입체크를 할 수 있다
   - 자바 컴파일러는 코드에서 잘못 사용된 타입 때문에 발생하는 문제점을 제거하기 위해 제네릭에 대해 강한 타입 체크를 한다.
   - 실행 시 타입 에러가 나는 것보다는 컴파일 시에 미리 타입을 강하게 체크해서 에러를 사전에 방지한다
2. 타입변환(casting)을 제거한다

```java
List list = new ArrayList();
list.add("hello");
String str = (String)list.get(0); //타입 변환을 해야한다
```

```java
List<String> list = new ArrayList();
list.add("hello");
String str = list.get(0); //타입 변환을 하지 않는다
```

​	다음과 같이 제네릭 코드로 수정하면 List에 저장되는 요소를 String 타입으로 국한하기

​	때문에 요소를 찾아올 때타입 변환을 할 필요가 없어 프로그램 성능이 향상한다

​	**이렇듯 제네릭은 클래스 내부에서 지정하는 것이 아닌 외부에서 사용자에 의해 지정된다**



## 제네릭 사용방법

보통 제네릭은 아래 표의 타입들이 많이 쓰인다

![image-20220627014516481](C:\Users\COM\AppData\Roaming\Typora\typora-user-images\image-20220627014516481.png)

반드시 한 글자일 필요는 없고, 반드시 설명과 일치해야할 필요도없다. 다만 대중적으로 통하는 암묵적인 규칙이 있을 뿐이다

```java
public class Box{
    private Object object;
    public void set(Object object) {this.object = object;}
    public Object get() {return object;}
}
```

```java
Box box = new Box();
box.set("hello");	//String 타입을 Object 타입으로 자동 타입 변환해서 저장
String str = (String) box.get(); //Object 타입을 String으로 강제 변환
```

이와 같이 Object 타입을 사용하면 모든 종류의 자바 객체를 가져올 수 있지만, 저장 할떄 타입변환이 필요하고 가져올떄도 필요하다



```java
public class Box<T> {
    private T t;
    public T get() {return t;}
    public void set(T t) {this.t = t;}
}
```

```java
public class BoxExample{
    public static void main(String[] args){
        Box<String> box1 = new Box<String>();
        box1.set("hello");
        
        String str = box1.get();
        
        Box<Integer> box2 = new Box<Integer>();
        box2.set(6);
        int value = box2.get();
    }
}
```

위의 예시처럼 제네릭을 활용하면 강제 형변환을 하지 않고 유연하게 형변환을 시킬 수 있다



### 멀티 타입 파라미터

- 두개 이상의 파라미터를 사용하는 것 (인자를 두개로 받는 HashMap을 연상)

```java
public class Product<T, M>{
    private T kind;
    private M model;
    
    public T getKind(){return this.kind;}
    public M getModel(){return this.model;}
    
    public void setKind(T kind) {this.kind = kind;}
    public void setModel(K model) {this.model = model;}
}
```

```java
public class ProductExample{
    public static void main(String[] args){
        Product<Tv, String> product1 = new Product<Tv, String>();
        product1.setKind(new TV());
        product.setModel("스마트Tv");
        Tv tv = product1.getKind();
        String tvModel = product1.getModel();
        
        Product<Car, String> product2 = new Product<Car, String>();
        product2.setKind(new Car());
        product2.setModel("디젤");
        Car car = product2.getKind();
        String carModel = product2.getModel();
    }
}
```

자바 7부터는 다이아몬드 연산자를 사용해서 다음과 같이 간단하게 작성할 수 있다

```java
Product<Tv, String> product = new Product<>();
```

