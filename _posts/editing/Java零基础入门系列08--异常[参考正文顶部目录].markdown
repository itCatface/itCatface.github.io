异常
就是程序运行过程中，遇到了问题，这就叫异常。
1,异常的体系
Throwable 其实应该分三种
Error
通常出现重大问题如：服务器宕机数据库崩溃等。不编写针对代码对其处理。
Exception
除了 RuntimeException 和其所有子类,其他所有的异常类都是在编译的时候必须要处理的,要么try,要么抛
RuntimeException
RuntimeException 和其所有的子类,都不会在编译的时候报异常,而是在运行时报异常,这时候我们就需要回头看看我们的代码是否有问题,比如角标越界,空指针等
2,jvm是如何处理异常的
jvm发现运算是已经违反了数学运算规则,java将这种常见的问题进行描述,并封装成了对象叫做ArithmeticException
当除0运算发生后,jvm将该问题打包成了一个异常对象.
并将对象抛给调用者main函数,new ArithmeticException("/by zero");
main函数收到这个问题时,有两种处理方式:
1,自己将该问题处理,然后继续运行
2,自己没有针对的处理方式,只有交给调用main的jvm来处理
jvm有一个默认的异常处理机制,就将该异常进行处理.并将该异常的名称,异常的信息.异常出现的位置打印在了控制台上
同时将程序停止运行
那么jvm里都封装了哪些对异常的处理呢
3,处理异常处理方式：

A：try...catch
格式：
    try {
        需要检测的代码；
    }
    catch(异常类  变量) {//异常类名 对象名= new 异常类名();
        异常处理代码；
    }
世界上最真情的相依,就是你在try,我在catch,无论你发神马脾气,我都默默接受,静静处理

public class Demo1_Exception {

    public static void main(String[] args) {
        Demo d = new Demo();                        //创建对象
        try {
            int num = d.div(10, 0);                 //调用div方法并将10和0给方法的参数
            System.out.println(num);                //打印调用方法的结果
        } catch (Exception e) {                     //当try检测出异常的时候,就跳到catch语句中
                                                    //接收异常Exception e =  new ArithmeticException("/ by zero");
            System.out.println(e);                  //打印异常对象的toString方法
            System.out.println(e.toString());
            System.out.println("错了,除数为零了"); //提示
        }
        System.out.println("11111111111111111111"); //异常处理完代码可以继续执行
    }

}

class Demo {
    public int div(int a,int b) {                   //a = 10,b = 0
        return a / b;                               // new ArithmeticException("/ by zero");
    }
}
try...catch(...)...finally

说一下final,finalize,finally的区别
1,final可以修饰类,可以修饰方法,可以修饰变量
2,finalize,在对象没有更多引用,垃圾回收的时候调用
3,finally 关闭流,数据库等,释放资源

public class Test1 {

    /**
     * @param args
     * finally的面试题
     */
    public static void main(String[] args) {
        Test t = new Test();                        //创建对象
        int num = t.getNum();                       //调用getNum()方法
        System.out.println(num);
    }

}

class Test {
    public int getNum() {
        int x = 10;                                 
        try {
            System.out.println(1/0);                //执行1/0会出现异常,创建new ArithmetiException(\ by zero);对象
            return x;                               //return语句          
        } catch (Exception e) {
            x = 20;                                 //将x值改为20
            return x;                               //return语句
        } finally {
            x = 30;                                 //将x值改为30
            System.out.println("finally执行了吗");  //输出语句
            //return x;             finally中不要写return语句
        }

    }
    /*
     * 当程序执行到try语句的时候,1/0违背了数学的运算规则出现异常,创建出new ArithmetiException(\ by zero)对象,程序跳转到catch语句中
     * 当程序跳转到catch语句中,又将x值改为了20,遇到return语句,return语句会建立一个返回路径,将x里面的20相当于装到一个箱子里,准备返回,在返回之前
     * 看有没有finally语句,如果有执行finally语句,但是虽然将x的值改为了30,也不会影响到返回路径中的值,所以最后的返回还是20
     */
}
可以有下面三种搭配形式：

