他的微博：http://www.havestyle.cn/post/60（看一看）
资料：http://wenku.baidu.com/link?url=p29-0f5_NwLzdCYuVjbqFbx7yuVQkY9RTrcxesDPah0qL5Yr7KQtFCL1y-XBeL82qcroR262ngFZIOTRlaTtJxFTDzAtn9BeaU0f2Q35hoW
###依赖注入，控制反转
* 依赖注入：由外部容器动态的将依赖对象注入组件中
* 控制反转：应用本身不负责依赖对象的创建及维护，将控制权移到外部容器，控制权的转移
*
###spring 的主要特性
* 降低耦合度，解耦


###配置
公共：
 
* spring.jar（见-springMVC)*http://www.cnblogs.com/BensonHe/p/3903050.html
* commons-logging.jar(日志)*


切面编程

* aspectjweaver.jar
* aspectjrt.jar
* cglib-nodep-2-1-3.jar //CGLIB 

jsr-250中的注解

* common-annotations.jar


###定义bean的方法(3种（bean静态工厂，bean的实例工厂）)：

* ``` <bean id="userDaoImpl" class="dao.impl.UserDaoImpl"></bean>```
  * ApplicationContext:   ApplicationContext context=new ClassPathXmlApplicationContext("bean.xml");//实例化对象，创建对象（直接加载，进行实例化 ，一般使用此方法（scope：singleton或默认，耗内存） 
       * ClassPathXmlApplicationContext:从类路径中加载
       * FileSystemXmlApplicationContext:从文件系统中加载
       * XmlWebApplicationContext:从web系统中加载
  * beanFactory:BeanFactory factory=new XmlBeanFactory(new ClassPathResource("bean.xml"))//把 bean 的信息载入，用的时候在实例化，节约内存 ，速度慢

###bean的作用域(http://blog.csdn.net/feihong247/article/details/7798474)
     
        eg:测试类
        ApplicationContext ctx = new ClassPathXmlApplicationContext("beans.xml");  
        PersonService personService1 = (PersonService)ctx.getBean("personService");  
        PersonService personService2 = (PersonService)ctx.getBean("personService");  
        System.out.println(personService1==personService2);  
* singleton  在一个bean对应一个对象实例(单例)

        1.<bean id="userDaoImpl" class="dao.impl.UserDaoImpl"></bean>
        2.<bean id="userDaoImpl" class="dao.impl.UserDaoImpl" scope="singleton"></bean>(spring-bean2.0以上)
        3.<bean id="userDaoImpl" class="dao.impl.UserDaoImpl" singleton="true"></bean>
    
        返回：true（说明一个对象实例）
* prototype   一个bean定义对应多个对象实例   

        1.<bean id="userDaoImpl" class="dao.impl.UserDaoImpl" scope="prototype"></bean>
        2.<bean id="userDaoImpl" class="dao.impl.UserDaoImpl" singleton="false"></bean>
        返回：false
* request      一次请求有效（java web）
* session      session级有效（java web）
* global-session   在web 中spring 容器ApplicationContext


### bean的生命周期
#####ApplicationContext
* 1.实例化（当程序加载bean.xml文件），把bean（scope =singleton）实例化到内存中
* 2.调用set方法调用属性
* 3.如果实现 BeanNameAware 接口(setBeanName) ，可以获得bean的id
* 4.如果实现 BeanFactoryAware接口（setBeanFactory）,则可以获取bean
* 5.如果实现 ApplicationContextAware (setApplicationContext)，获取上下文
* 6.如果bean 和 后置处理器（BeanPostProcssor） 关联，则调用 before
* 7. 如果调用InitialzingBean接口 ，AfterPropertiesSet 方法
* 8 如果调用定制的初始化方法 ，init方法 ：<bean init-method="init" 或注解方法：@PostConstruct 
* 9.后置处理器 BeanPostProcssor 的 after 方法
* 10. 使用bean
* 11. 定制销毁方法 <bean destory-meth0d="mydestory" /> 或 注解方法：@PreDestory

       

#####BeanFactory
* 1.实例化
* 2.设置属性值
* 3.调用BeanNameAware的setBeanName()方法
* 4.调用InitializingBean的afterPropertiesSet方法
* 5.调用定制的初始化方法
* 6.使用bean
* 7.DisposableBean 的destory()或定制销毁方法

