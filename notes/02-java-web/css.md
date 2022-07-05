# CSS入门

## 目录
<!--GFM-TOC -->
- [案例导航](#案例导航): 本期案例汇总
- [使用CSS完成网站首页的优化](#使用css完成网站首页的优化): 
- [使用div和CSS完成注册页面的优化](#使用div和css完成注册页面的优化): 
- [CSS部分小结](#css部分小结): 
<!--GFM-TOC -->



## 案例导航
- 使用CSS完成网站首页的优化
- 使用CSS完成网站注册页面的优化

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 使用CSS完成网站首页的优化
- ### 需求分析:
  - 由于使用html表格布局存在缺陷,那么我们要来考虑使用div+CSS来对页面进行优化
  - 表格布局的缺陷:
    - 嵌套层级太多, 一旦出现嵌套顺序错乱, 整个页面达不到预期效果
    - 采用表格布局,页面不够灵活, 动其中某一块,整个表格布局的结构全都要变
  
- ### 图片效果：
  - [网站首页-步骤分析]() 

- ### HTML的块标签:
  - div标签: 默认占一行, 自动换行
    - 代码示例：
    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title></title>
      </head>
      <body>
        <div>下雨了吗？</div>
        <div>下雨了吗？</div>
        <div>下雨了吗？</div>
        <div>下雨了吗？</div>
        <div>下雨了吗？</div>
        <div>下雨了吗？</div>
      </body>
    </html>
    ```
  - span标签: 内容显示在同一行
    - 代码示例：
    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title></title>
      </head>
      <body>
        <span>下雨了</span>
        <span>下雨了</span>
        <span>下雨了</span>
        <span>下雨了</span>
        <span>下雨了</span>
      </body>
    </html>
    ```

- ### CSS概述:
  - Cascading Style Sheets : 层叠样式表
    - 类比：红砖, 抹了一层水泥, 白灰
  - 主要用作用:
    - 用来美化HTML页面：HTML决定网页的骨架, CSS化妆，
    - 将页面的HTML和美化进行分离: 代码更简洁好管理
  - CSS的简单语法:
    - 在一个style标签中,去编写CSS内容,最好将style标签写在这个head标签中
    - 注：html是在body标签中写入内容
    - 示例：
    ```html
    <!--语法规则：-->
    <style>
      选择器{
        属性名称:属性的值;
        属性名称2: 属性的值2;
      }
    </style>

    <!--代码示例-->
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title></title>
        <style>
          div{
            color: brown;
            font-size: 50px;
          }
        </style>
      </head>
      <body>
        <!-- 改为红色字体，50像素字号 -->
        <div>恭喜发财</div>
        <div>红包拿来</div>
        <div>年年有余</div>
      </body>
    </html>
    ```

- ### CSS选择器: 
  - 选择器概述：
    - 帮助我们找到我们要修饰的标签或者元素(标签也叫元素)
    - 格式：注意每一行中间的冒号，结尾的分号
  - 元素选择器: 
    - 普适，标签名调用
    - 示例：
    ```html
    <!--语法规则：-->
    元素的名称{
      属性名称:属性的值;
      属性名称:属性的值;
    }

    <!--代码示例-->
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title></title>
        <style>
          span{
            color: coral;
          }/!--所有span的内容都改变颜色--/
        </style>
      </head>
      <body>
        <span>今天还下课吗？今天肝到地老天荒</span>
        <span>今天还下课吗？今天肝到地老天荒</span>
        <span>今天还下课吗？今天肝到地老天荒</span>
      </body>
    </html>
    ```
  - ID选择器: 
    - 先指定ID，后面才能使用ID
    - ID在整个页面中必须是唯一的(这里没问题，后面别的知识点有问题，只会识别第一个)
    - ID属性不要以数字开头，数字开头的ID在 Mozilla/Firefox 浏览器中不起作用。
    - 优先级：ID > 元素
    - 示例：
	```html
	<!--语法规则：-->
	以#号开头  
	#ID的名称{
	  属性名称:属性的值;
	  属性名称:属性的值;
	}

	<!--代码示例-->
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="utf-8">
			<title></title>
			<style>
				div{
					font-size: 60px;
				}
				#div10086{
					color: red;
				}
				#div1{
					color: green;
				}
			</style>
		</head>
		<body>
			<div id="div10086">java是世界上最好的语言</div>
			<div id="div1">PHP是世界上最好的语言</div>
			<div>c++是世界上最好的语言</div>
		</body>
	</html>
	```
  - 类选择器:
    - 先指定类，后面才能使用类
    - 用法类似ID选择器，但class可以在多个元素中使用 (对应ID的唯一性)
    - 类名的第一个字符不能使用数字！它无法在 Mozilla 或 Firefox 中起作用。
    - 优先级：ID > 类 > 元素
    - 示例：
	```html
	<!--语法规则：-->
	以 . 开头 
	.类的名称{
	   属性名称:属性的值;
		属性名称:属性的值;
	}

	<!--代码示例-->
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="utf-8">
			<title></title>
			<style>
				.fruit{
					color: red;
				}
				.vegetable{
					color: green;
				}
			</style>
		</head>
		<body>
			<div class="fruit">桃子</div>
			<div class="fruit">苹果</div>
			<div class="vegetable">茄子</div>
			<div class="fruit">菠萝</div>
			<div class="vegetable">青椒</div>
		</body>
	</html>
	```
  - 选择器分组: 
    - 格式：选择器1,选择器2{属性的名称:属性的值}
  - 属性选择器:
    - 示例：
     ```html
      a[title]：包含某属性
      a[titile='aaa']：包含属性为xx的语句 
      a[href][title]：同时包含多个属性
      a[href][title='aaa']：同时包含多个属性且属性值为xx的语句
     ``` 
  - 后代选择器: 
    - 格式：爷爷选择器 孙子选择器{}   
      - 空格隔开，找出所有的后代
  - 子元素选择器:  
    - 格式：父选择器  > 儿子选择器{} 
      - 只筛选子类，不包含子类的子类
  - 伪类选择器: 通常都是用在A标签上，超链接不同的点击状态显示不同的颜色
    - 代码示例： 略

- ### CSS的优先级
  - 按照选择器搜索精确度来编写: 
    - 行内样式 > ID选择器 > 类选择器  > 元素选择器
  - 就近原则: 哪个离得近,就选用哪个的样式：
    - 例如：同一行指定多个class时，按类选择器，style里的哪个选择器更靠近这一行就优先显示哪个
    - 更靠近：先class A，后写class B，则A距离下方代码更远，B拥有优先权         	

- ### CSS的引入方式:
  - 外部样式: 
    - 通过link标签引入一个外部的css文件(head标签内用link标签指向一个外部的css文件)
    - 思路：
      - 类似于把某方法集成到一个方法中，然后调用。
      - 这样方便改动时不需要每个调用的文件里都进行修改了 
      - 提高了代码复用性
    - css文件仅包含style里的部分，而在html中，需要把style标签删掉，并使用link标签调用css文件
    - 注意link格式：
      - `<link rel="stylesheet" href="style1.css"/>` -- 不自动显示时需要知道格式
    - 示例：
	```html
	<!--外部样式示例 -->
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="utf-8">
			<title></title>
			<link  rel="stylesheet" href="style1.css"/>
		</head>
		<body>
			<div class="fruit">橘子</div>
			<div class="fruit">西瓜</div>
			<div class="vegetable">洋葱</div>
			<div class="fruit">菠萝</div>
			<div class="vegetable">番茄</div>
		</body>
	</html>
	```

	```css
	/* style.css: 抽取出的css文件 */
	.fruit{
		color: pink;
	}
	.vegetable{
		color: green;
	}
	```
  - 内部样式: 
    - 直接在style标签内编写CSS代码(例如上面在html文件内的head标签内的style标签写)
  - 行内样式: 
    - 直接在标签中添加一个style属性, 编写CSS样式(语法同css语法)
    - 注意：行内style的引号里，每个样式设置完以后都要用分号作为结束，不要忘记
    - 注：仅针对某一行的格式，即使标记了类，也只能修改指定的行
    - 示例：
	```html
	<!--行内样式示例-->
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="utf-8">
			<title></title>
		</head>
		<body>
			<div class="fruit" style="color: green;">桃子</div>
			<div class="fruit">苹果</div>
			<div class="vegetable">茄子</div>
			<div class="fruit">菠萝</div>
			<div class="vegetable">青椒</div>
		</body>
	</html>
	```

- ### CSS浮动 : 
  - 浮动概述：
    - 浮动的元素会脱离正常的文档流,在正常的文档流中不占空间
    - 可应用于图片：
      - 使得文字环绕在图片周围 (注: 如果是div色块如示例，会叠在一起)
    - 元素的水平方向浮动，意味着元素只能左右移动而不能上下移动。
      - 一个浮动元素会尽量向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。
    - 浮动元素之后的元素将围绕它；浮动元素之前的元素将不会受到影响。
  - 浮动属性：
    - float属性: left / right
    - clear属性: 清除浮动
      - 应用：两行浮动会叠在一起，这时可以清楚浮动把他们隔开，相当于手动给浮动换行
      - both : 两边都不允许浮动
      - left: 左边不允许浮动
      - right : 右边不允许浮动
      - 注意：
        - clear是添加在浮动模块之间的，可以设为空模块，不是在下面的模块里添加clear
    - 浮动：流式布局
    - 示例：
	```html
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="utf-8">
			<title></title>
		</head>
		<body>
			<div style="float: left; background-color: red; width: 200px; height: 300px;"></div>
			<div style="float: left; background-color: blue; width: 200px; height: 300px;"></div>
			<div style="float: left; background-color: green; width: 200px; height: 300px;"></div>
			<div style="float: left; background-color: red; width: 200px; height: 300px;"></div>

			<div style="clear: both;"></div>

			<div style="float: left; background-color: blue; width: 200px; height: 300px;"></div>
			<div style="float: left; background-color: green; width: 200px; height: 300px;"></div>
			<div style="float: left; background-color: red; width: 200px; height: 300px;"></div>
		</body>
	</html>
	```

- ### css网站首页优化的步骤分析:
	1. 创一个最外层div
	2. 第一部份: LOGO部分: 嵌套三个div
	3. 第二部分: 导航栏部分 : 放置5个超链接
	4. 第三部分: 轮播图 
	5. 第四部分: < 重点！！ >
	6. 第五部分: 直接放一张图片
	7. 第六部分: 抄第四部分的
	8. 第七部分: 放置一张图片
	9. 第八部分: 放一堆超链接

- ### 代码实现:
	```html
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="UTF-8">
			<title></title>
			<style>

				.logo{
					float: left;
					width: 33%;
					/*border-width: 1px;
					border-style: solid;
					border-color: red;*/
					height: 60px;
					line-height: 60px;
			/*		border: 1px solid red;*/
				}


				.amenu{
					color: white;
					text-decoration: none;
					height: 50px;
					line-height: 50px;
				}

				.product{
					float: left; text-align: center; width: 16%; height: 240px;
				}

			</style>
		</head>
		<body>
			<!--
				1. 创一个最外层div
				2. 第一部份: LOGO部分: 嵌套三个div
				3. 第二部分: 导航栏部分 : 放置5个超链接
				4. 第三部分: 轮播图 
				5. 第四部分: 
				6. 第五部分: 直接放一张图片
				7. 第六部分: 抄第四部分的
				8. 第七部分: 放置一张图片
				9. 第八部分: 放一堆超链接
			-->
			<div>
				<!--2. 第一部份: LOGO部分: 嵌套三个div-->
				<div>
					<div class="logo">
						<img src="../img/logo2.png"/>
					</div>
					<div class="logo">
						<img src="../img/header.png"/>
					</div>
					<div class="logo">
						<a href="#">登录</a>
						<a href="#">注册</a>
						<a href="#">购物车</a>
					</div>
				</div>


				<!--清除浮动-->
				<div style="clear: both;"></div>


				<!--3. 第二部分: 导航栏部分 : 放置5个超链接-->
				<div style="background-color: black; height: 50px;">
					<a href="#" class="amenu">首页</a>
					<a href="#" class="amenu">手机数码</a>
					<a href="#" class="amenu">电脑办公</a>
					<a href="#" class="amenu">鞋靴箱包</a>
					<a href="#" class="amenu">香烟酒水</a>
				</div>


				<!--4. 第三部分: 轮播图--> 
				<div>
					<img src="../img/1.jpg" width="100%"/>
				</div>
				<!--5. 第四部分:--> 
				<div>
					<div><h2>最新商品<img src="../img/title2.jpg"/></h2></div>

					<!--左侧广告图-->
					<div style="width: 15%; height: 480px;  float: left;">
						<img src="../products/hao/big01.jpg" width="100%" height="100%"/>
					</div>
					<!--
				右侧商品
			-->
			<div style="width: 84%; height: 480px;float: left;">
				<div style="height: 240px; width: 50%; float: left;">
					<img src="../products/hao/middle01.jpg" height="100%" width="100%" />
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>

			</div>
				</div>

				<!--6. 第五部分: 直接放一张图片-->
				<div>
					<img src="../products/hao/ad.jpg" width="100%"/>
				</div>
				<!--7. 第六部分: 抄第四部分的-->
				<div>
					<div><h2>最新商品<img src="../img/title2.jpg"/></h2></div>

					<!--左侧广告图-->
					<div style="width: 15%; height: 480px;  float: left;">
						<img src="../products/hao/big01.jpg" width="100%" height="100%"/>
					</div>
					<!--
				右侧商品
			-->
			<div style="width: 84%; height: 480px;float: left;">
				<div style="height: 240px; width: 50%; float: left;">
					<img src="../products/hao/middle01.jpg" height="100%" width="100%" />
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>
						<div class="product">
					<img src="../products/hao/small08.jpg" />
					<p>高压锅</p>
					<p style="color: red;">$998</p>
				</div>

			</div>
				</div>

				<!--8. 第七部分: 放置一张图片-->
				<div>
					<img src="../img/footer.jpg" width="100%"/>
				</div>
				<!--9. 第八部分: 放一堆超链接-->
				<div style="text-align: center;">

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
				</div>
			</div>
		</body>
	</html>
	```

- ### 代码链接：
  - []()
 
<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC --> 



## 使用div和CSS完成注册页面的优化
- ### 需求分析
  - 由于html的注册页面也是用table布局的, 存在与首页同样的问题
  - 所以我们需要使用div+css对我们的注册页面进行美化
  - 总共是5部分内容

- ### 图片效果
  - [注册页面]() 

- ### 盒子模型
  - CSS的盒子模型: 万物皆盒子
  - 图片实例：
    - [盒子模型.png]() 
    - [盒子模型2.png]()
  - 内边距: 
    - padding-top:
    - padding-right:
    - padding-bottom:
    - padding-left:
    - 直接指定边距：默认按照顺时针上右下左的顺序赋值 <笔试可能的考点>

	```html
	padding: 10px;  上下左右都是10px
	padding:10px 20px;  上下是10px 左右是20px
	padding: 10px 20px 30px;  上 10px 右20px  下30px  左20px
	padding: 10px 20px 30px 40px;  上右下左, 顺时针的方向
	```
  - 外边距:
    - margin-top:
    - margin-right:
    - margin-bottom:
    - margin-left: 
  - 代码链接：
    - [盒子模型.html]() 

- ### CSS绝对定位:
  - position: absolute -- 参考物是绝对的网页边框，即网页的上边框和左边框
    - top: 控制距离顶部的位置
    - left: 控制距离左边的位置
    - 注：只有前面声明过绝对位置，后面的top、left才有效
  - 代码示例：
    - [绝对定位.html]()

- ### 步骤分析:
	1. 总共是5部分
	2. 第一部分是logo部分
	3. 第二部分是导航菜单
	4. 第三部分是注册部分
	5. 第四部分是footer图片
	6. 第五部分是一堆超链接

- ### 代码实现:
	```html
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="UTF-8">
			<title></title>
			 <link rel="stylesheet" type="text/css" href="../css/main.css"/>
		</head>
		<body>
			<!--
				1. 总共是5部分
				2. 第一部分是LOGO部分
				3. 第二部分是导航菜单
				4. 第三部分是注册部分
				5. 第四部分是FOOTER图片
				6. 第五部分是一堆超链接
			-->
			<div>

				<!--2. 第一部分是LOGO部分-->
				<div>
					<div class="logo">
						<img src="../img/logo2.png" />
					</div>
					<div class="logo">
						<img src="../img/header.png" />
					</div>
					<div class="logo">
						<a href="#">登录</a>
						<a href="#">注册</a>
						<a href="#">购物车</a>
					</div>
				</div>

				<!--清除浮动-->
				<div style="clear: both;"></div>
				<!--3. 第二部分是导航菜单-->
				<div style="background-color: black; height: 50px;">
					<a href="#" class="amenu">首页</a>
					<a href="#" class="amenu">手机数码</a>
					<a href="#" class="amenu">电脑办公</a>
					<a href="#" class="amenu">鞋靴箱包</a>
					<a href="#" class="amenu">香烟酒水</a>
				</div>
				<!--4. 第三部分是注册部分-->
				<div style="background: url(../image/regist_bg.jpg);height: 500px;">

					<div style="position:absolute;top:200px;left:350px;border: 5px solid darkgray;width: 50%;height: 50%;background-color: white;">
						<table width="60%" align="center">
							<tr>
								<td colspan="2"><font color="blue" size="6">会员注册</font>USER REGISTER</td>

							</tr>
							<tr>
								<td>用户名:</td>
								<td><input type="text"/></td>
							</tr>
							<tr>
								<td>密码:</td>
								<td><input type="password"/></td>
							</tr>
							<tr>
								<td>确认密码:</td>
								<td><input type="password"/></td>
							</tr>
							<tr>
								<td>email:</td>
								<td><input type="email"/></td>
							</tr>
							<tr>
								<td>姓名:</td>
								<td><input type="text"/></td>
							</tr>
							<tr>
								<td>性别:</td>
								<td><input type="radio" name="sex"/> 男
								<input type="radio" name="sex"/> 女
								<input type="radio" name="sex"/> 妖
								</td>
							</tr>
							<tr>
								<td>出生日期:</td>
								<td><input type="date"/></td>
							</tr>
							<tr>
								<td>验证码:</td>
								<td><input type="text"/></td>
							</tr>
							<tr>
								<td></td>
								<td><input type="submit" value="注册"/></td>
							</tr>
						</table>
					</div>

				</div>

				<!--5. 第四部分是FOOTER图片-->
				<div>
					<img src="../img/footer.jpg" width="100%"/>
				</div>
				<!--9. 第四部分: 放一堆超链接-->
				<div style="text-align: center;">

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
				</div>
			</div>
		</body>
	</html>
	```

- 代码链接：
  - [网站注册css优化.html]() 


<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## CSS部分小结
- CSS: 层叠样式表.
- CSS作用: 美化页面,提高代码的复用性
- 选择器:
  - 需要掌握的:
    - 元素选择器: 标签的名称
    - 类选择器:  以 '.' 开头
    - ID选择器: 以#开头,  #ID的名称  ID必须是唯一的
    - 优先级: 
      - 按照选择精确度: 行内样式  > ID选择器 > 类选择器 > 元素选择器
      - 就近原则
  - 扩展选择器:
    - 选择器分组:  选择器1,选择器2   以逗号隔开
    - 后代选择器:  爷爷 孙子   中间以空格隔开
    - 子元素选择器:  爸爸 > 儿子 
    - 属性选择器:   选择器[属性的名称='']
    - 伪类选择器:  超链接标签上使用  
- 浮动: float属性  left right
  - 清除浮动: clear: both left right
- 盒子模型:  顺时针 : 上右下左
  - padding : 内边距 ,控制的是盒子内容的距离
  - margin : 外边距 控制盒子与盒子之间的距离
  - 绝对定位: position: absolute
    - top:
    - left:

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



### END
