---
layout: post
title:  Homework 7 for UML
teaser: 系统分析与设计
date: 2018-5-12 12:00:10+00:00
category: UML
tags: [UML, HW]
---

1、用例图

![use_case](..\i\l9\use_case.png)

2、活动图

![activity](..\i\l9\activity.png)

3、领域模型

![domain](..\i\l9\domain.png)

4、状态模型

![state](..\i\l9\state.png)

5、系统顺序图

![system](..\i\l9\system.png)

### 操作协议

操作：修改专注时间

交叉引用：用例：选择种树时长

前置条件：无

后置条件：修改并显示新的时间与对应的树状态

#### 

操作：修改树种类

交叉引用：用例：选择树种

前置条件：无

后置条件：修改并显示新的树

#### 

操作：开始种树

交叉引用：用例：种树

前置条件：树的各项属性设置完成

后置条件：开始倒计时界面

#### 

操作：返回种树结果

交叉引用：用例：种树

前置条件：倒计时结束

后置条件：显示成功并返回金币奖励