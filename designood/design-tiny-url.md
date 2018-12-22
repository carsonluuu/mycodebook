# Tiny Url

Given a long url, make it shorter. To make it simpler, let's ignore the domain name.

You should implement two methods:

* `longToShort(url)`. Convert a long url to a short url.
* `shortToLong(url)`. Convert a short url to a long url starts with `http://tiny.url/`.

You can design any shorten algorithm, the judge only cares about two things:

1. The `short key`'s length should `equal to 6`\(without domain and slash\). And the acceptable characters are`[a-zA-Z0-9]`. For example:`abcD9E`
2. No two long urls mapping to the same short url and no two short urls mapping to the same long url.

### Example

Given url =`http://www.lintcode.com/faq/?id=10`, run the following code \(or something similar\):

```
short_url = longToShort(url) // may return http://tiny.url/abcD9E
long_url = shortToLong(short_url) // return http://www.lintcode.com/faq/?id=10
```

The short\_url you return should be unique short url and start with`http://tiny.url/`and`6`acceptable characters. For example "[http://tiny.url/abcD9E](http://tiny.url/abcD9E)" or something else.

The long\_url should be`http://www.lintcode.com/faq/?id=10`in this case.

### Note

两种方法，随机或者base62

都要建立long和short的映射关系

### Code

```java
// version 1: Random
public class TinyUrl {
    private Map<String, String> long2Short;
    private Map<String, String> short2Long;

    public TinyUrl() {
        long2Short = new HashMap<String, String>();
        short2Long = new HashMap<String, String>();
    }

    /**
     * @param url a long url
     * @return a short url starts with http://tiny.url/
     */
    public String longToShort(String url) {
        if (long2Short.containsKey(url)) {
            return long2Short.get(url);
        }

        while (true) {
            String shortURL = generateShortURL();
            if (!short2Long.containsKey(shortURL)) {
                short2Long.put(shortURL, url);
                long2Short.put(url, shortURL);
                return shortURL;
            }
        }
    }

    /**
     * @param url a short url starts with http://tiny.url/
     * @return a long url
     */
    public String shortToLong(String url) {
        if (!short2Long.containsKey(url)) {
            return null;
        }

        return short2Long.get(url);
    }

    private String generateShortURL() {
        String allowedChars = 
            "0123456789" +
            "abcdefghijklmnopqrstuvwxyz" + 
            "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

        Random rand = new Random();
        String shortURL = "http://tiny.url/";
        for (int i = 0; i < 6; i++) {
            int index = rand.nextInt(62);
            shortURL += allowedChars.charAt(index);
        }

        return shortURL;
    }
}
```

```java
/ version 2: base62
public class TinyUrl {
    public static int GLOBAL_ID = 0;
    private HashMap<Integer, String> id2url = new HashMap<Integer, String>();
    private HashMap<String, Integer> url2id = new HashMap<String, Integer>();
    
    private String getShortKey(String url) {
        return url.substring("http://tiny.url/".length());
    }

    private int toBase62(char c) {
        if (c >= '0' && c <= '9') {
            return c - '0';
        }
        if (c >= 'a' && c <= 'z') {
            return c - 'a' + 10;
        }
        return c - 'A' + 36;
    }
    
    private int shortKeytoID(String short_key) {
        int id = 0;
        for (int i = 0; i < short_key.length(); ++i) {
            id = id * 62 + toBase62(short_key.charAt(i));
        }
        return id;
    }

    private String idToShortKey(int id) {
        String chars = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String short_url = "";
        while (id > 0) {
            short_url = chars.charAt(id % 62) + short_url;
            id = id / 62;
        }
        while (short_url.length() < 6) {
            short_url = "0" + short_url;
        }
        return short_url;
    }

    /**
     * @param url a long url
     * @return a short url starts with http://tiny.url/
     */
    public String longToShort(String url) {
        if (url2id.containsKey(url)) {
            return "http://tiny.url/" + idToShortKey(url2id.get(url));
        }
        GLOBAL_ID++;
        url2id.put(url, GLOBAL_ID);
        id2url.put(GLOBAL_ID, url);
        return "http://tiny.url/" + idToShortKey(GLOBAL_ID);
    }

    /**
     * @param url a short url starts with http://tiny.url/
     * @return a long url
     */
    public String shortToLong(String url) {
        String short_key = getShortKey(url);
        int id = shortKeytoID(short_key);
        return id2url.get(id);
    }
}
```



