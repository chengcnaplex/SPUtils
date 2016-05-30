# SPUtils

SPUtils是针对Android SharedPreferences的工具，主要是为了对SharedPreferences进行简化操作，提供了一系列非常实用方法。
It is cool。

## 思路来源

编写这个工具主要是因为工作中写的App比较简单，每次都会使用Sharedpreferences，用多了，觉得麻烦，所以就想能不能操作更简单一点，于是这个工具就诞生了。

## SPUtils优点
* 对SharedPreferences获取数据提供了如下类似方法：

```
	public static String getString(Application application, String name, String key) {
		if (checkApplicationAndStrings(application, name, key)) {
			return getSP(application, name).getString(key, "").trim();
		}
		return "";
	}

	public static String getString(Application application, String key) {
		return getString(application, spFileName, key);
	}

	public static String getString(String name, String key) {
		return getString(application, name, key);
	}

	public static String getString(String key) {
		return getString(application, spFileName, key);
	}
```

* 对SharedPreferences设置数据提供了如下类似方法：

```
	public static void pushString(Application application, String name, String key, String value) {
		if (checkApplicationAndStrings(application, name, key, value)) {
			getSP(application, name).edit().putString(key, value.trim()).commit();
		}
	}

	public static void pushString(Application application, String key, String value) {
		pushString(application, spFileName, key, value);
	}

	public static void pushString(String name, String key, String value) {
		pushString(application, name, key, value);
	}

	public static void pushString(String key, String value) {
		pushString(application, spFileName, key, value);
	}
```

## 操作方法
* 使用如下方法先设置Application对象：

```
    SPUtils.setApplication(application);
```

* 后续的方法就可以随意使用，本人建议在使用之前，粗略的看一下源代码。
* 从下面的Demo中你就知道该怎么使用这个工具了:

```
    public static void testSPUtils(Application application) {

        setApplication(application);

        pushString("name", "China");
        Log.e("SPUtils", "name = " + (String)getValue("name", new String()));
        pushInt("int", 3);
        Log.e("SPUtils", "int = " + getValue("int", Integer.valueOf(0)));
        pushFloat("float", 3.14f);
        Log.e("SPUtils", "float = " + getValue("float", Float.valueOf(0)));
        
        HashMap<String, Object> keyValues = new HashMap<String, Object>();
        keyValues.put("name", "SZ");
        keyValues.put("address", "shenzhen");
        keyValues.put("float", 3.14f);
        keyValues.put("int", 3);
        keyValues.put("boolean", true);
        
        pushValues(keyValues);

        HashMap<String, Object> keyTypes = new HashMap<String, Object>();
        keyTypes.put("name", new String());
        keyTypes.put("address", new String());
        keyTypes.put("float", Float.valueOf(0));
        keyTypes.put("int", Integer.valueOf(0));
        keyTypes.put("boolean", Boolean.valueOf(false));
        
        Log.e(TAG, getValues(keyTypes).toString());

        Log.e("SPUtils", "age = " + getValue("age", Integer.valueOf(0)));
        Log.e("SPUtils", "int = " + getValue("int", Integer.valueOf(0)));
        Log.e("SPUtils", "float = " + getValue("float", Float.valueOf(0)));
        Log.e("SPUtils", "name = " + (String)getValue("name", new String()));
        
        /** 
         * output:
         *     E/SPUtils(8456): name = China
         *     E/SPUtils(8456): int = 3
         *     E/SPUtils(8456): float = 3.14
         *     E/SPUtils(8456): {boolean=true, address=shenzhen, float=3.14, int=3, name=SZ}
         *     E/SPUtils(8456): age = 0
         *     E/SPUtils(8456): int = 3
         *     E/SPUtils(8456): float = 3.14
         *     E/SPUtils(8633): name = SZ
         */

        }
    }
```


## 致谢

在这里得感谢程梦真，他在这个工具诞生的过程中，提供了宝贵的意见。

