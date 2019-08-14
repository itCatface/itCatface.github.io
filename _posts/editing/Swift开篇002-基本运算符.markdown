<font size=5>**PART_A 运算符**

1. **赋值运算符：`＝`**

	- **普通赋值**

		```swift
		var num
		num = 5
		```

	- **元组赋值**

		```swift
		let (x, y) = (0, 0)
		```

	- **`=` 操作不返回任何值**

2. **算数、组合赋值、自增自减、、负号、字符串拼接**

	- **求余时符号只看左边，可对浮点数求余**

		```swift
		let a = 3, b = 4
		
		// 算数运算
		var c = 0
		c = a + b
		c = a - b
		c = a * b
		c = a / b
		c = a % b
		
		// 组合赋值运算
		c += a
		c -= a
		c *= a
		c /= a
		c %= a
		
		// 自增自减运算
		c++ // 先自增，再返回值
		c--
		++c // 先返回值，再自增
		--c
		
		// 负号
		-c
		
		// 字符串拼接
		String str = "hello " + "world"
		```

3. **比较运算符**

	```swift
	let a = 3, b = 4
	
	a == b
	a != b
	a > b
	a >= b
	a < b
	a <= b
	```

4. **`? :` 三目运算符**

	```swift
	let num = 3
	num == 5 ? "yes" : "no"
	```

5. **`??` 空合运算符**

	- **判断a，若为空则返回b值，若不为空解封并返回a值**
	
	- **a必须是Optional类型**
	
	- **b的存储值类型必须和a一致**

		```swift
		var a:Int?, b = 5
		a ?? b
		a != nil ? a! : b
		```

6. **区间运算符**
	
	- **`a ... b` 闭区间**
		- **b必须大于a**
		
		- **半开区间：`a ..< b` 或者 `a >.. b`**
		
		- **数组遍历时：`0 ..< strArr.count`**

		```swift
		for x in 1 ... 9 {
		    for var y = 1; y <= x; y++ {
		        print("\(y) * \(x) = \(x * y)", terminator:"\t")
		        // 字符串插值：通过\()来插入实际值
		        // \()中不能包含非转义\、回车、换行符
		    }
		    print()
		}
		```

7. **逻辑运算**

 - **非：`!a`**
 
 - **与(短路)：`a && b`**
 
 - **或(短路)：`a || b`**

8. **推荐使用 `()` 来明确优先级**

<hr>

<font size=5>**PART_B 字符串**

>字符串是值类型

1. **初始化空字符串(两种方式等价)**

	- **`var str = ""`**
	
	- **`var str = String()`**

2. **判空**

	- **`str.isEmpty`**

3. **拼接**

	- **`var str = "hi " + "catface"`**

		```swift
		var str = "hello"
		let c : Character = "!"
		str.append(c) // str = "hello!"
		```

4. **字符 `Character`**

	- **初始化：`let c : Character = "!"`**

	- **字符数组构造字符串**

		```swift
		let characters : [Character] = ["c", "a", "t", "