# Maven

## 第一节 为什么使用Maven

### 1. 目前掌握的技术

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

### 2. 目前的技术在开发中的问题

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

### 1. Maven是一款服务于Java平台的自动化构建工具

    > Java平台 ※Maven本身也是用Java写的

        发展过程：
            Make → Ant → Maven → Gradle

        读音：
            梅文、麦文

        ※ Maven来源于美国俚语，意为内行、专家

### 2. 构建

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

### 3. 构建过程中的各个环节

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

### 4. 自动化构建

## 第三节 安装Maven核心程序

    1. 检查JAVA_HOME环境变量

    2. 解压Maven核心程序的压缩包，放在一个非中文无空格目录下

    3. 配置Maven的环境变量

        > MAVEN_HOME或M2_HOME

          - 值是bin目录的上一级

        > path

          - bin目录

    4. 验证

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

## 第十一二节 依赖

    11.1 Maven解析依赖信息时会到本地仓库中查找被依赖的jar包

    11.2 对于自己开发的工程，使用mvn install安装，存入本地仓库