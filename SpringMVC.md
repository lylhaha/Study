##SpringMVC　
SSM搭建：http://www.myexception.cn/vc-mfc/1960735.html

## SpringMVC 原理：
* 启动服务器，根据web.xml的配置加载DispatcherServlet,进行初始化
* 在根据servlet隐射请求，（*.do或/），并参考spring-servlet.xml文件，将具体的请求发给指定的controller
* 根据controller中的视图对象（ModelandView）给前端处理器，返回页面
##### 配置文件：
* dom.xml 要导入的包
* spring
 <font color="red">必有的
    * commons-logging-1.1.1.jar（日志包 ，必要的）
    * org.springframework.aop-3.1.1.Release.jar（AOP编程相关包）
    * org.springframework.beans-3.1.1.Release.jar（简捷操作bean的包）
    * org.springframework.spring-context-3.1.1.Release.jar（在bean包的基础上，用于处理资源文件及国际化）
    * org.springframework.spring-core-3.1.1.Release.jar（spring 核心包）
    * org.springframework.spring-context-support-3.1.1.Release.jar(对 spring-context感知，补充了它，更完善，有的地方用不着)
    * org.springframework.spring-web-3.1.1.Release.jar（web核心包，提供web层接口）
    * org.springframework.spring-webmvc-3.1.1.Release.jar（同web.servlet,web层一二个具体的实现包，DispatcherServlet位于次包中）
    * org.springframework.servlet-api-3.0-alpha-1.jar(servlet相关的包，HttpServletResponse等)
    * org.springframework.spring-asm-3.0-alpha-1.jar（asm字节码库）
    * org.springframework.spring-expression-3.1.1.Release.jar(spring的各种表达式语言)

    </font>
      *  org.freemarker:freemarker:2.3.23 (用freemarker)
      * org.apache.poi(excel相关的操作)
   

* web.xml：

* generatorContig.xml:<br />
连接数据库（jdbc,数据库名，账号，密码）读取mysql数据，设置文件位置，自动生成mapper,pojo,mapper.xml（注意：不需要写数据库语言）
* applecationContext-dao.xml(spring-mybatis.xml)：<br />
 数据库的一些列操作；将springmvc与mybatis结合，（设置db.properties存储数据库信息）1、设置数据源（dataSource）2.spring,mybatis相结合（sqlsessionFactory）3.s扫描mapper接口，并注入sqlsession 4。数据库事务处理(transactionManager)

* springmvc.xml: <br />
   自动扫描，试图渲染

###访问静态资源（js/css/jpg）http://blog.163.com/koko_qiang/blog/static/207213184201382091154584/
##### 注：<font color="blue"D>ispatcherServlet拦截"*.do "，则访问的到静态资源,如果是"/"，则拦截了所有对的请求，对静态资源拦截,静态文件要放在webroot下，不要放在web-inf下，放在web-inf下无权访问</font>
 3中方法：
 
* 方法一：web.xml中：default/servlet来处理,写在DispatcherServlet的前面，defaultServlet先拦截

         <servlet-mapping>
         <servlet-name>default</servlet-name>
         <url-pattern>*.jpg</url-pattern>
         </servlet-mapping>
         <servlet-mapping>
         <servlet-name>default</servlet-name>
         <url-pattern>*.js</url-pattern>
         </servlet-mapping>
         <servlet-mapping>
         <servlet-name>default</servlet-name>
         <url-pattern>*.css</url-pattern>
         </servlet-mapping> 

* 方法二：spring3.0.4后提供：一定要先配置  <mvc:annotation-driven />

         <mvc:resources mapping="/js/**" location="/js/"/>
* 方法三：<mvc:default-servlet-handler/>

         <mvc:default-servlet-handler/>



