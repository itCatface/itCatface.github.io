摘要

集合vs数组：集合只能保存对象；数组可保存对象和基本类型的值



一、Collection接口 Iterator接口

|--List (有序可重复，集合中每个元素都有其对应的顺序索引) ListIterator接口

|--Vector (数组)线程同步[被ArrayList替代]

|--ArrayList (数组)线程不同步；查找快增删慢

|--LinkedList (链表)线程不同步；增删快查找慢[经过一些方法可被当作堆栈或队列使用]



|--Queue[队列，类似List]



|--Set (实际上就是Collection，只是行为略有不同[不可包含重复元素])

|--HashSet (哈希表) 无序；不同步；集合元素值可以是null

判断元素相等：hashCode()返回值相等、equals()返回true

|--LinkedHashSet 输出时，元素的顺序总是与添加顺序一致[迭代性能略好于HashSet]

|--TreeSet (二叉树) 可对Set集合中的元素进行排序[自然排序和定制排序]



TreeSet

comparator() 
返回对此 set 中的元素进行排序的比较器；如果此 set 使用其元素的自然顺序，则返回 null。

first() 
返回此 set 中当前第一个（最低）元素。

last() 
返回此 set 中当前最后一个（最高）元素。

lower(E e) 
返回此 set 中严格小于给定元素的最大元素；如果不存在这样的元素，则返回 null。

higher(E e) 
返回此 set 中严格大于给定元素的最小元素；如果不存在这样的元素，则返回 null。

subSet(E fromElement, E toElement) 
返回此 set 的子集，其元素从 fromElement（包括）到 toElement（不包括）。

headSet(E toElement) 
返回此 set 的子集，其元素严格小于 toElement。

tailSet(E fromElement) 
返回此 set 的子集，其元素大于等于 fromElement。



自然排序 实现Comparable接口，复写compareTo方法

定制排序[比较器] 实现Comparetor接口，复写compare方法(可以用匿名内部类方式)







Collection接口定义了集合框架的共性功能 //集合中存储的都是对象的引用(地址)

1 添加

add(obj); //add()参数类型是Object，以便于接受任意类型对象

addAll(collection);

2 删除

remove(e);

removeAll(collection);

clear();

3 判断

contains(e);

containsAll(collection)

isEmpty();

4 获取

iterator();

size();

5 获取交集

retainAll(collection);

6 集合变数组

toArray();





List特有方法(可以操作角标的方法都是该体系的特有方法)：

1 增

add(index, e);

addAll(index, collection);

2 删

remove(index);

3 改

set(index, e);

4 查

get(index);

subList(from, to);

ListIterator listIterator(); //ListIterator是Iterator的子接口

indexOf(obj);

lastindexOf(obj);









LinkedList类的特有方法(JDK1.6后出现替代方法将NoSuchElementException→返回null)：

addFirst(); → offerFirst();

addLast(); → offerLast();

getFirst(); → peekFirst();

getLast(); → peekLast();

removeFirst(); → pollFirst();

removeLast(); → pollLast();





关于迭代器：其实就是集合的取出元素的方式[枚举：Vector特有的去除方式]

迭代时不能通过集合对象的方法操作集合汇总的元素→ConcurrentModificationException

只能对元素进行判断，取出，删除的操作，若要其他操作如增、改，就需要使用其子接口，ListIterator

Iterator it = al.iterator(); Enumeration en = ve.elements;

While(it.hasNext()){ while(en.hasMoreElements()){

sop(it.next()); sop(en.nextElements());

} }





二、Map接口[保存具有映射关系的数据]

|--Hashtable (哈希表)线程同步；不允许存null键值[被hashMap替代]

|--properties[读写属性文件]

|--HashMap (哈希表)不同步；key不可重复；允许存null键值

|--TreeMap (二叉树)不同步；可以给Map集合中的键排序



注：Hashtable、HashMap对key的要求与HashSet对集合元素的要求完全相同



Map定义的共性功能 //该集合存储键值对，而且要保证键的唯一性

1 增

put(key, value);

putAll(Map<? extends K, ? extends V>);

2 删

clear();

remove(key);

3 判

containsValue(value);

containsKey(key);

isEmpty();

4 查

get(key);

size();

Collection values();



Set entrySet();

Set keySet();



Map的内部类Entry，该类封装了一个key-value对，包含的方法如下

