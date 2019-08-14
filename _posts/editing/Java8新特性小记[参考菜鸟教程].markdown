# 部分新特性
1. **lambda** - 减少代码冗余，但可读性会略有降低

2. **操作符**
	
	1. **map** - 对于每一个元素都按照特定函数进行变换
	2. **flatMap** - 可进行元素的一对多/多对多的变换

---
> 全部测试案例
```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;
import java.nio.charset.StandardCharsets;
import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.util.*;
import java.util.function.BiFunction;
import java.util.function.IntBinaryOperator;
import java.util.function.Predicate;
import java.util.function.Supplier;
import java.util.stream.Collectors;

public class Java8Test {

    public static void main(String[] args) {

        lambda();
        varScope();

        methodQuote();

        methodInterface();

        methodDefault();

        stream();

        optional();

        nashorn();

        date();

        base64();
    }


    /**
     * 1. lambda
     * 闭包
     */
    private static void lambda() {
        IntBinaryOperator add = (int a, int b) -> a + b;
        IntBinaryOperator sub = (a, b) -> a - b;
        IntBinaryOperator multi = (int a, int b) -> a * b;
        IntBinaryOperator div = (a, b) -> a / b;
        BiFunction<String, String, Object> greet = (String s1, String s2) -> s1 + "! " + s2;
        System.out.println("4 + 2 = " + add.applyAsInt(4, 2));
        System.out.println("4 - 2 = " + sub.applyAsInt(4, 2));
        System.out.println("4 * 2 = " + multi.applyAsInt(4, 2));
        System.out.println("4 / 2 = " + div.applyAsInt(4, 2));
        System.out.println("greet to catface --> " + greet.apply("hi", "catface"));

        new Thread(() -> System.out.println("thread running...")).start();
    }


    /*
     * 1.2. 变量作用域
     */
    interface Callback {
        void complete(String msg);
    }

    private static void varScope() {
        String date = new Date().toString();
        Callback callback = msg -> System.out.println("you have msg: " + msg + " -- " + date);
        callback.complete("another day has gone, you are not alone...");
    }


    /**
     * 2. 方法引用
     * 使用::引用方法以减少代码冗余
     */
    static class Person {
        public static Person create(Supplier<Person> supplier) {
            return supplier.get();
        }

        public static void showCommonMsg(Person person) {
            System.out.println("person's common msg...");
        }

        public void showPrivateMsg(Person person) {
            System.out.println("person's private msg...");
        }

        public void eat() {
            System.out.println("is eating...");
        }
    }


    /**
     * 3. 函数式接口
     * 方便被转换为lambda
     */
    private static void methodQuote() {
        // 1. 构造器引用[Class<T>::new]
        Person[] persons = {Person.create(Person::new), Person.create(Person::new)};
        List<Person> peoples = Arrays.asList(persons);
        // 2. 静态方法引用[Class::static_method]
        peoples.forEach(Person::showCommonMsg);
        // 3. 特定对象的方法引用[instance::methodQuote]
        peoples.forEach(Person.create(Person::new)::showPrivateMsg);
        //4. 特定类的任意对象的方法引用[Class::methodQuote]
        peoples.forEach(Person::eat);

        // 方法引用实例
        String[] names = {"alistar", "akali", "ashe", "amumu", "ahri", "anivia", "annie"};
        Arrays.asList(names).forEach(System.out::println);
    }

    private static void methodInterface() {
        List<Integer> integers = Arrays.asList(-1, 0, 1, 3, 5, 7, 9, 11);
        System.out.print("集合中所有数据：");
        eval(integers, i -> true);

        System.out.print("集合中偶数：");
        eval(integers, i -> i % 2 == 0);

        System.out.print("集合中所有>4的数：");
        eval(integers, i -> i > 4);

    }

    private static void eval(List<Integer> list, Predicate<Integer> predicate) {
        for (Integer i : list) {

            if (predicate.test(i)) {
                System.out.print(i + " || ");
            }
        }
        System.out.println();
    }


    /**
     * 4. 接口默认方法
     * default为接口添加实现方法
     */
    interface Animal {
        // 1. 接口的默认方法可被重写
        default void run() {
            System.out.println("animal is running...[interface's default method]");
        }

        // 2. 接口的静态方法不可被重写
        static void eat() {
            System.out.println("animal is eating...[interface's static method]");
        }
    }

    static class Cat implements Animal {
        @Override
        public void run() {
            Animal.super.run();
            System.out.println("cat is running...");
        }
    }

    private static void methodDefault() {
        new Cat().run();
        Animal.eat();
    }


    /**
     * 5. Stream
     * 元素流
     */
    private static void stream() {
        // forEach[迭代] || limit[获取指定数量的流]
        new Random().ints().limit(7).forEach(System.out::println);

        // map
        List<Integer> integers = Arrays.asList(1, 5, 9, 3, 7, 9, 5, 2);
        List<Integer> collect1 = integers.stream().map(i -> i * 2).collect(Collectors.toList());
        System.out.println("map: " + collect1);

        // flatMap
        List<String> greets = Arrays.asList("hi", "hello", "welcome");
        List<String> names = Arrays.asList("alistar", "akali", "ahri");
        List<Object> collect = greets.stream().flatMap(strings -> names.stream().map(s -> strings + " - " + s)).collect(Collectors.toList());
        System.out.println("flatMap: " + collect);

        // filter || distinct[去重]
        List<Integer> collect2 = integers.stream().filter(i -> i > 4).distinct().collect(Collectors.toList());
        System.out.println("filter + distinct: " + collect2);

        // sorted排序
        List<Integer> collect3 = integers.stream().sorted(Comparator.comparingInt(o -> -o % 2)).collect(Collectors.toList());
        System.out.println("sorted with Comparator: " + collect3);

        // parallel[并行运行]
        List<String> strings = Arrays.asList("qq", "", "ww", "ee", "rr");
        List<String> collect4 = strings.parallelStream().filter(str -> !str.isEmpty()).collect(Collectors.toList());
        System.out.println("parallel: " + collect4);

        // reduce
        integers.stream().reduce((i1, i2) -> i1 + i2).ifPresent(System.out::println);
        integers.stream().reduce((i1, i2) -> i1 > i2 ? i1 : i2).ifPresent(System.out::println);
        integers.stream().reduce(Integer::min).ifPresent(System.out::println);

        // multi reduce
        testMultiReduce();

        // 统计
        IntSummaryStatistics intSummaryStatistics = integers.stream().mapToInt(x -> x).summaryStatistics();
        System.out.println("sum: " + intSummaryStatistics.getSum());
        System.out.println("max: " + intSummaryStatistics.getMax());
        System.out.println("min: " + intSummaryStatistics.getMin());
        System.out.println("average: " + intSummaryStatistics.getAverage());
        System.out.println("count: " + intSummaryStatistics.getCount());
    }

    private static void testMultiReduce() {
        ArrayList<List<String>> strings = new ArrayList<>();
        strings.add(Arrays.asList("1", "2", "3", "4"));
        strings.add(Arrays.asList("2", "3", "4", "5"));
        strings.add(Arrays.asList("3", "4", "5", "6"));

        // 非并行流
        Integer reduce1 = strings.stream().flatMap(Collection::stream).reduce(0,
                (str, i) -> str + Integer.valueOf(i), (i1, i2) -> {
                    // 非并行流，不会执行第三个参数
                    System.out.println("i1、i2: " + i1 + "、" + i2);
                    // 这里的返回值并没有影响返回结果
                    return null;
                });
        System.out.println("reduce1: " + reduce1);

        // 并行流
        Integer reduce2 = strings.parallelStream().flatMap(Collection::stream).reduce(0,
                (str, i) -> str + Integer.valueOf(i), (i1, i2) -> {
                    // u，t分别为并行流每个子任务的结果
                    System.out.println("i1、i2: " + i1 + "、" + i2);
                    return i1 + i2;
                });
        System.out.println("reduce2: " + reduce2);
    }


    /**
     * 6. Optional
     * 可为null的容器对象
     */
    private static void optional() {
        Integer i1 = null;
        Integer i2 = 7;

        Optional<Integer> o1 = Optional.ofNullable(i1);
        Optional<Integer> o2 = Optional.ofNullable(i2);

        System.out.println(sum(o1, o2));
    }

    private static Integer sum(Optional<Integer> a, Optional<Integer> b) {
        // Optional.isPresent
        System.out.println("第一个参数值存在: " + a.isPresent());
        System.out.println("第二个参数值存在: " + b.isPresent());

        // Optional.orElse: 不为空则值为a否则值为other默认值
        int i1 = a.orElse(0);
        //Optional.get(): 必须不为null否则报错
        int i2 = b.orElse(0);
        return i1 + i2;
    }


    /**
     * 7. Nashorn JS
     * 使用ScriptEngineManager在Java中执行JS
     */
    private static void nashorn() {
        ScriptEngineManager scriptEngineManager = new ScriptEngineManager();
        ScriptEngine nashorn = scriptEngineManager.getEngineByName("nashorn");

        String name = "catface";
        Integer result = null;

        try {
            nashorn.eval("print('" + name + "')");
            result = (Integer) nashorn.eval("10 + 2");

        } catch (ScriptException e) {
            System.out.println("执行脚本错误 : " + e.getMessage());
        }

        System.out.println(result != null ? result.toString() : null);
    }


    /**
     * 8. 日期时间API
     */
    private static void date() {
        LocalDateTime now = LocalDateTime.now();

        System.out.println(now + " || " + now.toLocalDate() + " || " + now.toLocalTime());
        System.out.println(now.getYear() + " || " + now.getMonthValue() + " || " + now.getDayOfMonth() + " || " + now.getDayOfYear() + " || " + now.getDayOfWeek() + " || " + now.getHour() + " || " + now.getMinute() + " || " + now.getSecond() + " || " + now.getNano());

        // 时区
        ZonedDateTime date = ZonedDateTime.parse("2015-12-03T10:15:30+05:30[Asia/Shanghai]");
        System.out.println(date);

        ZoneId zoneId = ZoneId.of("Europe/Paris");
        System.out.println("zoneId: " + zoneId + " || 当前时区：" + zoneId.systemDefault());
    }


    /**
     * 9. base64
     * 基本：输出被映射到一组字符A-Za-z0-9+/，编码不添加任何行标，输出的解码仅支持A-Za-z0-9+/
     * URL：输出映射到一组字符A-Za-z0-9+_，输出是URL和文件
     * MIME：输出隐射到MIME友好格式。输出每行不超过76字符，并且使用'\r'并跟随'\n'作为分割。编码输出最后没有行分割
     */
    private static void base64() {
        // 基本编码
        String encode = Base64.getEncoder().encodeToString("catface".getBytes(StandardCharsets.UTF_8));
        System.out.println("base64编码[基本] : " + encode);

        // 解码
        System.out.println("原始字符串 : " + new String(Base64.getDecoder().decode(encode), StandardCharsets.UTF_8));

        // URL编码
        encode = Base64.getUrlEncoder().encodeToString("catfaceWYH".getBytes(StandardCharsets.UTF_8));
        System.out.println("base64编码[URL] : " + encode);

        // MIME编码
        StringBuilder stringBuilder = new StringBuilder();
        for (int i = 0; i < 10; ++i) {
            stringBuilder.append(UUID.randomUUID().toString());
        }

        byte[] mimeBytes = stringBuilder.toString().getBytes(StandardCharsets.UTF_8);
        System.out.println("base64编码[MIME] : " + Base64.getMimeEncoder().encodeToString(mimeBytes));
    }
}
```