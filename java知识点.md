###关于获取URI，RUL的各类方法

basePath:http://localhost:8080/test/

getContextPath:/test 
getServletPath:/test.jsp 
getRequestURI:/test/test.jsp 
getRequestURL:http://localhost:8080/test/test.jsp 
getRealPath:D:\Tomcat 6.0\webapps\test\ 
getServletContext().getRealPath:D:\Tomcat 6.0\webapps\test\ 
getQueryString:p=fuck

地址：http://www.cnblogs.com/qq78292959/p/3793412.html

###request.getParamerterMap()
    获取URL 中的参数，返回Map-key :value
    作用： 防止参数名的相同， i=1&1=7

注意：request.getRequestURL,request.getParamerMap 适用于get,Post
     request.getQueryString()：获得get中的参数


###java默认字符集
JVM默认字符集——Charset.defaultCharset()
地址：http://www.cnblogs.com/riyueshiwang/p/4753677.html

##Vector（可变数组）
    一种数组
     ArrayList会比Vector快，他是非同步的，如果设计涉及到多线程，还是用Vector比较好一些
     /Vector的创建
    //使用Vector的构造方法进行创建
     Vector v = new Vector(4);

    //向Vector中添加元素
     //使用add方法直接添加元素
     v.add("Test0");
     v.add("Test1");
     v.add("Test0");
     v.add("Test2");
     v.add("Test2");

     //从Vector中删除元素
     v.remove("Test0"); //删除指定内容的元素
    v.remove(0); //按照索引号删除元素

    //获得Vector中已有元素的个数
    int size = v.size();
       System.out.println("size:" + size);

    //遍历Vector中的元素
    for(int i = 0;i < v.size();i++){
        System.out.println(v.get(i));
    }  
 -------------
Vector 类提供了实现可增长数组的功能，随着更多元素加入其中，数组变的更大。在删除一些元素之后，数组变小。 

##JAVA发送HTTP请求,返回HTTP响应内容

* 首先让我们先构建一个请求类（HttpRequester ）
* 创建HttpRespons:请求后的返回内容
    地址：http://www.jb51.net/article/47070.htm



##JAVA 中Properties类的操作
      类Properties（Java.util.Properties）
      主要用于读取Java的配置文件
      它提供了几个主要的方法：

      1． getProperty ( String key)，用指定的键在此属性列表中搜索属性。也就是通过参数 key ，得到 key 所对应的 value。

      2． load ( InputStream inStream)，从输入流中读取属性列表（键和元素对）。通过对指定的文件（比如说上面的 test.properties 文件）进行装载来获取该文件中的所有键 - 值对。以供 getProperty ( String key) 来搜索。

     3． setProperty ( String key, String value) ，调用 Hashtable 的方法 put 。他通过调用基类的put方法来设置 键 - 值对。

     4． store ( OutputStream out, String comments)，以适合使用 load 方法加载到 Properties 表中的格式，将此 Properties 表中的属性列表（键和元素对）写入输出流。与 load 方法相反，该方法将键 - 值对写入到指定的文件中去。

     5． clear ()，清除所有装载的 键 - 值对。该方法在基类中提供。

 


    地址：http://www.cnblogs.com/bakari/p/3562244.html

## JAVA中Synchroniaed的用法
     修饰一个代码块

     一个线程访问一个对象中的synchronized(this)同步代码块时，其他试图访问该对象的线程将被阻塞。

##使用multipart请求处理文件上传
  xml配置：
       
        <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">  
        <property name="defaultEncoding" value="utf-8"></property>   
        <property name="maxUploadSize" value="10485760000"></property>  
        <property name="maxInMemorySize" value="40960"></property>  
        </bean>   
  html 上传表单示例

    <form action="upload" enctype="multipart/form-data">

    <input type="file" name="myFile" />

    <input type="submit" value="Upload! " />
     实际上一个上传表单只需要满足如下两点。

     l  enctype属性的属性值设为multipart/form-data。

     2  input的type属性的属性值设为file。

   </form>

   <form action="upload" enctype="multipart/form-data">
 
   <input type="file" name="myFile" />

   <input type="submit" value="Upload! " />

   </form>
