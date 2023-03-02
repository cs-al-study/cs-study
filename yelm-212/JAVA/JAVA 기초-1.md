#   접근제어자

변수나 메서드의 사용 권한에 대해 접근 제어자를 사용하여 설정할수 있다.
`private -> default -> protected -> public` 순으로 보다 많은 접근을 허용한다.
-   **`public` 접근 제한자:**  자유롭게 사용 
-   **`protected` 접근 제한자:** 같은 패키지 또는 자식 클래스
-   **`private` 접근 제한자:** 외부에서 사용될 수 없도록 함
위 세 가지 접근 제한자를 별도로 설정하지 않으면, `default` 접근 제한을 가지며 해당 패키지 내에서만 접근이 가능하다.
#   클래스, 객체, 인스턴스 차이
- 클래스 
	- 객체를 만들어내기 위한 템플릿 혹은 청사진.
	- 클래스의 객체가 소유할 일련의 속성과 행동을 정의한다.
- 객체
	- 클래스를 이용해 만들어진 클래스의 인스턴스
	- 클래스로부터 정의된 속성을 가지고,클래스로부터 정의된 메소드를 사용할 수 있다
- 인스턴스
	- 메모리 상에 있는 하나의 객체를 의미함


#   Overloading vs Overriding

|         | Overloading | Overriding |
|---------|-----------------|-----------------|
| 파라미터   | 파라미터는 상이하나 이름이 동일한 여러개의 메소드를 가진다.| 하위 클래스의 메소드는 상위 클래스의 메소드와 동일한 파라미터 리스트를 가진다. |
| 반환값   | 다양한 반환 값을 가질 수 있다. | 상위 클래스와 동일한 리턴 타입을 가진다.|
| Method resolution  | 메소드가 호출될 때에 넘겨지는 전달인자의 수, 타입, 순서에 따라 컴파일 할 때 결정된다.   | 참조되는 객체의 실제 타입에 의해 결정된다.|
| 상속   | 상속으로 연관되지 않은 타 클래스 혹은 동일 클래스에서 일어날 수 있다.| 상속에 의해 연관 관계가 생기는 하위 클래스에서만 일어날 수 있다.|

#   Primitive type vs Reference type
| Aspect      | Primitive Type                 | Reference Type                                        |
| ----------- | ------------------------------ | ----------------------------------------------------- |
| 정의        | 언어 자체에 내장된 데이터 타입 | 프로그래머 혹은 언어에 의해 정의된 복잡한 데이터 타입 |
| 메모리 할당 | 스택                           | 힙                                                    |
| Pass by     | 값 (Value)                     | 주소 (Reference).                                     | 
| Null value  | null값 불가                    | null값 가능                                          |

##  Call by Reference vs Call by Value

| Aspect | Call by Value                                            | Call by Reference                                           |
| ------ | -------------------------------------------------------- | ----------------------------------------------------------- |
| 정의   | 메소드 또는 함수에 실제 값의 사본을 넘긴다               | 실제 값의 참조 값(주소)이 전달된다.                         |
| 메모리 | 값의 사본이 만들어지기 때문에 더 많은 메모리를 필요로 함 | 값의 사본을 만들 필요가 없으므로 메모리를 절약함            |
| 속도   | (상대적으로) 느림                                        | (상대적으로) 빠름                                           |
| 부작용 | 원본 값이 바뀌지 않으므로 부작용 없음                    | 함수/메소드 내의 원본 값이 변경되어 부작용을 유발할 수 있음 |

##   Wrapper Class
-  기본 타입에 해당하는 데이터를 객체로 포장해 주는 클래스
- 각각의 타입에 해당하는 데이터를 인수로 전달받아, 해당 값을 가지는 객체로 만들어줌

![](http://www.tcpschool.com/lectures/img_java_boxing_unboxing.png)
- Boxing : 기본 타입 데이터를 Wrapper 클래스의 인스턴스로 변환하는 과정
- Unboxing : Wrapper 클래스의 인스턴스에 저장된 값을 기본 타입 데이터로 꺼내는 과정
- 자바에서는 boxing과 unboxing이 필요한 상황에서 컴바일러가 자동으로 이를 처리해준다. (AutoBoxing / Unboxing)

```

Java program to demonstrate Autoboxing & AutoUnboxing

import java.util.ArrayList;
class Autoboxing
{
	public static void main(String[] args)
	{
		char ch = 'a';

		// Autoboxing- primitive to Character object conversion
		Character a = ch;

		ArrayList<Integer> arrayList = new ArrayList<Integer>();

		// Autoboxing because ArrayList stores only objects
		arrayList.add(25);

		// printing the values from object
		System.out.println(arrayList.get(0));
	     
	    // objects to data types (retrieving data types from objects)
        // unwrapping objects to primitive data types
		char newch = a;
		System.out.println(newch);
	}
}
```

