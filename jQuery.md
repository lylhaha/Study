基础语法是：$(selector).action()

    美元符号定义 jQuery
    选择符（selector）“查询”和“查找” HTML 元素
    jQuery 的 action() 执行对元素的操作
###就绪函数
     $(document).ready(function(){


        });
### 获取html 元素
* 元素选择器

        $("p"):<p>元素
        $("p.into")：class="into" 的<p>元素
        $("p#demo")：id="demo"的<p>元素
* 属性选择器

         $("[href]"):带有href属性的元素
         $("[href='#']"):带有href='#'的元素
         $("[href！='#']"):带有href不等于'#'的元素
* css选择器

         $("p").css("background-color","red");  
###jQuery效果
* 隐藏、显示

         hide（）
         show()
        toggle():切换
* 淡入、淡出

        fadeIn()：淡入，隐藏
        fadeOut():淡出，出现
        fadeToggle():切换
        fadeTo():渐变，给定透明度
* 滑动

        slideDown():向下滑动
        slideUp():向上滑动
        slidToggle():切换

* 动画

      animate();


###获取内容
* text():文本内容
* html():内容（包括html标记）
* val():返回表单字段的值

###获取属性的值
* attr();

###设置内容、属性
* text("xxx");
          
         $("#btn1").click(function(){
         $("#test1").text(function(i,origText){
             return "Old text: " + origText + " New text: Hello world! (index: " + i + ")";
           });
         });
    
* html("xxxxx");

         $("#btn2").click(function(){
         $("#test2").html(function(i,origText){
         return "Old html: " + origText + " New html: Hello <b>world!</b>(index: " + i + ")";
         });
           });
* val("xxxxx");

* 设置属性值

        $("button").click(function(){
        $("#w3s").attr("href","http://www.w3school.com.cn/jquery");
         });
          
          $("button").click(function(){
          $("#w3s").attr({
              "href" : "http://www.w3school.com.cn/jquery",
              "title" : "W3School jQuery Tutorial"
          });
           });

###添加元素
* append():元素结尾后插入内容

        $("p").append("Some appended text.");
* prepend():元素开头插入内容


###删除元素
* 删除被选元素及子元素
           
        remove （）
        $("p").remove(".italic");//设置删除元素的条件
* 删除被选元素子元素

        empty();


###jQuery向上遍历
* parent():被选元素的直接父元素,向上一级对DOM遍历

         $(document).ready(function(){
          $("span").parent();
           }); 
* parents():被选元素的所有祖先元素，知道<html>

         $(document).ready(function(){
          $("span").parents("ul");
            });//祖先元素为：ul
* parentsUntil():介于2个元素之间的祖先元素

         $(document).ready(function(){
         $("span").parentsUntil("div");
         });

###jQuery向下遍历

* children():下一级子元素 

         $(document).ready(function(){
         $("div").children();
         });
* find():所有子元素

         $(document).ready(function(){
         $("div").find("span");
         });
###jQuery水平遍历
* siblings():所有同胞元素

        $(document).ready(function(){
        $("h2").siblings();
        });
* next():下一个同胞元素

        $(document).ready(function(){
        $("h2").next();
        });
* nextAll():下面的所有同胞元素

         $(document).ready(function(){
         $("h2").nextAll();
         });

* nextUntil():两者之间的同胞元素

         $(document).ready(function(){
         $("h2").nextUntil("h6");
        });

### jQuery 过滤
* first():被选元素的首个元素

        $(document).ready(function(){
        $("div p").first();
         });

* last():最后一个元素
* eq():返回指定元素带有索引号的元素

        $(document).ready(function(){
        $("p").eq(0);
        });//第一个p

* filter():匹配的元素会被返回

         $(document).ready(function(){
         $("p").filter(".intro");
         });
* not():与filter()相反


##AJAX

      语法：   jQuery.ajax([settings])


       $.ajax({
					type : 'POST',
					url :"../../newsaction/achieveRoleList.json",
					data : {userName : arry[i]},
					dataType : 'json',
					success : function(data) {
						
					}
				});

* dateType:

   
   * "xml": 返回 XML 文档，可用 jQuery 处理。
   * "html": 返回纯文本 HTML 信息；包含的 script 标签会在插入 dom 时执行。
   * "script": 返回纯文本 JavaScript 代码。不会自动缓存结果。除非设置了 "cache" 参数。注意：在远程请求时(不在同一个域下)，所有 POST 请求都将转为 GET 请求。（因为将使用 DOM 的 script标签来加载）
   * "json": 返回 JSON 数据 。
   * "jsonp": JSONP 格式。使用 JSONP 形式调用函数时，如 "myurl?callback=?" jQuery 将自动替换 ? 为正确的函数名，以执行回调函数。
   * "text": 返回纯文本字符串，默认



       