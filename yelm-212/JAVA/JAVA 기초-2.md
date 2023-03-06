- interface vs abstract class 
![](https://media.geeksforgeeks.org/wp-content/uploads/Abstract-Class-vs-Interface.png)

| 추상 클래스 | 인터페이스 |
| --- | --- |
| 인스턴스화 할 수 없음 | 인스턴스화 할 수 없음 |
| 다른 클래스의 기본 클래스로 사용 | 어떤 클래스에서든 구현 가능한 추상 메서드 모음 |
| 추상 및 구상 메서드 모두 포함 가능 | 추상 메서드만 포함 가능 |
| 하위 클래스에서 추상 메서드를 구현해야 함 | 인터페이스를 구현하는 클래스는 모든 메서드에 대한 구현을 제공해야 함 |
| 인스턴스 변수와 생성자를 가질 수 있음 | 인스턴스 변수나 생성자를 가질 수 없음 |
| 메서드에 대한 기본 구현을 제공할 수 있음 | 메서드 시그니처만 포함 가능 |
| 하나의 추상 클래스만 상속 가능 | 여러 인터페이스를 구현 가능 |


추상 클래스를 사용하는 경우
1.  Java 애플리케이션에서 여러개의 클래스가 일부 코드를 공유함
2.  추상 클래스 내에 `non-static` 또는 `non-final` 필드를 정의하여 해당 필드가 속한 객체의 상태에 접근하고 수정할 수 있는 메서드를 통해 객체 상태를 변경함
3.  확장하는 클래스가 많은 공통 메서드 또는 필드를 가지거나 `public` 이외의 접근 제어자 (`protected`,`private`)에 대한 접근 권한이 필요한 경우.

인터페이스를 사용하는 경우
1.  total abstraction : 인터페이스 내에서 선언된 모든 메서드는 해당 인터페이스를 구현하는 클래스에서 구현함
2.  multiple inheritance : 클래스에서 하나 이상의 인터페이스를 구현함.
3.  특정 데이터 유형의 동작을 지정하고 해당 동작을 구현하는 클래스는 중요하지 않은 경우.

-   Checked Exception vs UnChecked Exception
  ![](https://user-images.githubusercontent.com/45676906/105691109-2cda9400-5f40-11eb-9003-a14873c2eaf2.png)

| Checked Exceptions                                              | Unchecked Exceptions                                               |
| --------------------------------------------------------------- | ------------------------------------------------------------------ |
| 메서드 시그니처에서 선언하거나 `try-catch` 블록으로 처리해야 함 | 메서드 시그니처에서 선언하지 않고 처리하지 않아도 됨               |
| `IOException`, `SQLException` 등이 예시                         | `NullPointerException`, `ArrayIndexOutOfBoundsException` 등이 예시 |
| 복구 가능한 오류에서 발생                                       | 프로그래밍 상 오류에서 발생                                        |
| 컴파일러가 `catch` 또는 `throws`로 처리 여부를 검증함           | 컴파일러가 처리 여부를 검증하지 않음                               |
| `Exception` 클래스에서 파생됨                                   | `RuntimeException` 클래스에서 파생됨                               |
| 발생시 롤백 안해도 됨                                                                | 예외 발생시 롤백함                                                                    |


-   static
	- 자바에서 변수 혹은 메서드를 static으로 선언하면 이는 특정 인스턴스에 속하기 보다는 클래스에 속하게 된다. (모든 객체가 이를 공유한다.)
	- 힙 영역이 아닌 static 영역에 할당된다.
-   final
	- 메소드에서, 더이상 하위 클래스에 `override`되지 않음을 나타낸다.
	- 어떠한 속성을 한번만 할당이 가능하게 한다.
-   generic
	- 아무거나 들어갈 수 있게 할려면 object 타입 쓰면 되는데 왜 제너릭 씀? -> 그러면 타입 검사, 변환시 오류 뜰수도 있으니까 코드가 길어짐. 이걸 간결하게 가능하게 하는게 제너릭
	- 컴파일 단계에서 타입을 검사할 수 있다.
	- 클래스나 메소드 내부에서 사용되는 객체의 타입 안정성을 높일 수 있다
	- 반환값에 대한 타입 변환 및 타입 검사에 들어가는 노력을 줄일 수 있다

```
import java.util.*;  
  
public interface Stack<E>{  
    void push(E item) throws Exception;  
    E pop() throws Exception;  
    int size();  
    boolean isEmpty();  
    boolean isFull();  
      
}
```

```
import java.util.*;  
  
public class NewStack<E> implements Stack<E>{  
    private E[] elements;  
    private int top ;  
  
    @SuppressWarnings("unchecked")  
    public NewStack(int size) {  
        this.elements  = (E[]) new Object[size];  
        this.top = -1;  
    }  
  
    public void push(E item) throws Exception {  
        if (this.isFull())  
                throw new Exception("Stack Is Full");  
        this.elements[++top] = item;  
    }  
  
    public E pop() throws Exception {// When stack is empty, it throws Exception  
            if (this.isEmpty())  
                throw new Exception("Stack Is Empty");  
        return this.elements[top--];  
    }  
  
    @Override  
    public int size() {  
        return this.elements.length;  
    }  
    
    @Override  
    public boolean isEmpty() {  
        return this.top < 0;  
    }  
    @Override  
    public boolean isFull() {  
        return top == elements.length - 1;  
    }  
  
    public String toString() {  
      String str = "Stack : ";  
      for (int i = 0; i < top; i++)  
         str += elements[i] + ", ";  
  
      return str + elements[top];  
   }  
  
  
}
```