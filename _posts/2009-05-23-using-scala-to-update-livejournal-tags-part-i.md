---
id: 73
title: 'Using Scala to update LiveJournal tags &#8211; Part I'
date: '2009-05-23T13:45:00-03:00'
guid: 'http://rnaufal.wordpress.com/2009/05/23/using-scala-to-update-livejournal-tags-part-i/'
lj_itemid:
    - '82'
lj_permalink:
    - 'http://rnaufal.livejournal.com/21132.html'
dsq_thread_id:
    - '102873622'
categories:
    - Uncategorized
tags:
    - closures
    - functional
    - java
    - jvm
    - programming
    - scala
---

Some days ago I started to use the [Scala](http://www.scala-lang.org/) programming language to update my Livejournal tags using its [XML-RPC](http://en.wikipedia.org/wiki/XML-RPC) protocol reference. First I had to check if some tags of mine were entered wrong, so I’ve done this Scala program to list all of them:

```scala
import org.apache.xmlrpc.client.XmlRpcClient;
import org.apache.xmlrpc.client.XmlRpcClientConfigImpl;
import org.apache.xmlrpc.client.XmlRpcCommonsTransportFactory;
import java.net.URL;
import java.util.Map
import java.util.HashMap
import scala.collection.immutable.TreeSet

object LJListTag {
     def main(args: Array[String]) {
        val config = new XmlRpcClientConfigImpl()
        config.setEnabledForExtensions(true);
        config.setServerURL(new URL("http://www.livejournal.com/interface/xmlrpc"))
        val client = new XmlRpcClient()
        client.setConfig(config)
        val params = new HashMap[String, String]
        params.put("username", "user")
        params.put("password", "password")
        var paramsToServer = new Array[Object](1)
        paramsToServer(0) = params
        val results = client.execute("LJ.XMLRPC.getusertags", paramsToServer).asInstanceOf[Map[String, String]];
        printEachTag(results)
    }

    def printEachTag(results: Map[String, String]) {
        var allTags = new TreeSet[String]
        val iterator = results.values().iterator()
            while(iterator.hasNext()) {
                val resultFromRPCData = iterator.next().asInstanceOf[Array[Any]]
                    resultFromRPCData.foreach(singleResult => allTags += extractTag(singleResult))
            }
            allTags.foreach(tag => println(tag))
        }

    def extractTag(singleResult: Any): String = {
        val tag = singleResult.asInstanceOf[HashMap[String, String]]
        return tag.get("name")
    }
}
```

Just fill your user and password to have all of your LiveJournal tags printed on the standard output. The experience was so amazing, since you can use all the Java libraries (Scala is fully interoperable with Java and runs on top of the JVM). I used a [TreeSet](http://www.scala-lang.org/docu/files/api/scala/collection/immutable/TreeSet$object.html) because I wanted print my tags sorted according its alphabetical order. I’m continuously studying Scala and its API, so the code above doesn’t use any advanced Scala constructs. If you have any suggestion about the code or how to use better the Scala constructs, post your comments here. It will be all appreciated.