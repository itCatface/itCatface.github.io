抽象类(abstract)
(1)只抽取了很多类 的方法的声明，为了保证不出问题，方法声明用abstract修饰
(2)抽象类的特点
A：一个类如果有了抽象方法，那么这个类必须是抽象类。抽象类里边可以没有抽象方法
B：抽象类是不能够被实例化的。不能够创建对象的
C：如果一个类继承抽象类，那么，它要么重写抽象类中的所有抽象方法，要么本身也是抽象类
(3)抽象类的成员特点
A：成员变量：子类可以直接继承抽象类中的成员变量。(抽象类中的成员变量可以和以前是一样的)
B：成员方法：抽象类中分为两种方法， 一种是抽象方法，这种方法在子类中必须要被实现。 一种是普通的方法。可以被子类直接继承使用
C：构造方法：抽象类不能被实例化，那么它有构造方法吗?抽象类是class，那么它就有构造方法。它的构造方法有用吗？有，为了让子类实例化的时候使用
(4)抽象类的相关问题：
A：抽象类中是否有构造函数？参照(3)里面的C
B：抽象关键字abstract不可以和哪些关键字共存？
private
私有的，外部直接无法访问。子类也同样无法访问
abstrac修饰的方法就是为了让子类继承并重写的
static
那么这个时候抽象方法就可以可以通过类名调用，但是这样是没有意义的
final
final修饰的方法不能被重写。所以它和abstract冲突
C：抽象类中可不可以没有抽象方法？
可以。如果这么做只有一个目的不让你创建这个类的对象
2:接口(interface)
(1)接口的由来：当一个类中所有的方法都是抽象的时候，定义为接口。
(2)成员特点：
A：只有成员变量和成员方法
B：成员变量：默认修饰符 public static final
int X = 20;
其实是这样的 public static final int X = 20;
C：成员方法 默认修饰符 public abstract
void show();
其实是这样的 public abstract void show();
(3)解决了java中只能单继承的问题。(对多继承进行了优化)

A：类与类：只能是单继承。 extends
B：接口与接口：可以是单继承，也可以是多继承。 extends
C：类与接口：可以是单实现，也可以是多实现。 implements
(4)接口特点：

A：接口是对外暴露的规则
B：接口是功能的扩展
C：接口降低了程序的耦合性
高内聚，低耦合
D：扩展说了下接口的理解
狭义的理解就是java中的接口
广义的理解就是：任何定义的规范都是接口
(5)接口和抽象类的区别：
A：抽象类只能被单继承；接口可以被多实现
B：
抽象类中的成员：
成员变量:可以是常量，也可以是变量
成员方法:可以是抽象的，也可以是非抽象的
构造方法:虽然不可以创建对象，但是可以给子类实例化用
接口中的成员：
成员变量：只能是常量。默认修饰符public static final
成员方法：只能是抽象的。默认修饰符public abstract
C：抽象类中定义的是体系结构中的共性的内容。接口中定义的是对象的扩展功能
D：抽象类被继承表示的是："is a"的关系。xx是yy中的一种。接口被实现表示的是: "like a"的关系。xx像yy中的一种
(6)学生：Student

A属性：学号,姓名,年龄
B方法：学习(study),吃饭(抽象eat),抽烟(是不是所有的学员都抽烟呢?),篮球(是不是所有的人都会打篮球呢?)
分析：学员都具备学习的行为和吃饭的行为,但是并不是所有的学员都抽烟,也不是所有的学员都打篮球
 interface Smoking {
    public abstract void smoking();
 }
 interface Sport{
    public abstract void playBasketBall();
 }
描述的是即会抽烟又会打篮球的学生：SmokeStudent extends Student implements Smoking, Sport

