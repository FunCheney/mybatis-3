## MyBatis 源码阅读
### 1.环境搭建
#### 1.1 准备条件
    IDEA
    gradle
      1.从gitHub克隆代码 https://github.com/mybatis/mybatis-3.git
      2.到clone下来的代码对应的pom.xml文件所在的地方，执行 gradle init --type pom 命令，先保证本机安装了gradle 2.0以上的版本
      3.删除原先的pom.xml文件
      4.在build.gradle 中加入 compile group: 'mysql', name: 'mysql-connector-java', version:'5.1.32'
    测试用例编写：
      1.在test目录下创建 package -> cn.fchen
      2.创建sql文件夹用来保存sql语句 sql -> UserTestSql.md 文件。
      3.编写数据库表‘user_test’ 对应的实体类 user
      4.编写UserMapper.xml 文件
      5.创建 resources 目录 
          在此目录下创建：mybatis-config-local.xml ->mybatis 配置文件
                       ：mybatis/UserMapper.xml 文件
      6.编写测试用例：myTest.java 测试结果;       
#### 1.2 Jdbc 与 Mybatis
    jdbc 连接数据库的步骤(JdbcTest.java):
      jdbc的4个参数：
        1.user用户名
        2.password密码
        3.URL定义了连接数据库时的协议、子协议、数据源标识。
        4.driverClass连接数据库所需的驱动
      连接步骤：
        1.加载驱动程序
        2.getConnection()方法获取连接
        3.创建statement类对象
        4.执行sql语句获取结果集
        5.释放资源
    mybatis 操作数据库的步骤(myTest.java)：
      1.加载核心配置文件（mybatis-config-local.xml）
      2.获取sqlSessionFactory对象  
      3.获取SqlSession对象
      4.获取mapper接口
      5.通过mapper执行sql语句并返回结果
      6.释放资源
#### 1.3 Mybatis 的基本构成
    1. SqlSessionFactoryBuilder(构造器)：他会根据配置信息或者代码生成SqlSessionFactory(工厂接口)
    2. SqlSessionFactory：依靠工厂来生成SqlSession(会话)
    3. SqlSession：是一个既可以发送sql去执行并返回结果，也可以获取Mapper的接口
    4. SQL Mapper：由Java接口或XMl文件构成，需要给出对应的SQL和映射规则。他负责发送SQL去执行并返回结果
   <div align="center">
    <img src="https://github.com/FunCheney/mybatis/blob/master/images/mybatis_01.png">
   </ div>
   
#### 1.4  SqlSessionFactoryBuilder对象
   ##### 1.4.1 XMLConfigBuilder 对象
                                      
                                        
