摘要
1. 希望所有错误都可以在编译时期被发现，程序运行前排除错误，余下的在运行时解决.



2. Java异常机制主要依赖于try、catch、finally、throw、throws五个关键字.



异常处理机制


使用try…catch捕获异常
若执行try块里的业务逻辑代码时出现异常，系统会自动生成一个Exception对象，该Exception对象被提交给Java运行时环境[这个过程被称为抛出(throw)异常]. 当Java运行时环境收到该Exception对象时，会寻找能处理该异常对象的catch块，若找到合适的catch块，则把该异常对象交给该catch块处理[这个过程被称为捕获(catch)异常]；若Java运行时环境找不到捕获异常的catch块，则运行时环境终止，Java程序也退出.



异常类的继承体系 [先捕获小异常，再捕获大异常]


Throwable

|------Error

 |------AWTError

|------IOError

|------LinkageError 

|------ThreadDeath

|------Exception

|------RuntimeException  

|------IndexOutOfBoundsException

|------NullPointerException 

|------ClassCastException

|------IOException 

|------SQLException





try {		
      int c = a / b;	 
} catch(IndexOutOfBoundsException iobe) {
      sop(数组越界：运行程序时输入参数不够)；
} catch(NumberFormatException nfe) {
      sop(数字格式异常：程序只能接收整数参数)；
} catch(ArithmeticException iobe ae) {
      sop(算术异常：除0异常)；
} catch(Exception e) {
      sop(未知异常)；
}
运行异常时应把Exception类对应的catch块放在最后面，父类异常的catch块排在子类异常catch块的后面[见本块标题].





访问异常信息[所有异常对象]
getMessage() 返回异常的详细描述字段.

printStackTrace() 将异常的跟踪栈信息输出到标准错误输出.

printStackTrace(printStream s) 将异常的跟踪栈信息输出到指定输出流.

getStackTrace() 返回异常的跟踪栈信息.



使用finally回收资源
·除非try块、catch块中调用了退出虚拟机（System.exit()）的方法，否则不管try块、catch块中执行怎样的代码出现怎样的情况，异常处理的finally块总会被执行.

·只有当finally块执行完成后，系统才会跳回来执行try、catch块里的return或throw语句.

·尽量避免在finally块中使用return、throw等导致方法终止的语句.



Checked异常和RuntimeException体系 [Java两种异常]
Checked异常[不推荐使用]

1. 对于程序中的Checked异常，Java要求必须显式捕获并处理该异常，或者显式声明抛出该异常. 增加了编程复杂度

2. 导致方法签名与异常耦合，若该方法是重写父类的方法，则该方法抛出的异常还会受到被重写方法所抛出异常的限制.


对于Checked异常的处理方式
1. 当前方法明确知道如何处理该异常→用try…catch块捕获该，再在对应的catch块中修复.

2. 当前方法不知道如何处理该异常→在定义该方法时声明抛出该异常.


使用throws声明抛出异常
程序无须使用try、catch块来捕获该异常了，让调用者处理.

限制：子类方法声明抛出的异常类型是父类方法声明抛出的异常类型的子类或相同.

   子类方法声明抛出的异常不允许比父类方法声明抛出的异常多.


使用throw抛出异常
1. 若throw语句抛出的异常是Checked异常→该throw语句要么处于try块里，显示捕获该异常，要么放在一个带throws声明抛出的方法中，即把该异常交给该方法的调用者处理.

2. 若throw语句抛出的异常是Runtime异常→无须上两条要求，程序既可以显式使用try…catch来捕获并处理该异常，也可完全不理会将该异常交给该方法调用者处理.


throws和throw的区别
1. throws使用在函数上throw使用在函数内.

2. throws后面跟的异常类，可以跟多个，用逗号隔开throw后跟的是异常对象.




自定义异常类[通常需要提供两个构造器]


public class DemoException extends Exception{		//RuntimeException
      Public DemoException();					        
      Public DemoExceotion(String msg) {			
            Super(msg);	
      }	
}	




// 通过super调用父类的构造器，该msg属性是对该异常的详细描述信息



异常处理的嵌套
catch和throw同时使用[大型企业级应用中常用]



Java7增强的throw语句


Java7提供的多异常捕获
捕获多种类型的异常时①多种异常类型之间用竖线（|）隔开②异常变量有隐式的final修饰，incident程序不能对异常变量重新赋值[捕获一中类型异常时，异常变量没有final修饰].



异常链[职责链模式]
捕获一个异常然后接着抛出另一个异常，并把原始异常信息保存下来，避免向上暴露太多实现细节



Java的异常跟踪栈
printStackTrace()打印异常的跟踪栈信息：

第一行的信息详细显示了异常的类型和异常的详细消息，接下来跟踪栈记录程序中所有的异常发生点，各行显示被调用方法中执行的停止位置，并标明类、类中的方法名，与故障对应的行.



异常的处理规则
1. 过度使用异常[异常只用于处理非正常情况，不要使用异常处理来代替正常的流程控制]

2. 不要使用过于庞大的try块

3. 避免使用catchAll语句

4. 不要忽略捕获到的异常

