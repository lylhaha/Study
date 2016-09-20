#注： JavaScript 区分大小写
###需从 JavaScript 访问某个 HTML 元素，您可以使用 <strong>document.getElementById(id)</strong> 方法。
##同过DOM 获取元素 或创建元素
* 通过标签名查找HTML元素
*  HTML DOM 添加新元素
###数据类型
* 1、字符串："" 或''(字符串断行需要使用反斜杠(\)

        var x = "Hello \
        World!";
* 2、数字类型： 可带小数点，可以不带
  
         极大或极小的数字可以通过科学（指数）计数法来书写：
         var y=123e5;      // 12300000
         var z=123e-5;     // 0.00123 
* bool (布尔) :ture false
        
        var x=true
        var y=false
* 数组
 
        var cars=new Array();
        cars[0]="a";
        cars[1]="a";
        或
        var cars=new Array("Audi","BMW","Volvo");
* 对象（对象由花括号分隔。在括号内部，对象的属性以名称和值对的形式 (name :value) 来定义。属性由逗号分隔：）
 
                 var person={firstname:"Bill", lastname:"Gates", id:5566};
                  对象属性有两种寻址方式：
                  name=person.firstname;
                  name=person["firstname"];
                   <script>
                   var person = {
                   firstName: "John",
                   lastName : "Doe",
                   id : 5566,
                    fullName : function() 
	                {
                     return this.firstName + " " + this.lastName;
                     }
                    };
                   document.getElementById("demo").innerHTML = person.fullName();
                  </script>
                  
* Underfined 和Null
 
                  Undefined:变量不含值
                  null:     清空变量
注：JavaScript 变量均为对象。当您声明一个变量时，就创建了一个新的对象。


###函数
* 不带参数

        <!DOCTYPE html>
         <html>
         <head>
           <script>
           function myFunction()
           {
            alert("Hello World!");
           }
          </script>
          </head>

           <body>
           <button onclick="myFunction()">Try it</button>
           </body>
           </html>
* 带参数

         function(var1,var2)
         {
         代码
         }
* 带返回值
      
         function myFunction(a,b)
         {
          return a*b;
         }

          document.getElementById("demo").innerHTML=myFunction(4,3);
      
##作用域（变量可以先使用，后声明）
*  局部变量：在函数内，var 定义
*  全局变量： 
   1、在函数外定义，所有函数都可以用

         var carName = " Volvo";

        // 此处可调用 carName 变量

        function myFunction() {

        // 函数内可调用 carName 变量

        } 


   2、  在函数内没有声明的（无var定义）

        // 此处可调用 carName 变量

        function myFunction() {
       carName = "Volvo";

      // 此处可调用 carName 变量

      }  
 
注 ：全局变量是window对象
     window.***

## 常见HTML事件

     事件 	       描述
     onchange 	   HTML 元素改变，常结合对输入字段的验证来使用
     onclick 	   用户点击 HTML 元素
     onmouseover   用户在一个HTML元素上移动鼠标
     onmouseout    用户从一个HTML元素上移开鼠标
     onkeydown 	   用户按下键盘按键
     onload 	   浏览器已完成页面的加载
      onfocus      获得焦点

## 数据类型转换
 * 转换成字符串
   
        1、数字转换成字符串：    String(123)，   (123).toString()<br >
        2、boolean 转换成字符串：String(false),  false.toString()<br >
        3、日期转换成字符串:String(Date()) ,    Date().toString()
 *  转换成数字
   
         1、字符串转换为数字：Number("3") //3  Number("") //0  
         2、 boolean 转换为数字:Number(false)//0 Number(true)//1
         3、日期转换为数字:Number(new Date())

##正则表达式（所有文本搜索和文本替换的操作）
      语法：/pattern/modifiers; 
* search()
* 
        var str = "Visit w3cschool";
        var n = str.search(/w3cschool/i); //在str 中找w3cschool 在第几个位置 返回：6
* replace()

        var str = "Visit Microsoft!";
        var res = str.replace("Microsoft", "w3cschool");//替换
        

        修饰符 可以在全局搜索中不区分大小写:
        修饰符 	描述
        i 	执行对大小写不敏感的匹配。
        g 	执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。
        m 	执行多行匹配。  
* test()  :
   检测一个字符串是否匹配某个模式，如果字符串中含有匹配的文本，则返回 true，否则返回 false。

        var patt = /e/;
        patt.test("The best things in life are free!"); 

###调试
 console.log();

###严格模式（use strict）避免一些不规范
      <script>
      "use strict";
       x = 3.14;       // 报错 (x 未定义)
       </script>

###表单校验
   * 必填
   
        if (x==null || x==""){
        alert("姓必须填写");
        return false;
        }
   * email验证

        function validateForm(){
	    var x=document.forms["myForm"]["email"].value;
	     var atpos=x.indexOf("@");
	    var dotpos=x.lastIndexOf(".");
	    if (atpos<1 || dotpos<atpos+2 || dotpos+2>=x.length){
		 alert("不是一个有效的 e-mail 地址");
		return false;
	     }
         }

   * 手机验证

         var reg = /^1[0-9]{10}$/;
        if (!reg.test(tell)) {
            alert("号码有误!");
            applyFlag = true;
            return;
        };

###消息框
* 警告框
  alert("xxxx");
* 确认框
   confirm("xxx");
* 提示框
   prompt("文本"，"默认值");
### 计时
var t=setTimeout("js语句",毫秒);
clearTimeout(t);
###cookie
   
         <html>
          <head>
        <script type="text/javascript">
      function getCookie(c_name)
        {
        if (document.cookie.length>0)
         {
          c_start=document.cookie.indexOf(c_name + "=")
         if (c_start!=-1)
          { 
          c_start=c_start + c_name.length+1 
           c_end=document.cookie.indexOf(";",c_start)
          if (c_end==-1) c_end=document.cookie.length
           return unescape(document.cookie.substring(c_start,c_end))
     } 
    }
      return ""
     }

        function setCookie(c_name,value,expiredays)
       {
          var exdate=new Date()
        exdate.setDate(exdate.getDate()+expiredays)
        document.cookie=c_name+ "=" +escape(value)+
          ((expiredays==null) ? "" : ";expires="+exdate.toGMTString())
          }

          function checkCookie()
         {
           username=getCookie('username')
         if (username!=null && username!="")
          {alert('Welcome again '+username+'!')}
          else 
          {
           username=prompt('Please enter your name:',"")
          if (username!=null && username!="")
            {
             setCookie('username',username,365)
           }
             }
         }
       </script>
          </head>

          <body onLoad="checkCookie()">
           </body>
            </html>

## JSON(重点)
    {"employees":[
    {"firstName":"John", "lastName":"Doe"},
    {"firstName":"Anna", "lastName":"Smith"},
    {"firstName":"Peter", "lastName":"Jones"}
    ]}
#####将JSON转换成JavaScript
*   eval
*   
         语法：var obj=eval("("+txt+")");
* JSON 解析器

         语法：JSON.parse(txt);
##AJAX(重点)
* 创建XMLHttpRequest对象

   * (所有现代浏览器（IE7+、Firefox、Chrome、Safari 以及 Opera）均内建 XMLHttpRequest 对象。)

          variable=new XMLHttpRequest();
    * 老版本的 Internet Explorer （IE5 和 IE6）使用 ActiveX 对象：
          variable=new ActiveXObject("Microsoft.XMLHTTP");
      
             var xmlhttp;
             if (window.XMLHttpRequest)
            {// code for IE7+, Firefox, Chrome, Opera, Safari
            xmlhttp=new XMLHttpRequest();
            }
            else
             {// code for IE6, IE5
              xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
             }
* 向服务器发送请求
     * Get
       
            xmlhttp.open("GET","test1.txt",true);
            xmlhttp.send(); 
            
             方法 	                         描述
            open(method,url,async) 	 规定请求的类型、URL 以是否异步处理请求。
                                      method：请求的类型GET 或 POST
                                      url：文件在服务器上的位置
                                     async：true（异步）或 false（同步）

               send(string) 	      将请求发送到服务器。

                                       string：仅用于 POST 请求
     * POST
                
             xmlhttp.open("POST","ajax_test.asp",true);
             xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
             xmlhttp.send("fname=Bill&lname=Gates");




* 服务器响应

         属性 	         描述
         responseText 	获得字符串形式的响应数据。
         responseXML 	获得 XML 形式的响应数据。


          <html>
             <head>
               <script type="text/javascript">
               function loadXMLDoc()
                {
               var xmlhttp;
               if (window.XMLHttpRequest)
               {// code for IE7+, Firefox, Chrome, Opera, Safari
                  xmlhttp=new XMLHttpRequest();
               }
               else
               {// code for IE6, IE5
                  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
                }
              xmlhttp.onreadystatechange=function()
                {
                    if (xmlhttp.readyState==4 && xmlhttp.status==200)
                     {
                       document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
                     }
                 }
                    xmlhttp.open("GET","/ajax/test1.txt",true);
                    xmlhttp.send();
                  }
             </script>
          </head>
         <body>

              <div id="myDiv"><h2>Let AJAX change this  text</h2></div>
        <button type="button" onclick="loadXMLDoc()">通过 AJAX 改变内容</button>

         </body>
              </html>