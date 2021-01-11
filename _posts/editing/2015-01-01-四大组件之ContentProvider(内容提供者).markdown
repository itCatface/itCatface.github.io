---
temp-layout:       post
temp-title:        "四大组件之ContentProvider(内容提供者)"
temp-subtitle:     ""
temp-date:         2015-01-01 12:00:00
temp-header-img:   "img/color-android-robot-green.png"
temp-tags:
    - android
---

# ContentProvider 如何实现数据共享

- Android 中如果想将自己应用的数据(一般多为数据库中的数据)提供给第三发 app，那么我们只能通过 ContentProvider 来实现

- ContentProvider 是应用程序之间共享数据的接口. 使用的时候首先自定义一个类继承 ContentProvider，然后覆写 `query`、`insert`、`update`、`delete` 等方法. 最后别忘了作为 android 四大组件之一必须在 AndroidManifest 文件中进行注册

- 第三方 app 可以通过 ContentResolver 类来访问该 Provider

- 第三方 app 可以通过注册 ContentObserver 观测该Provider操作后的数据库变化

# 为什么要用 ContentProvider? 它和 sql 的实现上有什么差别?

- ContentProvider 屏蔽了数据存储的细节，内部实现对用户完全透明，用户只需要关心操作数据的 uri 就可以了，ContentProvider 可以实现不同 app 之间共享

- Sql 也有增删改查的方法，但是 sql 只能查询本应用下的数据库. 而 ContentProvider 还可以去增删改查本地文件、.xml 文件的读取等

# ContentProvider、ContentResolver、ContentObserver 之间的关系

- **ContentProvider**：内容提供者，用于对外提供数据 

- **`ContentResolver.notifyChange(uri)`**：发出消息 

- **ContentResolver**：内容解析者，用于获取内容提供者提供的数据 

- **ContentObserver**：内容监听器，可以监听数据的改变状态 

- **`ContentResolver.registerContentObserver()`**：监听消息

# 如何访问 asserts 资源目录下的数据库?

- 获取 assert 目录下的 db 文件

	```java
	AssetManager assetManager = getAssets(); 
	InputStream is = assetManager.open("myuser.db"); 
	// 将文件拷贝到 /data/data/cc.catface.android.asserts.sqlite/databases/myuser.db 
	// 如果 databases 目录不存在则创建
	File file = new File("/data/data/cc.catface.android.asserts.sqlite/databases"); 
	if (!file.exists()) {
		file.mkdirs();
	}
	FileOutputStream fos = new FileOutputStream(new File(file, "myuser.db")); 
	byte[] buff = new byte[1024 * 8];
	int len = -1;
	while((len = is.read(buff)) != -1){
		fos.write(buff, 0, len);
	}
	fos.close();
	is.close();
	```

- 访问数据库

	```java
	SQLiteDatabase database = openOrCreateDatabase("myuser.db", MODE_PRIVATE, null);
	String sql = "select c_name from t_user"; 
	Cursor cursor = database.rawQuery(sql, null); 
	while(cursor.moveToNext()){
		String string = cursor.getString(0);
		Log.d("tag", string); 
	}
	cursor.close();
	database.close();
	```

# 如何在高并发下进行数据库查询

&emsp;&emsp;不要关联多表查询，减少链接时间，创建索引、将查询到的数据采用缓存策略等等

# 案例-查询联系人

1. 动态申请权限

	- 清单文件中添加权限申明
	
		```xml
		<uses-permission android:name="android.permission.READ_CONTACTS" />
		```
	
	- 代码中动态申请权限
	
		```java
		if (checkSelfPermission(Manifest.permission.READ_CONTACTS) != PackageManager.PERMISSION_GRANTED) {
		   requestPermissions(new String[]{Manifest.permission.READ_CONTACTS}, 1);
		}
		```

2. 获取联系人

	```java
	Cursor cursor = null;
	try {
	    cursor = getContentResolver().query(ContactsContract.CommonDataKinds.Phone.CONTENT_URI, null, null, null, null);
	    if (cursor != null) {
	        while (cursor.moveToNext()) {
	            String displayName = cursor.getString(cursor.getColumnIndex(ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME));
	            String number = cursor.getString(cursor.getColumnIndex(ContactsContract.CommonDataKinds.Phone.NUMBER));
	            Log.d("catface", "读取联系人：" + displayName + " || " + number);
	        }
	    }
	} catch (Exception e) {
	    e.printStackTrace();
	} finally {
	    if (cursor != null) {
	        cursor.close();
	    }
	}
	```

