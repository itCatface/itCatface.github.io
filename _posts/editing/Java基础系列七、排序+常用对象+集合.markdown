数据结构相关基础(PART A) & 集合点题(PART B)
(PART A)
一.排序
1. 选择排序
int[] arr = { 66,55,44,33,22,11 };
原理：如果拿0角标上的元素依次和后面的元素进行比较，第一次内循环结束后，最小值出现在了0角标位置。
arr[0]与arr[1-5]比了五次
arr[1]与arr[2-5]比了四次
arr[2]与arr[3-5]比了三次
arr[3]与arr[4-5]比了二次
arr[4]与arr[5]比了一次
你就想想我们是如何打星星
*****
****
***
**
*
arr[x]与arr[y]比较
数组长度是6
for (int x = 0;x < arr.length - 1;x++) {
    for (int y = x + 1;y < arr.length;y++) {
        if (arr[x] > arr[y]) {
            int temp = arr[x];
            arr[x] = arr[y];
            arr[y] = temp;
        }
    }
}

2. 冒泡排序

int[] arr = {66,55,44,33,22,11};
原理：两个相邻元素进行比较，第一次比较完以后，最大值出现在了最大角标处。
第一次:arr[0]与arr[1],arr[1]与arr[2],arr[2]与arr[3],arr[3]与arr[4],arr[4]与arr[5],比了五次
第二次:arr[0]与arr[1],arr[1]与arr[2],arr[2]与arr[3],arr[3]与arr[4]比了四次
第三次:arr[0]与arr[1],arr[1]与arr[2],arr[2]与arr[3]比了三次
第四次:arr[0]与arr[1],arr[1]与arr[2]比了二次
第五次:arr[0]与arr[1]比了一次
for (int x = 0;x < arr.length - 1; x++) {
    // -1防止角标越界
    // -x为了提高效率
    for (int y = 0;y < arr.length - 1 - x;y++) {//6
        if (arr[y] > arr[y+1]) {
            int temp = arr[y];
            arr[y] = arr[y+1];
            arr[y+1] = temp;
        }
    }
}
3. 查找

A：无序数组
int[] arr = {33, 22, 11, 44, 55, 66};
public static int getIndex(int[] arr, int key) {
    for (int x = 0;x < arr.length;x++) {
        if (key == arr[x]) {
            return x;
        }
    }
    return -1;
}
B：有序数组 二分查找
// 数组长度是6,最大角标值是5
public static int getIndex(int[] arr, int key) {
    int min = 0;
    int max = arr.length-1;
    int mid = (min + max)/2;
    while (key != arr[mid]) {
        if (key > arr[mid]) {
            min = mid + 1;
        }else if (key < arr[mid]){
            max = mid - 1;
        }
        if (min > max){
            return -1;
        }
        mid = (min + max)/2;
    }
    return mid;

}
Arrays工具类
sort()
binarySearch()
BigInteger
1. 创建对象
可以使用BigInteger(String)来创建一个很大的整数, 精度可以无限大, 值创建之后不会被改变(类似String)
2. 常用方法
BigInteger add(BigInteger val) // 加
BigInteger subtract(BigInteger val) // 减
BigInteger multiply(BigInteger val) // 乘
BigInteger divide(BigInteger val) // 除
BigInteger mod(BigInteger m ) // 模
BigInteger max(BigInteger val) // 两个数的最大值
BigInteger min(BigInteger val) // 两个数的最小值
BigDecimal
1. 创建对象
BigDecimal(double); // 不建议用,运算结果不精确
BigDecimal(String); // 可以,但是每次都要传字符串给构造函数
static BigDecimal valueOf(double) // 可以,而且可以直接传double数
因为double数是不精确,是无限接近那个数,用BigDemal这个类可以让其精确
2. 常用方法
BigDecimal add(BigDecimal augend)
BigDecimal subtract(BigDecimal subtrahend)
BigDecimal multiply(BigDecimal multiplicand)
BigDecimal divide(BigDecimal divisor)
时间类
1. Date
比较古老的一个类, 大多数方法已过时, 但通常我们还会用它来获取当前时间,new Date()可以创建日期对象, 然后使用SimpleDateFormat可以将其格式化成我们需要的格式,通常使用的格式为: "yyyy-MM-dd HH:mm:ss", 具体格式说明详见SimpleDateFormat类yyyy年MM月dd日 E HH:mm:ss
a.获取当前时间的毫秒值
Date d = new Date();
d.getTime(); // 获取的是1970年1月1日0时0分0秒到当前时间的毫秒值
System.currentTimeMillis();
b.将毫秒值转换成时间对象
Date d = new Date(毫秒值); // 通过毫秒值获取时间对象
Date d = new Date(); // 创建时间对象
d.setTime(毫秒值); // 根据毫秒值修改时间对象
2. Calendar
很多方法都是替代了Date类的方法, 最常用的就是
int get(int field)(Calendar.YEAR) // 通过传入的字段获取对应的值,(获取年对应的值)
void add(int field, int amount) // field代表传入的时间字段可以是年月日等,amount代表是数值,正数就是在传入的字段上加,负数减
void set(int field, int value) // field代表传入的时间字段可以是年月日等,value代表设置的值,想设置哪一年或月日等,就写哪个值
void set(int year, int month, int date)
可以对指定的字段获取, 设置, 以及增减 六.Math
提供了一些和数学运算相关的方法,
static double PI // 获取π(派)的值
static double floor(double a) // 是小于等于a这个double值的最大整数对应的double值
static double ceil(double a) // 是大于等于a这个double值的最小整数对应的double值
static long round(double a ) // 四舍五入,返回是一个long值
static double sqrt(double a) // 开平方
static double pow(double a, double b) //a是底数,b是指数返回的是a的b次幂
(PART B)
集合的概念
集合是一种容器, 长度可变, 可以存储任意类型的对象.
基本数据类型也可以装入集合, 但其实内部是先自动装箱成包装类对象, 然后再存入集合的.
集合的分类
Collection”一次存一个对象, 单列集合
List“可重复, 有索引,有序
ArrayList：数组实现, 查找快, 线程不安全
LinkedList：链表实现, 增删快, 线程不安全
Vector：数组实现, 线程安全
Set：不可重复, 没索引,无序
HashSet：使用哈希算法去重复, 效率高, 但元素无序
TreeSet：已排序, 可以指定一个顺序, 对象存入之后会按照指定的顺序排列
LinkedHashSet：HashSet的子类, 原理相同, 除了去重复之外还能保留存储顺序
Map

