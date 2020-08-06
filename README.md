# Maven

## 第一节 为什么使用Maven

    1.1 目前掌握的技术

        浏览器
          ↓
    视图层/表示层/表述层/表现层 ----> 视图层 H5/CSS/JS/JSP
          ↓                     |
          ↓                     --> 控制层 Servlet/Action/Handler
          ↓
        业务逻辑层             . . > Spring IOC AOP
          ↓
          ↓
        持久化层               ----> JDBC/DBUtils/Spring JDBCTemplate/Hibernate/MyBatis
          ↓
          ↓
        数据库                 ----> MySQL/Oracle

    1.2 目前的技术在开发中的问题

    ·一个项目就是一个工程
        > 如果一个项目非常庞大，就不适合继续使用package来划分模块了
          应该转变为一个模块对应一个工程的方式，便于分工合作

          - 借助于Maven，就可以将一个项目拆分为多个工程

    ·项目中需要的jar包必须手动“粘贴”、“复制”到WEB-INF/lib下
        > 同一个jar包重复出现在不同的项目工程中
          一方面浪费存储空间，另外也让工程比较臃肿

          - 借助于Maven，可以将jar包仅仅保存在“仓库”中，有需要时引用这个文件接口就可以了
          - 不需要真的把jar包复制过来

    ·jar包需要别人帮忙准备好，或到官网下载
        > 不同技术的官网提供jar包下载的形式是五花八门的
          有的技术的官网就是通过Maven或SVN来提供jar包下载的
          如果是以非正规的方式下载的jar包，其内容也很可能是不规范的

          - 借助于Maven，可以以一种规范的方式下载jar包
          - 因为所有知名的框架或第三方工具的jar包已经按照统一的规范存放在了Maven的仓库中

          Tips：“统一的规范”不仅对IT开发领域非常重要，对于整个人类社会都是非常重要的

    ·一个jar包依赖的其他jar包需要自己手动加入到项目中
        > commons-fileupload-xxx.jar → commons-io-xxx.jar一类的依赖关系经常会存在
          大型工程的依赖关系可以非常复杂，如果所有jar包之间的依赖关系都需要程序员非常了解，
          就会极大地增加学习成本

          - Maven会自动将被依赖的jar包导入工程

## 第二节 Maven是什么

    2.1 Maven是一款服务于Java平台的自动化构建工具

    > Java平台 ※Maven本身也是用Java写的

        发展过程：
            Make → Ant → Maven → Gradle

        读音：
            梅文、麦文

        ※ Maven来源于美国俚语，意为内行、专家

    2.2 构建

    > 概念：

        以
            ·Java源文件
            ·框架配置文件
            ·JSP
            ·HTML
            ·图片
        等资源作为原材料，去生产一个可以运行的项目的过程就称为“构建”。

        - 编译、部署、搭建

    > 编译：Java源文件[User.java] → 编译 → Class字节码文件[User.class]

    > 部署：一个B/S项目最终运行的并不是动态Web工程本身，而是Web工程“编译的结果”

        生的鸡      → 处理      → 熟的鸡
        动态Web工程 → 编译、部署 → 可以在服务器上执行的工程

        开发过程中，所有的路径或配置文件的类路径等都是以编辑结果的目录结构为标准的

        Tips:平时Eclipse里面工程的JRE System Library，Apache Tomcat是工程的运行时环境
            只是一组jar包的引用，并没有把jar包真的拷贝到工程中

    2.3 构建过程中的各个环节

    1. 清理：

      将以前编译得到的旧的字节码文件删除，为下一次编译做准备

    2. 编译：

      将Java源程序编译成class字节码文件

    3. 测试：

      自动化测试 => 提前准备好测试程序，自动调用Junit来进行测试

    4. 报告：

      测试程序执行的结果

    5. 打包：

      动态Web工程打war包，Java工程打jar包

    6. 安装：

      Maven特有的概念 - 将打包好的文件复制到仓库中指定的位置

    7. 部署：

      将动态Web工程生成的war包复制到Servlet容器的指定目录下，使其可以运行

    2.4 自动化构建

## 第三节 安装Maven核心程序

    1> 检查JAVA_HOME环境变量

    2> 解压Maven核心程序的压缩包，放在一个非中文无空格目录下

    3> 配置Maven的环境变量

        > MAVEN_HOME或M2_HOME

          - 值是bin目录的上一级

        > path

          - bin目录

    4> 验证

        mvn -v 查看Maven的版本

## 第四节 Maven的核心概念

    · 约定的目录结构
    · POM
    · 坐标
    · 依赖 ☆
    · 仓库
    · 生命周期/插件/目标
    · 继承
    · 聚合

