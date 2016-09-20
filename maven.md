##maven（结合string.xml）
    http://www.2cto.com/kf/201303/196131.html
    http://www.cnblogs.com/yakov/archive/2011/11/26/maven2_settings.html

http://blog.csdn.net/sky19891212/article/details/43924831


注意：<mirror >url 改为：http://repo.maven.apache.org/maven2
  
###知识点
     <localRepository />:用于本地库的存储位置设置（jar存放的位置,默认在m2/repository）,需要另外存放则换其他地址

     <pluginGroups />:

     <proxies />:设置 无法直接访问 中心库的用户
      
     
     <servers />:针对于pom-distributionManagement-开发库，此配置保存server信息
     注意：这是Server的ID(不是登录进来的user)，与Maven想要连接上的repository/mirror中的id元素相匹配
     
   
     <mirrors />:镜像库，覆盖中央库的默认地址（http://search.maven.org/）

      <profiles />:(类似于pom.xml-profile，单独使用不生效)定义其他开发库和插件开发库。repositories/pluginRepositories
      (releases,snapshots:
       产品版本：
       1.release:稳定版本  2.snapshot:不稳定，只是快照
      )
      
       <properties />:maven 的properties作为placeholder值
        包括以下的5种类型值：
        env.X，返回当前的环境变量
        project.x:返回pom中定义的元素值，如project.version
        settings.x：返回settings.xml中定义的元素
        java 系统属性：所有经过java.lang.System.getProperties()返回的值
        x：用户自己设定的值

      <activation />:激活profile
      <activeProfiles />:激活profile

###maven pom.xml 文件详解
http://blog.csdn.net/yaerfeng/article/details/26448417

查找对应的jar包dependency写法： http://mvnrepository.com/ 