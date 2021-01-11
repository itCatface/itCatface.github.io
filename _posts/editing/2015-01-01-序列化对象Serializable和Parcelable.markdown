---
temp-layout:       post
temp-title:        "序列化对象Serializable和Parcelable"
temp-subtitle:     ""
temp-date:         2015-01-01 12:00:00
temp-header-img:   "img/color-android-robot-green.png"
temp-tags:
    - android
---

# 创建方式
1. Serializable：java自带的序列化api，即实现该接口即可
	
	```java
	public class Person implements Serializable {
	
	    private static final long serialVersionUID = -4298488259928482555L;
	    private String name;
	    private int age;
	
	    public String getName() {
	        return name;
	    }
	
	    public void setName(String name) {
	        this.name = name;
	    }
	
	    public int getAge() {
	        return age;
	    }
	
	    public void setAge(int age) {
	        this.age = age;
	    }
	}
	```
	IDEA提供代码检查，会提示实现了Serializable的类未添加serialVersionUID字段，打开该检查方式如下
	![在这里插入图片描述](https://img-blog.csdnimg.cn/20190106202135276.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2l0Q2F0ZmFjZQ==,size_16,color_FFFFFF,t_70)
2. Parcelable：android提供的序列化方式，即实现该接口覆写接口提供的方法，并创建Creator<T>
	
	```java
	public class Student implements Parcelable {
	
	    private String name;
	    private int score;
	
	    public Student() {
	
	    }
	
	    public String getName() {
	        return name;
	    }
	
	    public void setName(String name) {
	        this.name = name;
	    }
	
	    public int getScore() {
	        return score;
	    }
	
	    public void setScore(int score) {
	        this.score = score;
	    }
	
	    public static final Creator<Student> CREATOR = new Creator<Student>() {
	        @Override public Student createFromParcel(Parcel in) {
	            return new Student(in);
	        }
	
	        @Override public Student[] newArray(int size) {
	            return new Student[size];
	        }
	    };
	
	    @Override public int describeContents() {
	        return 0;
	    }
	
	    @Override public void writeToParcel(Parcel dest, int flags) {
	        dest.writeString(name);
	        dest.writeInt(score);
	    }
	
	    private Student(Parcel in) {
	        name = in.readString();
	        score = in.readInt();
	    }
	}
	```

# 两者的简单比较

1. Serializable是JavaSE提供的api；Parcelable是android为了提升序列化性能单独提供的api

2. Serializable是通过IO读写序列化至磁盘，序列化过程中用到了反射，且会产生大量临时对象，会导致系统频繁GC，所以效率较低；Parcelable直接在内存中完成序列化过程，效率较高

3. 需要持久保存的数据建议使用Serializable，因为可以将数据序列化至磁盘上；android中通过Intent传递的序列化数据建议使用Parcelable，毕竟专门提供的方式嘛，实现方式麻烦点，但是效率高不少