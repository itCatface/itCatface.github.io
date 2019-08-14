<font size=5>**PART_ONLY 下标(`subscript`)**

1. **简介**

	- **下标可定义在类、结构体、枚举中，是访问集合、列表、序列元素的快捷方式**

2. **语法格式** 

	- **下标了设定为读写或只读**

		```swift
		// 读写
		subscript(index: Int) -> Int {
		    get {
		      // 返回一个适当的 Int 类型的值
		    }
		
			// newValue 类型与下标返回类型相同
		    set(newValue) {
		      // 执行适当的赋值操作
		    }
		}
		```

		```swift
		// 只读
		subscript(index: Int) -> Int {
		    // 返回一个适当的 Int 类型的值
		}
		```

3. **演示**
	
	```swift
	struct TimesTable {
	    let multiplier: Int
	    
	    // 只读的下标
	    subscript(index: Int) -> Int {
	        return multiplier * index
	    }
	}
	
	let threeTimesTable = TimesTable(multiplier: 3)
	// threeTimesTable[6] 的值为 18
	```

4. **下标用法举例(`Dictionary`)**

	- **本例通过下标返回将可选类型(`Int?`)**

	- **通过下标删除键对应的值：将键对应的值赋值为 `nil` 即可**

		```swift
		var animals = ["spider": 8, "ant": 6, "cat": 4]
		// 通过下标插入新的键值对
		animals["bird"] = 2
		```

5. **下标选项**

	- **下标可接受任意数量、类型的入参，下标的返回值也可是任意类型**

	- **下标可使用变量入参和可变参数，但不能用输入输出参数，也不能给参数设置默认值**

	- **类或结构体可提供多个下标实现，使用时通过入参的数量和类型自动匹配**

	- **下为矩形结构体的案例**

		```swift
		struct Matrix {
		    // 行列
		    let rows: Int, columns: Int
		    // 根据行列，得到数组值
		    var grid: [Double]
		    
		    init(rows: Int, columns: Int) {
		        self.rows = rows
		        self.columns = columns
		        
		        grid = Array(count: rows * columns, repeatedValue: 0.0)
		    }
		    
		    // 角标越界判断
		    func indexIsValidForRow(row: Int, column: Int) -> Bool {
		        return row >= 0 && row < rows && column >= 0 && column < columns
		    }
		    
		    // 下标
		    subscript(row: Int, column: Int) -> Double {
		        get {
		            assert(indexIsValidForRow(row, column: column), "Index out of range")
		            return grid[(row * columns) + column]
		        }
		        set {
		            assert(indexIsValidForRow(row, column: column), "Index out of range")
		            grid[(row * columns) + column] = newValue
		        }
		    }
		}
		
		// 构造 2*2 的矩阵实例
		var matrix = Matrix(rows: 2, columns: 2)
		    
		matrix[0, 1] = 1.5 // 赋值
		matrix[1, 0] = 3.2 // 赋值
		    
		let someValue = matrix[2, 2]
		// 越界：断言触发
		```