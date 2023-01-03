 ---
title: "How to append query params in url"
date: 2023-01-03T14:32:51+05:30
draft: false
---

We can use plain javascript to append query params to an url.

```javascript
    function appendQuery1(url, key, value){
        let appender = url.indexOf("?") > -1 ? "?" : "&";
        url = url + appender + key + "=" + value; 
        return url;
    }
```

nodejs provides module named "URL" which can be used for the same task

```javascript
    function appendQuery(url, key, value){
        let urlObj = new URL(url);
        urlObj.searchParams.append(key, value);
        return urlObj.toString();
    }
```
