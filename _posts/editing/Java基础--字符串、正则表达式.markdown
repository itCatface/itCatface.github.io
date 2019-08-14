字符串

String[字符串]

构造方法摘要

String() 
初始化一个新创建的 String 对象，使其表示一个空字符序列。



String(byte[] bytes) 
通过使用平台的默认字符集解码指定的 byte 数组，构造一个新的 String。



String(byte[] bytes, Charset charset) 
通过使用指定的 charset 解码指定的 byte 数组，构造一个新的 String。



String(byte[] bytes, int offset, int length) 
通过使用平台的默认字符集解码指定的 byte 子数组，构造一个新的 String。



String(byte[] bytes, int offset, int length, Charset charset) 
通过使用指定的 charset 解码指定的 byte 子数组，构造一个新的 String。



String(byte[] bytes, int offset, int length, String charsetName) 
通过使用指定的字符集解码指定的 byte 子数组，构造一个新的 String。



String(byte[] bytes, String charsetName) 
通过使用指定的 charset 解码指定的 byte 数组，构造一个新的 String。



String(char[] value) 
分配一个新的 String，使其表示字符数组参数中当前包含的字符序列。



String(char[] value, int offset, int count) 
分配一个新的 String，它包含取自字符数组参数一个子数组的字符。



String(int[] codePoints, int offset, int count) 
分配一个新的 String，它包含 Unicode 代码点数组参数一个子数组的字符。



String(String original) 
初始化一个新创建的 String 对象，使其表示一个与参数相同的字符序列；换句话说，新创建的字符串是该参数字符串的副本。



String(StringBuffer buffer) 
分配一个新的字符串，它包含字符串缓冲区参数中当前包含的字符序列。



String(StringBuilder builder) 
分配一个新的字符串，它包含字符串生成器参数中当前包含的字符序列。







方法摘要

boolean

contains(CharSequence s) 
当且仅当此字符串包含指定的 char 值序列时，返回 true。

boolean

contentEquals(StringBuffer sb) 
将此字符串与指定的 StringBuffer 比较。

boolean

equals(Object anObject) 
将此字符串与指定的对象比较。若二者字符序列相等时返回true，否则返回false。

boolean

equalsIgnoreCase(String anotherString) 
将此 String 与另一个 String 比较，不考虑大小写。

boolean

isEmpty() 
当且仅当 length() 为 0 时返回 true。

boolean

matches(String regex) 
告知此字符串是否匹配给定的正则表达式

boolean

startsWith(String prefix) 
测试此字符串是否以指定的前缀开始。

boolean

startsWith(String prefix, int toffset) 
测试此字符串从指定索引开始的子字符串是否以指定前缀开始。

boolean

endsWith(String suffix) 
测试此字符串是否以指定的后缀结束。

int

codePointAt(int index) 
返回指定索引处的字符（Unicode 代码点）。

int

compareTo(String anotherString) 
按字典顺序比较两个字符串。

int

compareToIgnoreCase(String str) 
按字典顺序比较两个字符串，不考虑大小写。

int

hashCode() 
返回此字符串的哈希码。

int

indexOf(int ch) 
返回指定字符在此字符串中第一次出现处的索引。

int

indexOf(int ch, int fromIndex) 
返回在此字符串中第一次出现指定字符处的索引，从指定的索引开始搜索。

int

indexOf(String str) 
返回指定子字符串在此字符串中第一次出现处的索引。

int

indexOf(String str, int fromIndex) 
返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引开始。

int

lastIndexOf(int ch) 
返回指定字符在此字符串中最后一次出现处的索引。

int

lastIndexOf(int ch, int fromIndex) 
返回指定字符在此字符串中最后一次出现处的索引，从指定的索引处开始进行反向搜索。

int

lastIndexOf(String str) 
返回指定子字符串在此字符串中最右边出现处的索引。

int

lastIndexOf(String str, int fromIndex) 
返回指定子字符串在此字符串中最后一次出现处的索引，从指定的索引开始反向搜索。

int

length() 
返回此字符串的长度。

String

concat(String str) 
将指定字符串连接到此字符串的结尾。

static String

copyValueOf(char[] data) 
返回指定数组中表示该字符序列的 String。

