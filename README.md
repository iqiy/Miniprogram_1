# Miniprogram_1
# 小程序开发学习

### Ⅰ 小程序可以做什么

1. 同app进行互补
2. 连接线上线下,可直接云端更新
3. 开发门槛低,成本低
4. 双线程模型,逻辑层和渲染层分开加载



### Ⅱ 开发前工作

1. 申请appID
2. 下载开发工具



### Ⅲ 小程序的数据绑定

- this.setData()
- bindtap绑定事件



### Ⅳ 小程序的MVVM架构

- MINA框架

- 小程序的很多开发需求被规定在配置文件中

- 常见配置文件

  - project.config.json 项目配置文件

  - sitemap.json 配置小程序及其页面是否允许被微信索引

  - app.json 全局配置

    - pages 用于指定小程序由哪些页面组成
    - window 用于指定窗口如何展示
    - tabBar 用于配置导航栏

  - page.json 页面配置

    

### Ⅴ 小程序的双线程模型

- 宿主环境: 微信客户端
- 双线程
  - 渲染层: WebView执行(wxml,wxss) 
  - 逻辑层: JSCore执行(js)
- 界面渲染过程: wxml+js+wxss文件,先转成JS对象,再转成真正的DOM树,渲染到界面



### Ⅵ 小程序生命周期函数

- APP(启动完成后台存活两小时)
  - onLaunch: 小程序初始化完成执行
  - onShow: 小程序界面显示出来执行
  - onHide: 界面被隐藏时执行
  - onError: 发生错误执行
- 注册App时做什么
  - 判断进入场景
  - 监听生命周期函数
  - 存放全局共享数据
- 注册页面做什么
  - 在生命周期函数中发送网络请求,从服务器获取数据
    - 页面周期函数
      1. onLoad: 页面被加载出来执行
      2. onShow: 页面显示出来执行
      3. onReady: 页面初次渲染完成时执行
      4. onHide: 页面被隐藏执行
      5. onUnload: 关闭页面时执行
  - 初始化一些数据
  - 监听wxml中的相关事件



### Ⅶ 内置常用组件

- Text组件
  - selectable属性,文本是否可选
  - space属性, 显示连续空格,决定空格大小(nbsp, ensp, emsp)
  - decode属性, 是否解码文本
- Button组件
  - size属性,控制按钮大小
  - type属性,控制按钮颜色
  - plain属性,中空效果
  - disable属性,不可用
  - loading属性,加载中效果
  - hover-class属性,指定按钮按下去的样式类
  - open-type属性,用户获取一些特殊性的权限,可以绑定一些特殊事件
- View组件
  - 块级元素,独占一行,类似div
  - class属性,添加样式类
  - hover-class属性,指定按下去的样式类
  - hover-stop-propagation属性,指定是否阻止本节点的祖先节点出现点击态
  - hover-start-time属性,按住后多久出现点击态,单位毫秒
  - hover-stay-time属性,手指松开后点击态保留时间,单位毫秒
- Image组件,默认大小320*240,行内块级元素
  - src属性,图片资源地址
  - mode属性,图片裁剪,缩放的模式
    - 默认值: scaleToFill 缩放模式，不保持纵横比缩放图片，使图片的宽高完全拉伸至填满 image 元素
    - aspectFit 缩放模式，保持纵横比缩放图片，使图片的长边能完全显示出来。也就是说，可以完整地将图片显示出来。
  - lazy-load属性,懒加载,在即将进入一定范围（上下三屏）时才开始加载,默认为false
  - binLoad属性,监听图片加载完成时触发
  - show-menu-by-longpress属性,开启长按图片显示识别小程序码菜单
- Input组件,用于接收用户的输入信息
  - value属性,输入框中的默认值
  - type属性,input 的类型,默认是text
  - placeholder属性,设置占位文字
  - confirm-type属性,设置键盘右下角按钮的文字，仅在type='text'时生效
  - bindinput属性,键盘输入时触发
