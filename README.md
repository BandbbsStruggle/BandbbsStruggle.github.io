# 小米手环8 小程序表盘 开发文档

#### 小米手环8的js渲染依赖于JerryScript

##### JerryScript 
物联网设备在CPU性能和内存空间方面皆存在严格受限，在使用V8引擎这类大型引擎时难免存在诸多不便。在此背景下，JerryScript引擎诞生了。JerryScript是由三星开发的一款炙手可热的轻量级引擎，其目的是让JavaScript开发者能够更好地构建物联网应用，它可以在RAM小于64KB和Flash小于200KB的设备上运行。

## 快速上手
#### 下载模拟器
首先，您需有一个合格的模拟器帮助您的开发
建议使用我开发的Band View，支持api相对来说是目前最多的，
下载链接：https://www.bandbbs.cn/threads/8956/#post-465494
#### 配置打包环境
配置一下java 1.8运行环境
cmd命令行输入java -jar 能提示版本信息即配置成
没有的话百度一下安装并配置环境变量

## 开发须知
#### 我所知环8目前不支持的api：
定时器
Math
Date
等

## 开始开发
### 控件模块
#### LABEL
``` javascript
create_label(id: any, x: any, y: any, w: any, h: any)
```
label控件可理解为text文本控件，创建方式如上
##### 子方法
###### set_label_text
设置 label 内容
不支持中文
调用方式：
``` javascript
set_label_text(id,'hello world')
```
###### set_label_font
设置 label 字体 (只支持静态字库里面的字体)
调用方式：
``` javascript
set_label_font(id, 4163)
```
这个静态字库是什么我不知道

###### set_label_color
设置 label 颜色
调用方式：
``` javascript
set_label_color(id, 0x5E4B42)
```
后面那个也可以是'#5E4B42'这样的

###### set_label_content_center
设置 label 内容居中显示
调用方式：
``` javascript
set_label_content_center(id)
```

###### set_label_content_align
设置 label 内容居中显示
调用方式：
``` javascript
set_label_content_align(id)
```
##### 代码示例
``` javascript
const label = create_label(0,10,20,80,100);
set_label_text(label, 'hello world');
set_label_font(label, 4163);
set_label_color(label, 0x5E4B42);
set_label_content_center(label);
set_label_content_align(label);
```
#### IMG
``` javascript
create_img(id: any, src: string, x: any, y: any)
```
创建方式如上
不用加后缀名！！！！！
默认为.png
##### 子方法
###### set_img_src
可以改变控件所展示的图片
调用方式：
``` javascript
set_img_src(goalImg,"lgoal")
```
第一个是 id，第二个是图片名称
##### 代码示例
``` javascript
const img = create_img(0,'obj.bin',20,80);
set_img_src(img,'array.bin')
```
#### BTN
``` javascript
create_btn(id: any, x: any, y: any, w: any, h: any)
```
创建方式如上
##### 子方法
无，仅可用控件通用方法
##### 代码示例
``` javascript
const btn = create_btn(0,'obj.bin',20,80);
addEvent(btn,[7],()=>{console.log('hello world')})
```

#### OBJ
``` javascript
create_obj(id: any, x: any, y: any, w: any, h: any)
```
可以理解为HTML中的div，Zepp OS的Group，创建方式如上
##### 子控件创建
控件的xy取决于obj控件的xy
代码示例
``` javascript
const obj = create_obj(0,2,2,3,4)
obj.create_btn(0,2,4,8,10)// x=4,y=6
```
##### 子方法
###### set_obj_size
设置对象大小
``` javascript
set_obj_size(obj, 168, 168)
```
后面两个所填参数分别为 w 和 h

###### set_obj_pos
设置对象位置
``` javascript
set_obj_pos(id, x, y)
```

###### set_obj_click
设置对象可点击事件
调用方式：
``` javascript
set_obj_click(id,func)
```
func 为函数，自己改

###### set_obj_hidden
设置对象隐藏
调用方式：
``` javascript
set_obj_hidden(id)
```

###### set_obj_display
设置对象显示
调用方式：
``` javascript
set_obj_display(id)
```

###### set_obj_style
设置对象和 style 绑定
调用方式我不到
style 咱等会讲

###### remove_obj_style
移除对象的 style 
顾名思义，我不到调用方式

###### set_obj_long_pressed_repeat
设置对象可重复长按事件
就是长按操作
调用方式我不到

###### set_obj_pressed
设置对象可按下事件
调用方式我不到

###### set_obj_pressing
设置对象可以一直按下事件
调用方式我不到

###### set_obj_released
设置对象释放事件
调用方式我不到

###### set_obj_del
删除对象
调用方式：
``` javascript
set_obj_del(id)
```

###### drag_event_handler
设置对象在拖拽后的位置
调用方式我不到

###### get_obj_x
获取对象 x 轴坐标
调用方式：
``` javascript
get_obj_x(id)
```

###### get_obj_y
获取对象 y 轴坐标
调用方式：
``` javascript
get_obj_y(id)
```

