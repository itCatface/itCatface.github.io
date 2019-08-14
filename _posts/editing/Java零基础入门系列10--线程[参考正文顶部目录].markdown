一.线程的概念
1.什么是线程
线程是程序执行的一条路径, 一个进程中可以包含多条线程
多线程并发执行可以提高程序的效率, 可以同时完成多项工作
2.多线程的应用场景
红蜘蛛同时共享屏幕给多个电脑
迅雷开启多条线程一起下载
QQ同时和多个人一起视频
服务器同时处理多个客户端请求
二.开启新线程
1.继承Thread

定义类继承Thread
重写run方法
把新线程要做的事写在run方法中
创建线程对象
开启新线程, 内部会自动执行run方法
public class Demo2_Thread {

    /**
     * @param args
     */
    public static void main(String[] args) {
        MyThread mt = new MyThread();                           //4,创建自定义类的对象
        mt.start();                                             //5,开启线程

        for(int i = 0; i < 3000; i++) {
            System.out.println("bb");
        }
    }

}
class MyThread extends Thread {                                 //1,定义类继承Thread
    public void run() {                                         //2,重写run方法
        for(int i = 0; i < 3000; i++) {                         //3,将要执行的代码,写在run方法中
            System.out.println("aaaaaaaaaaaaaaaaaaaaaaaaaaaa");
        }
    }
}
2.实现Runnable

定义类实现Runnable接口
实现run方法
把新线程要做的事写在run方法中
创建自定义的Runnable的子类对象
创建Thread对象, 传入Runnable
调用start()开启新线程, 内部会自动调用Runnable的run()方法

public class Demo3_Runnable {
    /**
     * @param args
     */
    public static void main(String[] args) {
        MyRunnable mr = new MyRunnable();                       //4,创建自定义类对象
        //Runnable target = new MyRunnable();
        Thread t = new Thread(mr);                              //5,将其当作参数传递给Thread的构造函数
        t.start();                                              //6,开启线程

        for(int i = 0; i < 3000; i++) {
            System.out.println("bb");
        }
    }
}

class MyRunnable implements Runnable {                          //1,自定义类实现Runnable接口
    @Override
    public void run() {                                         //2,重写run方法
        for(int i = 0; i < 3000; i++) {                         //3,将要执行的代码,写在run方法中
            System.out.println("aaaaaaaaaaaaaaaaaaaaaaaaaaaa");
        }
    }

}
3.两种方式的区别

查看源码的区别:

a.继承Thread : 由于子类重写了Thread类的run(), 当调用start()时, 直接找子类的run()方法
b.实现Runnable : 构造函数中传入了Runnable的引用, 成员变量记住了它, start()调用run()方法时内部判断成员变量Runnable的引用是否为空, 不为空编译时看的是Runnable的run(),运行时执行的是子类的run()方法
继承Thread

好处是:可以直接使用Thread类中的方法,代码简单
弊端是:如果已经有了父类,就不能用这种方法
实现Runnable接口
好处是:即使自己定义的线程类有了父类也没关系,因为有了父类也可以实现接口,而且接口是可以多实现的
弊端是:不能直接使用Thread中的方法需要先获取到线程对象后,才能得到Thread的方法,代码复杂
4.用匿名内部类实现两种线程的方式

继承Thread类

new Thread() {                                                  //1,new 类(){}继承这个类
    public void run() {                                         //2,重写run方法
        for(int i = 0; i < 3000; i++) {                         //3,将要执行的代码,写在run方法中
            System.out.println("aaaaaaaaaaaaaaaaaaaaaaaaaaaa");
        }
    }
}.start();
实现Runnable接口

new Thread(new Runnable(){                                      //1,new 接口(){}实现这个接口
    public void run() {                                         //2,重写run方法
        for(int i = 0; i < 3000; i++) {                         //3,将要执行的代码,写在run方法中
            System.out.println("bb");
        }
    }
}).start(); 
三.Thread类常用方法
1.获取名字
通过getName()方法获取线程对象的名字
2.设置名字