## 第五节 第一个Maven工程

    5.1 目录结构

        > 根目录： 工程名
        > src目录： 源码
        > pom.xml: Maven工程的核心配置文件
        > main目录： 存放主程序
        > test目录： 存放测试程序
        > java目录： 存放java源文件
        > resources目录： 存放框架配置文件或其他工具的配置文件(.xml .properties)

      Hello
        |--src
        |   |--main
        |   |   |--java
        |   |   |--resources
        |   |--test
        |       |--java
        |       |--resources
        |--pom.xml

    5.2 为什么要遵守约定的目录结构？

        ·Maven负责项目的自动化构建，以编译过程为例：

          - Maven要进行自动编译，必须要知道java源文件保存的位置

        ·如果自定义的结构想要让框架知道，有两种方法：

          - 以配置的方式明确告诉框架
          - 遵守框架内部约定

        ·共识：
          约定 > 配置 > 编码

## 第六节 常用Maven命令

    6.1 注意：

        执行与构建过程相关的Maven命令，必须进入pom.xml所在的目录

          - 编译
          - 测试
          - 打包

          ...

    6.2 常用命令

      ·mvn clean：清理
      ·mvn compile：编译主程序
      ·mvn test-compile：编译测试程序
      ·mvn test：执行测试
      ·mvn package：打包
      ·mvn install：安装
      ·mvn site：生成站点

      ·mvn deploy：部署（少用）

## 第七节 关于联网的问题

    7.1 Maven的核心程序中仅仅定义了抽象的生命周期，具体的工作必须由特定的插件来完成。
        特定的插件并不包含在Maven的核心程序中。

    7.2 当执行的Maven命令需要用到某些特定插件时，Maven核心程序首先会到本地仓库中查找

    7.3 本地仓库的默认目录：
        \User的家目录\.m2\repository

    7.4 Maven如果在本地仓库中找不到需要的插件，那么它会自动连接外网，到中央仓库去下载

    7.5 如果此时无法连接外网则构建失败

    7.6 可以指定本地仓库目录到事先准备好的位置
        %MAVEN_HOME%\conf\settings.xml

          - <localRepository>/path/to/local/repo</localRepository>

## 第八节 POM

    8.1 含义
        Project Object Model， 项目对象模型

        ※DOM：Document Object Model，文档对象模型

    8.2 pom.xml对于Maven工程是核心配置文件，与构建过程相关的一切设置都在这个文件中进行。

        ※重要程度相当于web.xml之于Web工程

## 第九节 坐标

    9.1 数学中的坐标

    

        在平面上使用(x,y)两个向量可以唯一定位平面中的一个点；
        在空间上使用(x,y,z)三个向量可以唯一定位空间中的一个点。

    9.2 Maven的坐标

        使用下面三个向量在仓库中唯一定位一个Maven工程

        > groupId: 公司或组织域名倒序 + 项目名
            <groupId>pt.learn.maven</groupId>

        > artifactId: 模块名
            <artifactId>Hello</artifactId>

        > version: 版本
            <version>1.0.0</version>

        ※合起来简称为gav

    9.3 Maven工程坐标与仓库中路径的对应关系

        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>4.0.0.RELEASE</version>

        仓库/org/springframework/spring-core/4.0.0.RELEASE/spring-core-4.0.0.RELEASE.jar

## 第十节 仓库

    10.1 仓库有两类：

        ·本地仓库

            - 本地部署的仓库，为当前电脑上所有Maven工程服务

        ·远程仓库

          1. 私服
            - 搭建在局域网环境中，为局域网范围内的所有Maven工程服务

              用户 -------| Nexus |------- Maven Central
              用户 -------|  私服  |-------- Apache
                                  |-------- 其他远程仓库

          2. 中央仓库
            - 架设在Internet上，为全世界所有Maven工程服务

          3. 中央仓库的镜像
            - 架设在各个大洲，为中央仓库分担流量
            - 提升用户访问的速度

    10.2 仓库中保存的内容：Maven工程

        ·Maven自身需要的插件

        ·第三方框架或工具的jar包
            ※第一方：jdk 第二方：开发者

        ·我们自己开发的Maven工程

## 第十一节 第二个Maven工程

    10.1 目录结构

      HelloFriend
        |--src
        |   |--main
        |   |   |--java
        |   |   |--resources
        |   |--test
        |       |--java
        |       |--resources
        |--pom.xml

      pom.xml内添加一个依赖

      <dependency>
          <groupId>pt.maven</groupId>
          <artifactId>Hello</artifactId>
          <version>0.0.1-SNAPSHOT</version>
      </dependency>

