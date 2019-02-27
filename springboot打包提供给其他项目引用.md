### springboot打包提供给其他项目引用
#### 1. 剔除不需要的文件：如Application和ApplicationTests
#### 2. 打包
 不能使用springboot自带打包：
 
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

 而应当使用普通maven打包：

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>

**刚开始我使用了spring-boot-maven-plugin打包，出现了bug。虽然目的项目引用了该打包项目，
但是任然无法引用jar中的类，因为springboot-maven-plugin打包的第一级目录为Boot-INF，无法引用。**

1. *注：Maven中的dependency的scope作用域详解*
    1. test范围指的是测试范围有效，在编译和打包时都不会使用这个依赖
    2. compile范围指的是编译范围有效，在编译和打包时都会将依赖存储进去
    3. provided依赖：在编译和测试的过程有效，最后生成war包时不会加入，诸如：servlet-api，因为servlet-api，tomcat等web服务器已经存在了，如果再打包会冲突
    4. runtime在运行的时候依赖，在编译的时候不依赖
2. *注：加入本地maven路径：*
     C:\Users\ofcard\.m2\repository\com\scn7th\ding-robot-bind-send\0.0.1-SNAPSHOT>mvn install:install-file -Dfile=ding-robot-bind-send-0.0.1-SNAPSHOT.jar -DgroupId=com.scn7th -DartifactId=ding-robot-bind-send -Dversion=0.0.1-SNAPSHOT -Dpackaging=jar
3. *注：java启动jar包（如启动springboot项目jar包）：*
     java –jar xx.jar




