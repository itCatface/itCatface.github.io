---
temp-layout:       post
temp-title:        "Android中Java和JS方法互调"
temp-subtitle:     "通过案例介绍Android的WebView中JavaScript和Java原生方法的互相调用"
temp-date:         2015-01-01 12:00:00
temp-author:       "catface"
temp-header-img:   "img/color-black.png"
temp-header-mask:  0.3
temp-catalog:      true
temp-multilingual: false
temp-edit status:  ed
temp-tags:
    - 混合开发
---

# Java调用Js方法

- **无参：使用WebView控件`loadUrl()`方法，传入`"javascript:jsMethod()"`即可调用`jsMethod()`方法**

- **带参：同上，并将参数加上即可`"javascript:jsMethodWithArg(" + args参数 + ")"`**


# Js调用Java方法

- **使用WebView控件的`addJavascriptInterface()`方法，传入一个Object对象和一个String标记(Js通过该标记调用Object对象内写好的方法)**

- **关于带不带参数，即Object内的方法和Js调用时配合定义好参数格式，准确传入即可**


# 完整案例

1. **html + Js**

	``` html
	<html>
		<head>
			<meta http-equiv="Content-Type"	content="text/html;charset=utf-8">
			<script type="text/javascript">
	
				/*js通过Java给的String标记:Catface调用Java中Object内定义的方法*/
				function jsCallJavaWithArgs(text) {
		        	Catface.showToast(text);
		    	}
	
		   		function jsCallJava() {
		        	Catface.showToast();
		    	}
	
		    	/*java调用js方法*/
		    	function javaCallJs(){
			 		document.getElementById("content").innerHTML += "<br>java调用了js函数";
				}
	
				function javaCallJsWithArgs(args){
			 		document.getElementById("content").innerHTML += ("<br>" + args);
				}
	
				function javaCallJsWithArgs2(args) {
					var sum = 0;
					for(var i = 0; i < args; i++) {
						sum += i;
					}
			 		document.getElementById("content").innerHTML += ("<br>" + sum);
				}
			</script>
		</head>
	
		<body>
			<input type="button" value="js调用java代码(带参)" onClick="jsCallJavaWithArgs('我从js写到java上啦')" /><br/>
			<input type="button" value="js调用java代码" onClick="jsCallJava()" /><br/>
			<div id="content">java调用js函数_内容显示……</div>
		</body>
	</html>
	```

2. **xml**

	``` xml
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    android:orientation="vertical" >
	    <Button
	        android:id="@+id/bt_01"
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:text="java调用js函数" />
	
	    <Button
	        android:id="@+id/bt_02"
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:text="java调用js函数(带参)" />
	
	    <Button
	        android:id="@+id/bt_03"
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:text="java调用js函数(带参2)" />
	
	    <WebView
	        android:id="@+id/wv_main"
	        android:layout_width="match_parent"
	        android:layout_height="match_parent" />
	</LinearLayout>
	```

3. **Java**

	``` java
	public class MainActivity extends Activity {
		private WebView wv_main;
	
		@SuppressLint("SetJavaScriptEnabled")
		@Override
		protected void onCreate(Bundle savedInstanceState) {
			super.onCreate(savedInstanceState);
			setContentView(R.layout.activity_main);
			
			wv_main = (WebView) findViewById(R.id.wv_main);	
			wv_main.getSettings().setJavaScriptEnabled(true);	
			wv_main.loadUrl("file:///android_asset/index.html");
			 
			findViewById(R.id.bt_01).setOnClickListener(new OnClickListener() {
				@Override public void onClick(View v) {
					wv_main.loadUrl("javascript:javaCallJs()");
				}
			});
			findViewById(R.id.bt_02).setOnClickListener(new OnClickListener() {
				@Override public void onClick(View v) {
					wv_main.loadUrl("javascript:javaCallJsWithArgs(" + "'我从java写到js上啦'" + ")");
				}
			});
			findViewById(R.id.bt_03).setOnClickListener(new OnClickListener() {
				@Override public void onClick(View v) {
					wv_main.loadUrl("javascript:javaCallJsWithArgs2(" + 10 + ")");
				}
			});
			
			// arg1:Object对象；arg2:String标记
			wv_main.addJavascriptInterface(new JavaMethod(this), "Catface");
		}
	
		public class JavaMethod {
			Context ctx;
	
			JavaMethod(Context ctx) {
				this.ctx = ctx;
			}
	
			@JavascriptInterface
			public void showToast(String text) {
				Toast.makeText(ctx, text, Toast.LENGTH_SHORT).show();
			}
	
			@JavascriptInterface
			public void showToast() {
				Toast.makeText(ctx, "js调用了java代码", Toast.LENGTH_SHORT).show();
			}
		}
	}
	```

## 补1：Crosswalk中相互调用方式

- **Java调用Js方法仅修改一点点即可**
	
	``` java
	xv_main.load("javascript:javaCallJs()", null);
	```

	``` java
	xv_main.load("javascript:javaCallJsWithArgs2(" + "'java调用js啦'" + ")", null);
	```

- **Js调用Java方法与原生调用同理，但需在Activity的onCreate()中添加**
	
	``` java
	XWalkPreferences.setValue("enable-javascript", true);
	XWalkPreferences.setValue(XWalkPreferences.REMOTE_DEBUGGING, true);
	```

## 补2：Cordova + Crosswalk中相互调用方式

- **Js调用Java：在CordovaActivity中添加`this.appView.addJavascriptInterface()`即可，参数传递方式同上**

	>注意`@JavascriptInterface`的包类路径是：`org.xwalk.core.JavascriptInterface`.即Crosswalk下的API，别导错.
	
	``` java
	this.appView.addJavascriptInterface(new Object() {
		@JavascriptInterface 
		public void showToast(String text) {
			Toast.makeText(getApplicationContext(), text, Toast.LENGTH_SHORT).show();
		}
	
		@JavascriptInterface
		public void showToast() {
			Toast.makeText(getApplicationContext(), "js调用了java代码", Toast.LENGTH_SHORT).show();
		}
	}, "Catface");
	```

- **Java调用Js**

	``` java
	// 在CordovaActivity或者CordovaPlugin(插件)类中调用方法如下.
	appView.loadUrl("javascript:compare(" + arg1 + "," + arg2 + ")");

	// 在CordovaActivity的init()方法或者CordovaPlugin的onCreate()方法中务必添加，否则后果自负.
	appView.loadUrl("file:///android_asset/www/index.html");
	super.setIntegerProperty("loadUrlTimeoutValue", Integer.MAX_VALUE);
	```