getKey(); 返回key值

getValue(); 返回value值

setValue(value); 设置Entry类包含的value值，并返回新设置的value值







Properties里的key、value都是字符串。三方法修改key、value值，两方法读写Field文件

String

getProperty(String key) 
用指定的键在此属性列表中搜索属性

String

getProperty(String key, String defaultValue) 
用指定的键在属性列表中搜索属性。

Object

setProperty(String key, String value) 
调用 Hashtable 的方法 put。

void

load(InputStream inStream) 
从输入流中读取属性列表（键和元素对）。

void

store(OutputStream out, String comments) 
以适合使用 load(InputStream) 方法加载到 Properties 表中的格式，将此 Properties 表中的属性列表（键和元素对）写入输出流。



TreeMap方法摘要

Map.Entry<K,V>

firstEntry() 
返回一个与此映射中的最小键关联的键-值映射关系；如果映射为空，则返回 null。

K

firstKey() 
返回此映射中当前第一个（最低）键。

SortedMap<K,V>

headMap(K toKey) 
返回此映射的部分视图，其键值严格小于 toKey。

NavigableMap<K,V>

headMap(K toKey, boolean inclusive) 
返回此映射的部分视图，其键小于（或等于，如果 inclusive 为 true）toKey。

Map.Entry<K,V>

higherEntry(K key) 
返回一个键-值映射关系，它与严格大于给定键的最小键关联；如果不存在这样的键，则返回 null。

K

higherKey(K key) 
返回严格大于给定键的最小键；如果不存在这样的键，则返回 null。

Map.Entry<K,V>

lastEntry() 
返回与此映射中的最大键关联的键-值映射关系；如果映射为空，则返回 null。

K

lastKey() 
返回映射中当前最后一个（最高）键。

Map.Entry<K,V>

lowerEntry(K key) 
返回一个键-值映射关系，它与严格小于给定键的最大键关联；如果不存在这样的键，则返回 null。

K

lowerKey(K key) 
返回严格小于给定键的最大键；如果不存在这样的键，则返回 null。

NavigableMap<K,V>

subMap(K fromKey, boolean fromInclusive, K toKey, boolean toInclusive) 
返回此映射的部分视图，其键的范围从 fromKey 到 toKey。

SortedMap<K,V>

subMap(K fromKey, K toKey) 
返回此映射的部分视图，其键值的范围从 fromKey（包括）到 toKey（不包括）。

SortedMap<K,V>

tailMap(K fromKey) 
返回此映射的部分视图，其键大于等于 fromKey。

NavigableMap<K,V>

tailMap(K fromKey, boolean inclusive) 
返回此映射的部分视图，其键大于（或等于，如果 inclusive 为 true）fromKey。



Map接口的取出方式

|--keySet()：将所有键存入Set集合，因Set具备迭代器。再根据get方法获取每一个键对应的值

|--entrySet()：将Map中映射关系存入Set[这个关系的数据类型：Map.Entry(Map的static内部接口)]

Ste keySet<key> = map.keySet();  Set<Map.entry<key,value>> entrySet = map.entrySet();

Iterator<key> it = keySet.iterator();   Iterator<Map.entry<key,value>> it = entrySet.iterator();

while(it.hasNext()){  while(it.hasNext()){

Object key = it.next(); Map.Entry<key,value> me = it.next();

Object value = map.get(key); sop(me.getKey()+”:”+me.getValue());

sop(key+”:”+value);       } }





Iterator接口[遍历集合、删除元素]    ListIterator接口[遍历集合、删除元素；向前迭代、添加元素]

Iterator接口定义了三种方法：     ListIterator增加了如下方法：

hasNext(); hasPrevious();

next(); previous();

remove(); add();

Iterator it = booklist.iterator(); ListIterator lit = bookList.listIterator();

while(it.hasNext()){ while(lit.hasPrevious()){

sop(it.next()); } sop(lit.previous()); }



注 使用Iterator迭代访问Collection集合元素时，Collection集合里的元素不能被改变，只有通过Iterator的remove方法删除上一次next方法返回的集合元素才可以，否则→ConcurrentModificationException





增强for循环[JDK1.5版本新特]：

//对集合进行遍历[必须明确被遍历的目标，只能获取集合元素，但不能对集合进行操作]