- Scroll-view组件,实现局部滚动
  - scroll-x属性,水平滚动
  - scroll-y属性,垂直滚动
  - bindscroll属性,滚动时触发事件
- 组件的共同属性
  - id 组件唯一标识
  - class 组件的样式类
  - style 组件的内联样式
  - hidden 组件是否显示
  - data-* 自定义属性
  - bind\*/catch\* 组件的事件



### Ⅷ wxss&wxml&wxs

#### 1.wxss

- 页面样式的三种写法,优先级: 行内>页内>全局
  - 行内样式/内联样式,直接在标签内添加style属性
  - 页内样式,添加样式类class,在相应的wxss文件中设置样式
  - 全局样式,添加样式类class,在全局的app.wxss文件中设置样式
- 小程序支持的选择器,权重分配: ! Important > style="" > #id > .class > element
  - .class
  - \#id
  - element
  - ::after 
  - ::before
- wxss中的单位: rpx ,可自适应屏幕大小,规定屏幕宽度为750rpx
- wxss的样式导入,使用 @import ' ' 导入其他样式文件
  - 官方样式库: github.com/Tencent/weui-wxss

#### 2.wxml

- 格式类似于html
- 大小写敏感
- 逻辑判断
  - wx:if
  - wx:elif
  - wx:else
- hidden和wx:if在隐藏组件时的区别
  - hidden隐藏,组件依然存在
  - wx:if隐藏,组件没有被创建
- 列表渲染-wx:for
  - 遍历数组需要写在 {{}} 中,遍历出的每个元素名称默认为item,索引为index
  - wx:for-item="" , wx:for-index="" 可以指定遍历的名称和索引,便于多层遍历名称重复
  - {{}}中为数字,可以直接遍历这个数字
  - 使用wx:for需要绑定一个wx:key属性,提高性能
    - 列表中插入新元素,如果没有key,后面的所有元素的位置都会改变
- block标签
  - 只是包装元素
  - 包裹一组标签,便于对一组标签进行相同操作
  - 性能高,代码可读性好
- template标签
  - 为了进行代码的复用,需要有name属性,使用模板时用is属性指定模板的name
  - 模板中的内容,没有被引用的时候,不会生效
  - 模板文件导入不能使用include,只能使用import,且不能递归导入;include不能导入template/wxs,但是可以进行递归导入

#### 3.wxs

- 小程序的脚本语言,与JavaScript不同,类似于过滤器
- wxml不能直接调用Page/Component中定义的函数
- wxs的两种写法
  - wxml中写wxs代码需要在wxs标签中写,且需要有module属性,wxml元素想要使用还需要有exports导出
  - 定义在单独的wxs文件中,再使用wxs标签进行导入,必须使用相对路径

#### 4.Mustache语法

- {{ }} 取值,内容也可以是表达式,三目运算也可以使用

  

###  Ⅸ 事件

- 常见事件
  - touchstart 手指触摸动作开始
  - touchmove 手指触摸后移动
  - touchcancel 手指触摸动作被打断
  - touchend 手指触摸动作结束
  - tap 点击
  - longpress 手指触摸后,超过350ms再离开
- 事件对象
  - 当某个事件触发时,会产生一个事件对象,并且这个对象被传入到回调函数中
    - 事件对象属性:
      1. type(事件类型) 
      2. timeStamp(时间戳) 
      3. target(触发事件的组件的属性集合) 
      4. currentTarget(当前组件的一些属性值集合)
      5. detail(额外信息,) 
      6. touches(触摸事件,记录当前停留在屏幕中的触摸点信息的数组) 
      7. changedTouches(触摸事件,记录当前变化的触摸点信息的数组)
    - touches和changedTouches的区别
      1. 在touchend中不同
      2. 多指触摸时不同
- 事件的参数传递
  - 传递: data-属性名
  - 获取: event.currentTarget.dataset.属性名
- 事件冒泡和事件捕获
  - bind: 一层层传递, catch: 阻止事件进一步传递
  - 事件捕获从外向内: capture-bind/capture-catch
  - 事件冒泡从内向外: bind/catch



