---
title: Built-In Database Upgrades
author: mnash
layout: post
permalink: /built-in-database-upgrades/
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
  - Software Craftsmanship
tags:
  - automated
  - database
  - dbdeploy
  - Java
  - Maven
---
Often times an application (web application or otherwise) involves a database for storing it&#8217;s persistent data. As the application evolves over time, the database needs to change, and sometimes existing data needs to be updated to reflect those changes. 

How do we keep the app in sync with the schema changes of the corresponding database, in all the environments we might deploy into &#8211; such as local, testing, perhaps staging, and production? In some situations we want to re-create the database from scratch (such as a testing environment, for instance). In others (such as a production environment), we definitely **don&#8217;t** want to re-create the database, but just make carefully scripted modifications. In all cases, we want to make only the necessary modifications, based on the current state of the database.

A tool that a colleague recently recommended to me for this job is [dbdeploy][1], a utility for maintaining synchronization between our application and our database. Dbdeploy is less complex than other solutions, such as Database Migrations in Rails, arguably easier to implement and more portable to non-Ruby/Rails environments, and uses just SQL as the language to express the database changes.

Like Migrations, dbdeploy allows us to quickly and easily script our database changes, then apply those changes as required to a specific database instance in each of our deployment environments.

We can create a series of simple SQL files, like

*   001\_create\_base.sql
*   002\_expand\_customer_name.sql
*   003\_add\_order_status.sql
*   004\_update\_customers.sql

&#8230;and so forth. Each file represents a single simple change to our database schema, and is numbered in the order in which they occur. We don&#8217;t edit them, but add new ones as further changes are made, to ensure backwards-compatibility with all versions of our database.

Dbdeploy uses a change-log table, added to each of our target databases, to keep track of which scripts have already been run in that environment, automatically producing a script containing the set of changes that bring the current database up to the latest specification, including only the necessary changes and updates.

Dbdeploy comes with a command-line interface and an Ant task implementation, each of which is very straightforward to use. DbDeploy by default does not apply the changes, however &#8211; it only produces an SQL script that we can then review and either apply manually or via a second Ant task (or other means). Both dbdeploy and this second task need the connection information for the database supplied, however &#8211; the driver, JDBC URL, login and password. This is where I started to think &#8220;this can be simpler&#8221;&#8230;

If we&#8217;re deploying an application whose configuration already includes the necessary data to connect to the database, we could employ dbdeploy in a different way that overcomes this issue, as well as adding a few other advantages.

Let&#8217;s say in our development environment we keep our dbdeploy delta scripts in a directory that gets bundled into our finished application as resources. Maven can easily do this if you just put the files in the src/main/resources directory (by default), for instance. Now our database scripts can be bundled with our application automatically every time it&#8217;s built, without having any extra files to worry about.