HashMap
LinkedHashMap
TreeMap
Hashtable
Map一次存两个对象, 键值对 * HashMap 使用哈希算法对键去重复, 效率高, 但无序 * LinkedHashMap 使用哈希算法去重复, 并且保留存储顺序 * TreeMap 使用二叉树算法排序, 可以自定义顺序 * Hashtable 类似HashMap, 线程安全, 效率略低, 不允许null键和null值

集合的常用方法
1. 常用方法
add(Object obj)：向集合中添加一个元素, 添到最后的位置
get(int index)：获取集合中指定位置的元素
size()：获取集合的长度
add(int index, Object obj)：向集合中添加一个元素, 添到指定位置
set(int index, Object obj)：把集合中指定位置的元素替换
remove(int index)：删除集合中指定位置的元素
remove(Object obj)：删除集合中包含的obj对象(遍历集合中的元素如果传入的元素equals某个元素就调用remove方法,注意:角标要--)
2. 迭代集合
a. for循环：从0循环到集合的size() - 1, 每次获取其中一个
b. 迭代器：调用iterator()方法获取迭代器, 使用hasNext()判断是否包含下一个元素, 使用next()获取下一个元素
c. 增强for循环：for (类型 变量名 : 容器) { 循环体 } 容器中有多少个元素就执行多少次循环体, 每次循环变量指向容器中不同的元素
3. 迭代时删除的问题
a. for循环：删除时由于后面的元素会向前移动, 所以删除之后循环变量要--
b. 迭代器：要删除元素时必须使用Iterator中的remove()否则会抛出异常
c. 增强for循环：不能删除
List的三个儿子
List的三个儿子特点：
List
ArrayList
底层数据结构是数组，查询和修改快，增删慢
线程不安全，效率高
Vector
底层数据结构是数组，查询慢(相对应ArrayList)，增删慢(相对应LinkedList)
线程安全，效率低
LinkedList
底层数据结构是链表，查询和修改慢，增删快
线程不安全，效率高
ArrayList(存储字符串和自定义对象)
Vector(存储字符串和自定义对象)
有自己的特殊功能(方法)
但是不用，被新功能给替代了
LinkedList(存储字符串和自定义对象)
有自己的特殊功能。可以很方便的操作头和尾
案例：
A:ArrayList存储字符串并去除重复值
B:ArrayList存储自定义对象并去除重复值
需求：我们认为同姓名和同年龄的人即为同一个人
C:用LinkedList模拟栈数据结构
泛型(理解)
泛型是一种把明确类型放在了创建对象或者调用方法时候才去明确的特殊的类型
格式：
<数据类型>引用数据类型
好处：
A：解决了黄色警告线问题
B：把运行期间的转换异常给提前到了编译期间
C：优化了程序设计，不需要做强制类型转换了
泛型的前世今生
A：泛型类
B：泛型方法
C：泛型接口
泛型的使用
看API中的类或者接口,其后是否跟有<>,如果有，就是泛型的应用
一般在集合中用
HashSet(LinkedHashSet)