static String

copyValueOf(char[] data, int offset, int count) 
返回指定数组中表示该字符序列的 String。

String

replace(char oldChar, char newChar) 
返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。

String

substring(int beginIndex) 
返回一个新的字符串，它是此字符串的一个子字符串。

String

substring(int beginIndex, int endIndex) 
返回一个新字符串，它是此字符串的一个子字符串。

String

toLowerCase() 
使用默认语言环境的规则将此 String 中的所有字符都转换为小写。

String

toUpperCase() 
使用默认语言环境的规则将此 String 中的所有字符都转换为大写。

String

trim() 
返回字符串的副本，忽略前导空白和尾部空白。

static String

valueOf(char[] data) 
返回 char 数组参数的字符串表示形式。

static String

valueOf(char[] data, int offset, int count) 
返回 char 数组参数的特定子数组的字符串表示形式。

static String

valueOf(double/float/int/long/chat/boolean/Object 对应参数x) 
返回 x 参数的字符串表示形式。

String[]

split(String regex) 
根据给定正则表达式的匹配拆分此字符串。

byte[]

getBytes() 
使用平台的默认字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。

byte[]

getBytes(String charsetName) 
使用指定的字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。

char

charAt(int index) 
返回指定索引处的 char 值。

char[]

toCharArray() 
将此字符串转换为一个新的字符数组。





StringBuffer[线程安全的可变字符序列] & StingBuilder[线程不同步的可变字符序列]

主要操作是 append 和 insert 方法，可重载这些方法，以接受任意类型的数据。

StringBuffer

append(char[] str) 
将 char 数组参数的字符串表示形式追加到此序列。

StringBuffer

append(char[] str, int offset, int len) 
将 char 数组参数的子数组的字符串表示形式追加到此序列。

StringBuffer

append(Object obj) 
追加 Object 参数的字符串表示形式。

StringBuffer

append(String/StringBuffer str/sb) 
将指定的字符串/Stringbuffer追加到此字符序列。

StringBuffer

appendCodePoint(int codePoint) 
将 codePoint 参数的字符串表示形式追加到此序列。

StringBuffer

insert(int offset, char[] str) 
将 char 数组参数的字符串表示形式插入此序列中。

StringBuffer

insert(int index, char[] str, int offset, int len) 
将数组参数 str 的子数组的字符串表示形式插入此序列中。

StringBuffer

insert(int offset, Object obj) 
将 Object 参数的字符串表示形式插入此字符序列中。

StringBuffer

insert(int offset, String str) 
将字符串插入此字符序列中。

StringBuffer

reverse() 
将此字符序列用其反转形式取代。

StringBuffer

replace(int start, int end, String str) 
使用给定 String 中的字符替换此序列的子字符串中的字符。

StringBuffer

delete(int start, int end) 
移除此序列的子字符串中的字符。

StringBuffer

deleteCharAt(int index) 
移除此序列指定位置的 char。

void

setCharAt(int index, char ch) 
将给定索引处的字符设置为 ch。

int

capacity() 
返回当前容量。





正则表达式[强大的字符串处理工具，简化书写]

优点：简化对字符串的复杂操作

弊端：符号定义越多，正则越长，阅读性越差

具体操作功能：

|--匹配：就是String类中的matches()

String qq = "123a454";

String regex = "[1-9]\\d{4,14}";

boolean flag = qq.matches(regex);

|--切割：就是String类中的split()

|--替换：就是String类中的replaceAll()

   若regex中有定义组，可以在第二参数中通过$符号获取正则表达式中已有的组

|--获取：

1·将正则表达式封装成对象 Pattern p = Pattern.compile(reg);

2·将正则对象和要操作的字符串相关联，获取正则匹配器引擎    Matcher m  = p.matcher(str);

3·通过Matcher对象中的方法对字符串进行各种操作

boolean

matches(String regex) 
告知此字符串是否匹配给定的正则表达式。

String

replaceAll(String regex, String replacement) 
使用给定的 replacement 替换此字符串所有匹配给定的正则表达式的子字符串。

String[]

split(String regex) 
根据给定正则表达式的匹配拆分此字符串。