java :
    
     MultipartHttpServletRequest multipartRequest = (MultipartHttpServletRequest) request;//将request转换为MultupartHttpServletRequest,首先为MultipartResolver处理
     MultipartFile imgFile1 = multipartRequest.getFile ("fileUpload");//获得文件
     String fileName = imgFile.getOriginalFilename();//获得文件名
    地址：http://blog.csdn.net/a1314517love/article/details/24183273


## java裁图（im4Java）
  下载ImageMagick-6.9.1-8-Q16-x86-dll 只有32位， 所以jdk32位安装
 
       上传截图作品： 首先上传的是整张图片，通过MulipartHttpServletRequest 获取文件（同下载文件）储存在本地，
     在新建一个文件地址用于存贮裁剪过的图片
       public static void cutImage(String srcPath, String newPath, int x, int y, int x1, int y1)  throws Exception {
           int width = x1 - x;
        int height = y1 - y;
        IMOperation op = new IMOperation();
        op.addImage(new String[]{srcPath});
        op.crop(Integer.valueOf(width), Integer.valueOf(height), Integer.valueOf(x), Integer.valueOf(y));
        op.addImage(new String[]{newPath});
        ConvertCmd convert = new ConvertCmd();
        String osName = System.getProperty("os.name").toLowerCase();
        if(osName.indexOf("win") != -1) {//判断操作系统是否含win,没有返回-1
            convert.setSearchPath(PropertiesUtil.getProperty("wanmei", "system.local.imagemagic"));
        }

        convert.run(op, new Object[0]);
    }

地址：http://blog.csdn.net/tiantiandjava/article/details/10080581



## POI 导入，导出Excel
 导入apache poi jar包




## ImageIO 处理图像（缩放，放大等）
 * 上传图片，上传到本地：首先根据MultipleHttpServletRequest 获得image，在本地新建image地址，进行复制




## xx.compareTo(xx)
* 对于字符串的比较：先一个一个字符比较ASCII码，输出对应的ASCII差
 若第一个字母同，则转到第二个字母，若都相同 ，返回字符长度的差
         
    tring s1 = "abc"; 
    String s2 = "abcd"; 
    String s3 = "abcdfg"; 
    String s4 = "1bcdfg"; 
    String s5 = "cdfg"; 
    System.out.println( s1.compareTo(s2) ); // -1 (前面相等,s1长度小1) 
    System.out.println( s1.compareTo(s3) ); // -3 (前面相等,s1长度小3) 
    System.out.println( s1.compareTo(s4) ); // 48 ("a"的ASCII码是97,"1"的的ASCII码是49,所以返回48) 
    System.out.println( s1.compareTo(s5) ); // -2 ("a"的ASCII码是97,"c"的ASCII码是99,所以返回-2)
* Date()的比较 ：装换为了毫秒的比较
### 随机数
           
           Random random = new Random();
        //参数length，表示生成几位随机数
        for (int i = 0; i < length; i++) {
            //随机决定输出字母还是数字
       //   String charOrNum = random.nextInt(2) % 2 == 0 ? "char" : "num";//强制为输出数字
            String charOrNum = "num";
            if ("char".equalsIgnoreCase(charOrNum)) {
                //输出是大写字母还是小写字母
                int temp = random.nextInt(2) % 2 == 0 ? 65 : 97;//65-90大写，97以上小写
                val += (char) (random.nextInt(26) + temp);
            } else if ("num".equalsIgnoreCase(charOrNum)) {
                val += String.valueOf(random.nextInt(10));//输出0-9数字
            }
        }
###StringUtils的isBlank与isEmply
isEmply: str==null 或 str.length()==0<br />
isBlank: StringUtils.isBlank(null) = true<br />
StringUtils.isBlank("") = true<br />
StringUtils.isBlank(" ") = true

###手机发送验证码

















###邮箱发送验证码