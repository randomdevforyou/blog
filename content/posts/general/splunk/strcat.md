 ---
title: "How to concat strings in splunk"
date: 2023-01-03T14:32:51+05:30
draft: true
---

While using splunk we need to concat two fields to create a new field. We can use ***strcat*** function for the same.


```
    strcat field1 field2 newField
```

This will contenate *field1* and *field2* to the new field *newField*. e.g if field1 value is *foo* and field2 value is *bar*, newField value will be *foobar*

We can also use text for concatenation.

```
    strcat field1 " " field2 newField
```

If field1 value is *foo* and field2 value is *bar*, newField value will be *foo bar*.