通过构造函数可以传入String类型的名字
new Thread("康师傅") {
    public void run() {
        for(int i = 0; i < 1000; i++) {
            System.out.println(this.getName() + "....aaaaaaaaaaaaaaaaaaaaaaa");
        }
    }
}.start();

new Thread("周老虎") {
    public void run() {
        for(int i = 0; i < 1000; i++) {
            System.out.println(this.getName() + "....bb");
        }
    }
}.start(); 
通过setName(String)方法可以设置线程对象的名字
Thread t1 = new Thread() {
    public void run() {
        for(int i = 0; i < 1000; i++) {
            System.out.println(this.getName() + "....aaaaaaaaaaaaaaaaaaaaaaa");
        }
    }
};

Thread t2 = new Thread() {
    public void run() {
        for(int i = 0; i < 1000; i++) {
            System.out.println(this.getName() + "....bb");
        }
    }
};
t1.setName("芙蓉姐姐");
t2.setName("凤姐");

t1.start();
t2.start();
3.获取当前线程对象

Thread.currentThread(), 主线程也可以获取
new Thread(new Runnable() {
    public void run() {
        for(int i = 0; i < 1000; i++) {
            System.out.println(Thread.currentThread().getName() + "...aaaaaaaaaaaaaaaaaaaaa");
        }
    }
}).start();

new Thread(new Runnable() {
    public void run() {
        for(int i = 0; i < 1000; i++) {
            System.out.println(Thread.currentThread().getName() + "...bb");
        }
    }
}).start();
Thread.currentThread().setName("我是主线程");                    //获取主函数线程的引用,并改名字
System.out.println(Thread.currentThread().getName());       //获取主函数线程的引用,并获取名字
4.休眠

Thread.sleep(毫秒,纳秒), 控制当前线程休眠若干毫秒1秒= 1000毫秒 1秒 = 1000 * 1000 * 1000纳秒 1000000000

