---
temp-layout:       post
temp-title:        "AsyncTask的使用"
temp-subtitle:     ""
temp-date:         2015-01-01 12:00:00
temp-header-img:   "img/color-android-robot-green.png"
temp-tags:
    - android
---

# 写在前面

- **AsyncTask简介**

	>AsyncTask异步任务，是Android提供给我们的一个处理异步任务的类. 通过该类，可以实现UI线程和后台线程间的通讯. 后台线程执行异步任务，并将结果及进度传递给UI线程，由UI线程做相应处理和显示.

- **为什么使用异步任务(子线程操作)**

	- Android中只有UI线程能进行更新UI的操作. 这样能保证UI的稳定性和准确性，避免多个线程同时对UI进行操作，造成UI混乱.
	- 但Android是一个多线程的OS，一些耗时操作，如请求网络、图片加载、文件读取等放在UI线程会造成后面任务的阻塞，从而出现ANR(Application Not Responding)异常. 所以需要将耗时操作放在子线程中执行，这样既避免了Android的单线程模型，又避免了ANR异常.

- **AsyncTask为何而生**

	- UI线程能更新UI，子线程不能更新UI.
	- 当子线程操作过程中需要更新UI时需借助Handler，比较麻烦.
	- AsyncTask方便我们在子线程中更新UI. 即对基于线程池的子线程和Handler的封装.

# **AsyncTask类的介绍**

- **构建AsyncTask子类的参数**

	>**`AsyncTask<Params, Progress, Result>`**是一个抽象类，通常用于被继承. 继承AsyncTask需要指定如下三个泛型参数
    >
    >1. **Params：启动任务时输入的参数类型(如String).**
    >2. **Progress：后台任务执行中返回进度值的类型(如Integer).**
    >3. **Result：后台任务执行完成后返回结果的类型(如Bitmap).**

- **构建AsyncTask子类的回调方法**

    1. **`doInBackground()`**：必须重写，异步执行后台线程要完成的任务，耗时操作将在此方法中完成.
    
    2. **`onPreExecute()`**：执行后台耗时操作前被调用，通常用于进行初始化操作.
    
    3. **`onPostExecute()`**：当doInBackground方法完成后，系统将自动调用此方法，并将doInBackground方法返回的值传入此方法. 通过此方法进行UI的更新.
    
    4. **`onProgressUpdate()`**：当在doInBackground方法中调用publishProgress方法更新任务执行进度后，将调用此方法. 通过此方法我们可以知晓任务的完成进度.

# 案例一、加载图片

- **AsyncTask的实现**

	```java
	/**
	 * 1. 体验AsyncTask各个方法的执行顺序
	 *    onPreExecute最先执行. 然后执行doInBackground
	 *    doInBackground调用publisProgress()后执行onProgressUpdate 
	 *    doInBackground执行结束返回结果给onPostExecute执行
	 * 
	 * 2. 加载网络图片onPostExecute
	 */
	// arg1、2、3参考上面AsyncTask类的介绍
	// arg1：输入的图片地址类型. arg2：异步任务执行完毕返回的结果类型
	class MyAsyncTask extends AsyncTask<String, Void, Bitmap> {
	
	    @Override protected void onPreExecute() {
	        super.onPreExecute();
	        pb.setVisibility(View.VISIBLE);
	        LogTool.d(TAG, "onPreExecute..."); // 异步任务执行之前的初始化操作
	    }
	
		// 可变参数为启动任务时输入的参数类型
	    @Override protected Bitmap doInBackground(String... params) {
	
	        // 获取传递进来的参数，即图片地址
	        String url = params[0];
	        Bitmap bitmap = null;
	        URLConnection conn;
	        InputStream is = null; // 使用InputStream读取流数据
	        BufferedInputStream bis = null;
	
	        try {
	            conn = new URL(url).openConnection();
	            is = conn.getInputStream();
	            bis = new BufferedInputStream(is);
	            bitmap = BitmapFactory.decodeStream(bis);
	        } catch (IOException e) {
	            e.printStackTrace();
	        } finally {
	            try {
	                is.close();
	                bis.close();
	            } catch (IOException e) {
	                e.printStackTrace();
	            }
	        }
	        LogTool.d(TAG, "doInBackground...");
	        publishProgress(); // 异步任务执行过程中调用onProgressUpdate更新界面进度
	        return bitmap;
	    }
	
		// 参数为doInBackground执行完毕返回的结果对象
	    @Override protected void onPostExecute(Bitmap bitmap) {
	        super.onPostExecute(bitmap);
	        pb.setVisibility(View.GONE);
	        iv.setImageBitmap(bitmap);
	        LogTool.d(TAG, "onPostExecute...");
	    }
	
		// 被doInBackground使用publishProgress后进行进度的更新
	    @Override protected void onProgressUpdate(Void... values) {
	        super.onProgressUpdate(values);
	        LogTool.d(TAG, "onProgressUpdate...");
	    }
	}
	```