迭代器除了遍历，还可进行remove动作；若用ListIterator 还可在遍历过程中对集合记性增删改查动作

只为遍历→增强for

遍历集合并且过程中需操作元素→迭代器

遍历数组并且过程中需操作元素→传统for(因为可以定义角标，通过角标操作元素)



使用foreach循环遍历集合元素

for(String s : arraylist){

sop(s); }

注 同Iterator的注





Enumeration接口[遍历Vector、Hashtable、BitSet] hasMoreElements()、nextElements()









泛型<>[JDK1.5安全机制]

当使用集合时，将集合中要存储的数据类型作为参数传递到<>中即可

|--优点： 将运行时期出现问题ClassCastException转移到了编译时期。减少了运行时出现的问题，安全。

避免强制转换

|--

注意：静态方法不可访问类上定义的泛型。若静态方法操作的数据类型不确定，可将泛型定义在方法上



通配符 ？ 泛型的限定：

    ？ extends E: 可以接收E类型或者E的子类型。上限。

    ？ super E: 可以接收E类型或者E的父类型。下限





Collections：集合框架的工具类。里面定义的都是静态方法，不需创建对象

排序操作

Collections.swap(List<T> list, int i, int j); 在指定列表的指定位置处交换元素

Collections.shuffle(List<T> list); 使用默认随机源对指定列表置换

Collections.sort(List<T> list); 根据元素自然顺序对指定列表按升序排序

Collections.sort(List<T> new ComparatorByLen()); 根据指定比较器产生顺序对指定列表排序

Class ComparatorByLen implements Comparator<String>{

public int compare(String s1, String s2){

Int temp = s1.length()-s2.length();

Return (temp == 0)?S1.compareTo(s2) : temp; } }

查找、替换操作

static int binarySearch(List list, key);

static Object max(coll);

static Object max(coll, Comparator comp);

static Object min(coll);

static Object min(coll, Comparator comp);

static void Collections.fill(List<T> list, obj); 用制定元素替换指定列表中的所有元素

static int frequency(c, obj);

static int indexOfSubList(list, sublist);

static int lastIndexOfSubList(list, sublist);

Collections.replaceAll(List list, oldValue, newValue); 用新值替换列表中的所有某一指定旧值



同步控制

Collections类中提供多个synchronizedXxx()方法，可将指定集合包装成线程同步的集合，解决安全问题

Collection c = Collections.synchronizedCollection(new ArrayList());

List list = Collections.synchronizedList(new ArrayList());

Set s = Collections.synchronizedSet(new HashSet());

Map m = Collections.synchronizedMap(new HashMap());



Arrays：数组对象的工具类、里面定义的都是静态方法

String[] arr = {"abc","cc","kkkk"};

List<String> list = Arrays.asList(arr); 将指定数组转成固定大小的列表(可用集合方法操作数组中的元素:contains、get、indexOf、subList... 但若增删→UnsupportedOperationException

//若数组中元素都是对象，则转成集合时，数组中的元素就直接转成集合中的元素

若数组中的元素都是基本数据类型，则会将该数组作为集合中的元素存在//



集合变数组：Collection接口中的toArray() 【用处：限定了对元素的增删操作】

//指定类型的数组到底要定义多长？

String[] arr = al.toArray(new String[al.size()]);    创建一个刚刚好的数组最优，因为：

当指定类型的数组长度小于集合size，则该方法内部创建一个新的数组，长度为集合的size

当指定类型的数组大于集合size，则不会创建新数组而直接使用该数组，多余存储元素的位置默认null//





方法的可变参数[必须定义在参数列表的结尾]

int[] arr = {3,4};

show(arr);

int[] arr1 = {2,3,4,5};

show(arr1); //虽少定义了多个方法，但每次都要定义一个数组作为实际参数

其实就是上一种数组参数的简写形式，不用每一次都手动建立数组对象

只要将操作的元素作为参数传递即可，隐式将这些参数封装成了数组

public static void show(String str,int... arr){

sop(arr.length); }

show("haha",2,3,4,5,6);

show(2,3,4,5,6,4,2,35,9,"heh");



静态导入：

[当类名重名时，需指定具体的包名

当方法重名时，需指定具备所属的对象或者类]

import java.util.*;

import   static java.lang.System.*;  //导入了System类中所有静态成员









