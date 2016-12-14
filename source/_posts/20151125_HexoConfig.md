title:  GitHub Blog 配置流程
date: 2016-01-01 00:00:00
categories: Hexo
tags: [Hexo,NexT,GitHub]
---

最近有些时间，弄了个自己的博客。过程比较麻烦，正好这第一篇先记录构建流程吧。

## 准备工具
* 空间：[Github](https://github.com/)，免费300M。
* 环境：[Node.js](https://nodejs.org)
* Blog架构：[Hexo](http://hexo.io/)
* Blog主题：[NexT](https://github.com/iissnan/hexo-theme-next)
* Git工具：版本1.9.5
* 域名：[万网](http://wanwang.aliyun.com/)

## 操作步骤  
###	创建本地工程
* 1 安装 **Git 1.9.5**
* 2 安装 **node-v4.2.1-64x**
* 3	建立本地工程目录。*eg:F:\blog\may*
* 4 在此目录中点击右键 选择 **Git Bash** 打开控制台程序。
	* 4.1 控制台中输入	`npm install -g hexo`  
	*[注：由于国外npm源经常被墙，直接配置国内淘宝的npm源（每10分钟与国外源同步一次）。
	系统盘里找到 .npmrc 文件，改成： `registry=http://registry.npm.taobao.org`。
	]*  
* 5 初始化 hexo  
    `hexo init`  
    此时你的文件夹里应该已经有了hexo的工程。
* 6 安装npm  
    `npm install`
* 7 生成工程  
    `hexo g`
* 8 运行工程  
    `hexo s` *[注：浏览器打开，本地运行成功！]*  
###	同步到GitHub
* 1 注册Git账号。
* 2 创建 **Repository**。*eg:XXX/XXX.github.io*
* 3 修改站点配置文件 **_config.yml**  
		deploy:
		type: git  
		repository:https://github.com/XXX/XXX.github.io.git  
		branch: master
* 4 设置 **ssh key**
	* 4.1 查看是否已经存在 sshkey。  
		`ls -al ~/.ssh`  
		若存在则删除。
	* 4.2 输入 `ssh-keygen -t rsa -C"你的git账号"`
	* 4.3 输入  
		`eval 'ssh-agent -s' ` 
		`ssh-add`
	* 4.4 在github里添加这个key 随便起个名字
	* 4.5 输入 `ssh -T git@github.com`
	* 4.6 生成工程，并上传。  
		`Hexo g`  
		`Hexo d`
* 5 如果报错 *ERROR Deployer not found:git*  
	输入 `npm install hexo-deployer-git -save`，再重新生成上传工程即可！

### 外网域名映射
	在source文件夹里添加 CNAME 文件 [注：没有扩展名] ，设置域名映射。  
	内容为 www.xxx.com   

# 运行浏览器看看效果吧，应该大功告成了!
		