We can also include dbdeploy in our classpath, instead of using it as a separate utility, and wrap up our application as a single jar file that includes our database definition scripts. We can extract these files from our application jar on demand with code like this (we don&#8217;t show the getResources method for clarity, but it gets a list of resource paths matching a specified pattern from our current classpath):

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
  public static String extractScripts() throws Exception {
        File scriptsDir = new File(SCRIPT_DIR_NAME);
        if (!scriptsDir.exists())
            if (!new File(SCRIPT_DIR_NAME).mkdirs())
                throw new RuntimeException("Could not create dir &#039;scripts&#039;");
        Collection&lt;String&gt; scripts = getResources(".*.sql");
        for (String script : scripts)
            extractToDir(script);
        return SCRIPT_DIR_NAME;
    }

    private static void extractToDir(String script) throws Exception {
        String endName = new File(script).getName();
        InputStream in = script.getClass().getResourceAsStream("/" + endName);
        if (in == null)
            throw new RuntimeException("Can&#039;t find resource " + endName);
        FileOutputStream fos = new FileOutputStream(new File(SCRIPT_DIR_NAME + "/" + endName));
        byte[] buf = new byte[1024];
        int i = 0;
        while ((i = in.read(buf)) != -1)
            fos.write(buf, 0, i);
        fos.close();
    }
&lt;/code&gt;
</pre>
</div>

Let&#8217;s say our main application is invoked with &#8220;java -jar someApplication-1.0.jar&#8221;. This implies we&#8217;ve set up a default main class and method in our jar meta-data &#8211; it&#8217;s the same as saying &#8220;java -cp someApplication-1.0.jar com.point2.main.MyMainClass&#8221;, just easier to type.

Nothing stops us having another main class, however, that we can invoke on demand, e.g.:  
java -cp someApplication-1.0.jar com.point2.main.DbDeploy

Code like this allows us to run dbdeploy on our extracted scripts, while passing it the database connection info we already know:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
 public static void prepScripts(String dbType, String driverName, String dbUrl, String userName, String password) throws Exception {
        com.dbdeploy.DbDeploy runner = new com.dbdeploy.DbDeploy();
        runner.setDbms(dbType);
        runner.setDriver(driverName);
        runner.setUrl(dbUrl);
        runner.setOutputfile(new File("scripts/output.sql"));
        runner.setUserid(userName);
        runner.setPassword(password);
        runner.setScriptdirectory(new File(SCRIPT_DIR_NAME));
        runner.go();
    }
&lt;/code&gt;
</pre>
</div>

This code produces our &#8220;output.sql&#8221; script, which contains exactly the required changes to our specified database to bring it up to date:

Then we can actually execute the resulting script (if we want to) via a method like so:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
 public static void applyScript(String script, String driverName, String dbUrl, String userName, String password) throws Exception {
        StringBuilder sb = new StringBuilder();
        FileInputStream fstream = new FileInputStream(SCRIPT_DIR_NAME + "/" + script);
        
        DataInputStream in = new DataInputStream(fstream);
        BufferedReader br = new BufferedReader(new InputStreamReader(in));
        String strLine;
        while ((strLine = br.readLine()) != null) {
            sb.append(strLine);
            sb.append("n");
        }
        in.close();
        executeSql(sb.toString(), driverName, dbUrl, userName, password);
    }

    private static void executeSql(String sql, String driverName, String dbUrl, String userName, String password) throws Exception {
        Driver driver = (Driver) Class.forName(driverName).newInstance();
        Connection connection = driver.connect(dbUrl, null);
        Statement statement = connection.createStatement();
        statement.executeUpdate(sql);
        connection.close();
    }
&lt;/code&gt;
</pre>
</div>

Doing this starts a sequence that 

1.  Extracts the database change scripts from the jar file
2.  Uses the application&#8217;s own configuration to get the JDBC Driver, URL, login and password information
3.  Invokes dbdeploy (internally) to create the database update script appropriate to whatever database we&#8217;re connected to
4.  Optionally, if we include the &#8220;execute&#8221; option on our command-line, run the resulting script &#8211; if necessary, creating the &#8220;change log&#8221; table used by dbdeploy in the process

As a finishing touch, we can examine the changelog table and determine exactly what incremental version our target database has been brought up to, and compare this to a known required version number in our application. In this way, our application can automatically verify that the dbdeploy process has been done on the database it&#8217;s being run against &#8211; and if it isn&#8217;t, we can output the proper command-line to perform the upgrade as a suggestion to the user (or even do it automatically, if permissable in our environment).

Now, instead of having a number of extra pieces to deploy to our target environment, we&#8217;re down to one nice tidy self-contained jar file, and we can choose to either simply update the database immediately or dump the script so we can examine what it&#8217;s going to do first, and either then decide to go ahead and apply or apply the changes manually ourselves.

Compared to dbdeploy in either Ant or standalone mode we&#8217;ve got the following advantages:

1.  We keep the simplicity of our single-jar deployment
2.  We can upgrade our database in any environment our application can run in &#8211; no need for extra tools
3.  We don&#8217;t need to repeat our database configuration information in two places &#8211; so they can&#8217;t get out of sync and end up running against the wrong database
4.  We ensure that the scripts required for the current version of the code are always with the code
5.  We guarantee that our application always runs against the database versioned to the expected state

I definitely recommend dbdeploy for this type of scenario.

<div class="g-plusone" data-annotation="inline" data-width="300">
</div>

<!-- Place this tag after the last +1 button tag. -->

  


<div class="st-callout hastitle lightblue center" >
  <h4 class="st-callout-title ">
    Principles and Practices
  </h4>
  
  <div class="inside">
    <i>Tired of the Software Development Grind?</i> Know it can be done better? Check out my book: <a href="http://jglobal.com/principles-and-practices">Principles and Practices of Software Craftsmanship</a> or sign up for my <a href="http://jglobal.com/dispatches/">Craftsmanship Dispatches</a> newsletter.
  </div>
</div>

<div class="clear">
</div>

 [1]: http://dbdeploy.com/