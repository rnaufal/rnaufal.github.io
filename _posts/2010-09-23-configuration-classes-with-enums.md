---
id: 324
title: 'Configuration classes with Enums'
date: '2010-09-23T19:18:37-03:00'
author: rnaufal
layout: single
guid: 'http://rafaelnaufal.com/blog/?p=324'
dsq_thread_id:
    - '146123313'
categories:
    - Uncategorized
tags:
    - 'effective java'
    - enum
    - java
    - properties
    - singleton
---

As I mentioned on my previous [post](http://rafaelnaufal.com/blog/2010/09/07/singleton-in-java-with-enum-types/), an alternative implementation to create Singleton in Java is with Enum types.

Extending the idea, it is interesting to create classes which read configuration values from [Properties](http://download.oracle.com/javase/6/docs/api/java/util/Properties.html) files with Enum classes. Below is an example:

```

public enum Configuration {

    HOST("host"),
    PORT("port"),
    MAIL_SERVER("mailServer"),
    INPUT_DIRECTORY("inputDirectory"),
    OUTPUT_DIRECTORY("outputDirectory");

    private static Properties properties;
    static {
        properties = new Properties();
        try {
            properties.load(Configuration.class.getClassLoader().getResourceAsStream(
                "configuration.properties"));
        } catch (Exception e) {
            throw new RuntimeException("Error when loading configuration file", e);
        }
    }

    private String key;

    Configuration(String key) {
        this.key = key;
    }

    public String getKey() {
        return key;
    }

    public String getValue() {
        return properties.getProperty(key);
    }
}
```

Configuration classes which read values from properties files should be Singletons that are loaded once on the application startup time.

The Configuration values can be used this way:

```

System.out.println(Configuration.HOST.getValue());
```

This example shows that the key and value from properties are stored with Enum constants. They are type-safe, they can be easily accessed through code completion in your favourite IDE and they can take advantage of refactoring tools.