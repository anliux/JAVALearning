# HTML入门

## 目录
<!--GFM-TOC -->
- [案例导航](#案例导航): 汇总所有案例
- [网站信息页面](#网站信息页面): HTML概述, HTML语法规范, HBuilder, 需求分析, 代码实现
- [网站图片信息页面](#网站图片信息页面): img标签, 文件路径, 代码实现
- [网站友情链接页面](#网站友情链接页面): 列表标签ul/ol, 超链接标签a, 代码实现
- [网站首页](#网站首页): 表格标签table, 合并单元格, 表格嵌套, 网站首页实现思路分析(以表格划分后分步填充实现)
- [网站注册页面](#网站注册页面): 表单标签form, 跳转方式get/post, input的type参数, 背景图片插入等
- [网站后台页面展示](#网站后台页面展示): 框架标签frameset, frame常用属性, 框架中点击跳转的实现
- [内容回顾](#内容回顾): 简单回顾涉及到的标签
- [参考链接](#参考链接): 菜鸟HBuilder和HTML；w3school
<!--GFM-TOC -->



## 案例导航
- 网站信息页面案例
- 网站图片信息页面案例
- 网站友情链接页面案例
- 网站首页案例
- 网站注册页面案例
- 网站后台页面案例

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 网站信息页面
- ### 需求分析:
  - 我们公司需要一个对外宣传的网站介绍,介绍公司的主要业务,公司的发展历史,公司的口号等等信息
  - 页面示例：
    ![网站信息页面]()

- ### HTML概述:
  - HTML: Hyper Text Markup Language 超文本标记语言
    - 超文本: 比普通文本功能更加强大,可以添加各种样式
    - 标记语言: 通过一组标签.来对内容进行描述. <关键字> , 是由浏览器来解释执行
  - 注意：HTML是解释型语言(弱语言)，出现小错误，比如文本放到了标签外面，浏览器在解释的时候会自动调整和矫正小错误
    - 谷歌浏览器：右键--显示网页源代码 或 检查，查看网页源码
  - 学习文档：W3School(一个学习网站)
  - 代码示例：
    ```html
    <h1>静夜诗</h1>
    <b><i>--李白</i> </b> <br/>
    <p>床前明月光,</p>
    <p>地上鞋两双,</p>
    <p>举头望明月,</p>
    <p>低头思故乡.</p>
    ```

- ### HTML语法规范
  - `<!DOCTYPE html>`：最上面是一个文档声明，不需要成对
  - 根标签 html，成对
  - html文件主要包含两部分. 头部分和体部分
    - 头部分head: 主要是用来放置一些页面信息
       - title：标签页显示标题；如果不写title，标签显示的是路径
       - meta charset：解析使用的码表
    - 体部分body: 主要来放置HTML页面的内容
  - 通过标签来对内容进行描述,标签通常都是由开始标签和结束标签组成 
  - 标签不区分大小写, 官方建议使用小写
    - 大写也对，但规范是小写
    - 标签一定要保证是成对出现的
    - 标签可嵌套，注意内外成对出现 (虽然浏览器解析时可能会矫正此类错误)
  - 代码示例：
  ```html
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title></title>
      </head>
      <body>
        <!--balabala......-->
      </body>
    </html>
  ```

- ### HBuilderX
  - #### 简介
    - HBuilder是DCloud（数字天堂）推出的一款支持HTML5的Web开发IDE。 
    - HBuilder的编写用到了Java、C、Web和Ruby。
    - HBuilder本身主体是由Java编写。它基于Eclipse，所以顺其自然地兼容了Eclipse的插件
    - 是HTML5的常用编辑工具
    - HBuilder: 官网下载即可
    - 学习参考链接: [菜鸟教程：HBuilderX 使用教程](https://www.runoob.com/w3cnote/hbuilder-intro.html)
  - #### 使用
    - 文件 -- 新建 -- web项目, 或新建 -- 项目 -- 基本的HTML项目(包含初始css,js,img等文件)
    - 目录顺序：项目-文件-html文件
    - 运行: 在默认浏览器运行，快捷键ctrl+R
    - 注：之前好像运行才会更新到浏览器显示，现版本保存后会自动更新显示到浏览器
  - #### 常用的快捷键
    ```html
    Ctrl + R  					运行当前网页/刷新当前网页
    Ctrl + Shift + /            注释当前行
    Command + /				mac: 加注释，同eclipse
    Ctrl + D 					删除光标当前所在的行
    Ctrl + Shift + R 			复制当前行到下一行
    Ctrl + Enter 				将光标移动到下一行
    Ctrl + Shift + Enter 		将光标定位在上一行
    ```

- ### 步骤分析:
  - 公司简介 需要标题:
    - body:
   		- head: `<h1></h1>`: 1-6级标题，其他会显示为普通文本格式 (标签未定义)
      - `<br/>`: 换行，空标签，没有内容可以修饰，不需要成对		
      - b : 加粗
      - i : 斜体
      - strong: 加粗, 带语义标签 
      - em:  斜体, 带语义标签
      - 注：“带语义”：搜索引擎友好，建议使用，例如盲人朗读时会加重语气，b/i则没有此类效果
    - 标签：都是预定义好的，不能去创造标签，例如<h88></h88>，未定义，仍然显示未普通文本格式
  - 水平分割线:
    - 水平分割线的标签：`<hr />`
  - 四个段落:
    - 段落标签：`<p></p>`
  - 第一个段落字体需要红色:
    - font格式：
      - 格式：`<font 属性名称="属性的值">`
      - 示例：`<font color="red" size="7" face="仿宋"> 文本 </font>>`
    - font 常用标签 
      - color: 颜色
      - size: 改变字体大小，范围1-7，默认3
      - face: 改变字体

- ### 代码实现:
  ```html
  <html>
    <head>
      <meta charset="UTF-8">
      <title>网站信息页面</title>
    </head>
    <body>
      <!--
        1. 公司简介 需要标题
        2. 水平分割线
        3. 四个段落
        4. 第一个段落字体需要红色
      -->
      <h3>公司简介</h3>

      <hr />
      <p>
      <font color="red">“中关村黑马程序员训练营”</font>是由<b><i>传智播客</i></b>联合中关村软件园、CSDN，并委托传智播客进行教学实施的软件开发高端培训机构，致力于服务各大软件企业，解决当前软件开发技术飞速发展，而企业招不到优秀人才的困扰。 目前，“中关村黑马程序员训练营”已成长为行业“学员质量好、课程内容深、企业满意”的移动开发高端训练基地，并被评为中关村软件园重点扶持人才企业。
      </p>
      <p>
      <strong>黑马程序员</strong>的学员多为大学毕业后，<em>有理想、有梦想，</em>想从事IT行业，而没有环境和机遇改变自己命运的年轻人。黑马程序员的学员筛选制度，远比现在90%以上的企业招聘流程更为严格。任何一名学员想成功入学“黑马程序员”，必须经历长达2个月的面试流程，这些流程中不仅包括严格的技术测试、自学能力测试，还包括性格测试、压力测试、品德测试等等测试。毫不夸张地说，黑马程序员训练营所有学员都是精挑细选出来的。百里挑一的残酷筛选制度确保学员质量，并降低企业的用人风险。
      </p>
      <p>
      中关村黑马程序员训练营不仅着重培养学员的基础理论知识，更注重培养项目实施管理能力，并密切关注技术革新，不断引入先进的技术，研发更新技术课程，确保学员进入企业后不仅能独立从事开发工作，更能给企业带来新的技术体系和理念。
      </p>
      <p>
      一直以来，黑马程序员以技术视角关注IT产业发展，以深度分享推进产业技术成长，致力于弘扬技术创新，倡导分享、 开放和协作，努力打造高质量的IT人才服务平台。
      </p>
    </body>
  </html>
  ```

- ### 代码链接
  - []()

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 网站图片信息页面 
- ### 需求分析:
  - 在网站中通常需要显示LOGO图片

- ### img标签: 
  - 格式：`<img 属性1="xxx" 属性2="xxx" />`, 注意最后有个斜杠
  - 常用的属性：
    - width : 宽度，参数为像素值或缩放百分比 
      - eg.`<img width="500px" />` 或 `<img width="30%"/>`
    - height: 高度 - 注意，不是heigth
      - eg. `<img height="500px" />`
      - 注：单位px(像素)；宽高指定其一，另一会等比缩放，两个都指定，图片显示可能会变形
    - src :  指定文件路径，图片文件可放在项目的img文件夹下
      - eg. `<img src="../img/figure.jpg" />`
    - alt:  图片加载失败时的提示内容 (图片加载失败小图标可能不同浏览器不同)
      - eg. `<img alt="这张图片可能加载有问题" />`

- ### 文件路径
  - 相对路径
  - 示例：
    ```html
        ./		代表的是当前路径，可不写，默认
        ../ 	代表的上一级路径：例如图片在文件所在的文件夹平级的路径
        ../../	上上一级路径：例如图片在文件外两层的路径下
    ```

- ### 代码实现
    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="UTF-8">
        <title></title>
      </head>
      <body>
        <!--
          常用属性:
            src : 指定图片路径
            width : 指定图片宽度
            height : 图片高度
            alt : 文件加载失败时的提示信息
        -->
        <img src="../img/美女22.jpg" width="500px" alt="这张图片可能加载问题" />
      </body>
    </html>


    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="UTF-8">
        <title></title>
      </head>
      <body>
        <!--在网页中显示图片-->
        <img src="../img/logo2.png" width="30%"/>
        <img src="../image/header.jpg" width="30%" />
      </body>
    </html>
    ```

- ### 代码链接
  - []()

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 网站友情链接页面 
- ### 需求分析
  - 在我们的网站中,通常会显示友商公司的网站链接
  - 例如：
    - 百度
    - 新浪微博
    - 黑马程序员...

- ### 列表标签: 
  - 无序列表:  ul 示例：`<ul type="square">`
    - type: 小圆圈circle, 小圆点disc(默认样式), 小方块square
  - 有序列表: ol
    - type: 指定序号的类型，1,a ,A,I,
    - start : 指定是起始索引，参数是数字

- ### 超链接标签a
  - 点击链接,跳转去指定网站
  - a 超链接标签 `<a href="URL" target="blank..">显示文本</a>`
  - 常用的属性:
    - href: 指定要跳转去的链接地址  		
      - 绝对URL：指链接地址指向另一个站点，需要加上http协议，例：href=“http://www.php.cn/”
      - 相对URL：指向站点内某个文件，如果访问的是本网站的html文件,可以直接写文件路径，例：href="/course/list/1.html"
      - 锚URL：指向页面中的锚，例：href="#top", 回到最顶部(也可：`href="#"`)
      - 参考：[html中href什么意思](https://m.php.cn/article/417929.html)
    - target : 以什么方式打开，前两种常用
      - `_self`: 默认打开方式,在当前窗口打开
      - `_blank`:  新起一个标签页打开页面
      - `_parent`:  在父框架集中打开被链接文档。没有父，则使用默认`_self`
      - `_top`: 在整个窗口中打开被链接文档。没有父，则使用默认`_self`
      - framename: 在指定的框架中打开被链接文档。（详见网站后台页面部分）

- ### 代码实现
    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title></title>
      </head>
      <body>
        <ul type="square">
          <li>百度</li>
          <li>新浪微博</li>
          <li>新浪微博</li>
          <li>新浪微博</li>
          <li>黑马程序员</li>
        </ul>
        <ol type="A" start="3">
          <li><a href="https://www.baidu.com/" target="_self">百度</a></li>
          <li><a href="https://github.com/anliux" target="_blank">GitHub: Anliux</a></li>
          <li>黑马程序员</li>
        </ol>
      </body>
    </html>
    ```

### 代码链接
- []()
- []()

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 网站首页 
- ### 需求分析:
  - 根据产品文档,完成商城首页
  - 显示效果如图: ![]()

- ### 表格标签table
  - table标签的常用的属性: (也可以用到tr/td标签中)
    - border：表格边框的粗细值		
    - bgcolor : 背景色
    - width : 宽度
    - height : 高度
    - align : 对齐方式 (参数：center, left, right, justify(两端对齐))
    - tr 标签：表格的行
    - td 标签：表格的列
  - 注：
    - 表格的行和列需要嵌套，按照table-tr-td的顺序使用
    - 如果m*n的表格没有每一个都赋值，没赋值的单元格会空着，行列末尾的空单元格会没有边框
  - 合并单元格: td的两个属性标签
    - colspan : 跨列操作 eg. `<td colspan="2">x</td>`
    - rowspan : 跨行操作 eg. `<td rowspan="2">x</td>`
	  - colspan和rowspan的参数：表示以本格为基准，横向或纵向合并单元格行或者列的数量
	    - 可以同时使用，即横向和纵向同时合并某几行和某几列 eg.`<td colspan="2" rowspan="2">x</td>`
	  - 注意: 跨行或者跨列操作之后,被占掉的格子需要删除掉
  - 表格的嵌套:
    - 在td中可以嵌套一个表格
    - 在原本方法表格中元素的位置放入新的表格`<table>...</table>`
    - 小技巧：想要让表格中嵌套的小表格填充满，可以使用宽度和高度的100%分别拉满，例如`width="100%"`

- ### 思路技巧
  - 先分析产品需求页面的构成，并按表格划分几行几列，作为框架，后面分每部分进行内容的填充
  - 写代码时：先搭建表格框架，然后填充每部分；填充时，可以先把表格边框显示出来，更清晰
  - 善用width="100%"

- ### 步骤分析
  1. 创建一个8行一列的表格
  2. 第一部份: LOGO部分: 嵌套一个一行三列的表格
  3. 第二部分: 导航栏部分 : 放置5个超链接
  4. 第三部分: 轮播图 
  5. 第四部分: 嵌套一个三行7列表格
  6. 第五部分: 直接放一张图片
  7. 第六部分: 抄第四部分的
  8. 第七部分: 放置一张图片
  9. 第八部分: 放一堆超链接

- ### 代码实现
    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="UTF-8">
        <title></title>

      </head>
      <body>
        <!--
          1. 创建一个8行一列的表格
          2. 第一部份: LOGO部分: 嵌套一个一行三列的表格
          3. 第二部分: 导航栏部分 : 放置5个超链接
          4. 第三部分: 轮播图 
          5. 第四部分: 嵌套一个三行7列表格
          6. 第五部分: 直接放一张图片
          7. 第六部分: 抄第四部分的
          8. 第七部分: 放置一张图片
          9. 第八部分: 放一堆超链接
        -->
        <table  width="100%" >
          <!--第一部份: LOGO部分: 嵌套一个一行三列的表格-->
          <tr>
            <td>
              <table  width="100%">
                <tr>
                  <td>
                    <img src="../img/logo2.png" />
                  </td>
                  <td>
                    <img src="../image/header.jpg" />
                  </td>
                  <td>
                    <a href="#">登录</a>
                    <a href="#">注册</a>
                    <a href="#">购物车</a>
                  </td>
                </tr>
              </table>
            </td>
          </tr>
          <!--第二部分: 导航栏部分 : 放置5个超链接-->
          <tr bgcolor="black">
            <td height="50px">
              <a href="#"><font color="white">首页</font></a>
              <a href="#"><font color="white">手机数码</font></a>
              <a href="#"><font color="white">鞋靴箱包</font></a>
              <a href="#"><font color="white">电脑办公</font></a>
              <a href="#"><font color="white">香烟酒水</font></a>
            </td>
          </tr>
          <!--第三部分: 轮播图 -->
          <tr>
            <td>
              <img src="../img/1.jpg" width="100%" />
            </td>
          </tr>
          <!--第四部分: 嵌套一个三行7列表格-->
          <tr>
            <td>
              <table  width="100%" height="500px"> 
                <tr>
                  <td colspan="7">
                    <h3>最新商品<img src="../img/title2.jpg"></h3>
                  </td>
                </tr>
                <tr align="center">
                  <!--左边大图的-->
                  <td rowspan="2" width="206px" height="480px">
                    <img src="../products/hao/big01.jpg" />
                  </td>
                  <td colspan="3" height="240px">
                    <img src="../products/hao/middle01.jpg" width="100%" height="100%" />								
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                </tr>
                <tr align="center">

                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                </tr>
              </table>
            </td>
          </tr>
          <!--第五部分: 直接放一张图片-->
          <tr>
            <td>
              <img src="../products/hao/ad.jpg" width="100%" />
            </td>
          </tr>
          <!--第六部分: 抄第四部分的-->
          <tr>
            <td>
              <table  width="100%" height="500px"> 
                <tr>
                  <td colspan="7">
                    <h3>热门商品<img src="../img/title2.jpg"></h3>
                  </td>
                </tr>
                <tr align="center">
                  <!--左边大图的-->
                  <td rowspan="2" width="206px" height="480px">
                    <img src="../products/hao/big01.jpg" />
                  </td>
                  <td colspan="3" height="240px">
                    <img src="../products/hao/middle01.jpg" width="100%" height="100%" />								
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                </tr>
                <tr align="center">

                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                  <td>
                    <img src="../products/hao/small06.jpg" />
                    <p>洗衣机</p>
                    <p><font color="red">$998</font></p>
                  </td>
                </tr>
              </table>
            </td>
          </tr>
          <!-- 第七部分: 放置一张图片-->
          <tr>
            <td>
              <img src="../image/footer.jpg" width="100%" />
            </td>
          </tr>
          <!--第八部分: 放一堆超链接-->
          <tr>
            <td align="center">

              <a href="#">关于我们</a>
              <a href="#">联系我们</a>
              <a href="#">招贤纳士</a>
              <a href="#">法律声明</a>
              <a href="#">友情链接</a>
              <a href="#">支付方式</a>
              <a href="#">配送方式</a>
              <a href="#">服务声明</a>
              <a href="#">广告声明</a>
              <br />
    Copyright © 2005-2016 传智商城 版权所有
            </td>
          </tr>
        </table>
      </body>
    </html>

    ```

### 代码链接
- []()


<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 网站注册页面
- ### 需求分析:
  - 编写一个HTML页面
  - 显示效果如图所示：![]()

- ### 表单标签：
  - 表单标签form的参数：
  	- action: 指定提交的地址，对应submit的跳转地址，如路径+网址		
  	- method: 
      - get方式: <默认>提交方式,会将参数(给了name参数的每条input数据)拼接在跳转后的网址后, 有大小限制 -- 4k
      - post方式: 会将参数封装在请求体中, 而不会拼接在网址后；没有大小的限制
  	      - (如果因为路径有中文而错误，可以直接从本地用浏览器打开该文件)
  	- input: 	input的内容放在form标签中间
  - input: 
    - 格式：`文本：<input type="xxxx" name="username" .../><br />`
    - input的参数：
      - type: 指定输入项的类型
      - placeholder : 指定默认的提示信息，显示在还没有输出内容的空格里
      - name : 在表单提交的时候,当作参数的名称
      - id : 给输入项取一个名字, 以便于后期我们去找到它,并且操作它
  - type: 指定输入项的类型，参数如下
    - text : 文本
    - password :  密码框，显示未非明文密码
    - radio :		单选按钮，互斥项需要指定为相同name，则不能同时选
    - checkbox :  复选框，一般多条input-checkbox并列
    - file 	 : 上传文件	
    - date    : 日期类型 (可以在弹出的日历里选择某日期)
    - datetime-local: 日期类型，显示年月日和本地的时分时间
    - tel     : 手机号 (手机应该会唤出小键盘)
    - number   : 只允许输入数字 (输入其他非数字后会提示需要输入数字)
    - textarea : 文本域, 可以输入一段文本
      - cols : 指定宽度，可无单位
      - rows : 指定的是高度，可无单位
    - select  : 下拉列表
      - option : 选择项
      - 格式：select里包option和文本 			
  - 需要包在表单标签里才能生效：
    - submit   : 提交按钮
    - button 	 : 普通按钮
    - reset	 : 重置按钮
    - hidden  : 隐藏域，用来存放页面的一些ID信息				 

- ### 步骤分析
  1. logo部分
  2. 导航栏
  3. 注册部分
  4. 页脚图片
  5. 网站声明信息

- ### 代码示例:
  - 仅展示注册部分，其余部分省略（详见代码链接）
    ```html
    <form action="注册入门案例.html">
      <table width="60%" align="center"> 
        <tr>
          <td colspan="2"><font color="blue" size="5">会员注册</font> USER REGISTER</td>
        </tr>
        <tr>
          <td>用户名:</td>
          <td>
            <input type="text"  placeholder="请输入用户名"/>
          </td>
        </tr>
        <tr>
          <td>密   码:</td>
          <td>
            <input type="password"  placeholder="请输入密码"/>
          </td>
        </tr>
        <tr>
          <td>确认密码:</td>
          <td>
            <input type="password"  placeholder="请再次输入密码"/>
          </td>
        </tr>
        <tr>
          <td>email:</td>
          <td>
            <input type="text"  placeholder="请输入邮箱"/>
          </td>
        </tr>
        <tr>
          <td>姓名:</td>
          <td>
            <input type="text"  placeholder="请输入真实姓名"/>
          </td>
        </tr>
        <tr>
          <td>性别:</td>
          <td>
            <input type="radio" name="sex" /> 男
            <input type="radio" name="sex" /> 女
            <input type="radio" name="sex" /> 妖
          </td>
        </tr>
        <tr>
          <td>出生日期:</td>
          <td>
            <input type="date"  />
          </td>
        </tr>
        <tr>
          <td>验证码:</td>
          <td>
            <input type="text"  />
          </td>
        </tr>
        <tr>
          <td></td>
          <td>
            <input type="submit" value="注册"  />
          </td>
        </tr>
      </table>
    </form>
    ```

- ### 代码链接
  - [表单demo.html]()
  - 

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 网站后台页面展示
- ### 需求分析:
  - 我们前面已经做完了首页商品展示, 那么我们需要一个页面用来编辑我们的商品信息, 还有商品分类, 用户购买之后,还得有订单管理页面
  - 本部分主要讲：从框架角度，对页面布局进行分区，例如邮箱主页(第一行一列，第二行两列且左窄右宽)

- ### frameset
  - 框架标签: frameset
    - 对页面进行分区
  - 注意: 使用了frameset必须将body删掉,否则页面会有问题
  - 格式：frameset设置行列比，里面的frame设置每个页面对应的源文件
    - 设置行列比：cols/rows="百分比，逗号隔开，最后一个可以用星号代替"
  - frame的常用属性:
    - src: 引入的html文件路径
    - name: 指定框架的名称

- ### 代码示例
    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title></title>
      </head>
      <frameset cols="10%, 50%, *">
        <frame src="aaa.html"/>
        <frame src="bbb.html"/>
        <frame src="ccc.html"/>
      </frameset>
    </html>
    ```

- ### 框架中点击跳转
  - 概述：
    - 将某个frame进行命令，如name="rightFrame"
    - 然后可以在超链接中设置targe="rightFrame"
    - 则这个超链接的跳转会显示在指定的frame里
  - 场景：点左侧框架中的收件箱，会在右侧框架中显示收件箱页面

- ### 步骤分析
  - 首先分区：先分区两行，后在第二行再次分区两列
  - 收件箱跳转：指定data文件；设置右框架name；左分区的源文件写超链接a指向data文件，并收件箱target设为右框架
  - 注意：右框架名：在后台页面设置(分区页面)，而左分区的跳转是在左分区指向的源文件中设置

- ### 代码实现
    ```html
    <!--网站后台页面.html-->
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title></title>
      </head>
      <frameset rows="15%,*">
        <frame src="aaa.html"/>
        <frameset cols="15%,*">
          <frame src="bbb.html" />
          <frame src="ccc.html" name="rightFrame" />
        </frameset>
      </frameset>
    </html>

    <!--bbb.html-->
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title></title>
      </head>
      <body bgcolor="green">
        <a href="data.html" target="rightFrame">收件箱</a><br />
        <a href="#">发件箱</a><br />
        <a href="#">垃圾箱</a><br />	
      </body>
    </html>
    ```

### 代码链接
- []()

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 内容回顾
- 网站信息案例
  - 字体标签 font
    - color: 颜色
    - size:  大小 1~7
    - face: 改变字体
  - p 段落标签
  - h标题标签 : 1~6
  - br 换行
  - hr 水平线
  - b 加粗
  - i  斜体
  - strong : 加粗  包含语义
  - em : 斜体  包含语义
- 网站图片案例
  - img标签
    - src : 指定图片的路径
    - width: 宽度
    - height: 高度 - 注意，不是heigth
    - alt : 图片加载错误时的提示信息
  - 相对路径:
    - ./  代表的是当前路径
    - ../  代表的上一级路径
    - ../../ 代表的上上一级路径
- 友情链接:
  - ul: 无序列表
    - type :
  - ol: 有序列表
    - type : 样式
    - start : 起始索引
  - li : 列表项
  - a 超链接标签
    - href : 要访问的链接地址
    - target : 打开方式
- 网站首页
  - table标签
    - border: 指定边框 (参数为"xx px")
    - width : 宽度 (参数为"xx px")
    - height : 高度 (参数为"xx px")
    - bgcolor : 背景颜色 (参数为"red/yellow"等)
    - align : 对齐方式 (参数为"center"等)
      - 注：table居中指表格相对整个页面居中，tr/td居中指单元格中的文字居中
  - tr标签
  - td标签
    - colspan: 跨列操作
    - rowspan: 跨行操作
  - 表格单元格的合并
  - 表格的嵌套
- 网站注册页面：
  - 表单标签form的参数：
    - action: 指定提交的地址，对应submit的跳转地址，如路径+网址		
    - method: 打开方式 get/post
    - input:  input的内容放在form标签中间
  - input: 输入标签
    input的参数：
    - type: 指定输入项的类型
    - placeholder : 指定默认的提示信息，显示在还没有输出内容的空格里
    - name : 在表单提交的时候,当作参数的名称
    - id : 给输入项取一个名字, 以便于后期我们去找到它,并且操作它  
  - type: 指定输入项的类型 - 参数如下
    - text : 文本
    -	password :  密码框，显示未非明文密码
    - radio :		单选按钮，互斥项需要指定为相同name，则不能同时选
     -checkbox :  复选框，一般多条input-checkbox并列
    - file 	 : 上传文件	
    - date    : 日期类型 (可以在弹出的日历里选择某日期)
    - datetime-local: 日期类型，显示年月日和本地的时分时间
    - tel     : 手机号 (手机应该会唤出小键盘)
    - number   : 只允许输入数字 (输入其他非数字后会提示需要输入数字)
    - textarea : 文本域, 可以输入一段文本
    - cols : 指定宽度，可无单位
    - rows : 指定的是高度，可无单位
    -	select  : 下拉列表
    	-	option : 选择项 (格式：select里包option和文本)
  - 需要包在表单标签里才能生效：
    -	submit: 提交按钮
    -	button: 普通按钮
    -	reset: 重置按钮
    -	hidden: 隐藏域，用来存放页面的一些ID信息
- 网站后台页面:
  - 框架标签frameset：
    - 设置行列比：cols/rows
    - 内嵌若干frame
  - frame的常用属性:
    - src: 引入的html文件路径
    - name: 指定框架的名称 (框架中点击跳转可用)

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 参考链接
- [菜鸟教程：HBuilder的使用](https://www.runoob.com/w3cnote/hbuilder-intro.html)
- [菜鸟教程：HTML](https://www.runoob.com/html/html-tutorial.html)
- [w3school](https://www.w3school.com.cn/)

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



### END