- **AsyncTask的调用**

    ```java
    /**
     * 在UI线程(如onCreate()方法)中创建异步任务实例
     */	
    private static final String TAG = "AsyncTaskActivity";
    
    private static final String IMAGE_URL = "..."; // 图片地址
     
    private ImageView iv;
    private ProgressBar pb;
    
    // 这里有个BUG，由AsyncTask底层线程机制导致. 在案例二中提供解决方案.
    private MyAsyncTask myTask;
    
    @Override protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_async_task);
    
        iv = (ImageView) findViewById(R.id.iv_bg);
        pb = (ProgressBar) findViewById(R.id.pb_bg);
    
        // *** execute中的参数将传递给doInBackground() ***
        myTask = new MyAsyncTask();
        myTask.execute(IMAGE_URL);
    }
    ```

# 案例二、更新进度

- **AsyncTask的实现**

	```java
	class ProgressBarAsyncTask extends AsyncTask<Void, Integer, Void> {
	
	    @Override protected Void doInBackground(Void... voids) {
	        // 通过for循环模拟进度条的进度
	        for (int i = 0; i < 30; i++) {
	            if (isCancelled()) {
	                break;
	            }
	            // 通过publishProgress方法将调用onProgressUpdate来更新进度
	            publishProgress(i);
	            // 通过休眠模拟耗时操作
	            SystemClock.sleep(300);
	        }
	        /**
	         * 当for循环全部执行完毕才会进行下一个Task任务，由AsyncTask底层的基于线程池引起的
	         *
	         * 解决方案，将AsyncTask生命周期与当前所在Activity绑定
	         */
	        return null;
	    }
	
	    @Override protected void onProgressUpdate(Integer... values) {
	        super.onProgressUpdate(values);
	        if (isCancelled()) { // 若线程结束，进度条置空
	            return;
	        }
	        // 通过publishProgress方法传过来的值进行进度更新
	        pb_schedule.setProgress(values[0]);
	    }
	}
	```


- **绑定AsyncTask的生命周到Activity中**

	```java
	@Override protected void onPause() {
	    super.onPause();
	    if (pbTask != null && pbTask.getStatus().equals(AsyncTask.Status.RUNNING)) {
	        // 注意：cancel方法仅将AsyncTask任务置为CANCEL状态，并未真正结束线程
	        pbTask.cancel(true);
	    }
	}
	```
- **AsyncTask的调用**

	```java
	private ProgressBarAsyncTask pbTask;
	
	@Override protected void onCreate(Bundle savedInstanceState) {
	    super.onCreate(savedInstanceState);
	    setContentView(R.layout.activity_async_task);
	
	    pb_schedule = (ProgressBar) findViewById(R.id.pb_schedule);
	    
	    pbTask = new ProgressBarAsyncTask();
	    pbTask.execute(); // 输入参数为空
	}
	```

# 使用AsyncTask的注意事项

- 必须在UI线程中创建AsyncTask的实例.
- 只能在UI线程中调用AsyncTask的`execute()`方法.
- AsyncTask被重写的四个方法是系统自动调用的，不应手动调用.
- 每个AsyncTask只能被执行一次，多次执行将会引发异常.
- AsyncTask的四个方法，只有`doInBackground()`方法是运行在其他线程中，其他三个方法都运行在UI线程中，可以对UI进行更新操作.
