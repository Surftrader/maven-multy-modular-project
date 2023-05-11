Create a multy modular project
1. Create two project into the folder
a)
mvn archetype:generate -DgroupId=com.vogella -DartifactId=com.vogella.maven.api -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
b)
mvn archetype:generate -DgroupId=com.vogella -DartifactId=com.vogella.maven.consumer -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
2. Create parent pom.xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.vogella</groupId>
  <artifactId>com.vogella.parent</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>pom</packaging>

  <name>com.vogella.parent</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>11</maven.compiler.source>
    <maven.compiler.target>11</maven.compiler.target>
  </properties>

  <modules>
    <module>com.vogella.maven.api</module>
    <module>com.vogella.maven.consumer</module>
  </modules>
</project>
3. Update pom.xml in com.vogella.maven.api project
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>com.vogella</groupId>
    <artifactId>com.vogella.parent</artifactId>
    <version>1.0-SNAPSHOT</version>
  </parent>

  <groupId>com.vogella</groupId>
  <artifactId>com.vogella.maven.api</artifactId>
  <version>1.0-SNAPSHOT</version>

</project>
4. Update pom.xml in com.vogella.maven.consumer project
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>com.vogella</groupId>
    <artifactId>com.vogella.parent</artifactId>
    <version>1.0-SNAPSHOT</version>
  </parent>

  <groupId>com.vogella</groupId>
  <artifactId>com.vogella.maven.consumer</artifactId>
  <version>1.0-SNAPSHOT</version>

</project>
5. Update parent pom.xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.vogella</groupId>
  <artifactId>com.vogella.parent</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>pom</packaging>

  <name>com.vogella.parent</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>11</maven.compiler.source>
    <maven.compiler.target>11</maven.compiler.target>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>
  </dependencies>


  <modules>
    <module>com.vogella.maven.api</module>
    <module>com.vogella.maven.consumer</module>
  </modules>
</project>
6. Check build
mvn clean verify
7. Update parent pom.xml
<build>
    <plugins>
      <plugin>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>2.22.2</version>
      </plugin>
      <plugin>
        <artifactId>maven-failsafe-plugin</artifactId>
        <version>2.22.2</version>
      </plugin>
    </plugins>
  </build>
<dependencies>
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter-api</artifactId>
      <version>5.7.2</version>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter-engine</artifactId>
      <version>5.7.2</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
8. Change tests in api
package com.vogella.maven.api;

import static org.junit.jupiter.api.Assertions.assertTrue;

import org.junit.jupiter.api.Test;

/**
 * Unit test for simple App.
 */
public class AppTest
{
    @Test
    public void shouldAnIswerWithTrue()
    {
        App app = new App();
        assertTrue( true );
    }
}
9. Change tests in consumer
package com.vogella.maven.consumer;

import static org.junit.jupiter.api.Assertions.assertTrue;

import org.junit.jupiter.api.Test;

/**
 * Unit test for simple App.
 */
public class AppTest
{
    /**
     * Rigorous Test :-)
     */
    @Test
    public void shouldAnswerWithTrue()
    {
        System.out.println("THIS IS A TEST");
        assertTrue( true );
    }
}
10. Define API (create class)
package com.vogella.maven.api;

public interface TaskService {

}
11. Define usage (add dependency in consumer pom.xml)
<dependencies>
    <dependency>
        <groupId>com.vogella</groupId>
        <artifactId>com.vogella.maven.api</artifactId>
        <version>1.0-SNAPSHOT</version>
    </dependency>
  </dependencies>
12. Change App class into consumer project to use API
package com.vogella.maven.consumer;

import com.vogella.maven.api.TaskService;

public class App
{
    public static void main( String[] args )
    {
        System.out.println( "Hello World!" );
        TaskService taskService;
    }
}
13. Check
mvn clean verify
14. Run
mvn clean install
15. Create executable jar-file. Add ... into pom.xml (consumer project)
<build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-assembly-plugin</artifactId>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                        <configuration>
                            <archive>
                                <manifest>
                                    <mainClass>
                                        com.vogella.maven.consumer.App
                                    </mainClass>
                                </manifest>
                            </archive>
                            <descriptorRefs>
                                <descriptorRef>jar-with-dependencies</descriptorRef>
                            </descriptorRefs>
                        </configuration>
                    </execution>
                </executions>
                </plugin>
        </plugins>
    </build>
16. Create maven wrapper. Run:
mvn -N io.takari:maven:wrapper
17. Check wrapper
Windows: mvnw.cmd clean verify
Linux/Mac: ./mvnw clean verify 




