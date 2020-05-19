Custom Redis Plugin For Maven
==================

Embedded Test Pure Java Redis Server Plugin for Maven POM


Basic example
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

Are you see this message you are ready to go: ```[INFO] Starting Redis(forked=false) server...```


Integration tests example
-----------------


Configure plugin as follow steps:
```xml
<plugin>
    <groupId>com.arbade.maven.plugins</groupId>
    <artifactId>redis-maven-plugin</artifactId>
    <version>1.0.1</version>
    <configuration>
        <forked>true</forked>
    </configuration>
    <executions>
        <execution>
            <id>start-redis</id>
            <phase>pre-integration-test</phase>
            <goals>
                <goal>run</goal>
            </goals>
        </execution>
        <execution>
            <id>stop-redis</id>
            <phase>post-integration-test</phase>
            <goals>
                <goal>shutdown</goal>
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

