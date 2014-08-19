---
title: Springing into Jars
author: mnash
layout: post
permalink: /springing-into-jars/
related_exlink_1:
  - 
related_exlink_1_desc:
  - 
related_exlink_2:
  - 
related_exlink_2_desc:
  - 
related_exlink_3:
  - 
related_exlink_3_desc:
  - 
related_exlink_4:
  - 
related_exlink_4_desc:
  - 
related_exlink_5:
  - 
related_exlink_5_desc:
  - 
categories:
  - Tips and Tricks
tags:
  - Java
  - Maven
  - spring
  - webapps
---
While the powerful Spring Framework is commonly used for Java web applications, there no reason you can&#8217;t also use it for good old-fashioned command-line apps as well.

I recently had occasion to take a large web application and attempt to break a bit out of it to run as a standalone jar, and made a few interesting discoveries along the way.

Let&#8217;s say you want to run the following main method:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
package com.point2;

import com.point2.MyBeanClass;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class MyMainClass {

    public static void main(String args[]) {
         try {
             MyBeanClass myClass = getMyBean("beanId");
             myClass.doImportantWork();
         } catch (Exception e) {
             e.printStackTrace();
         }
    }

    private static MyBeanClass getMyBean(String beanId) {
        ApplicationContext applicationContext =
            new ClassPathXmlApplicationContext("classpath:spring-beans.xml");
        return (MyBeanClass) applicationContext.getBean(beanId);
    }
}
&lt;/code&gt;
</pre>
</div>

This class simply creates the Spring application context, gets a bean, and executes the doImportantWork method on it. As it&#8217;s a main method, we can call it from the command-line, with no container or deployment required, if we could put our webapp into an executable jar, along with all it&#8217;s dependencies (which include Spring).

As I was lucky enough to have a Maven project for my webapp, my first thought was to use the Maven &#8220;assembly&#8221; plugin to create a single jar file with all required classes. This worked fine, creating my webapp-1.0-jar-with-dependencies.jar as advertised. The problem came when I tried to run my command-line app. I created a little script like so:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
java -cp target/webapp-1.0-jar-with-dependencies.jar com.point2.MyMainClass
&lt;/code&gt;
</pre>
</div>

And executed it. Immediately Spring complained about not being able to find NamespaceHandlers for some obscure namespace I used in my Spring configuration files.

Hmph.

After a long dig through the relevant doc, it turns out that several of the Spring jar files have a file called &#8220;spring.schemas&#8221; in their META-INF directories, and a corresponding file called &#8220;spring.handlers&#8221; that says where to get the appropriate handlers for the schemas they understand. Unfortunately, the files are not the same in all of the various Spring dependency jars &#8211; in other words, the schemas and handlers in one Spring jar are different from the schemas and handlers in another.

When the assembly plugin puts all these jars together into one uber-jar, the &#8220;last man in wins&#8221;, in other words, whatever Spring jar is processed last has it&#8217;s spring.schema and spring.handlers file end up in the uber-jar, overwriting the others.

This results in Spring not being able to find the proper list of handlers on startup, hence my kaboom.

There&#8217;s an open bug discussing this problem in the Jira for the assembly plugin, but fortunately there&#8217;s another option: The [maven &#8220;shade&#8221; plugin.][1]

Add the following plugin magic to your POM&#8217;s build section:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
 &lt;plugin&gt;
    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
    &lt;artifactId&gt;maven-shade-plugin&lt;/artifactId&gt;
    &lt;executions&gt;
        &lt;execution&gt;
            &lt;phase&gt;package&lt;/phase&gt;
            &lt;goals&gt;
                &lt;goal&gt;shade&lt;/goal&gt;
            &lt;/goals&gt;
            &lt;configuration&gt;
                &lt;transformers&gt;
                    &lt;transformer implementation="org.apache.maven.plugins.shade.resource.AppendingTransformer"&gt;
                        &lt;resource&gt;META-INF/spring.handlers&lt;/resource&gt;
                    &lt;/transformer&gt;
                    &lt;transformer implementation="org.apache.maven.plugins.shade.resource.AppendingTransformer"&gt;
                        &lt;resource&gt;META-INF/spring.schemas&lt;/resource&gt;
                    &lt;/transformer&gt;
                &lt;/transformers&gt;
            &lt;/configuration&gt;
        &lt;/execution&gt;
    &lt;/executions&gt;
&lt;/plugin&gt;

&lt;/code&gt;
</pre>
</div>

The &#8220;AppendingTransformer&#8221; bit is where we tell the plugin to concatenate together all resources with the same name, instead of just using the most recent one encountered.

Then change the <packaging> element in your project&#8217;s POM to say &#8220;jar&#8221; instead of &#8220;war&#8221;, and do a 

<pre>&lt;code&gt;
mvn package
&lt;/code&gt;
</pre>

Now you end up with a jar file called &#8220;webapp-1.0.jar&#8221; instead of the war file in your target directory, but this time with all the proper spring.schema and spring.handler files appended together.

Now you can say 

<pre>&lt;code&gt;
java -cp target/webapp-1.0.jar com.point2.MyMainClass
&lt;/code&gt;
</pre>

And Spring happily winds up an application context and works as expected.

Happy jar-ing!

 [1]: http://maven.apache.org/plugins/maven-shade-plugin/index.html