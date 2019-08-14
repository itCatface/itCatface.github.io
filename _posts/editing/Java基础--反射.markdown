所有的框架和服务器开发都是用的反射技术，学好反射对日后更深层次的开发是非常重要的。

通过反射可以动态的获取类的成员，在不想改动源代码的情况下修改类，这样我们就可以通过反射技术将这个类加载进来。我们在框架用xml文件进行配置的时候，实际上就是获取到类名使用反射动态的加载进来，大大提高了可扩展性，另外再访问私有属性的时候是访问不到的，因为它不可见，如果非要访问的话可以用暴力反射进行访问

实例：



[java] view plaincopy

/* 
 * 执行字节码文件中一个方法。 
 */  
private static void getSingleMethod() throws ClassNotFoundException, Exception, Exception {  
    Class clazz = Class.forName("cn.test.demo.Person");  
    //指定要运行的方法  
    Method method = clazz.getMethod("show2", null);  
    //调用此方法并运行  
    method.invoke(clazz.newInstance(), null);  
}  
  
/* 
 * 当动态加载的类中的没有空参数构造函数时。 
 * 需要获取指定的构造函数进行该字节码文件对象的初始化。 
 */  
private static void getConstructor() throws Exception {  
    Class clazz = Class.forName("cn.test.demo.Person");  
    //获取到指定参数类型的构造函数对象。  
    Constructor constructor = clazz.getConstructor(String.class);  
    //通过构造器创建该类的实例  
    Person p = (Person)constructor.newInstance("zhangan");  
    //获取要调用的方法  
    Method method = clazz.getMethod("show",int.class);  
    //执行方法，获取返回值  
    String str = (String)method.invoke(p, 88);  
    System.out.println("str="+str);  
}  
  
/* 
 * 获取指定类中的方法。 
 */  
private static void getClassMethod() throws ClassNotFoundException {  
    Class clazz = Class.forName("cn.test.demo.Person");  
    //获取包括父类的方法，只能获取共有的方法  
    Method[] methods = clazz.getMethods();  
    //不能获取父类的方法可以获取指定类的私有和共有的方法  
    methods = clazz.getDeclaredMethods();  
    for(Method m : methods){  
        System.out.println(m.toString());  
    }  
}  
  
/* 
 * 获取字节码文件对象的三种方式 
 */  
private static void demoGetClass() throws ClassNotFoundException {  
      
    //方式一，getClass();  
    Person p = new Person();  
    Class clazz = p.getClass();  
    System.out.println(clazz.getName());  
      
    //方式二，每一个类都有一个属性 .class.  
    Class c2 = Person.class;  
    System.out.println(c2.getName());  
      
    //方式三，通过Class类中的一个static方法forName获取一个字节码文件对象。  
    //给forName传值必须是类的全名称。  
    Class c3 = Class.forName("cn.test.demo.Person");  
    System.out.println(c3.getName());  
}  
Person.java:



[java] view plaincopy

public class Person {  
  
    private String name;  
    public Person(){  
        System.out.println("person run");  
    }  
    public Person(String name){  
        this.name =name;  
        System.out.println("-------------");  
    }  
      
    public String show(int num){  
        System.out.println("num="+num+"--show run--"+name);  
        return "hahha";  
    }  
      
    public void show2(){  
        System.out.println("------123-------");  
    }  
    public void haha(String s){  
        System.out.println("haha="+s);  
    }  
    private void function(){  
        System.out.println("functio run");  
    }  
}  




总结：

1.加载类的三种方式：

[java] view plaincopy

//加载类方法1：  
String classname ="cn.itcast.bean.Person";  
Class clazz1=Class.forName(classname); //获取类的字节码拿到类  
  
//加载类方法2：  
Class clazz2=Person.class;  //在框架中用的不多  
  
//加载类方法3：  
Class clazz3=new Person().getClass();  



2.反射构造方法创建类的实例：

构造函数有四种方式：无参、有参、多个参数、私有构造函数。

[html] view plaincopy

public Person(){}  
  
public Person(String name){  
    this.name=name;  
}  
public Person(String name,List list){  
      
}  
private Person(Set set){  
      
}  

        针对以上四种构造方法的反射如下：

[java] view plaincopy

