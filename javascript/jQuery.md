# jQuery 基础语法与概念

-   **jQuery 定义**  
    jQuery 用 **$** 作为函数入口，通过调用 **$(*selector*).*action*()** 方法对匹配的 HTML 元素进行操作。

    -   **选择符（selector）** ：负责“查询”和“查找” DOM 中的 HTML 元素。
    -   **action() 方法**：对所选元素进行指定的操作。

-   **基本实例**

    ```
    $(this).hide();       // 隐藏当前元素
    $("p").hide();        // 隐藏所有 <p> 元素
    $("p.test").hide();   // 隐藏所有 class="test" 的 <p> 元素
    $("#test").hide();    // 隐藏 id="test" 的元素
    ```

* * *

# jQuery 入口与文档就绪事件

-   **jQuery 入口函数（Document Ready）**  
    确保 DOM 在完全加载后再执行 jQuery 代码，从而避免操作未加载的节点。

    -   标准写法：

        ```
        $(document).ready(function(){
          // 开始写 jQuery 代码...
        });
        ```

    -   简洁写法：

        ```
        $(function(){
          // 开始写 jQuery 代码...
        });
        ```

-   **与原生 js 的入口函数对比**

    ```
    window.onload = function(){
      // 执行代码（注意 window.onload 需等待所有资源加载完成）
    };
    ```

* * *

# 元素选择器

-   **基本选择器**

    -   标签选择器：`$("p")` – 选取所有 `<p>` 元素
    -   id 选择器：`$("#test")` – 选取 id 为 test 的元素
    -   class 选择器：`$(".test")` – 选取 class 为 test 的元素

-   **其他常用选择器示例**

    | 表达式          | 说明                                             |
    | ------------ | ---------------------------------------------- |
    | $("*")       | 选取所有元素                                         |
    | $(this)      | 选取当前 HTML 元素                                   |
    | $("p.intro") | 选取 class 为 intro 的所有 `<p>` 元素                  |
    | $("p:first") | 选取第一个 `<p>` 元素                                 |
    | $(":button") | 选取所有 type="button" 的 `<input>` 与 `<button>` 元素 |

* * *

# 引入 jQuery 文件

引入自定义或下载的 jQuery 文件，可以通过如下方式添加到 HTML 文件的 `<head>` 部分或文档尾部（推荐在底部以便页面先加载内容）：

```
<script src="my_jquery_functions.js"></script>
```

* * *

# 事件处理

jQuery 将各种事件封装得非常方便，可对鼠标、键盘、表单、文档/窗口等事件做出响应。

## 常见事件分类

