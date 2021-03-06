title:  关于Update和FixedUpdate的理解
date: 2016-01-08 10:33:26
categories: Unity
tags: [Update,FixedUpdate]
---

前些天充话费送了个手机，明知机器性能肯定很烂，但白得的永远是好的，心里还是高兴了一下。
正好最近的手游项目出来demo,公司的小米测试机跑的很是欢快。想着装我的"话费机"里试试。虽然有
一定的心里准备，但运行的速度还是让我出乎意料。战斗中人物的移动以及各种技能特效子弹飞行的速度
异常的缓慢。
虽说这不是我们的目标机型，但是为了让我这样用"话费机"的人也能玩上游戏，自然是想想优化方案了。

### 问题表现：低端机运行战斗表现缓慢，无法容忍！
战斗表现缓慢，人物子弹位移缓慢的原因自然是机器性能太差，导致FPS极低造成的。
同事查看战斗逻辑代码，发现战斗逻辑基本都写在Update()方法里，而这个方法是每帧渲染前调用。
也就是逻辑与渲染同步，因此机器性能变慢导致逻辑变慢，才有的之前的现象。
**Update() 每帧触发一次**

### 解决问题：将战斗相关代码都放在FixedUpdate()里，果然运行流畅了许多，可以接受了！
**FixedUpdate() 固定间隔时间触发一次**
理论上忽略机器性能的问题 Update()与FixedUpdate()在同样时间间隔内触发次数应该相同。
然并卵！现实就是现实，你无法忽略手机设备的性能差异尤其是Android系手机。
*那所有逻辑都写在 FixedUpdate()不就完了？*
真实情况是：相同时间相同频率下 Update()执行次数一定小于 FixedUpdate()次数！
*你还要为你的程序效率着想！*

# 好钢用在刀刃上，可以将表现战斗的主要逻辑放在FixedUpdate()里，其他UI等的渲染逻辑放在 Update()里，具体问题具体分析！

