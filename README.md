acm-resover
==================
本项目fork自[hiho-resolver](https://github.com/hiho-coder/hiho-resolver)，用于ACM系列竞赛的滚榜。
相比原项目，主要优化了动画效率，更改了界面配色，并丰富了文档。

# 截图

![screenshot](screenshots/shot1.gif)

使用教程
------------------------

## 1. 准备数据

NKOJ的旧版后台有导出比赛榜单数据功能，在导出前可按照提示输入打星选手的用户名和学校。

或者也可以自己构造数据，json的格式在文档末尾。

数据输入的代码在`js/main.js`的最后，`$.getJSON("contest.json", function(data){..})`

默认是使用根目录下的`contest.json`，可以直接把准备好的数据贴到里面去。

## 2. 搭建服务器

1. 网页必须以http协议访问，准备一个web服务器，Windows推荐用WAMP，MacOS推荐用MAMP。
2. 把整个工程文件拷贝到服务器的目录下，在浏览器中访问index.html即可。

## 2.1 本地访问方式
Chrome启动时加入如下参数即可
```
--disable-web-security --user-data-dir=%TEMP%
```

## 3. 操作说明

不停按方向键右即可。
应根据题目数量调整浏览器显示缩放率，至少80%以下否则会有溢出

**如果切换了数据源，需要清空浏览器缓存再刷新。**

## 修改封榜时间

修改`hiho-resolver.js`的第6行
```JavaScript
	this.frozen_seconds = 3600*4;
```
**注意**: 这里的frozen_seconds是指**从比赛开始后多少秒后开始封榜**，而不是最后有多少秒封榜

## JSON格式

```
{
  problem_count: 10,
  solutions: {... },
  users: {... }
}
```

solution的格式，key可以任意，problem下标从1开始:

```
381503: {
  user_id: "1",
  problem_index: "1",
  verdict: "AC",
  submitted_seconds: 22
},
381504: {
  user_id: "2",
  problem_index: "1",
  verdict: "WA",
  submitted_seconds: 23
},
```

user的格式，其中key即为user的id，要和solution中对上：

```
1: {
  name: "花落人亡两不知",
  college: "HZNU",
  is_exclude: true
},
2: {
  name: "大斌丶凸(♯｀∧´)凸",
  college: "HDU",
  is_exclude: false
},
3: {
  name: "天才少女队",
  college: "PKU",
  is_exclude: true
},
```