###### refr_obj_pos
刷新对象位置
调用方式：
``` javascript
refr_obj_pos(id)
```
##### 代码示例
``` javascript
const obj = create_obj(0, 2, 4, 8,10)
set_obj_size(obj, 168, 168)
set_obj_pos(obj, 2, 168)
set_obj_click(obj,()=>{console.log('hello world')})
set_obj_hidden(obj)
set_obj_display(obj)
set_obj_del(obj)
get_obj_x(obj)
refr_obj_pos(obj)
get_obj_y(obj)
```
#### ARC
``` javascript
create_arc(id: any, x: any, y: any, w: any, h: any, start: any, end: any, timeLabel)
```
创建方式如上,timeLabel意义不明
##### 子方法
###### set_arc_fg_color
设置前景色
``` javascript
set_arc_fg_color(id, 0x68A6EF)
```
后面那个也可以是'#5E4B42'这样的

###### set_arc_fg_width
设置前弧宽度
``` javascript
set_arc_fg_width(id, 6)
```
###### set_arc_fg_redius
设置前弧半径
``` javascript
set_arc_fg_redius(id, 20)
```
###### set_arc_bg_color
设置背景色
``` javascript
set_arc_bg_color(id, 0xBCD1EA)
```
后面那个也可以是'#5E4B42'这样的

###### set_arc_bg_width
设置背景弧宽度
``` javascript
set_arc_bg_width(id, 6)
```
###### set_arc_bg_redius
设置背景弧半径
``` javascript
set_arc_bg_redius(id, 20)
```
###### obj_modify_value
在 arc 上设置一个倒计时功能，实时更新 arc 的值
``` javascript
obj_modify_value(id, 200 , 200)
```
第一个是 id，第二个是图片名称
##### 代码示例
``` javascript
const arc = create_arc(0, 0, 210, 330, 0, 10, 10, null);
set_arc_fg_color(arc, 0x68A6EF)
set_arc_fg_width(arc, 6)
set_arc_fg_redius(arc, 20)
set_arc_bg_color(arc, 0xBCD1EA)
set_arc_bg_width(arc, 6)
set_arc_bg_redius(arc, 20)
obj_modify_value(arc, 200 , 200)
```
#### LINE
``` javascript
create_line(id: any,x: any, y: any, w: any, h: any)
```
貌似是这样的
##### 子方法

###### set_line_point
设置 2 个点的坐标（2 点确定一条直线）
``` javascript
set_line_point(id, 120, 140)
```
后面两个所填参数分别为 x 和 y

###### set_line_width
设置线的宽度
调用方式：
``` javascript
set_line_width(id, 2)
```

###### set_line_color
设置线的颜色
调用方式：
``` javascript
set_line_color(line, 0xE0, 0x7C, 0x65)
```


###### create_multiple_line
创建多条线
调用方式我不到

###### set_multiple_line_point
设置多条线上的多个点
调用方式我不到

###### set_line_point_num
设置多条线中有几个点是有效的
调用方式我不到

###### clear_multiple_line_point
清除所有的点坐标
调用方式我不到

###### set_line_dash_width
设置虚线的实线长度
调用方式我不到

###### set_line_dash_gap
设置虚线中实线之间的 gap
调用方式我不到
##### 代码示例
``` javascript
const line = create_line(0,1,2)
set_line_point(line, 120, 140)
set_line_width(line, 2)
set_line_color(line, 0xE0, 0x7C, 0x65)
```
#### 控件通用接口
##### addEvent
注册点击事件
``` javascript
addEvent(id,[7],()=>{console.log('hello world')})
```
第三个是执行的函数
第二个嘛，7 代表 click，1 代表 mousedown，8 代表 mouseup

##### registerEvent
销毁点击事件
``` javascript
registerEvent(em3)
```
##### rotate_90_degrees
设置对象旋转 90 度
``` javascript
rotate_90_degrees(id, 90, 90)
```
##### move_horizontal
设置对象在 X 方向移动
``` javascript
move_horizontal(id, -72, 800)
```
##### move_vertical
设置对象在 Y 方向移动
``` javascript
move_vertical(id, 90, 90)
```
### 文件模块
#### saveDataToFile
``` javascript
saveDataToFile(obj:{any})
```
存储数据，接受一个对象，对象里面包含key与value
代码示例
``` javascript
saveDataToFile({
    hello: 'hello world',
    world: 'world world'
})
```
#### readDataToFile
``` javascript
readDataToFile(obj:{any})
```
读取数据，接受一个对象，对象里面包含key
代码示例
``` javascript
readDataToFile({
    hello,
    world
})
```
#### write
同步地写入文件
调用方法未知

#### read
同步地读取文件
调用方法未知

### 公共接口
#### reg_event_callback
注册事件回调函数（C 调用 JS 的接口）
emm 不到

#### get_event_src
获取当前事件源
emm 不到

#### get_event_code
获取当前事件 Id
emm 不到

#### exit_game
退出游戏
``` javascript
exit_game()
```
#### get_js_parent
获取当前对象的父节点
``` javascript
get_js_parent()
```

#### my_pow
求 x 的 y 次幂
``` javascript
my_pow(m,2)
```

#### my_sqrt
开方函数
``` javascript
my_sqrt(my_pow(b,2)-4*a*c))/(2*a)
```

#### rand_num
获取一个100-1000的随机数
``` javascript
rand_num()
```

#### EventMap
``` javascript
new EventMap(0, [13],func, true)
``` 
GMF写成了构造函数，我不知道具体意思

### style接口
#### create_style
创建一个 style
我不到

#### set_style_opa
设置背景透明度
我不到

#### set_style_bg
设置背景颜色
我不到

#### reset_style
重置 style
我不到