## 第十二节 依赖

    12.1 Maven解析依赖信息时会到本地仓库中查找被依赖的jar包

      ※ 对于自己开发的工程，使用mvn install安装，存入本地仓库

    12.2 依赖的范围

        <scope>compile<scope>

        有三个常用参数：
        
                  对主程序是否有效  对测试程序是否有效  是否参与打包
        compile     有效            有效                参与        ex. spring-core
        test        无效            有效               不参与       ex. junit
        provided    有效            有效               不参与       ex. servlet-api
                                                  （运行时由其它组件
                                                   比如WebServer提供）

    12.3 依赖按照依赖来源可以分两种：

      ·直接依赖

        - 直接写在自己工程的pom.xml中的依赖

      ·间接依赖

        - 由被依赖项目传递来的依赖

    12.4 依赖的传递性

      > 好处：
          可以传递的依赖不必在每个模块工程中都重复声明，
          在“最下面”的工程中依赖一次即可

      > 注意：
          非compile范围的依赖不可以传递，
          故而test和provided范围的依赖每次使用都要个别声明

    12.5 依赖的排除

      > 需要设置依赖排除的场合

        - 第三方提供
        - 正在开发中的不稳定版

      > 依赖排除的设置方式
        <dependency> - 引入了不需要的依赖的工程本体
          <exclusions>
            <exclusion>
              <groupId>commons-logging</groupId>
              <artifactId>commons-logging</artifactId>
            </exclusion>
          </exclusions>
        </dependency>

      > 依赖排除可以消除依赖性，排除过后，后面的工程也不会收到被中途排除的依赖了

    12.6 依赖的原则

      > 作用：
          解决模块工程之间的jar包冲突

        ·情景1
            MakeFriends           ←--  ！冲突  --→ log4j_v1.2.14采用

              - HelloFriend         |
                - log4j_v1.2.14   -→|
                - Hello             |
                  - log4j_v1.2.17 -→|

          >> Maven依赖采用原则1：就近优先

        ·情景2
            MakeFriends           ←--  ！冲突  --→ log4j_v1.2.14采用

              - HelloFriend         |
                - log4j_v1.2.14   -→|
              - Hello               |
                - log4j_v1.2.17   -→|

          >> Maven依赖采用原则2：路径相同时，先声明者优先
              ※先声明：dependency标签的出现顺序

    12.7 统一管理依赖的版本

        ·情景1
            一批Spring的jar包的依赖版本都是4.0.0.RELEASE，
            想要统一升级到4.1.1.RELEASE，怎么办？

            >> 解决方案：
              ·配合<properties>标签统一声明版本号
              ·在需要统一版本的位置，使用${标签名}引用声明的版本号

                <properties>
                  <springVer>4.1.1.RELEASE</springVer>
                </properties>

                <dependency>
                  <groupId>org.springframework</groupId>
                  <artifactId>spring-core</artifactId>
                  <version>${springVer}</version>
                </dependency>

            ※properties标签不局限于版本号，各种需要自定义的变量都可以使用，比如全局字符集等

## 第十三节 生命周期

    13.1 含义

        Maven的生命周期就是指各个构建环节的执行顺序

        Maven的核心程序中定义了抽象的生命周期，各个生命周期的具体工作由插件来执行

    13.2 三套相互独立的生命周期

        ·Clean Lifecycle

          - 在进行真正的构建之前进行一些清理工作

        ·Default Lifecycle

          - 构建的核心部分：编译、测试、打包、安装、部署等

        ·Site Lifecycle

          - 生成项目报告、站点、发布站点

        每套生命周期都由一组阶段（Phase）组成

    13.3 Clean生命周期 - mvn clean
        · pre-clean
        · clean
        · post-clean

    13.4 Default生命周期
        · validate
        · generate-sources
        · process-sources
        · generate-resources
        · process-resources
        · compile
        · process-classes
        · generate-test-sources
        · process-test-sources
        · generate-test-resources
        · process-test-resources
        · test-compile
        · process-test-classes
        · test
        · prepapre-package
        · package
        · pre-integration-test
        · integration-test
        · post-integration-test
        · verify
        · install
        · deploy

    13.5 Site生命周期 - mvn site
        · pre-site
        · site
        · post-site
        · site-deploy

    13.6 特点

        Maven核心程序为了更好地实现自动化构建，有以下特点：
        
          不论执行生命周期的哪一个阶段，都是从这个生命周期最初的阶段开始执行到指定阶段

    13.7 插件和目标

        ·生命周期的各个阶段仅仅定义了要执行的任务是什么
        ·各个阶段和插件的目标是对应的
        ·相似的目标有特定的插件来完成