//反射无参的构造函数  
@Test  
public void test2 () throws Exception{  
    String classname ="cn.itcast.bean.Person";  
    Class clazz1=Class.forName(classname);  //加载类  
    Constructor c=clazz1.getConstructor(null);//拿到无参的构造函数  
    Object obj =c.newInstance(null);    //创建实例对象  
    System.out.println(obj);  
}  
//反射有参的构造函数  
@Test  
public void test3 () throws Exception{  
    String classname ="cn.itcast.bean.Person";  
    Class clazz1=Class.forName(classname);   
    Constructor c=clazz1.getConstructor(String.class);//拿到有参的构造函数  
    Object obj =c.newInstance("aaa");   //创建实例对象  
    System.out.println(obj);  
}  
//反射有多个参数的构造函数  
@Test  
public void test4 () throws Exception{  
    String classname ="cn.itcast.bean.Person";  
    Class clazz1=Class.forName(classname);   
    Constructor c=clazz1.getConstructor(String.class,List.class);//拿到多个参数的构造函数  
    Object obj =c.newInstance("bbb",new ArrayList());     
    System.out.println(obj);  
}  
//反射私有的构造函数  
@Test  
public void test5 () throws Exception{  
    String classname ="cn.itcast.bean.Person";  
    Class clazz1=Class.forName(classname);   
    Constructor c=clazz1.getDeclaredConstructor(Set.class);//得到类里面声明的成员  
    c.setAccessible(true);      //暴力反射  
    Object obj =c.newInstance(new HashSet());     
    System.out.println(obj);  
}  


3.反射方法：

          方法共有五几种形态：

[java] view plaincopy

public void a1(){  
    System.out.println("hahaa");  
}  
  
public void a2(String name){  
    System.out.println(name);  
}  
  
public String a3(String name ,String password){  
    return name+password;  
}  
  
private String a4(List list){  
    return list.toString();  
}  
  
private static void a5(String arr[]){  
    System.out.println(Arrays.asList(arr));  
}  
 
            针对五种形态的反射方法如下：

[java] view plaincopy

//反射无参方法  
@Test  
public void test1() throws Exception{  
    Person  p=new Person();  
    Class clazz=Class.forName("cn.itcast.bean.Person");//拿到类  
    Method m=clazz.getMethod("a1",null);    //反射无参数的构造方法  
    m.invoke(p,null);   //执行无参构造方法  
}  
//反射一个参数的方法  
@Test  
public void test2() throws Exception{  
    Person  p=new Person();  
    Class clazz=Class.forName("cn.itcast.bean.Person");  
    Method m=clazz.getMethod("a2",String.class);    //反射有参数的构造方法  
    m.invoke(p,"aaaaa");      
}  
//反射多个参数的方法  
@Test  
public void test3() throws Exception{  
    Person  p=new Person();  
    Class clazz=Class.forName("cn.itcast.bean.Person");  
    Method m=clazz.getMethod("a3",String.class,String.class);     
    String result=(String) m.invoke(p,"aaaaa","bbbbbb");      
    System.out.println(result);  
}  
//反射私有的方法  
@Test  
public void test4() throws Exception{  
    Person  p=new Person();  
    Class clazz=Class.forName("cn.itcast.bean.Person");  
    Method m=clazz.getDeclaredMethod("a4",List.class);  //得到声明的方法  
    m.setAccessible(true);  //暴力反射  
    String result=(String) m.invoke(p,new ArrayList());   
    System.out.println(result);  
}   
//反射私有的静态方法  
@Test  
public void test5() throws Exception{  
    Class clazz=Class.forName("cn.itcast.bean.Person");  
    Method m=clazz.getDeclaredMethod("a5",String [].class);   
    m.setAccessible(true);  //暴力反射  
    m.invoke(null,(Object)new String []{"1","2"});    
}   



4.反射字段

       反射私有字段

[java] view plaincopy

//反射私有字段  
@Test  
public void test1() throws Exception{  
    Person p =new Person();  
    Class clazz=Class.forName("cn.itcast.bean.Person");  
    Field f=clazz.getDeclaredField("name"); //拿到字段  
    f.setAccessible(true);  
    f.set(p,"frk");     //封装值  
    String name=(String) f.get(p);//得到值  
    System.out.println(name);  
} 