try...catch(...)
try...catch(...)...finally
try...finally               是不能进行异常处理的,必须抛出
B：抛出 throws throw

throws:用于标识函数暴露出的异常。thorws用在函数上，后面跟异常类名(可以由多个,隔开)。

throw:用于抛出异常对象。throw用在函数内，后面跟异常对象。new Exception();

public class Demo3_Throws {

    /**
     * @param args
     * @throws Exception 
     * try catch和throws的区别
     * 如果后续代码想要继续执行,只能try
     * 如果后续代码不想继续执行,只能throws
     * 
     * Exception 和RuntimeException的区别
     * RutimeException是运行时异常,需要程序员回来修改自己的代码
     * Exception是编译时异常,遇到编译时异常,必须处理,要么try,要么throws(未雨绸缪异常)
     */
    public static void main(String[] args) throws Exception {
        Person p = new Person();
        p.setAge(-17);
        System.out.println(p.getAge());

        System.out.println("222222222222222222222");
    }

}

class Person {
    private int age;

    public Person() {                   //alt + shift + s + c 生成空参数的构造函数
        super();

    }

    public Person(int age) {            //alt + shift + s + o 根据字段生成有参数的构造函数
        super();
        this.age = age;
    }

    public int getAge() {               //alt + shift + s + r 生成set和get方法
        return age;
    }

    public void setAge(int age) throws Exception {
        if(age > 0 && age < 200) {
            this.age = age;
        }else {
            /*Exception e = new Exception("年龄非法");
            throw e;*/
            throw new Exception("年龄非法");                    //用异常处理
            //System.out.println("年龄非法");                   //以前是这样处理的
        }
        /*
         * throw和throws的区别
         * throw写在方法内,后面跟的是异常对象
         * throws写在方法上,后面跟的是异常类名
         */
    }

    @Override
    public String toString() {          //alt + shift + s + s 生成toString方法
        return "Person [age=" + age + "]";
    }
}
C：到底用谁？

你能处理，建议处理。try...catch...finally
你处理不了，抛出。
在实际开发中,是分层开发,底层代码是能抛出尽量抛出,用日志记录住异常信息,并提供解决方案        
4,异常体系常见方法
A：getMessage() ：返回此 throwable 的详细消息字符串。
class Throwable {
    String detailMessage;
    Throwable(){}

    Throwable(String message) {
        this.detailMessage = message;
    }

    public String getMessage() {
        return detailMessage;
    }
}
B：toString()：获取异常类名和异常信息，返回字符串。
C：printStackTrace()：获取异常类名和异常信息，以及异常出现在程序中的位置。返回值void。
5,自定义异常

    自定义类继承Exception或者其子类(RuntimeException)

    class MyException extends Exception{
        MyException(){}

        MyException(String message){
            super(message); //将信息传递给父类,调用父类封装好的构造方法
        }
    }

    class Student {
        public void giveAge(int age) throws MyException {
            if(age>40 || age<16) {
                //throw new MyExcetpion("建议不学了");
                MyExcepiont my = new MyExcetpion("建议不学了");
                throw my;
            }
            else {
                System.out.println("可以学习Java");
            }
        }
    }
E：RuntimeException和Exception
    区别：RuntimeException就是要你改代码的。你可以不处理。
6,异常总结
RuntimeException以及其子类如果在函数中被throw抛出，可以不用在函数上声明。
子类覆盖父类方法时，子类的方法必须抛出相同的异常或父类异常的子类。(父亲坏了,儿子不能比父亲更坏)
如果父类抛出了多个异常,子类覆盖父类时,只能抛出相同的异常或者是他的子集,子类不能抛出父类没有的异常
如果被覆盖的方法没有异常抛出,那么子类的方法绝对不可以抛出异常,如果子类方法内有异常发生,那么子类只能try,不能throws
当try对应多个catch时,最顶层的异常要放在最下面,反过来分析如果最顶层的异常放在第一行,那根据多态原理,后面的catch就没用了,一般面试的时候会这么问,开发的时候不会抛有继承关系的异常