具体搭建方法：
Intellij IDEA创建Maven Web项目<br />
http://developer.51cto.com/art/201405/439918_all.htm<br />
    
     @Controller
     负责注册一个bean 到spring 上下文中
     @RequestMapping

     注解为控制器指定可以处理哪些 URL 请求

    　@RequestBody

      该注解用于读取Request请求的body部分数据，使用系统默认配置的HttpMessageConverter进行解析，然后把相应的数据绑定到要返回的对象上 ,再把HttpMessageConverter返回的对象数据绑定到 controller中方法的参数上  

      @ResponseBody

      该注解用于将Controller的方法返回的对象，通过适当的HttpMessageConverter转换为指定格式后，写入到Response对象的body数据区         
      @ModelAttribute 

       在方法定义上使用 @ModelAttribute 注解：Spring MVC 在调用目标处理方法前，会先逐个调用在方法级上标注了@ModelAttribute 的方法

      在方法的入参前使用 @ModelAttribute 注解：可以从隐含对象中获取隐含的模型数据中获取对象，再将请求参数 –绑定到对象中，再传入入参将方法入参对象添加到模型中 

      @RequestParam
      在处理方法入参处使用 @RequestParam 可以把请求参 数传递给请求方法

       @PathVariable

       绑定 URL 占位符到入参

     　@ExceptionHandler

      注解到方法上，出现异常时会执行该方法

     @ControllerAdvice

    　使一个Contoller成为全局的异常处理类，类中用@ExceptionHandler方法注解的方法可以处理所有Controller发生的异常

      http://www.admin10000.com/document/6436.html
### spring 接受数据（获取网页数据）
* form(表单)

          web:

          <form action="<%=request.getContextPath()%>/save.do" method="post">
         用户名：<input type="text" name="username" ><br />
          密码：<input type="password" name="password"> <br />
          <input type="submit" value="保存用户">
          </form>

         controller:
         * @RequestParam（也可以非表单）
         public String add( @RequestParam("username")String username,@RequestParam("password")String password)
         * 参数形同（同struct2）
         public String add( String username,String password)

* 使用HttpServletRequest获取

        @RequestMapping("/login.do")  
        public String login(HttpServletRequest request){  
        String name = request.getParameter("name")  
        String pass = request.getParameter("pass")  
        }  
* 自动注入bean

        <form action="login.do">  
        用户名：<input name="name"/>  
        密码：<input name="pass"/>  
        <input type="submit" value="登陆">  
        </form>  
  
        //封装的User类  
        public class User{  
        private String name;  
        private String pass;  
        }

        
          @RequestMapping("/login.do")  
         public String login(User user)  
         {  
         syso(user.getName());  
         syso(user.getPass());  
         }  
      
### 向页面传值
* 使用ModelAndView对象

        public ModelAndView age( int age){
        ModelAndView modelAndView=new ModelAndView("name");
        modelAndView.addObject("age",age);
        return  modelAndView;
* 使用ModelMap,Model对象(  model.addAttribute("user",user);  )

         
        @RequestMapping("/login.do")  
        public　String login(String name,String pass ,ModelMap model){  
        User user  = userService.login(name,pwd);  
        model.addAttribute("user",user);  
        model.put("name",name);  
        return "success";  
          }  
* 使用@ModelAttribute注解

               
        @RequestMapping("/login.do")  
        public String login(@ModelAttribute("user") User user){  
        //TODO  
        return "success";  
         }  
      
         @ModelAttribute("name")  
         public String getName(){  
        return name;  
              }  
      
* 使用HttpServletRequest 和 Session  然后setAttribute()，就和Servlet中一样 
       
          @RequestMapping("/login.do")  
          public String login(String name,String pwd  ， ModelMap model,HttpServletRequest request){  
          User user = serService.login(name,pwd);  
          HttpSession session = request.getSession();  
          session.setAttribute("user",user);  
          model.addAttribute("user",user);  
          return "success";  
        } 
       


* 重定向

        1.使用RedirectView
        public ModelAndView login(){  
         RedirectView view = new RedirectView("regirst.do");  
         return new ModelAndView(view);  
        }  
          2.
           public String login(){  
           //TODO  
             return "redirect:regirst.do";  
            }


     
       
###具体文档：http://wenku.baidu.com/link?url=M1-p2bsHR8eHEPlNXUql1PdcJiCfm9d97_5Pav8VugUQsHrIE_hHsIA14_6DKcpOu8SbDf7bnOY37Da4Qr2IXFzZbBxlXsM28rlBLNYV5bK
##思想
IoC:控制反转    DI:注入依赖

http://www.cnblogs.com/xdp-gacl/p/4249939.html
     

      


##出现的问题
* el 表达式不能使用<br >
      jsp版本问题<br >
   解决方法：
        
       * 1.手动打开el :在.jsp开头加上 
             
             <%@ page isELIgnored="false" %>
       * 2.修改web.xml 版本换到2.4 以上 

            <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee 
            http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
               version="3.1">
                 ......
            </web-app>
　　

　　    