new Thread() {
    public void run() {
        for(int i = 0; i < 10; i++) {
            System.out.println(getName() + "...aaaaaaaaaaaaaaaaaaaaaa");
            try {
                Thread.sleep(10);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}.start();

new Thread() {
    public void run() {
        for(int i = 0; i < 10; i++) {
            System.out.println(getName() + "...bb");
            try {
                Thread.sleep(10);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}.start();
5.守护

setDaemon(), 设置一个线程为守护线程, 该线程不会单独执行, 当其他非守护线程都执行结束后, 自动退出
Thread t1 = new Thread() {
    public void run() {
        for(int i = 0; i < 50; i++) {
            System.out.println(getName() + "...aaaaaaaaaaaaaaaaaaaaaa");
            try {
                Thread.sleep(10);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
};

Thread t2 = new Thread() {
    public void run() {
        for(int i = 0; i < 5; i++) {
            System.out.println(getName() + "...bb");
            try {
                Thread.sleep(10);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
};

t1.setDaemon(true);                     //将t1设置为守护线程

t1.start();
t2.start();
6.加入

join(), 当前线程暂停, 等待指定的线程执行结束后, 当前线程再继续
join(int), 可以等待指定的毫秒之后继续
final Thread t1 = new Thread() {
    public void run() {
        for(int i = 0; i < 50; i++) {
            System.out.println(getName() + "...aaaaaaaaaaaaaaaaaaaaaa");
            try {
                Thread.sleep(10);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
};

Thread t2 = new Thread() {
    public void run() {
        for(int i = 0; i < 50; i++) {
            if(i == 2) {
                try {
                    //t1.join();                        //插队,加入
                    t1.join(30);                        //加入,有固定的时间,过了固定时间,继续交替执行
                    Thread.sleep(10);
                } catch (InterruptedException e) {

                    e.printStackTrace();
                }
            }
            System.out.println(getName() + "...bb");

        }
    }
};

t1.start();
t2.start();
四.线程之间的同步
1.什么情况下需要同步
当多线程并发, 有多段代码同时执行时, 我们希望某一段代码执行的过程中CPU不要切换到其他线程工作. 这时就需要同步.
如果两段代码是同步的, 那么同一时间只能执行一段, 在一段代码没执行结束之前, 不会执行另外一段代码.
2.同步代码块

使用synchronized关键字加上一个锁对象来定义一段代码, 这就叫同步代码块
多个同步代码块如果使用相同的锁对象, 那么他们就是同步的

class Printer {
    Demo d = new Demo();
    public static void print1() {
        synchronized(d){                //锁对象可以是任意对象,但是被锁的代码需要保证是同一把锁,不能用匿名对象
            System.out.print("黑");
            System.out.print("马");
            System.out.print("程");
            System.out.print("序");
            System.out.print("员");
            System.out.print("\r\n");
        }
    }

    public static void print2() {   
        synchronized(d){    
            System.out.print("传");
            System.out.print("智");
            System.out.print("播");
            System.out.print("客");
            System.out.print("\r\n");
        }
    }
}
3.同步方法

使用synchronized关键字修饰一个方法, 该方法中所有的代码都是同步的

class Printer {
    public static void print1() {
        synchronized(Printer.class){                //锁对象可以是任意对象,但是被锁的代码需要保证是同一把锁,不能用匿名对象
            System.out.print("黑");
            System.out.print("马");
            System.out.print("程");
            System.out.print("序");
            System.out.print("员");
            System.out.print("\r\n");
        }
    }
    /*
     * 非静态同步函数的锁是:this
     * 静态的同步函数的锁是:字节码对象
     */
    public static synchronized void print2() {  
        System.out.print("传");
        System.out.print("智");
        System.out.print("播");
        System.out.print("客");
        System.out.print("\r\n");
    }
}
4.线程安全问题

多线程并发操作同一数据时, 就有可能出现线程安全问题
使用同步技术可以解决这种问题, 把操作数据的代码进行同步, 不要多个线程一起操作

public class Demo2_Synchronized {

    /**
     * @param args
     * 需求:铁路售票,一共100张,通过四个窗口卖完.
     */
    public static void main(String[] args) {
        TicketsSeller t1 = new TicketsSeller();
        TicketsSeller t2 = new TicketsSeller();
        TicketsSeller t3 = new TicketsSeller();
        TicketsSeller t4 = new TicketsSeller();

        t1.setName("窗口1");
        t2.setName("窗口2");
        t3.setName("窗口3");
        t4.setName("窗口4");
        t1.start();
        t2.start();
        t3.start();
        t4.start();
    }

}

class TicketsSeller extends Thread {
    private static int tickets = 100;
    static Object obj = new Object();
    public TicketsSeller() {
        super();

    }
    public TicketsSeller(String name) {
        super(name);
    }
    public void run() {
        while(true) {
            synchronized(obj) {
                if(tickets <= 0) 
                    break;
                try {
                    Thread.sleep(10);//线程1睡,线程2睡,线程3睡,线程4睡
                } catch (InterruptedException e) {

                    e.printStackTrace();
                }
                System.out.println(getName() + "...这是第" + tickets-- + "号票");
            }
        }
    }
}
5.死锁问题

多线程同步的时候, 如果同步代码嵌套, 使用相同锁, 就有可能出现死锁
尽量不要嵌套使用

private static String s1 = "筷子左";
private static String s2 = "筷子右";
public static void main(String[] args) {
    new Thread() {
        public void run() {
            while(true) {
                synchronized(s1) {
                    System.out.println(getName() + "...拿到" + s1 + "等待" + s2);
                    synchronized(s2) {
                        System.out.println(getName() + "...拿到" + s2 + "开吃");
                    }
                }
            }
        }
    }.start();

    new Thread() {
        public void run() {
            while(true) {
                synchronized(s2) {
                    System.out.println(getName() + "...拿到" + s2 + "等待" + s1);
                    synchronized(s1) {
                        System.out.println(getName() + "...拿到" + s1 + "开吃");
                    }
                }
            }
        }
    }.start();
}

一.线程的方法
1.yield让出cpu
2.setPriority()设置线程的优先级
二.单例设计模式
单例设计模式：保证类在内存中只有一个对象。

如何保证类在内存中只有一个对象呢？

(1)控制类的创建，不让其他类来创建本类的对象。private
(2)在本类中定义一个本类的对象。Singleton s;
(3)提供公共的访问方式。 public static Singleton getInstance(){return s}
单例写法两种：

(1)饿汉式 开发用这种方式。
//饿汉式
class Singleton {
    //1,私有构造函数
    private Singleton(){}
    //2,创建本类对象
    private static Singleton s = new Singleton();
    //3,对外提供公共的访问方法
    public static Singleton getInstance() {
        return s;
    }

    public static void print() {
        System.out.println("11111111111");
    }
}
(2)懒汉式 面试写这种方式。多线程的问题？
//懒汉式,单例的延迟加载模式
class Singleton {
    //1,私有构造函数
    private Singleton(){}
    //2,创建本类对象
    private static Singleton s;
    //3,对外提供公共的访问方法
    public static Singleton getInstance() {
        if(s == null)
            //线程1,线程2
            s = new Singleton();
        return s;
    }

    public static void print() {
        System.out.println("11111111111");
    }
}
(3)第三种格式
class Singleton {
    private Singleton() {}

    public static final Singleton s = new Singleton();//final是最终的意思,被final修饰的变量不可以被更改
}
Runtime类是一个单例类
Runtime r = Runtime.getRuntime();
//r.exec("shutdown -s -t 300");     //300秒后关机
r.exec("shutdown -a");              //取消关机
Timer类:计时器

public class Demo5_Timer {
    /**
     * @param args
     * 计时器
     * @throws InterruptedException 
     */
    public static void main(String[] args) throws InterruptedException {
        Timer t = new Timer();
        t.schedule(new MyTimerTask(), new Date(114,9,15,10,54,20),3000);

        while(true) {
            System.out.println(new Date());
            Thread.sleep(1000);
        }
    }
}
class MyTimerTask extends TimerTask {
    @Override
    public void run() {
        System.out.println("起床背英语单词");
    }

}
三.线程之间的通信
1.什么时候需要通信
多个线程并发执行时, 在默认情况下CPU是随机切换线程的
如果我们希望他们有规律的执行, 就可以使用通信, 例如每个线程执行一次打印
2.怎么通信
如果希望线程等待, 就调用wait()
如果希望唤醒等待的线程, 就调用notify();
这两个方法必须在同步代码中执行, 并且使用同步锁对象来调用
3.多个线程通信的问题
notify()方法是随机唤醒一个线程
notifyAll()方法是唤醒所有线程
JDK5之前无法唤醒指定的一个线程
如果多个线程之间通信, 需要使用notifyAll()通知所有线程, 用while来反复判断条件
四.JDK5之后的线程控制
1.同步
使用ReentrantLock类的lock()和unlock()方法进行同步
2.通信
使用ReentrantLock类的newCondition()方法可以获取Condition对象
需要等待的时候使用Condition的await()方法, 唤醒的时候用signal()方法
不同的线程使用不同的Condition, 这样就能区分唤醒的时候找哪个线程了
五.同步与非同步类的总结
StringBuffer和StringBuilder,StringBuffer是线程安全的,效率低,StringBuilder是线程不安全的,效率高
Vector和ArrayList,Vector是线程安全的,效率低,ArrayList是线程不安全的,效率高
Hashtable和HashMap,Hashtable是线程安全的,效率低,HashMap是线程不安全的,效率高