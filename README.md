# Maven

## 第一章 为什么使用Maven

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
    ·jar包需要别人帮忙准备好，或到官网下载
    ·一个jar包依赖的其他jar包需要自己手动加入到项目中