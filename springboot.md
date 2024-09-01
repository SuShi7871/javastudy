# springboot

## 快速上手SpringBoot

```java
@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String hello() {
        return "Hello Spring Boot!";
    }
}
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
//访问路径：	http://localhost:8080/hello
```

### 开发环境热部署

- Spring Boot提供了spring-boot-devtools组件，使得无须手动重启Spring Boot应用即可重新编译、启动项目，大大缩短编译启动的时间。
- devtools会监听classpath下的文件变动，触发Restart类加载器重新加载该类，从而实现类文件和属性文件的热部署。
- 并不是所有的更改都需要重启应用（如静态资源、视图模板），可以通过设`spring.devtools.restart.exclude`属性来指定一些文件或目录的修改不用重启应用

```xml-dtd
<!--使用optional=true表示依赖不会传递，即该项目依赖devtools；其他项目如果引入此项目生成的JAR包，则不会包含devtools-->
<dependency>    
	<groupId>org.springframework.boot</groupId>    
	<artifactId>spring-boot-devtools</artifactId>    
	<version>true</version>
</dependency>
```

在application.properties中配置devtools。

```xml-dtd
# 在application.properties中配置devtools。
spring.devtools.restart.enabled=true
# 设置重启目录
spring.devtools.restart.additional-paths=src/main/java
# 设置不重启目录spring.devtools.restart.exclude=static/**
# 系统的端口配置
server.port=8081
```

application.properties的其他配置

```xml-dtd
# 关闭运行日志图表（banner)
spring.main.banner-mode=off
# 设置运行日志的显示级别
logging.level.root=debug
```

### parent和starter

整体上来说，<font color="#ff0000"><b>使用parent可以帮助开发者进行版本的统一管理</b></font>

```xml-dtd
<properties>
    <hibernate.version>5.4.32.Final</hibernate.version>
    <hibernate-validator.version>6.2.0.Final</hibernate-validator.version>
    <junit.version>4.13.2</junit.version>
</properties>
<!--引用了上述信息中定义的依赖版本属性值-->
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>${hibernate.version}</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>${junit.version}</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```

starter定义了使用某种技术时对于依赖的固定搭配格式，也是一种最佳解决方案，<font color="#ff0000"><b>使用starter可以帮助开发者减少依赖配置</b></font>

所有的starter中都会依赖下面这个starter，叫做spring-boot-starter。这个starter是所有的SpringBoot的starter的基础依赖，里面定义了SpringBoot相关的基础配置

```xml-dtd
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
    <version>2.5.4</version>
    <scope>compile</scope>
</dependency>
```

项目中的pom.xml定义了使用SpringMVC技术，但是并没有写SpringMVC的坐标，而是添加了一个名字中包含starter的依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

在spring-boot-starter-web中又定义了若干个具体依赖的坐标

```xml-dtd
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
        <version>2.5.4</version>
        <scope>compile</scope>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-json</artifactId>
        <version>2.5.4</version>
        <scope>compile</scope>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-tomcat</artifactId>
        <version>2.5.4</version>
        <scope>compile</scope>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
        <version>5.3.9</version>
        <scope>compile</scope>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.3.9</version>
        <scope>compile</scope>
    </dependency>
</dependencies>
```

**starter与parent的区别**

​	朦朦胧胧中感觉starter与parent好像都是帮助我们简化配置的，但是功能又不一样，梳理一下。

​	<font color="#ff0000"><b>starter</b></font>是一个坐标中定了若干个坐标，以前写多个的，现在写一个，<font color="#ff0000"><b>是用来减少依赖配置的书写量的</b></font>

​	<font color="#ff0000"><b>parent</b></font>是定义了几百个依赖版本号，以前写依赖需要自己手工控制版本，现在由SpringBoot统一管理，这样就不存在版本冲突了，<font color="#ff0000"><b>是用来减少依赖冲突的</b></font>

### yml格式和yaml格式

yml和yaml的格式如下

```xml-dtd
server:
  port: 81
```

yml和yaml文件格式是一模一样的，只是文件后缀不同，所以可以合并成一种格式来看。

## springboot整合其他模块

### 整合MyBatis

导入坐标

```xml-dtd
<!--1.导入mybatis与spring整合的jar包-->
<dependency>    
	<groupId>org.mybatis</groupId>    
	<artifactId>mybatis-spring</artifactId>    
	<version>1.3.0</version>
</dependency>
<!--导入spring操作数据库必选的包-->
<dependency>    
	<groupId>org.springframework</groupId>    
	<artifactId>spring-jdbc</artifactId>    
	<version>5.2.10.RELEASE</version>
</dependency>
 <!--1.导入对应的starter-->
 <dependency>
      <groupId>org.mybatis.spring.boot</groupId>
      <artifactId>mybatis-spring-boot-starter</artifactId>
      <version>2.2.0</version>
  </dependency>

  <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <scope>runtime</scope>
 </dependency>
```

Spring核心配置



























































