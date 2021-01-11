---
temp-layout:       post
temp-title:        "startActivityForResult()使用说明"
temp-subtitle:     ""
temp-date:         2015-01-01 12:00:00
temp-header-img:   "img/color-android-robot-green.png"
temp-tags:
    - android
---

# 一、写在前面
>实际开发中，不可避免的就是需要在Activity之间传递数据，并接收返回结果继续自己的逻辑操作.这就不得不请出如下几位：

- **`startActivity(Intent)`**：最常用和基本的Activity跳转.
- **`startActivityForResult(Intent, int)`：重点**
	- arg1：这个Intent对象可以携带数据.
	- arg2请求码：标识跳转的目标Activity，必须>=0.
- **`setResult(int, Intent)`**
	- arg1返回码：标识返回成功或者失败.
	- arg2：这个Intent对象当然也可以携带数据.
- **`onActivityResult(int, int, Intent)`**
	- arg1请求码：即startActivityForResult中的请求码，对应目标Activity.
	- arg2返回码：即setResult中的成功或着失败的标识.
	- arg3：即setResult返回的携带数据的Intent对象.
- **`Intent`**：主要是携带数据.当然`setClass`跳转的本职是必须的.
- **`Bundle`**：主要是封装让Intent对象携带的数据.

# 二、案例
>本篇例子主要逻辑：Activity_A使用Bundle对象封装姓名(String)、年龄(int)、图片(Parcelable)，通过Intent对象传给Activity_B. Activity_B拿到后，在姓名和年龄上分别做简单处理，再返回给Activity_A. Activity_A拿到后显示，另外Activity_B拿到图片直接显示.

- **Activity_A的xml布局**
	```xml
	<Button
		android:id="@+id/bt_A"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:text="start for result" />
	
	<TextView
		android:id="@+id/tv_A"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:text="default play..." />
	```

- **Activity_A**

	```java
	@Override
	protected void onCreate(Bundle savedInstanceState) {
	    super.onCreate(savedInstanceState);
	    setContentView(R.layout.activity_A);
	
	    findViewById(R.id.bt_A).setOnClickListener(new View.OnClickListener() {
	        @Override public void onClick(View view) {
	
	            // 先把要跳转的Activity信息放入Intent对象.
	            Intent intent = new Intent(Activity_A.this, Activity_B.class);
	
	            // 用Bundle对象封装姓名、年龄、图片.
	            Bundle bundle = new Bundle();
	            bundle.putString("nameA", "Activity_B's name is : ");
	            bundle.putInt("ageA", 12);
	            bundle.putParcelable("icon", BitmapFactory.decodeResource(getResources(), R.mipmap.ic_launcher));
	
	            // 将Bundle捆绑进Intent对象.
	            intent.putExtras(bundle);
	
	            startActivityForResult(intent, 1); // arg2:必须>=0.和下面的requestCode对应目标Activity.
	        }
	    });
	}
	
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	    super.onActivityResult(requestCode, resultCode, data);
	    switch (requestCode) {
	        case 1: // 这个和上面的arg2对应起来，确定接收Activity_B返回的信息.
	            switch (resultCode) {
	                case RESULT_OK:
	                    Bundle extras = data.getExtras();
	                    String name = extras.getString("nameB");
	                    int age = extras.getInt("ageB");
	
	                    ((TextView) findViewById(R.id.tv_A)).setText(name + " :: " + age);
	            }
	    }
	}
	```

- **Activity_B的xml布局**

	```xml
	<TextView
	    android:id="@+id/tv_B"
	    android:layout_width="match_parent"
	    android:layout_height="wrap_content"
	    android:text="default desplay..." />
	
	<ImageView
	    android:id="@+id/iv_B"
	    android:layout_width="wrap_content"
	    android:layout_height="wrap_content" />
	
	<Button
	    android:id="@+id/bt_B"
	    android:layout_width="wrap_content"
	    android:layout_height="wrap_content"
	    android:layout_alignParentRight="true"
	    android:text="back to Activity_A" />
	```

- **Activity_B**

	```java
	@Override
	protected void onCreate(Bundle savedInstanceState) {
	    super.onCreate(savedInstanceState);
	    setContentView(R.layout.activity_main2);
	
	    Bundle extras = getIntent().getExtras();
	
	    final String nameA = extras.getString("nameA");
	    final int ageA = extras.getInt("ageA");
	    Bitmap bitmap = extras.getParcelable("icon");
	
	    ((TextView) findViewById(R.id.tv_B)).setText(nameA + "::" + ageA);
	    ((ImageView) findViewById(R.id.iv_B)).setImageBitmap(bitmap);
	
	    findViewById(R.id.bt_B).setOnClickListener(new View.OnClickListener() {
	        @Override public void onClick(View view) {
	
	            Intent intent = new Intent();
	
	            Bundle bundle = new Bundle();
	            bundle.putString("nameB", nameA + "catface");
	            bundle.putInt("ageB", ageA + 12);
	
	            intent.putExtras(bundle);
	
	            // 此处换了一个装Activity跳转信息的方式,灵活运用.
	            intent.setClass(getApplicationContext(), Activity_A.class);
	            setResult(RESULT_OK, intent);
	            finish();
	        }
	    });
	}
	```

- **案例过程展示**
	1. 首先展示Activity_A
		![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwMTIwMjA0MTM3MTUx?x-oss-process=image/format,png)
	2. 点击按钮，携带姓名、年龄、图片到Activity_B
		![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwMTIwMjAzODAyOTc4?x-oss-process=image/format,png)
	3. 点击按钮，携带数据返回到Activity_A
		![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwMTIwMjAzOTE2NTcy?x-oss-process=image/format,png)