### Ⅹ 组件化开发

- 组件化: 拆分功能模块

- 自定义组件

  - 由 json wxml wxss js 文件组成
  - 首先需要在json文件中进行自定义组件声明,将component字段设为true
  - 标签名只能使用小写字母,中划线,下划线,不要以 wx-为前缀
  - 自定义组件中也可以引用其他自定义组件,需要进行注册之后才能使用

- 使用自定义组件时,需要在相应的 json 文件中进行注册

- 在全局 app.json 文件中注册自定义组件之后,在其他页面中都可以使用

- 组件中不允许使用id选择器,属性选择器,标签选择器

- 组件和样式页面细节

  - 组件中的样式类与宿主页面的样式类互不影响,options属性的styleIsolation默认值为isolated
  - 在组件的js文件中配置options属性的styleIsolation为apply-shared,页面样式类会影响组件样式类
  - 在组件的js文件中配置options属性的styleIsolation为shared,会相互影响

- 组件和页面通信

  - 给自定义组件传递数据-properties
  - 给自定义组件传递样式-externalClasses

- 组件向外传递事件

  - 子组件监听事件的发生,并把事件发送出去 this.triggerEvent()
  - 父组件监听子组件的事件,再绑定对应的事件

- 获取组件对象的方式

  - this.selectComponent('class/id')

- 插槽slot

  - 可以替换组件中的slot标签
  - 使用多插槽,需要给每一个插槽设置name属性,且需要在组件的js文件中设置options属性的multipleSlots为true

- Component构造器

  - properties: 定义传入的属性

  - data: 定义内部属性

  - methods: 定义方法

  - options: 额外配置选项

  - externalClasses: 引用外部样式

  - observers: 属性和数据监听

  - pageLifetimes: 页面生命周期

    - show(): 监听页面显示
    - hide(): 监听页面隐藏
    - resize(): 监听页面尺寸改变

  - lefetimes: 组件生命周期

    - created(): 监听组件被创建

    - attached(): 组件被添加到页面

    - ready(): 组件被渲染出来

    - moved(): 组件被移动到另一个节点

    - detached(): 组件被移除

      

### ⅩⅠ 网络请求

- 简单的网络请求 wx.request()

  - url: 服务器接口地址
  - data: 请求参数
  - header: 请求头
  - method: 请求方法
  - dataType: 返回数据格式

- 封装请求方法

- ```js
  export default function request(options){
  	return new Promise(resolve, reject) => {
  		wx.request({
  			url: options.url,
  			method: options.method || 'get',
  			data: options.data || {},
  			success: resolve,
  			fail: reject
  		})
  	}
  }
  ```



### ⅩⅡ 小程序展示弹窗

- wx.showToast
- wx.showModal
- wx.showLoading
- wx.showActionSheet



### ⅩⅢ 小程序页面分享

- js文件中配置onShareAppMessage
  - title: 展示标题
  - path: 分享的路径
  - imageUrl: 分享展示图片
- 设置button的open-type属性为share,可以直接调用onShareAppMessage



### ⅩⅣ 小程序登录流程

1. 调用wx.login获取code
2. 调用wx.request发送code到我们自己的服务器(服务器会返回一个登录态标识,比如token)
3. 将登录态的的标识token存储,以便下次使用
4. 请求需要登录态标准的接口时,携带token



### ⅩⅤ 小程序页面跳转

- 通过navigator组件跳转
  - url: 指定跳转路径
  - open-type: 指定跳转类型
    - navigate: 默认跳转方式
    - redirect: 跳转会关闭当前页面
    - switchTab: 跳转tabbar页面
    - relaunch: 跳转会关闭其他所有页面
    - navigateBack: 返回跳转
    - navigateBack delta="2",返回两级
- 通过wx的API跳转
  - wx.navigateTo()
  - wx.redirectTo()
  - wx.navigateBack()
- 跳转过程中的数据传递
  - 参数可以通过 ? 连接在url上