# 案例-完整的使用

## 步骤一、server app中定义ContentProvider

```java
public class FileProvider extends ContentProvider {
    private final String TAG = "catface";

    private static final Pair<String, Integer> TABLE_TEXT = new Pair<>("table_text", 0);
    private static final Pair<String, Integer> TABLE_AUDIO = new Pair<>("table_audio", 1);
    private static final Pair<String, Integer> TABLE_VIDEO = new Pair<>("table_video", 2);


    // 主机名
    private static final String AUTHORITY = "cc.catface.provider.server";
    private static final Uri HOST_URI = Uri.parse("content://" + AUTHORITY);

    private static UriMatcher mUriMatcher;

    // 本地匹配规则
    static {
        mUriMatcher = new UriMatcher(UriMatcher.NO_MATCH);
        mUriMatcher.addURI(AUTHORITY, TABLE_TEXT.first, TABLE_TEXT.second);
        mUriMatcher.addURI(AUTHORITY, TABLE_AUDIO.first, TABLE_AUDIO.second);
        mUriMatcher.addURI(AUTHORITY, TABLE_VIDEO.first, TABLE_VIDEO.second);
    }

    public FileProvider() {
        Log.d(TAG, "constructor...");
    }

    @Override
    public boolean onCreate() {
        Log.d(TAG, "create...");
        return true;
    }

    @Nullable
    @Override
    public String getType(@NonNull Uri uri) {
        int match = mUriMatcher.match(uri);
        if (match == TABLE_TEXT.second) {
            return TABLE_TEXT.first;
        }
        if (match == TABLE_AUDIO.second) {
            return TABLE_AUDIO.first;
        }
        if (match == TABLE_VIDEO.second) {
            return TABLE_VIDEO.first;
        }
        return null;
    }

    @Nullable
    @Override
    public Uri insert(@NonNull Uri uri, @Nullable ContentValues values) {
        // Log.d(TAG, "insert-->uri: " + uri + " || values's size: " + values.size()); // 打印所有入参
        String tableName = getType(uri);
        if (null == getContext() || null == values || null == tableName) return null;
        if (tableName.equals(TABLE_TEXT.first)) {
            TextInfo info = new TextInfo();
            if (values.containsKey("uuid")) info.setUuid(values.getAsString("uuid"));
            if (values.containsKey("text")) info.setText(values.getAsString("text"));
            if (values.containsKey("create_time")) info.setCreateTime(values.getAsLong("create_time"));
            if (values.containsKey("search_count")) info.setSearchCount(values.getAsInteger("search_count"));
            long rowId = DBHelper.getInstance().getTextInfoDAO().insert(info);
            getContext().getContentResolver().notifyChange(HOST_URI, null);
            return ContentUris.withAppendedId(uri, rowId);
        }
        return null;
    }

    @Override
    public int delete(@NonNull Uri uri, @Nullable String selection, @Nullable String[] selectionArgs) {
        // Log.d(TAG, "delete-->uri: " + uri + " || selection: " + selection + " || selectionArgs: " + Arrays.asList(selectionArgs).toString());   // 打印所有入参
        getContext().getContentResolver().notifyChange(HOST_URI, null); // 数据库发生变化通知客户app的观察者
        return DBHelper.getInstance().getTextInfoDAO().deleteByText(selectionArgs[0]);
    }

    @Override
    public int update(@NonNull Uri uri, @Nullable ContentValues values, @Nullable String selection, @Nullable String[] selectionArgs) {
        // Log.d(TAG, "update-->uri: " + uri + " || values's size: " + values.size() + " || selection: " + selection + " || selectionArgs: " + Arrays.asList(selectionArgs).toString());    // 打印所有入参
        int rowId = DBHelper.getInstance().getTextInfoDAO().updateText(selectionArgs[0], selectionArgs[1]);
        getContext().getContentResolver().notifyChange(HOST_URI, null);
        return rowId;
    }

    @Nullable
    @Override
    public Cursor query(@NonNull Uri uri, @Nullable String[] projection, @Nullable String selection, @Nullable String[] selectionArgs, @Nullable String sortOrder) {
        // Log.d(TAG, "query-->uri: " + uri + " || projection[]: " + Arrays.asList(projection).toString() + " || selection: " + selection + " || selectionArgs[]: " + Arrays.asList(selectionArgs).toString() + " || sortOrder: " + sortOrder);    // 打印所有入参
        Cursor cursor = DBHelper.getInstance().getTextInfoDAO().select4CP(-1, 0);
        cursor.setNotificationUri(getContext().getContentResolver(), HOST_URI);
        return cursor;
    }
}
```