### 属性注入
         
    <bean id=" " class=" " >
       <property name=""  value=""  />
       //给数组 赋值
       <property name="" >
         <list>
            <value>xx</value>
            <value>xx</value>
          </list>
        </property>
        //给list 赋值 有序  可存放相同对象
        <property name=" List" >
          <list>
             <ref bean="a" />
             <ref bean="b" />
          </list>
        </property>
         //给Set 赋值 无序  存放不同对象
        <property>
            <set>
              <ref bean="a"/>
              <ref bean="b"/>
         </property>
        //给Map 赋值 键-值
          <map>
            <entry key="1" vlaue="a" />
            <entry key="2" vlaue="b" />
           
     </bean>
 
     <bean id="a" class="  ">
      <property name="a" />
     </bean>

     <bean id="b" class=" " >
       <property name="b" />
     </bean>
 
### 自动装配bean 的属性值(尽量不用)
* no ：不自动装配 什么都不写，autowire的默认值
* byName:通过名字自动配置 id=""

       <bean id=" " class="" autowire="byName >
       </bean>
* byType:通过数据类型 名字可以不同，类型多个匹配报错

        <bean id=" " class="" autowire="byType >
       </bean>
* constructor:匹配constructor

       <bean id=" " class="" autowire="constructor >
       </bean>
* autodetct：byType,constructor 自动匹配 二选一（constructor优先级更高）

        <bean id=" " class="" autowire="autodetct" >
       </bean>
* default:beans中设置default-autowire="",bean中autowire="default" 指的就是beans中的
* 
          <beans xxxxxxxxxxxxxxxxx
 
          default-autowire="byName/byType/constructor/>

        <bean id=" " class="" autowire="default" >
       </bean>

###注解
<context:annotation-config />:开启自动注解、


###spring提供的特殊的bean
* xx.properties :key=values
   
        写法一： <bean class=" PropertyPlaceHolderVonfigurer">
        <property name="locations">
        <list>
        <value>xx.properties</value>
        <value>xx.properties</value>
        </list>
        </property>
        </bean>

        写法二：引用一个或多个properties文件
           <context:property-placeholder location="   .../xx1.properties, .../xx2.properties"/>



###正则表达式  -------------------不懂
* .  --------    用来匹配任何一个字符“g.f”-“gaf”、“g*f”等
* [] --------    只有[]里的指定字符才能匹配 , g[abc]f---gaf,gbf,gcf
* * ---------     表示匹配次数，*左边的符号的出现次数，可以任意次数  ，g.*f--gaf,gaaf
* ? ---------    匹配0或1次，？左边的符号出现的次数
* \ ---------     连接符 


## AOP
* PointCut：注入代码的位置
    * 静态切入点
    * 动态切入点
* advice:注入的代码
* advisor:配置器