一个类只能继承一个类,但是可以实现多个接口,每实现一个接口,功能就扩展了一部分
SmokeStudent ss = new SmokeStudent();
ss.eat();
ss.study();
ss.smoking();
ss.playBasketBall();
package
1. 定义包
使用package关键字在类的第一条语句定义包名
包名必须全部小写, 一般用域名
2. 编译带包的类
javac -d <目录> 源文件名.java
例如：javac -d . Person.java 编译到当前目录
3. 默认包
如果一个类没有加上package关键字定义包名, 它是在一个默认的包中,以前我们使用的类都没有定义包, 默认都在同一个包中, 互相直接可以直接访问
如果两个类定义了包, 并且是相同的包, 也可以直接访问
4. 运行带包的类
java 包名.类名(全限定名)
例如：java cn.itcast.day11.PackageDemo
5. 访问权限
private：私有, 只有当前类可用. 类是不能私有的
default：同包中的类可用. 类默认也是只能同包内使用
protected：保护, 同包中的类和子类可用. 类不能使用这个修饰符
public：公有, 所有的类都可用. 如果一个类希望被其他包中类使用, 必须使用* public修饰. public的类必须和文件名一致
6. 导入其他包中的类
首先要使用的类必须是public修饰的
使用import关键字可以导入其他包中的类
a：星号方式导入. 导入指定包中所有的类. 如果当前包中有同名的类, 优先使用当前包中的
b：类名方式导入. 导入指定包中指定的类. 无论当前包中是否有需要的类, 都使用导入的包中的类
如果一个类中要是用两个包中同名的类, 那么每次使用的时候都加上包名即可
7. 有包类和无包类之间的访问问题
无包的类能访问有包的类吗?
有包的类能访问无包的类吗?
8. 重点
写类的时候要加上包名
类要public, 并且类名和文件名一致
导入类要写类名
编译用-d, 运行带包名
内部类
成员内部类
A定义：在一个外部类中有成员变量和成员方法,那么成员内部类就是把整个一个类当成了外部类的成员对待了
B访问方式：内部类访问外部类,内部类可以直接访问外部类,包括私有成员,因为内部类拥有外部类的引用是类名.this
外部类访问内部类,外部类访问外部类的成员,必须要建立内部类的对象
格式：外部类名.内部类名 = 外部类对象.内部类对象;
Outer.Inner oi = new Outer().new Inner(); // outer代表外部类,Inner代表内部类
C存放位置：在外部类里,在外部类的成员方法外
D修饰符：final、abstract、public、private、protected和static等,那么被static修饰的就是下面所说的
(2)静态内部类
A定义：就是在成员内部类的基础上加上static
B格式：外部类名.内部类名 = 外部类名.内部类对象; Outer.Inner oi = new Outer.Inner();
C存放位置：和成员内部类一样,就是多了个static
(3)局部内部类
A定义：在外部类成员方法中定义的内部类,他更像局部变量
B注意：
第一：方法内部类只能在定义该内部类的方法内实例化，不可以在此方法外对其实例化
第二：方法内部类对象不能使用该内部类所在方法的非final局部变量。因为方法的局部变量位于栈上，只存在于该方法的生命期内。当一个方法结束，其栈结构被删除，局部变量成为历史。但是该方法结束之后，在方法内创建的内部类对象可能仍然存在于堆中！例如，如果对它的引用被传递到其他某些代码，并存储在一个成员变量内。正因为不能保证局部变量的存活期和方法内部类对象的一样长，所以内部类对象不能使用它们
第三：方法内部类的修饰符。与成员内部类不同，方法内部类更像一个局部变量。可以用于修饰方法内部类,的只有final和abstract
第四：静态方法内的方法内部类。静态方法是没有this引用的，因此在静态方法内的内部类遭受同样的待遇，即：只能访问外部类的静态成员
(4)匿名内部类：没有名字的内部类。它是内部类的简化写法。是局部内部类的一种
A前提：内部类可以继承或实现一个外部类或者接口
B格式为：new 外部类名或者接口名(){覆盖类或者接口中的抽象的方法，(也可以自定义内容。)}
C简单理解：就是建立一个带内容的外部类或者接口的子类的匿名对象
D匿名内部类几种常用方式
a：继承式的匿名内部类
b：接口式(也可以叫实现式的,名字无所谓)的匿名内部类
c：参数式的匿名内部类
interface Inter {
    public abstract void show1();
    public abstract void show2();
}

// 有名字的内部类
class Outer {
    public void method() {
        class Inner implements Inter {
            public void show1() {
                System.out.println("show1");
            }

            public void show2() {
                System.out.println("show1");
            }
        }
    }
    public void show() {
        Inter in = new Inner(); // 父类引用指向子类对象
        in.show1();
        in.show2();

    }
}

// 匿名内部类(重点,android里面用的多,awt的监听器用的多)
class Outer {
    public void method() {
        // 匿名内部类对象调用方法
        new Inter() {
            public void show1() {
                System.out.println("show1");
            }

            public void show2() {
                System.out.println("show1");
            }
        }.show1();

        new Inter() {
            public void show1() {
                System.out.println("show1");
            }

            public void show2(){
                System.out.println("show1");
            }
        }.show2();

        // 匿名内部类对象的另一种调用方式,父类引用指向子类对象
        Inter in = new Inter() {
            public void show1() {
                System.out.println("show1");
            }

            public void show2() {
                System.out.println("show1");
            }
        };
        in.show1();
        in.show2();
    }
}
(5)什么时候使用匿名内部类呢？

通常在使用方法是接口类型参数，并该接口中的方法只有一个时，可以将匿名内部类作为参数传递
