---
layout: post
title:  "好久没写了，来一发json相关的"
date:   2016-06-30 00:26:00 +0800
categories: code
---

工作将近一年，json基本上是每天至少一遇啊（if coding）

好了，废话少说，今天主要是想来记录一下fastjson的使用的，体验了一下，发现json基本上就是傻瓜式的使用，只要记住JSON这个对象的两个方法，基本就能走遍天下了~~

直接上代码：

```java
        //1.list
        List<String> list = new ArrayList<String>();
        list.add("John");
        list.add("Sam");
        System.out.println(JSON.toJSONString(list));
        String listJson = "[\"John\",\"Sam\"]";
        List<String> parseList = (List<String>)JSON.parse(listJson);
        System.out.println(parseList.size());
        
        //2.map
        Map<String, String> map = new HashMap<String, String>();
        map.put("Jack", "Ma");
        map.put("Tom", "Chen");
        System.out.println(JSON.toJSONString(map));
        String mapJson = "{\"Tom\":\"Chen\",\"Jack\":\"Ma\"}";
        Map<String, String> parseMap = (Map<String, String>) JSON.parse(mapJson);	
        System.out.println(parseMap.size());
        parseMap = JSON.parseObject(mapJson, Map.class);
        System.out.println(parseMap.size());
        
        //3.set
        Set<String> set = new HashSet<String>();
        set.add("Hello");
        System.out.println(JSON.toJSONString(set));
        String setJson = "[\"Hello\"]";
        Set<String> parseSet = JSON.parseObject(setJson, Set.class);
        System.out.println(parseSet.size());
        
        //4.array
        String[] array = {"First", "Second"};
        System.out.println(JSON.toJSONString(array));
        String arrayJson = "[\"First\",\"Second\"]";
        String[] parseArray = JSON.parseObject(arrayJson, String[].class);
        System.out.println(parseArray.length);
```


由于平时无论是jackson还是json-lib，在使用过程中对于集合的一个处理还是不够灵活，所以一个新的json库，首先我最关心的必须是集合类和java Object之间的转化，从上面的代码可以看出，fastjson在这方面做得实在是太棒了，只要记住JSON.toJSONString，JSON.parseObject和JSON.parse，基本就可以解决所有的转化问题了。当然在这里比较担心的可能就还有性能问题了~另外一个就是如果是复杂类里的域在java定义和json字符串之间有差异的时候，fastjson会如何处理，这也是一个值得测试的点，先mark下这两点，下回分解


未完待续。。。