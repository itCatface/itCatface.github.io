<font size=5>**初始化顺序**

- **题**

	```
	public class Demo01 {
		public static void main(String[] args) {
			Card card = new Card();
			card.f();
		}
	}
	
	class Tag {
		Tag(int marker) {
			System.out.println("Tag(" + marker + ")");
		}
	}
	
	class Card {
		Tag t1 = new Tag(1); 
	
		Card() {
			System.out.println("Card()");
			t3 = new Tag(33); 
		}
	
		Tag t2 = new Tag(2); 
	
		void f() {
			System.out.println("f()");
		}
		Tag t3 = new Tag(3); 
	}
	```

	> 在一个类里，初始化的顺序是由变量在类内的定义顺序决定的. 即使变量定义大量遍布于方法定义的中间，
那些变量仍会在调用任何方法之前得到初始化——甚至在构建器调用之前.
	
   >	Tag(1)
	Tag(2)
	Tag(3)
	Card()
	Tag(33)
	f()

<hr>

<font size=5>**关于`==`**

- **题**

	>`String str = "a" + "b" + 1;`的编译结果为：`String str = "ab1";`
因为都是常量，所以编译器认为叠加会得到固定值，就在编译时优化的. 

	```
	public class Demo02 {
		public static void main(String[] args) {
			test();
		}
		
		
		public static void test() {
			String a = "a";
			final String c = "a";
			
			String b = a + "b";
			String d = c + "b";
			String e = getA() + "b";
			
			String compare = "ab";
			
			System.out.println(b == compare);
			System.out.println(d == compare);
			System.out.println(e == compare);
		}
		
		private static String getA() {
			return "a";
		}
	}

	// false -- a作为局部变量，其值具有不确定性
	// true  -- 由于final不可变，编译器直接将c赋值为"a"
	// false -- 编译器不会查看getA()方法内部逻辑
	```
	
	<hr>

<font size=5>**交换变量**

- **A**

	```
	int temp = a;
	a = b;
	b = temp;
	```

- **B：存在越界问题**

	```
	a = a + b;
	b = a - b;
	a = a - b;
	```

- **C：通过最低级的CPU位运算，效率极高，且不会越界**
	
	```
	a = a ^ b;
	b = a ^ b;
	a = a ^ b;
	```