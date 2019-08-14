继承extends，不支持多继承，但支持多层继承



如何使用一个继承体系中的功能呢？



想要使用体系，先查阅体系父类的描述，因为父类中定义的是该体系中共性功能。

通过了解共性功能，就可以知道该体系的基本功能。

那么这个体系已经可以基本使用了。

那么在具体调用时，要创建最子类的对象，为什么呢？

一是因为有可能父类不能创建对象，

二是创建子类对象可以使用更多的功能，包括基本的也包括特有的。





简单一句话：查阅父类功能，创建子类对象使用功能。

---------------------------------------------------

1.多态的体现：

向上转型：父类的引用指向了自己的子类对象，这样的话，父类引用就变成父类成员，使用的方法是子父类的交集，也就是子类继承父类后重写的方法

向下转型:强制将父类的引用，转成子类对象。记住不能将父类转成子类，因为父类本身不具备子类有的内容



1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

abstract class Animal{ abstract void eat();}

class Cat extends Animal{

public void eat(){

System.out.println("吃鱼");

}

public void catchMouse(){

System.out.println("抓老鼠");

}

}

class Dog extends Animal{

public void eat(){

System.out.println("吃骨头");

}

publci void kanJia(){

System.out.pritnln("吃骨头");

}

}

public static void function(Animal a) //Animal a=new Cat();

{

a.eat;

if(a instanceof Cat){

Cat c=(Cat)a;

c.catchMouse();

}else if(a instanceof Dog){

Dog c=(Dog)a;

c.kanJia();

}

}

main(){

function(cat);

function(dog);

}



--



向上转型    

Animal a=new Cat();

a.eat





向下转型

Cat c =(Cat)a



if (a instanceof Type)    判断对象是否是继承或者等于某个Type类

if (this.getClass()==obj.getClass)判断对象的类型是否和某个类相同



-----------------------

面试题，一般开发不会出现

小技巧：

在多态总花姑娘成员函数的特点：

在编译时期：查阅 引用型所属的类中 是否有调用的方法。如果有，编译通过，如果没有，就编译失败

在运行时期：查阅对象所属类中是否有调用的方法

简单方法总结就是：成员函数在多态调用时，编译看左边，运行看右边





Animal a=new Cat();

a.eat

a.catchMouse

左边： Animal是否有catchMouse方法,如果没有，就已经是编译不通过了

右边：Cat是否有catchMouse eat方法，如果有，那么就用Cat方法，如果没有就会用父类方法，那么就会运行失败（因为父类一般是抽象类）





在多态中，成员变量的特点：

无论编译和运行，都参考左边（引用型变量所属的类）



静态成员的话，是不用参考右边的，因为不需要对象，所以，左边哪个类调用静态成员或者方法，就是该类的静态成员或者方法，就是该类的静态所属

---



赋值的多态

Quadrangle obj=new Square();声明的变量obj是Quadrangle类型的，而赋值却是Square类型的实际变量

Quadrangle obj1=new Parallelogram();   



Suqare newObj=(Square)quaObj;   强制类型转换



多态数组--将父类数组元素进行子类的对象赋值

1

2

3

4

5

6

Quadrangle[] quadrangles=new Quadrangle[3];

quadrangles[0]=new Square();

quadrangles[1]=new Parallelogram();

for (Quadrangle obj:quadrangles){

obj.draw();

}





返回类型的多态--通过定义父类类型的方法，返回父类型的初始值

1

2

3

4

public Quadrangle getQuadrangle(){

Quadrangle tmp=new Quadrangle();

return tmp;

}



方法的多态--将父类方法用于的参数定义为父类成员，那么调用此方法的子类成员都也可以调用父类方法

1

2

3

4

5

public void alldraw(Quadrangle quadrangle){

quadrangle.draw;

}

Quadrangle.alldraw(square);

Quadrangle.alldraw(parallelogram);





将父类Quadrangle  进行继承给    Suqare和Parallelogram。

然后利用Quadrangle类格式变成数组格式，然后将子类对象的实参  赋值给父类的对象，在用foreach进行输出每个元素的draw()方法。

---------------------------------------------------------------------------------

1

2

3

4

5

public class Quadrangle{

public void draw(){

System.out.println("绘制自身图形");

}

}

--------------------------



1

2

3

4

5

public class Square extends Quadrangle {

public void draw(){

System.out.println("正方形");

}

}

----------------------------

1

2

3

4

5

public class Parallelogram extends Quadrangle {

public void draw(){

System.out.println("长方形");

}

}





-------------------------------

1

2

3

4

5

6

7

8

9

10

11

public class Demo{

public static void main(String[] args){

Quadrangle[] quadrangles=new Quadrangle[3];

quadrangles[0]=new Square();

quadrangles[1]=new Square();

quadrangles[2]=new Square();

for (Quadrangle obj:quadrangles){

obj.draw();

}

}

}