## 步骤二、server app清单文件中注册

```xml
<provider
    android:name="cc.catface.provider.server.FileProvider"
    android:authorities="cc.catface.provider.server"
    android:enabled="true"
    android:exported="true"
    android:multiprocess="true" />
```

## 步骤三、client app调用provider

1. uri

	```java
	Uri uri = Uri.parse("content://cc.catface.provider.server/table_text");
	```

2. 增

	```java
	ContentValues values = new ContentValues();
	values.put("uuid", UUID.randomUUID().toString());
	values.put("text", binding.etText.getText().toString().trim());
	values.put("create_time", System.currentTimeMillis());
	values.put("search_count", Integer.valueOf(binding.etCount.getText().toString()));
	Uri insertUri = getContentResolver().insert(uri, values);
	Log.d("catface", "insert-->insertUri: " + insertUri.toString());
	```

3. 删

	```java
	int rowId = getContentResolver().delete(uri, null, new String[]{binding.etDeleteText.getText().toString().trim()});
	Log.d("catface", "delete-->rowId: " + rowId);
	```
	
4. 改

	```java
	int rowId = getContentResolver().update(uri, new ContentValues(), null, new String[]{binding.etOldText.getText().toString().trim(), binding.etNewText.getText().toString().trim()});
	Log.d("catface", "update-->rowId: " + rowId);
	```
	
5. 查

	```java
	Cursor cursor = getContentResolver().query(uri, null, null, null, null);
	if (null == cursor) return;
	while (cursor.moveToNext()) {
	    String text = cursor.getString(cursor.getColumnIndex("text"));
	    long create_time = cursor.getLong(cursor.getColumnIndex("create_time"));
	    Log.d("catface", "query: " + text + " || " + create_time);
	}
	cursor.close();
	```

### client app中使用ContentObserver

1. 定义并初始化ContentObserver

	```java
	class CustomObserver extends ContentObserver {
		public CustomObserver(Handler handler) {
	        super(handler);
	    }
	
	    @Override
	    public void onChange(boolean selfChange, Uri uri) {
	        Log.d("catface", "CustomObserver-->onChange-->uri: " + uri + " || selfChange: " + selfChange);
	    }
	}
	
	CustomObserver mProviderObserver = new CustomObserver(new Handler());
	```

2. 注册ContentObserver

	```java
	getContentResolver().registerContentObserver(Uri.parse("content://cc.catface.provider.server/table_text"), true, mProviderObserver);
	```

3. 解注册ContentObserver

	```java
	getContentResolver().unregisterContentObserver(mProviderObserver);
	```

## 数据实体

```java
@Entity(tableName = "text_info")
public class TextInfo {
    
    @NonNull @PrimaryKey private String uuid;
    private String text;
    @ColumnInfo(name = "create_time") private long createTime;
    @ColumnInfo(name = "search_count") private int searchCount;
	
	// getter & setter
}
```

## 数据库操作

```java
@Dao
public interface TextInfoDAO {

    @Insert(onConflict = OnConflictStrategy.REPLACE)
    long insert(TextInfo info);

    @Query("delete from text_info where text=:text")
    int deleteByText(String text);

    @Query("update text_info set text=:newText where text=:oldText")
    int updateText(String oldText, String newText);

    @Query("select * from text_info order by create_time desc limit :pageSize offset :pageSize * :page")
    Cursor select4CP(int pageSize, int page);
}
```
