---
temp-layout:       post
temp-title:        "关于网络_HttpUrlConnection&HttpClient"
temp-subtitle:     ""
temp-date:         2015-01-01 12:00:00
temp-header-img:   "img/color-android-robot-green.png"
temp-tags:
    - android
---

# 前言

1. **本节我们不使用 WebView，因为它帮我们封装好了从服务器请求数据的过程、以及对服务器返回的数据进行解析的过程，仅 loadUrl() 一行代码就完美的将页面展示出来了**

2. **Android 中一般有两种方式发送 HTTP 请求：HttpURLConnection、HttpClient(2.3后淘汰).  我们体验手动向服务器发送请求以及从服务器获得流数据的过程**

3. **本节完成上述 2. 的内容：从服务器请求数据.  关于数据的解析，将在下节介绍**

4. **注意：网络请求(耗时操作)应在子线程中处理，否则抛出 NetworkOnMainThreadException 异常**

# HttpURLConnection 的使用方法简介

- **PART_A 从服务器获取数据**

	- 创建URL对象，传入地址
	
	- 打开链接，获取 **HttpURLConnection** 对象

	- 设置请求方式：GET 一般表示从服务器获取数据 | POST 一般表示向服务器提交数据
	
	- 设置连接超时

	- 设置读取超时，此时连接已成功
	
	- 获取服务器返回的流数据

		```java
		/**
		 * GET 请求获取网络数据
		 */
		private static final int TIMEOUT_IN_MILLIONS = 5000;
	
		public static String doGet(final String url) {
        
	        HttpURLConnection conn = null;
	        InputStream is = null;
	
	        try {
	            conn = (HttpURLConnection) new URL(url).openConnection();
	            conn.setRequestMethod("GET");
	            conn.setConnectTimeout(TIMEOUT_IN_MILLIONS);
	            conn.setReadTimeout(TIMEOUT_IN_MILLIONS);
	            if (conn.getResponseCode() == 200) {
	                // 获取网络返回的输入流
	                is = conn.getInputStream();
					// 输入流转字符串
	                return stream2String(is);
	            }
	        } catch (IOException e) {
	            e.printStackTrace();
	        } finally {
	            try {
	                if (is != null) {
	                    is.close();
		            }
	            } catch (IOException e) {
	                e.printStackTrace();
	            }
	            conn.disconnect();
	        }
	        return null;
	    }


		/**
		 * 输入流转字符串
		 */
		public static String stream2String(InputStream is) {
			ByteArrayOutputStream baos = null;
		   try {
		        // 字节数组输出流
		        baos = new ByteArrayOutputStream();
		
		        int len = 0;
		        byte[] buffer = new byte[1024];
		        while ((len = is.read(buffer)) != -1) {
		            baos.write(buffer, 0, len);
		        }
		        return baos.toString();
		  
		    } catch (IOException e) {
		        e.printStackTrace();
		        return null;
		    } finally {
		        try {
		            if (baos != null) {
		                baos.close();
		            }
		        } catch (IOException e) {
		            e.printStackTrace();
		        }
		        try {
		            if (is != null) {
		                is.close();
		            }
		        } catch (IOException e) {
		            e.printStackTrace();
		        }
		    }
		}


	    /**
	     * 字符串转输入流
	     */
	    public static InputStream string2Stream(String str) {
	        return new ByteArrayInputStream(str.getBytes());
	    }
		```

	- 调用
		
		```java
		/**
		 * 子线程中处理网络请求
		 */
		new Thread(new Runnable() {
		    @Override
		    public void run() {
			    String result = HttpUtils.doGet("http://10.0.2.2:8080/json.json");
		    }
		}).start();
		```
		
	- 下一篇介绍如何解析服务器传来的数据(主要格式：xml、json)

- **PART_B 向服务器提交数据**

	- 仅需修改请求方法为 POST 请求，并传入提交参数即可

		```java
		conn.setRequestMethod("POST");
		conn.setDoOutput(true);
        conn.setDoInput(true);
        
		DataOutputStream out = new DataOutputStream(conn.getOutputStream());
		out.writeBytes("username=catface&password=123");
		```
		
# HttpClient的使用方法简介

1. **HttpClient是Apache提供的访问网络的接口. 并对数据做了一定的封装**

2. **与HttpURLConnection的作用和效果差不多，只是使用方式上稍有区别**

3. **PART_A 从服务器获取数据**

	- 创建HttpClient对象，注意是 new DefaultHttpClient()
	
	- 创建HttpGet对象，并将传入地址
	
	- 执行GET请求，获取服务器返回的信息

	- 判断仅当请求成功时，获取数据实体并使用U8编码转换成字符串
		
		```java
		new Thread(new Runnable() {
			@Override
			public void run() {
				try {
					
					// HttpClient请求网络的初始化操作
					HttpClient client = new DefaultHttpClient();
					HttpGet httpGet = new HttpGet("http://jianshu.com");
					HttpResponse response = client.execute(httpGet); 
		
					if (response.getStatusLine().getStatusCode() == 200) {
						HttpEntity entity = response.getEntity(); 
						// 服务器返回的流数据含中文时指定U8编码.否则乱码
						final String result = EntityUtils.toString(entity, "UTF-8");
					}
				} catch (ClientProtocolException e) {
					e.printStackTrace();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}).start();
		```

4. **PART_B 向服务器提交数据**

	```java
	HttpPost httpPost = new HttpPost("http://jianshu.com"); // POST请求
	List<NameValuePair> params = new ArrayList<NameValuePair>();
	params.add(new BasicNameValuePair("username", "catface")); // NameValuePair封装提交参数
	params.add(new BasicNameValuePair("password", "123"));
	UrlEncodedFormEntity entity = new UrlEncodedFormEntity(params, "utf-8"); // 编码
	httpPost.setEntity(entity);
	httpClient.execute(httpPost);
	```