#### Interception Around  ：继承MethodInterceptor

          /**
         * Interception around 通知 在JoinPoint前后执行
         * Created by user on 2016/9/13.
         */
        public class LogAround implements MethodInterceptor {
        private Logger logger=Logger.getLogger(this.getClass().getName());

        /**
        * getArguments()；获取参数
        * @param methodInvocation 可以获取方法的名称
        *                         procceed():执行被调用的方法
        * @return 返回被调用的方法的返回值
        * @throws Throwable
        */
        @Override
         public Object invoke(MethodInvocation methodInvocation) throws Throwable {
        logger.log(Level.INFO,methodInvocation.getArguments()[0]+"开始审查元素。。。");
        try {
            Object result=methodInvocation.proceed();//返回值即是被调用的方法的返回值
            return  result;
        }finally {
            logger.log(Level.INFO,methodInvocation.getArguments()[0]+"审查结束。。。。");
        }


        }


        beans.xml文件中；
         <bean id="finance" class="dao.FinanceImplements"/>
        <bean id="logAroundProxy1" class="org.springframework.aop.framework.ProxyFactoryBean">
        <!--接口-->
        <property name="proxyInterfaces">
            <value>dao.impl.FinanceInterface</value>
        </property>
        <!--advice-->
        <property name="target">
            <ref bean="finance" />
        </property>
        <!--advisor-->
        <property name="interceptorNames">
            <value>logAround</value>
        </property>
    </bean>
####before 通知 ：JoinPoint 前执行 继承MethodBeforeAdvice

    /**
     * Before 通知 只在JoinPoint 前执行
     * Created by user on 2016/9/13.
    */
    public class LogBefore implements MethodBeforeAdvice{
    private Logger logger=Logger.getLogger(this.getClass().getName());
    @Override
    public void before(Method method, Object[] objects, Object o) throws Throwable {
        logger.log(Level.INFO,objects[0]+"开始审核。。。。。");

    }
    }

####After Returning通知 继承AfterReturningAdvice

    /**
    * After Returning通知只在JoinPoint的后面执行
    * Created by user on 2016/9/14.
    */
    public class LogAfter implements AfterReturningAdvice{
    private Logger logger=Logger.getLogger(this.getClass().getName());
    @Override
    public void afterReturning(Object o, Method method, Object[] objects, Object o1) throws Throwable {
        logger.log(Level.INFO,objects[0]+"审核数据完成。。。。");

    }
####Throw通知 在JoinPoint 抛出异常时执行 继承ThrowsAdvice


###CGLIB     代理的是没有接口的target
 * 引入jar:cglib-nodep.jar
      
        <dependency>
          <groupId>cglib</groupId>
          <artifactId>cglib-nodep</artifactId>
          <version>3.1</version>
        </dependency>

* 代理的是没有接口的target

         <bean id="logAroundProxy" class="org.springframework.aop.framework.ProxyFactoryBean">
         <propert name="proxyTargetClass">
            <value>true</value>
        </property>//增加
        <!--接口-->
        <property name="proxyInterfaces">
            <value>dao.impl.TimeBookInterface</value>
        </property>
        <!--advise-->
        <property name="target">
            <ref bean="timeBook"/>
        </property>
        <!--advisor-->
        <property name="interceptorNames">
            <list>
                <value>logAround</value>
            </list>
        </property>
    </bean>
      

### 自动代理 DefaultAdvisorAutoProxyCreator（无需在手动写代理ProxyFactoryBean） 无需知道target目标类

    <!--自动代理-->
    <bean id="autoProxyCreator" class="org.springframework.aop.framework.autoproxy.DefaultAdvisorAutoProxyCreator">

    </bean>
    <!--before-->

    <bean id="logBeforeAutoAdivsor" class="org.springframework.aop.support.RegexpMethodPointcutAdvisor">
        <property name="advice">
            <ref bean="logBefore" />
        </property>
        <!--指定dao开头的fangfa -->
        <property name="patterns">
            <value>.*do.*</value>
        </property>
    </bean>
    <!--after-->

    <bean id="logAfterAutoAdvisor" class="org.springframework.aop.support.RegexpMethodPointcutAdvisor">
        <property name="advice">
            <ref bean="logAfter"/>
        </property>
        <property name="patterns">
            <value>.*do.*</value>
        </property>
    </bean>

###事务处理
######关系数据库
* Begin Transaction(启动事务处理)
* Commit 或 RollBack（提交或回滚）
* End Transaction（提交事务处理）

JDBC:
       
    private DataSource dataSource;
    public void setDataSource(DataSource dataSource){
       this.dataSource=dataSource;
    }
    Connection conn=null;
    Statement stmt=null;
    try{
       //获取数据连接
       conn=dataSource.getConnection();
       //开启事务
        conn.setAutoCommit(false);
        stmt=conn.createStatement();
        //执行相应操作
         stmt.excuteUpadat("");
         //提交
          conn.commit();             
     }catch(SQLException e){
     if(conn!-null){
        try{
         //执行不成功，回滚
           conn.rollback();
           }catch（SQLException ex）
        }finally{
           //关闭stmt
         if(stmt!=null){
            try{
             stmt.close();
              }catch(SQLException ex){}
           }
          if(conn!=null){
              try{
             conn.close();
              }

           } 
         }
         
       }


####分布式事务处理（处理多个数据库）

####编程式事务处理
DAO:

    public class HelloDao {
    private DataSource dataSource;
    private PlatformTransactionManager transactionManager;

    //通过注入依赖来完成管理，xml
    public DataSource getDataSource() {
        return dataSource;
    }

    public void setDataSource(DataSource dataSource) {
        this.dataSource = dataSource;
    }

    public PlatformTransactionManager getTransactionManager() {
        return transactionManager;
    }

    public void setTransactionManager(PlatformTransactionManager transactionManager) {
        this.transactionManager = transactionManager;
    }

    /**
     * 推荐使用create()
     * execute；执行事务
     * TransactionCallback->doInTransaction:进行各种数据库操作
     * 成功：commit
     * 失败:rollbacOnException()；事务回滚
     */
    //进行事务处理
    public int create(String msg) {
        //TransactionTemplate:已编程的方式实现事务控制，无状态且线程安全,需PlatformTransactinManager
        TransactionTemplate transactionTemplate = new TransactionTemplate(transactionManager);

        Object result = transactionTemplate.execute(
                new TransactionCallback() {
                    @Override
                    public Object doInTransaction(TransactionStatus transactionStatus) {
                        //TODO:执行新增的操作，向数据库新增一笔记录

                        return null;
                    }
                });
        return 1;

    }

    /**
     *doInTransactionWithoutResult:没有返回值
     */
    public void createNO(String msg){
        TransactionTemplate transactionTemplate=new TransactionTemplate(transactionManager);
        transactionTemplate.execute(new TransactionCallbackWithoutResult() {
            @Override
            protected void doInTransactionWithoutResult(TransactionStatus transactionStatus) {
                JdbcTemplate jdbcTemplate=new JdbcTemplate(dataSource);
                jdbcTemplate.update("");//TODO:执行数据库操作
            }
        });

    }
    /**
     * DefaultTransactionDefinition：预定义
     * @param msg
     * @return
     */
    //自己进行rollback commit
    public int createSelf(String msg) {
        DefaultTransactionDefinition def = new DefaultTransactionDefinition();
        TransactionStatus status = transactionManager.getTransaction(def);//声明事务开始
        try {
            //使用JdbcTemplate操作
            JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
            jdbcTemplate.update("");//TODO:数据库caoz
        }catch (DataAccessException ex){
            //也可以status.setRollBackOnly();
            transactionManager.rollback(status);
            throw ex;
        }finally {
            transactionManager.commit(status);
        }
        return 1;


    }
    }


xml 
       
    <!--设定DataSource-->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName">
            <!--数据库类型-->
            <value></value>
        </property>
        <!--设定URL-->
        <property name="url">
            <value></value>
        </property>
        <!--设定用户-->
        <property name="username">
            <value>lyl</value>
        </property>
        <property name="password">
            <value>11111</value>
        </property>
    </bean>
    <!--设定transactinManager-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource">
            <ref bean="dataSource"/>
        </property>
    </bean>
    <!--Dao-->

    <bean id="helloDAo" class="dao.HelloDao">
        <property name="dataSource">
            <ref bean="dataSource"/>
        </property>
        <property name="transactionManager">
            <ref bean="transactionManager"/>
        </property>
    </bean>



####声明式事务处理

jar:

* aopalliance.jar 
* cglib-nodep.jar

Dao:

        /**
        * 声明式事务
         * Created by user on 2016/9/20.
        */
         public class HelloDaoMajor {
         private DataSource dataSource;
         private JdbcTemplate jdbcTemplate;
          //通过依赖注入
         public void setDataSource(DataSource dataSource) {
        this.dataSource = dataSource;
        jdbcTemplate=new JdbcTemplate( dataSource);
         }

        //在xml中配置事务处理
          public void create(String msg){
           jdbcTemplate.update("");
          }


xml:

     <!--设定DataSource-->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName">
            <!--数据库类型-->
            <value></value>
        </property>
        <!--设定URL-->
        <property name="url">
            <value></value>
        </property>
        <!--设定用户-->
        <property name="username">
            <value>lyl</value>
        </property>
        <property name="password">
            <value>11111</value>
        </property>
    </bean>
    <!--设定transactinManager-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource">
            <ref bean="dataSource"/>
        </property>
    </bean>
    <!--Dao-->
    <bean id="helloDaoMajor" class="dao.HelloDaoMajor"/>
     <!--声明式事务处理-->
    <!--方法1：-->
    <bean id="helloDaoMajorProxy" class="org.springframework.transaction.interceptor.TransactionProxyFactoryBean">
        <property name="transactionManager">
            <ref bean="transactionManager"/>
        </property>
        <property name="target">
            <ref bean="helloDaoMajor"/>
        </property>
        <!--对create()方法进行事务管理，新建事务管理-->
        <property name="transactionAttributes">
            <props>
                <prop key="create*">PROPAGATION_REQUITED</prop>
            </props>
        </property>
    </bean>

    <!--方法2：-->
    <bean id="transactionInterceptor" class="org.springframework.transaction.interceptor.TransactionInterceptor">
        <property name="transactionManager">
            <ref bean="transactionManager"/>
        </property>
        <!--新建事务-->
        <property name="transactionAttributes">
            <value>
                dao.HelloDaoMajor.create*=PROPAGATION_REQUITED
            </value>
        </property>
    </bean>
    <bean id="helloDaoMajorProxyA" class="org.springframework.aop.framework.ProxyFactoryBean">
        <property name="interceptorNames">
            <value>transactionInterceptor,helloDaoMajor</value>
        </property>
    </bean>


    </beans>

####xml 实现DataSource 注入
* Spring 自带的DriverManagerDataSource

        <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName">
            <!--数据库类型-->
            <value></value>
        </property>
        <!--设定URL-->
        <property name="url">
            <value></value>
        </property>
        <!--设定用户-->
        <property name="username">
            <value>lyl</value>
        </property>
        <property name="password">
            <value>11111</value>
        </property>
    </bean>

 
* DBCP连接池

 jar: jakarta-commons 中的commons-collections.jar,commons-dbcp.jar,commons-pool.jar
   
     <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
      <version>3.1</version>
    </dependency>
    <dependency>
      <groupId>commons-dbcp</groupId>
      <artifactId>commons-dbcp</artifactId>
      <version>1.4</version>
    </dependency>
    <dependency>
      <groupId>commons-pool</groupId>
      <artifactId>commons-pool</artifactId>
      <version>1.6</version>
    </dependency>

* Tomcat JNDI

要在Tomat 的server.xml中添加配置 

###JdbcTemplate 事务处理

Dao:

    public class HelloDAOJdbcTemplate {
    private JdbcTemplate jdbcTemplate;
    private PlatformTransactionManager transactionManager;
    private String sql;

    public void setTransactionManager(PlatformTransactionManager transactionManager) {
        this.transactionManager = transactionManager;
    }

    public void setJdbcTemplate(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    public void setSql(String sql) {
        this.sql = sql;
    }

    //使用JDBCTemplate
    public int create(String msg) {
        DefaultTransactionDefinition df = new DefaultTransactionDefinition();
        TransactionStatus status = transactionManager.getTransaction(df);//事务开始
        int result = 0;
        try {
            result = jdbcTemplate.update("");//TODO:数据库操作
            jdbcTemplate.update(this.sql);//在xml 中写具体数据库操作
        } catch (Exception ex) {
            transactionManager.rollback(status);
        } finally {
            transactionManager.commit(status);
            return result;
        }


    }
    }
xml:

     <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName">
            <!--数据库类型-->
            <value></value>
        </property>
        <!--设定URL-->
        <property name="url">
            <value></value>
        </property>
        <!--设定用户-->
        <property name="username">
            <value>lyl</value>
        </property>
        <property name="password">
            <value>11111</value>
        </property>
    </bean>

     <!--设定transactinManager-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource">
            <ref bean="dataSource"/>
        </property>
    </bean>


    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource">
            <ref bean="dataSource"/>
        </property>
    </bean>
    <bean id="helloDAOJdbc" class="dao.HelloDAOJdbcTemplate">
        <property name="jdbcTemplate">
            <ref bean="jdbcTemplate"/>
        </property>
        <property name="transactionManager">
            <ref bean="transactionManager"/>
        </property>
        <property name="sql">
            <value></value>
        </property>

    </bean>


##Spring Web 

  spring-servlet.xml配置

        <?xml version="1.0" encoding="UTF-8"?>
       <beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd">

       <!--设置映射-->
       <bean id="urlMapping" class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
           <property name="mappings">
                 <props>
                        <prop key="helloWord">helloWordController</prop>
                        <prop key="FormController">formController</prop>
                        <prop key="formMultiController">formMuliController</prop>
                 </props>
           </property>
              
       </bean>
       <!--定义视图-->
       <bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
              <!--Jsp/Servlet视图-->
              <property name="viewClass">
                     <value>org.springframework.web.servlet.view.JstlView</value>
              </property>
              <!--jsp存放的目录-->
              <property name="prefix">
                     <value>/WEB-INF/jsp/</value>
              </property>
              <!--jsp文件后缀-->
              <property name="suffix">
                     <value>.jsp</value>
              </property>
       </bean>

          <!--异常的页面处理 出错进入界面outexception-->
       <bean id="exceptionResolver" class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
              <property name="exceptionMappings">
                     <props>
                            <prop key="java.lang.Exception">outException</prop>
                            <prop key="java.lang.Throwable">outException</prop>

                     </props>
              </property>

       </bean>
       <!--定义Controller-->
       <bean id="helloWordController" class="controller.HelloWorldController">
              <property name="helloWorld">
                     <value>HelloWorld</value>
              </property>
              <property name="viewPage">
                     <value>index</value>
              </property>
       </bean>
       <bean id="formController" class="controller.FormController">
              <property name="commandClass">
                     <value>vo.HelloWorld</value>
              </property>
              <property name="viewPage">
                     <value>formShow</value>
              </property>
       </bean>
       <bean id="formMuliController" class="controller.FormMutiController">
              <property name="methodNameResolver">
                     <ref bean="pareMethodResolver"/>
              </property>
              <property name="viewPage">
                     <value>formShow</value>
              </property>
       </bean>
       <bean id="pareMethodResolver" class="org.springframework.web.servlet.mvc.multiaction.ParameterMethodNameResolver">
              <property name="paramName">
                     <value>method</value>
              </property>

       </bean>

     </beans>




####SimpleFormController(过时) 表单操作
#### MultiActionController 多个操作

    /**
     * 多种控制
     * Created by user on 2016/9/23.
     */
    public class FormMutiController extends MultiActionController {
    private Logger logger=Logger.getLogger(this.getClass().getName());
    private String viewPage;

    public String getViewPage() {
        return viewPage;
    }

    public void setViewPage(String viewPage) {
        this.viewPage = viewPage;
    }

    public ModelAndView insert(HttpServletRequest request,HttpServletResponse response){

        String helloWord=request.getParameter("msg");
        Map model=new HashMap();
        model.put("helloWord","insert"+helloWord);
        return new ModelAndView(getViewPage(),model);
    }
    public ModelAndView update(HttpServletRequest request,HttpServletResponse response){
        String helloWord=request.getParameter("msg");
        Map model=new HashMap();
        model.put("helloWord","update"+helloWord);
        return new ModelAndView(getViewPage(),model);
    }
    public ModelAndView delete(HttpServletRequest request,HttpServletResponse response){
        String helloWord=request.getParameter("msg");
        Map model=new HashMap();
        model.put("helloWord","update"+helloWord);
        return new ModelAndView(getViewPage(),model);
    }
    }

Jsp

     <form name="form" action="formMultiController" method="post">
     欢迎<input type="text" name="msg" value=""/><br />
     <input type="submit" name="method" value="insert"/><br>
     <input type="submit" name="method" value="update"/><br>
     <input type="submit" name="method" value="delete"/><br>

     </form>

xml

     <bean id="formMuliController" class="controller.FormMutiController">
              <property name="methodNameResolver">
                     <ref bean="pareMethodResolver"/>
              </property>
              <property name="viewPage">
                     <value>formShow</value>
              </property>
       </bean>
       <bean id="pareMethodResolver" class="org.springframework.web.servlet.mvc.multiaction.ParameterMethodNameResolver">
              <property name="paramName">
                     <value>method</value>
              </property>

       </bean>








####处理异常的页面

    <!--异常的页面处理-->
     <bean id="exceptionResolver" class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
              <property name="exceptionMappings">
                     <props>
                            <prop key="java.lang.Exception">outException</prop>
                            <prop key="java.lang.Throwable">outException</prop>

                     </props>
              </property>

       </bean>



#### 数据绑定
* 自定义标签


* Validator


####本地化支持


####日志
* log4j（http://blog.csdn.net/azheng270/article/details/2173430/）

log4j格式

    #配置根Logger
    log4j.rootLogger  =   [ level ]   ,  appenderName1 ,  appenderName2 ,  …
    #配置日志信息输出目的地Appender
    log4j.appender.appenderName =fully.qualified.name.of.appender.class ....
    配置日志信息的格式（布局）
    log4j.appender.appenderName.layout  =  fully.qualified.name.of.layout.class
    log4j.appender.appenderName.layout.option1  =  value1  
　　 

详解            

            log4j中有五级logger 输出级别:  
               FATAL 0   
               ERROR 3   
               WARN 4   
               INFO 6   
               DEBUG 7 
           ----------------------------------
 
           log4j配置相关说明
            %p 输出优先级，即DEBUG，INFO，WARN，ERROR，FATAL   
            %r 输出自应用启动到输出该log信息耗费的毫秒数 
            %c 输出所属的类目，通常就是所在类的全名   
            %t 输出产生该日志事件的线程名  
            %m 输出代码中指定的信息  
            %n 输出一个回车换行符，Windows平台为“\r\n”，Unix平台为“\n”        
            %d 输出日志时间点的日期或时间，默认格式为ISO8601，也可以在其后指定格式，比如：%d{yyyy MM dd HH:mm:ss,SSS}，输出类似： 2002年10月18日 22：10：28，921   
            %l 输出日志事件的发生位置，包括类目名、发生的线程，以及在代码中的行数。举例：Testlog4.main(TestLog4.java:10) 
             --------------------------------------------
             log4j提供4种布局:   
              org.apache.log4j.HTMLLayout（以HTML表格形式布局）  
              org.apache.log4j.PatternLayout（可以灵活地指定 布局模式），  
              org.apache.log4j.SimpleLayout（包含日志信息的级别和信息字符串）
              org.apache.log4j.TTCCLayout（包含日志产生的时间、线程、类别等等信息 
              --------------------------
             Appender 为日志输出目的地，Log4j提供的appender有以下几种：
             org.apache.log4j.ConsoleAppender（控制台），
             org.apache.log4j.FileAppender（文件），
             org.apache.log4j.DailyRollingFileAppender（每天产生一个日志文件），
             org.apache.log4j.RollingFileAppender（文件大小到达指定尺寸的时候产生一个新的文件），
             org.apache.log4j.WriterAppender（将日志信息以流格式发送到任意指定的地方
    
具体：
log4j.properties

      log4j.rootLogger=DEBUG,console,FILE    
    
     log4j.appender.console=org.apache.log4j.ConsoleAppender    
     log4j.appender.console.threshold=INFO    
     log4j.appender.console.layout=org.apache.log4j.PatternLayout    
     log4j.appender.console.layout.ConversionPattern=%d{yyyy-MM-dd HH\:mm\:ss} [%5p] - %c -%F(%L) -%m%n    
    
    log4j.appender.FILE=org.apache.log4j.RollingFileAppender    
    log4j.appender.FILE.Append=true    
    log4j.appender.FILE.File=E\:/logs/log4jtest.log    
    log4j.appender.FILE.Threshold=INFO    
    log4j.appender.FILE.layout=org.apache.log4j.PatternLayout    
    log4j.appender.FILE.layout.ConversionPattern=%d{yyyy-MM-dd HH\:mm\:ss} [%5p] - %c -%F(%L) -%m%n    
    log4j.appender.FILE.MaxFileSize=10MB  

web.xml

       <!--配置log4j-->
    <context-param>
        <param-name>webAppRootKey</param-name>
        <param-value>SpringMVCExercise.root</param-value>
    </context-param>
    <context-param>
        <param-name>log4jConfigLocation</param-name>
        <param-value>/WEB-INF/log4j.properties</param-value>
    </context-param>
    <context-param>
      <param-name>log4jRefreshInterval</param-name>
      <param-value>60000</param-value>
    </context-param>

    <listener>
        <listener-class>org.springframework.web.util.Log4jConfigListener</listener-class>
    </listener>

* logback