Custom Redis Plugin For Maven
==================

Embedded Test Pure Java Redis Server Plugin for Maven POM


Usage
-----------------

add plugin to your pom:
```xml
<plugin>
    <groupId>com.arbade.maven.plugins</groupId>
    <artifactId>redis-maven-plugin</artifactId>
    <version>1.0.1</version>
</plugin>
```

run ```mvn redis:run```

When you see this message,you are ready to go: ```[INFO] Redis-Server Started...```


Integration tests example
-----------------


Configure plugin as follow steps:
```xml
                    <plugin>
                        <groupId>com.arbade.maven.plugins</groupId>
                        <artifactId>redis-maven-plugin</artifactId>
                        <version>1.0.1</version>
                        <executions>
                            <execution>
                                <id>start-redis</id>
                                <phase>pre-integration-test</phase>
                                <goals>
                                    <goal>compileRun</goal>
                                </goals>
                            </execution>
                            <execution>
                                <id>stop-redis</id>
                                <phase>post-integration-test</phase>
                                <goals>
                                    <goal>compileShutdown</goal>
                                </goals>
                            </execution>
                            <execution>
                                <id>run-redis</id>
                                <phase>run-redis</phase>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
```

Now you will be able to run your integration Redis-backed tests with ```mvn clean verify```

After then, you will be able to see this message you are ready to go about your integration test
``` 
-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running com.arbade.maven.plugins.redis.example.tests.ConnectionTest
PONG
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.149 sec
Results :
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] --- redis-maven-plugin:1.0.1:shutdown (stop-redis) @ redis-maven-plugin-example ---
[INFO] Shutting down Redis server...
[INFO] Redis server shutdown completed
```
Basic example
-----------------

Firstly,you will be able to add useful dependency for running up Redis Server on Java

```xml
       <dependencies>
         <dependency>
            <groupId>redis.clients</groupId>
            <artifactId>jedis</artifactId>
            <version>2.2.1</version>
            <scope>compile</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>com.github.kstyrc</groupId>
            <artifactId>embedded-redis</artifactId>
            <version>0.6</version>
        </dependency>
      </dependencies>
```

Secondly,you have to use redis custom plugin for Runtime server running up...

run ```mvn redis:run```

Are you see this message you are ready to go: ```[INFO] Redis-Server Started...```



Thirdly,you can create Jedis Pool Config for Pool Connection...
When you create pool connection, you will be able to set key<-> value insert to Redis-Cli from Java
```java
public class Connection {
    public static void main(String[] args) {

        JedisPoolConfig jedisPoolConfig = new JedisPoolConfig();
        JedisPool pool = new JedisPool(jedisPoolConfig, "localhost", 6379);
        pool.getResource().set("arda", "demir");
        System.out.println(pool.getResource().get("arda"));
    }
}

```
Finally, you will be able to see value of setting up key's on console output.

```
/Library/Java/JavaVirtualMachines/jdk-11.0.7.jdk/Contents/Home/bin/java -javaagent:/Applications/IntelliJ IDEA.app/Contents/lib/idea_rt.jar=57549:/Applications/IntelliJ IDEA.app/Contents/bin -Dfile.encoding=UTF-8 -classpath /Users/arbade/Desktop/example/target/classes:/Users/arbade/.m2/repository/junit/junit/4.11/junit-4.11.jar:/Users/arbade/.m2/repository/org/hamcrest/hamcrest-core/1.3/hamcrest-core-1.3.jar:/Users/arbade/.m2/repository/redis/clients/jedis/2.2.1/jedis-2.2.1.jar:/Users/arbade/.m2/repository/commons-pool/commons-pool/1.6/commons-pool-1.6.jar:/Users/arbade/.m2/repository/com/github/kstyrc/embedded-redis/0.6/embedded-redis-0.6.jar:/Users/arbade/.m2/repository/com/google/guava/guava/18.0/guava-18.0.jar:/Users/arbade/.m2/repository/commons-io/commons-io/2.4/commons-io-2.4.jar:/Users/arbade/.m2/repository/org/springframework/spring-beans/5.2.6.RELEASE/spring-beans-5.2.6.RELEASE.jar:/Users/arbade/.m2/repository/org/springframework/spring-core/5.2.6.RELEASE/spring-core-5.2.6.RELEASE.jar:/Users/arbade/.m2/repository/org/springframework/spring-jcl/5.2.6.RELEASE/spring-jcl-5.2.6.RELEASE.jar Connection
demir

Process finished with exit code 0

```
When you check the redis-cli from terminal,you can be used to following steps(Installed Redis on MacOS) :
```
redis-server
```
```
> redis-cli
arbade@Ardas-MacBook-Pro ~ % redis-cli
127.0.0.1:6379> 
```
```
127.0.0.1:6379> get arda
"demir"
```