-   **鼠标事件**

    | 事件名称       | 说明                             | 链接参考                                                              |
    | ---------- | ------------------------------ | ----------------------------------------------------------------- |
    | click      | 单击鼠标时触发                        | [click](https://www.runoob.com/jquery/event-click.html)           |
    | dblclick   | 双击鼠标时触发                        | [dblclick](https://www.runoob.com/jquery/event-dblclick.html)     |
    | mouseenter | 当鼠标指针进入元素时触发                   | [mouseenter](https://www.runoob.com/jquery/event-mouseenter.html) |
    | mouseleave | 当鼠标指针离开元素时触发                   | [mouseleave](https://www.runoob.com/jquery/event-mouseleave.html) |
    | hover      | 模拟光标悬停：鼠标进入触发一个函数，鼠标离开触发另外一个函数 | [hover](https://www.runoob.com/jquery/event-hover.html)           |

-   **键盘事件**

    | 事件名称     | 说明        | 链接参考                                                          |
    | -------- | --------- | ------------------------------------------------------------- |
    | keypress | 键盘按键按下时触发 | [keypress](https://www.runoob.com/jquery/event-keypress.html) |
    | keydown  | 按键按下时触发   | [keydown](https://www.runoob.com/jquery/event-keydown.html)   |
    | keyup    | 按键释放时触发   | [keyup](https://www.runoob.com/jquery/event-keyup.html)       |

-   **表单事件**

    | 事件名称   | 说明           | 链接参考                                                      |
    | ------ | ------------ | --------------------------------------------------------- |
    | submit | 表单提交时触发      | [submit](https://www.runoob.com/jquery/event-submit.html) |
    | change | 表单中元素内容改变时触发 | [change](https://www.runoob.com/jquery/event-change.html) |
    | focus  | 元素获得焦点时触发    | [focus](https://www.runoob.com/jquery/event-focus.html)   |
    | blur   | 元素失去焦点时触发    | [blur](https://www.runoob.com/jquery/event-blur.html)     |

-   **文档/窗口事件**

    | 事件名称   | 说明           | 链接参考                                                      |
    | ------ | ------------ | --------------------------------------------------------- |
    | load   | 页面或图片加载完成时触发 | [load](https://www.runoob.com/jquery/event-load.html)     |
    | resize | 窗口尺寸发生变化时触发  | [resize](https://www.runoob.com/jquery/event-resize.html) |
    | scroll | 页面滚动时触发      | [scroll](https://www.runoob.com/jquery/event-scroll.html) |
    | unload | 页面卸载时触发      | [unload](https://www.runoob.com/jquery/event-unload.html) |

## 示例：鼠标悬停事件（hover）

```
$("#p1").hover(
  function(){
    alert("你进入了 p1!");
  },
  function(){
    alert("拜拜! 现在你离开了 p1!");
  }
);
```

* * *

# 动画效果

jQuery 提供了多种内置动画方法，包括显示/隐藏、渐变、滑动以及自定义动画。

## 显示与隐藏

-   **hide() 与 show()**  
    可以使用以下方法控制元素的显示和隐藏，同时支持设置速度（"slow"、"fast"或毫秒数）以及回调函数：

    ```
    $(selector).hide(speed, callback);
    $(selector).show(speed, callback);
    ```

    *示例：*

    ```
    $(document).ready(function(){
      $(".hidebtn").click(function(){
        $("div").hide(1000, "linear", function(){
          alert("Hide() 方法已完成!");
        });
      });
    });
    ```

-   **toggle()**  
    用于在 hide() 和 show() 方法间切换，语法与前述方法类似：

    ```
    $(selector).toggle(speed, callback);
    ```

## 淡入淡出效果

-   **fadeIn()**  
    用于淡入已隐藏的元素：

    ```
    $(selector).fadeIn(speed, callback);
    ```

-   **fadeOut()**  
    用于淡出可见元素：

    ```
    $(selector).fadeOut(speed, callback);
    ```

-   **fadeToggle()**  
    切换元素的淡入淡出效果：

    ```
    $(selector).fadeToggle(speed, callback);
    ```

    *示例：*

    ```
    $("button").click(function(){
      $("#div1").fadeToggle();
      $("#div2").fadeToggle("slow");
      $("#div3").fadeToggle(3000);
    });
    ```

-   **fadeTo()**  
    使元素的透明度渐变到指定的不透明度（范围 0～1）：

    ```
    $(selector).fadeTo(speed, opacity);
    ```

    *示例：*

    ```
    $("button").click(function(){
      $("#div1").fadeTo("slow", 0.15);
      $("#div2").fadeTo("slow", 0.4);
      $("#div3").fadeTo("slow", 0.7);
    });
    ```

## 滑动效果

-   **slideDown()**  
    向下滑动显示元素：

    ```
    $(selector).slideDown(speed, callback);
    ```

-   **slideUp()**  
    向上滑动隐藏元素：

    ```
    $(selector).slideUp(speed, callback);
    ```

-   **slideToggle()**  
    在 slideDown() 与 slideUp() 间切换：

    ```
    $(selector).slideToggle(speed, callback);
    ```

## 自定义动画：animate()

-   **基本用法**  
    使用 **animate()** 方法可以创建自定义动画，其语法如下：

    ```
    $(selector).animate({ params }, speed, callback);
    ```

    -   **params**：一个对象，用来定义需要变化的 CSS 属性及其目标值。
    -   **speed**：动画持续时间，可用 "slow"、"fast" 或具体的毫秒数。
    -   **callback**：动画执行完毕后回调的函数名称。

-   **使用相对值**  
    对属性值可以使用相对操作符（+= 或 -=）表示相对于当前值进行增减：

    ```
    $("button").click(function(){
      $("div").animate({
        left: '250px',
        height: '+=150px',
        width: '+=150px'
      });
    });
    ```

-   **预定义动画值**  
    可使用 "show"、"hide"、"toggle" 作为动画值：

    ```
    $("button").click(function(){
      $("div").animate({height: 'toggle'});
    });
    ```

-   **队列动画**  
    当多个 animate() 调用顺序执行时，jQuery 会自动将它们排队依次运行：

    ```
    $("button").click(function(){
      var div = $("div");
      div.animate({height: '300px', opacity: '0.4'}, "slow");
      div.animate({width: '300px', opacity: '0.8'}, "slow");
      div.animate({height: '100px', opacity: '0.4'}, "slow");
      div.animate({width: '100px', opacity: '0.8'}, "slow");
    });
    ```

## 停止动画：stop()

-   **基本用法**  
    用于在动画或效果未完成时立即停止它们。  
    语法：

    ```
    $(selector).stop(stopAll, goToEnd);
    ```

    -   **stopAll**（可选）：是否清除动画队列，默认值为 false（仅停止当前动画，队列中的动画仍会执行）。
    -   **goToEnd**（可选）：是否立即完成当前动画，默认值为 false。

# HTML
## 获取内容和属性
- text() - 设置或返回所选元素的文本内容
- html() - 设置或返回所选元素的内容（包括 HTML 标签）
- val() - 设置或返回表单字段的值
-  attr() - 获取属性值
实例
```js
$("#btn1").click(function(){
  alert("Text: " + $("#test").text());
});
$("#btn2").click(function(){
  alert("HTML: " + $("#test").html());
});
$("#btn1").click(function(){
  alert("值为: " + $("#test").val());
});
$("button").click(function(){
  alert($("#runoob").attr("href"));
});
```
### 回调函数
text()、html()、val()、attr()回调函数有两个参数：被选元素列表中当前元素的下标，以及原始（旧的）值。然后以函数新值返回您希望使用的字符串
```js
$("#btn1").click(function(){
    $("#test1").text(function(i,origText){
        return "旧文本: " + origText + " 新文本: Hello world! (index: " + i + ")"; 
    });
});
 
$("#btn2").click(function(){
    $("#test2").html(function(i,origText){
        return "旧 html: " + origText + " 新 html: Hello <b>world!</b> (index: " + i + ")"; 
    });
});
```
 ## 添加元素
 - append() - 在被选元素的结尾插入内容（仍然在该元素的内部）
 - prepend() - 在被选元素的开头插入内容（仍然在该元素的内部）
 - after() - 在被选元素之后插入内容
 - before() - 在被选元素之前插入内容
实例
```js
function appendText(){
    var txt1="<p>文本-1。</p>";              // 使用 HTML 标签创建文本
    var txt2=$("<p></p>").text("文本-2。");  // 使用 jQuery 创建文本
    var txt3=document.createElement("p");
    txt3.innerHTML="文本-3。";               // 使用 DOM 创建文本 text with DOM
    $("body").append(txt1,txt2,txt3);        // 追加新元素
}

function afterText()
{
    var txt1="<b>I </b>";                    // 使用 HTML 创建元素
    var txt2=$("<i></i>").text("love ");     // 使用 jQuery 创建元素
    var txt3=document.createElement("big");  // 使用 DOM 创建元素
    txt3.innerHTML="jQuery!";
    $("img").after(txt1,txt2,txt3);          // 在图片后添加文本
}

```
## 删除元素
- remove() - 删除被选元素（及其子元素）
- empty() - 从被选元素中删除子元素（可接受一个参数，允许您对被删元素进行过滤）
```javascript
$("#div1").remove();
$("#div1").empty();
$("p").remove(".italic");  //删除 class="italic" 的所有 <p> 元素

```

##  获取并设置 CSS 类
-   addClass() - 向被选元素添加一个或多个类
-   removeClass() - 从被选元素删除一个或多个类
-   toggleClass() - 对被选元素进行添加/删除类的切换操作
-   css() - 设置或返回样式属性
```
$("button").click(function(){
  $("body div:first").addClass("important blue");
});

$("button").click(function(){
  $("h1,h2,p").removeClass("blue");
});

$("button").click(function(){
  $("h1,h2,p").toggleClass("blue");
});

//设置 CSS 属性
$("p").css("background-color","yellow");

//返回 CSS 属性
$("p").css("background-color");

```

## 尺寸
-   width() 方法设置或返回元素的宽度（不包括内边距、边框或外边距）
-   height()  方法设置或返回元素的高度（不包括内边距、边框或外边距）
-   innerWidth() 方法返回元素的宽度（包括内边距）
-   innerHeight() 方法返回元素的高度（包括内边距）
-   outerWidth()   方法返回元素的宽度（包括内边距和边框）
-   outerHeight()  方法返回元素的高度（包括内边距和边框）


# 遍历
## 祖先
-   parent()        返回被选元素的直接父元素。
-   parents()       返回被选元素的所有祖先元素，它一路向上直到文档的根元素 (<html>)   
-   parentsUntil()  回介于两个给定元素之间的所有祖先元素 （介于）

## 后代
-   children()  返回被选元素的所有直接子元素
-   find()      返回被选元素的后代元素，一路向下直到最后一个后代

## 同胞
-   siblings()  返回被选元素的所有同胞元素
-   next()      回被选元素的下一个同胞元素
-   nextAll()   回被选元素的所有跟随的同胞元素
-   nextUntil() 返回介于两个给定参数之间的所有跟随的同胞元素
-   prev()      
-   prevAll()
-   prevUntil()
```js
$(document).ready(function(){
  $("h2").nextUntil("h6");
});
```

## 过滤
- first()  返回被选元素的首个元素
- last() 方法返回被选元素的最后一个元素
- eq() 方法返回被选元素中带有指定索引号的元素
- filter() 方法允许您规定一个标准。不匹配这个标准的元素会被从集合中删除，匹配的元素会被返回
- not() 方法返回不匹配标准的所有元素
```js
$(document).ready(function(){
  $("div p").first();
});

$(document).ready(function(){
  $("div p").last();
});

$(document).ready(function(){
  $("p").eq(1);
});

$(document).ready(function(){
  $("p").filter(".url");
});

$(document).ready(function(){
  $("p").not(".url");
});
```