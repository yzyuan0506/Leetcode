index:
-key: a sequence of random number(6 digits)
-value: long url

revIndex:
-key: long url
-value: a sequence of random number(6 digits)

```java
public class Codec {
    Map<String, String> index = new HashMap<String, String>();
    Map<String, String> revIndex = new HashMap<String, String>();
    static String BASE_HOST = "http://tinyurl.com/";
    // Encodes a URL to a shortened URL.
    public String encode(String longUrl) {
        if(revIndex.containsKey(longUrl)) return BASE_HOST+revIndex.get(longUrl);
        String charSet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
        String key = null;
        do {
            StringBuilder sb = new StringBuilder();
            for(int i=0;i<6;i++) {
                int j = (int) (Math.random() * charSet.length());
                sb.append(charSet.charAt(j));
            }
            key = sb.toString();
        } while(index.containsKey(key));
        index.put(key, longUrl);
        revIndex.put(longUrl, key);
        return BASE_HOST+key;
    }

    // Decodes a shortened URL to its original URL.
    public String decode(String shortUrl) {
        return index.get(shortUrl.replace(BASE_HOST, ""));
    }
}
```

Use toString() to assign StringBuilder to a string variable

use replace(str1, str2) to replace str1 with str2

HashMap: put(), containsKey(), get()

Math.random(): return a double number range from 0.00 to 1.00

use (int) for type coersion

"do while" loop: make sure no duplicate key!  