1. HashSet原理
我们使用Set集合都是需要去掉重复元素的, 如果在存储的时候逐个equals()比较, 效率较低,哈希算法提高了去重复的效率, 降低了使用equals()方法的次数.
当HashSet调用add()方法存储对象的时候, 先调用对象的hashCode()方法得到一个哈希值, 然后在集合中查找是否有哈希值相同的对象.
如果没有哈希值相同的对象就直接存入集合.
如果有哈希值相同的对象, 就和哈希值相同的对象逐个进行equals()比较,比较结果为false就存入, true则不存.
2. 将自定义类的对象存入HashSet去重复
类中必须重写hashCode()和equals()方法.
hashCode()：属性相同的对象返回值必须相同, 属性不同的返回值尽量不同(提高效率).
equals()：属性相同返回true, 属性不同返回false,返回false的时候存储.
迭代(遍历)

1. List
a. 普通for循环, 使用get()逐个获取
b. 调用iterator()方法得到Iterator, 使用hasNext()和next()方法
c. 增强for循环, 只要可以使用Iterator的类都可以用
d. Vector(x)集合可以使用Enumeration的hasMoreElements()和nextElement()方法
2. Set
a. 调用iterator()方法得到Iterator, 使用hasNext()和next()方法
b. 增强for循环, 只要可以使用Iterator的类都可以用
TreeSet

1. 特点
TreeSet是用来排序的, 可以指定一个顺序, 对象存入之后会按照指定的顺序排列
2. 使用方式
a. 自然顺序(Comparable)
TreeSet类的add()方法中会把存入的对象提升为Comparable类型
调用对象的compareTo()方法和集合中的对象比较
根据compareTo()方法返回的结果进行存储
b. 比较器顺序(Comparator)
创建TreeSet的时候可以制定 一个Comparator
如果传入了Comparator的子类对象, 那么TreeSet就会按照比较器中的顺序排序
add()方法内部会自动调用Comparator接口中compare()方法排序
c. 两种方式的区别
TreeSet构造函数什么都不传, 默认按照类中Comparable的顺序(没有就报错ClassCastException)
TreeSet如果传入Comparator, 就优先按照Comparator
Map集合
1. Map集合的特点
Map集合一次存储两个对象, 一个键对象, 一个值对象
键对象在集合中是唯一的, 可以通过键来查找值
2. Map常用方法
put()：存储一条记录, 一个键和一个值
get()：根据键对象获取值
containsKey()：判断是否包含指定的键
containsValue()：判断是否包含指定的值
remove(key)：根据键删除一条记录
size()：Map集合中的记录数
values()：得到所有的值对象组成的一个Collection集合
3. 迭代Map集合
a. keySet()
先调用keySet()方法从Map集合中获取所有Key组成的一个Set集合
迭代Set集合可以得到每一个Key
然后再调用get()方法通过Key获取每一个Value
b. entrySet()
先调用entrySet()方法从Map集合中获取所有Entry(键值对)组成的一个Set集合
迭代Set集合可以得到每一个Entry
然后再调用getKey()和getValue()方法得到每一个Key和每一个Value
4. HashMap
在使用HashMap存储键值对的时候, 先调用Key对象的hashCode()方法计算一个哈希值, 在Map中查找是否有相同哈希值的Key对象
如果没有哈希值相同的Key对象, 这个键值对直接存入
如果有哈希值相同的Key对象, 那么就进行equals比较
比较结果为false就存入, true则覆盖原Value
5. LinkedHashMap
HashMap的子类, 算法相同, 但保留了存储的顺序
6. TreeMap
在使用TreeMap存储键值对的时候, 会使用Key对象和集合中已存储的Key对象进行比较, 确定二叉树上的位置
比较的方式和TreeSet指定的方式相同, Comparable和Comparator
7. Hashtable(x)
类似HashMap, 线程安全, 效率略低, 不允许null键和null值
集合的迭代
1. Collection
Iterator：通过iterator()方法得到迭代器, 调用hasNext()和next()方法进行迭代
Foreach：for (类型 变量名 : 容器) { 循环体 }
2. Map
keySet()：得到所有的键组成的Set, 遍历Set得到每一个键, 然后再分别获取值
entrySet()：得到所有的Entry组成的Set, 遍历Set得到每一个Entry, 再分别getKey()和getValue()
3. List
Iterator
Foreach
for：根据索引定义for循环, 调用get()方法根据索引获取每一个元素
4. Vector
Iterator
Foreach
for
Enumeration: 类似Iterator, 通过elements()方法得到Enumeration, 调用hasMoreElements()和nextElement()方法进行迭代
重点(必须会的)
1. 了解ArrayList, LinkedList, HashSet, TreeSet, HashMap, TreeMap的特点
2. 会迭代ArrayList, LinkedList, HashSet, TreeSet, HashMap, TreeMap
3. 会用哈希算法(hashCode,equals), 会用二叉树算法(Comparable,Comparator)
