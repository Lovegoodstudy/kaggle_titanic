# 例子：泰坦尼克号乘客分析

---

[TOC]

---


## 泰坦尼克号乘客分析简介

这是一个 Kaggle 上的经典比赛 [Titanic: Machine Learning from Disaster](https://www.kaggle.com/c/titanic)，通过机器学习对泰坦尼克号乘客进行死亡预测。

这一小节中我们将会在 Russell Cloud 上示范这个例子 ，你可以在这个例子中学会如何创建 Jupyter Notebook 模式下的任务，数据集引用以及添加依赖等操作。


### 项目准备

对于这个项目，你需要准备：

* [注册 RussellCloud 账号](http://russellcloud.com/#regist)

* [安装 *russell-cli* 终端工具](/get-started/install.md)

* Clone 项目文件，[Git地址](https://github.com/Lovegoodstudy/titanic.git)

```bash

# clone代码

$ git clone https://github.com/Lovegoodstudy/titanic.git

```


### 使用 russell-cli 命令行工具登录 RussellCloud

```bash

# 使用russell login命令

$ russell login

```

这会提示你将要打开 RussellCloud 的页面，输入 y 表示确认打开浏览器，稍等几秒中会打开一个网页。输入 n 则不会打开网页，那你需要提前准备好 Token 。在浏览器登录，将会出现一个页面让你拷贝你的 Token 。

接下来你需要将这个 Token 复制下来并粘贴到终端中，粘贴的时候终端并不会显示它，所以不用担心它没有显示，粘贴一次就可以回车确认。

![登录成功](https://github.com/Lovegoodstudy/titanic/raw/master/.img/kaggle-titanic-loginsuccess.png)


### 数据集准备

项目未动，数据先行。这一步将帮助你上传这个例子用到的数据集。

**当然你也可以跳过此步骤，直接使用我们此例的公用数据集 ID ：309252b75bb84eb89b01f47c3a1f78a5**

* 打开[RussellCloud](http://russellcloud.com/)的主页并登录，来到控制台，创建一个数据集。

* 创建成功后，在该数据集主页的概览下复制数据集概览ID，下面初始化数据集会用到。

* 使用 russell-cli 工具初始化和上传数据集。

```bash

# 打开数据集所在目录

$ cd kaggle_titanic/data/

# 数据集初始化，此处<data_overview_id>是刚才在网页上复制的数据集概览ID

$ russell data init --id <data_overview_id>

# 数据集上传

$ russell data upload

```

上传成功后你将会获得数据集版本 ID ，**请务必记下这个 ID ，稍后运行项目时挂载数据集则需要用到这个 ID**。

![初始化及上传数据集](https://github.com/Lovegoodstudy/titanic/raw/master/.img/kaggle-titanic-datasetupload.png)


### 初始化和上传并启动项目

接下来就是激动人心的项目初始化和启动过程啦，这里我们演示的例子是一个 IPython NoteBook 项目，所以我们要使用网页可视化操作的 Jupyter Notebook 模式来启动。

* 首先来到 RussellCloud的控制台新建一个项目。

* 创建成功后，在该项目主页的概览下复制数据集概览 ID ，下面初始化项目会用到。

* 设置安装依赖及使用 russell-cli 工具初始化项目

```bash

# 打开代码所在目录

$ cd ../code

# 由于本项目需要使用seaborn库进行数据可视化，因此在项目下创建russell_requirements.txt来指示系统安装依赖

$ echo "seaborn" >> russell_requirements.txt

# 绑定远程项目，此处<project_id>是刚才在网页上复制的项目概览 ID

$ russell init --id <project_id>

```

![设置安装依赖及项目初始化](https://github.com/Lovegoodstudy/titanic/raw/master/.img/kaggle-titanic-projectinit.png)

* 使用 russell run 上传并启动项目

```bash

# 以jupyter模式启动，可能需要等待一小会，返回相应浏览器可访问的notebook链接。

# 此处<data_id>是你需要挂载的数据集的版本 ID ，由上一步数据集操作最终获得。如果你没有记下版本 ID ，可以通过网页端数据集页面“版本”查看并复制版本 ID 。这里<data_id>后的:data是用于指定挂载名称，数据目录会挂载到系统的 /input/挂载名称 的目录下，这里就是 /input/data 下。

$ russell run --mode jupyter --data <data_id>:data

```

由于我们使用的是 jupyter 模式，成功运行项目后将会自动打开网页端 Jupyter NoteBook 。

![成功运行项目](https://github.com/Lovegoodstudy/titanic/raw/master/.img/kaggle-titanic-projectrunsuccess.png)

* 使用 Jupyter Notebook 操作

打开 Jupyter Notebook 之后我们可以做很多方便的修改，提供了上传 UPLOAD ，运行终端等等。如果你有一些依赖的包忘记在上传的 requirements 文件中写了的话，可以在这里运行终端使用 pip 安装。下面是演示。
然后我们就可以在这里打开 .ipynb 文件运行项目啦！

![Jupyter Notebook运行终端命令](https://github.com/Lovegoodstudy/titanic/raw/master/.img/kaggle-titanic-jupyternewterminal.png)

* 使用完毕后，使用 russell-cli 的stop命令结束

jupyter 模式下，任务不会自动关闭而是一直运行，除非达到最大时间。为了资源利用以及省下大家的银子，我们这里使用 russell stop 命令结束 task 。

```bash

russell stop <run_id>

russell status <run_id>

```

![task请求stop并用status命令查看task状态](https://github.com/Lovegoodstudy/titanic/raw/master/.img/kaggle-titanic-taskstop.png)

完成！