| 生命周期阶段   | 插件目标     | 插件                  |
|--------------|-------------|-----------------------|
| compile      | compile     | mave-compiler-plugin  |
| test-compile | testCompile | maven-compiler-pulgin |

        ·可以将目标看做调用插件的“命令”

## 第十四节 在Eclipse中使用Maven插件

    14.1 Eclipse通常已经内置了插件

    14.2 基本操作
        ·创建Maven的Java工程
        ·创建Maven的JavaWeb工程
        ·执行Maven命令

## 第十五节 第三个Maven工程

    15.1 设置通过Maven创建的工程的JDK版本

        > settings.xml

          <profiles>
            <profile>
              <id>jdk-1.8</id>
              <activation>
                <activeByDefault>true</activeByDefault>
                <jdk>1.8</jdk>
              </activation>
              <properties>
                <maven.compiler.source>1.8</maven.compiler.source>
                <maven.compiler.target>1.8</maven.compiler.target>
                <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
              </properties>
            </profile>
          </profiles>

    15.2 在Eclipse中创建Maven Project
        ※勾选create a single project生成经典目录结构

        - packing处下拉选择jar则为Java Project

        - packing处下拉选择war则目标为JavaWeb Project

           ·対生成的工程右键properties
           ·Project Facets
           ·Dynamic Web Module取消勾选，Apply
           ·Dynamic Web Module勾选，打开提示的Further configuration available
           ·Content directory
                WebContent -> src/main/webapp
           ·勾选Generate web.xml deployment descriptor
           ·OK => Apply

## 第十六节 继承

    16.1 为什么需要继承

      ·情景
          各工程有以下test范围的依赖：

            Hello => junit_v4.0
            HelloFriend => junit_v4.0
            MakeFriends => junit_v4.9
        
          现在想要统一管理各个模块工程中对junit依赖的版本，怎么办？

      >> 方案：

          将junit依赖版本统一提取到“父”工程中，在子工程中声明依赖时不指定版本
          就会以父工程中的版本为准，同时也便于修改

    16.2 步骤

      ·创建一个Maven工程，打包方式为pom

      ·在子工程中，声明对父工程的引用
          <parent>
            <groupId>pt.maven</groupId>
            <artifactId>Parent</artifactId>
            <version>0.0.1-SNAPSHOT</version>
            <relativePath>../Parent</relativePath>
          </parent>

      ·将子工程的坐标与父工程坐标中重复的内容删除

      ·在父工程中声明junit的依赖
          <dependencyManagement>
            <dependencies>
              <dependency>
                ...
              </dependency>
            </dependencies>
          </dependencyManagement>

      ·在子工程中删除junit依赖的版本信息
        ※但是依然可以强制指定自己的依赖的版本号

    16.3 注意

        配置父工程之后要先安装父工程才可以构建子工程

## 第十七节 聚合

    17.1 作用

        一次性安装多个模块工程

    17.2 配置方式

        在一个“总聚合工程”中，配置各个参与聚合的模块

        <modules>
          <!-- 指定各个子工程的相对路径 -->
          <module>../Hello</module>
          <module>../HelloFriend</module>
        </modules>

        ※可以是父工程，也可以另做聚合工程
        ※Maven会自动调整子工程之间的依赖关系

## 第十八节 自动部署

    利用build标签配置当前构建过程中的特殊设置

    <build>
      <finalName>JojaMarket</finalName>

      <!-- 构建过程中需要的插件 -->
      <plugins>
        <plugin>

          <!-- cargo是一家专门从事“启动Servlet容器”的组织 -->
          <groupId>org.codehaus.cargo</groupId>
          <artifactId>cargo-maven2-plugin</artifactId>
          <version>1.2.3</version>

          <!-- 针对插件进行的配置 -->
          <configuration>
            <!-- 容器的位置 -->
            <container>
              <containerId>tomcat8x</containerId>
              <home>C:\workspace\apache-tomcat-8.5.57</home>
            </container>
            <configuration>
              <type>existing</type>
              <home>C:\workspace\apache-tomcat-8.5.57</home>
              <properties>
                <cargo.servlet.port>8989</cargo.servlet.port>
              </properties>
            </configuration>
          </configuration>

          <!-- 配置插件在什么情况下执行 -->
          <executions>
            <execution>
              <id>cargo-run</id>
              <!-- 生命周期的阶段 -->
              <phase>install</phase>
              <!-- 插件的目标 -->
              <goals>
                <goal>run</goal>
              </goals>
            </execution>
          </executions>
        </plugin>
      </plugins>
    </build>

    命令行里mvn install执行之后就可以自动部署到Server上了

## 第十九节 Maven酷站

    可以在<http://mvnrepository.com/>上查找各种依赖的坐标信息
