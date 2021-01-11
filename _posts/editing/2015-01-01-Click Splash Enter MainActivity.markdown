---
temp-layout:       post
temp-title:        "Click Splash Enter MainActivity"
temp-subtitle:     ""
temp-date:         2015-01-01 12:00:00
temp-header-img:   "img/color-android-robot-green.png"
temp-tags:
    - android
---

# 参考[鸿神原文](http://blog.csdn.net/lmj623565791/article/details/23613403)

1. **默认 AActivity 为闪屏页，BActivity 为主页面**

2. **`Intent.FLAG_ACTIVITY_SINGLE_TOP`说明**

	- **当用户点击 HOME 键后，时刻一到并不会自动开启 BActivity，而是后端自动跳转完成**
	
	- **当用户进入本 APP 其他页面时，时刻一到自动跳转至 BActivity**

		```java
		public class AActivity extends Activity {
		
		    private Handler handler = new Handler() {
		        @Override
		        public void handleMessage(Message msg) {
		            Intent it = new Intent(getApplicationContext(), BActivity.class);
		            
		            // 当用户进入该APP其他页面时,时刻一到自动跳转至B页面
		            it.setFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
		            startActivity(it);
		            finish();
		
		            handler.removeMessages(-1);
		        }
		    };
		
		    @Override
		    protected void onCreate(Bundle savedInstanceState) {
		        super.onCreate(savedInstanceState);
		        setContentView(R.layout.activity_a);
		
		        handler.sendMessageDelayed(handler.obtainMessage(-1), 3000);
		    }
		
		    @Override
		    public boolean onTouchEvent(MotionEvent event) {
		        if (event.getAction() == MotionEvent.ACTION_UP) {
		            handler.sendMessage(handler.obtainMessage(-1));
		            finish();
		        }
		        return super.onTouchEvent(event);
		    }
		}
		```