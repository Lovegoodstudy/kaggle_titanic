# 例子：泰坦尼克号乘客分析



## 泰坦尼克号乘客分析简介



这是一个 Kaggle 上的经典比赛 [Titanic: Machine Learning from Disaster](https://www.kaggle.com/c/titanic)，通过机器学习对泰坦尼克号乘客进行死亡预测。

这一小节中我们将会在 Russell Cloud 上示范这个例子 ，你可以在这个例子中学会如何创建 Jupyter Notebook 模式下的任务，数据集引用以及添加依赖等操作。





### 项目准备



对于这个项目，你需要准备：

* [注册 RussellCloud 账号](http://russellcloud.com/#regist)

* [安装 *russell-cli* 终端工具](http://docs.russellcloud.com/get-started/install.html)

* Clone 项目文件，[Git地址](https://github.com/LovegoodStudy/kaggle_titanic.git)

```bash

# clone代码

$ git clone https://github.com/LovegoodStudy/kaggle_titanic.git

```

![Clone示例](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-gitclone.png)





### 使用 russell-cli 命令行工具登录 RussellCloud



```bash

# 使用russell login命令

$ russell login

Authentication token page will open in your browser. Continue? [Y/n]

```

这会提示你将要打开 RussellCloud 的页面，输入 y 表示确认打开浏览器，稍等几秒中会打开一个网页。输入 n 则不会打开网页，那你需要提前准备好 Token 。在浏览器登录，将会出现一个页面让你拷贝你的 Token 。

![主页的Token复制](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-logintoken1.png)

![欢迎页Token复制](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-logintoken1.png)

接下来你需要将这个 Token 复制下来并粘贴到终端中，粘贴的时候终端并不会显示它，所以不用担心它没有显示，粘贴一次就可以回车确认啦。

![登录成功](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-loginsuccess.png)





### 数据集准备



项目未动，数据先行。这一步将帮助你上传这个例子用到的数据集。

**当然你也可以跳过此步骤，直接使用我们此例的公用数据集 ID ：309252b75bb84eb89b01f47c3a1f78a5**

* 打开RussellCloud的主页并登录，来到控制台，创建一个数据集。

![创建数据集](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-datasetpage.png)

![创建数据集](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-datasetnew.png)

* 创建成功后，在该数据集的概览下复制数据集概览ID，下面初始化数据集会用到。

![数据集概览ID](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-datasetoverviewID.png)

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

![初始化及上传数据集](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-datasetupload.png)





### 初始化和上传并启动项目



接下来就是激动人心的项目初始化和启动过程啦，这里我们演示的例子是一个 IPython NoteBook 项目，所以我们要使用网页可视化操作的 Jupyter Notebook 模式来启动。

* 首先来到 RussellCloud的控制台新建一个项目。

![创建项目](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-projectpage.png)

![创建项目](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-projectnew.png)

* 创建成功后，在该项目的概览下复制数据集概览 ID ，下面初始化项目会用到。

![项目概览ID](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-projectoverviewID.png)

* 设置安装依赖及使用 russell-cli 工具初始化项目

```bash

# 打开代码所在目录

$ cd ../code

# 由于本项目需要使用seaborn库进行数据可视化，因此在项目下创建russell_requirements.txt来指示系统安装依赖

$ echo "seaborn" >> russell_requirements.txt

# 绑定远程项目，此处<project_id>是刚才在网页上复制的项目概览 ID

$ russell init --id <project_id>

```

![设置安装依赖及项目初始化](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-projectinit.png)

* 使用 russell run 上传并启动项目

```bash

# 以jupyter模式启动，可能需要等待一小会，返回相应浏览器可访问的notebook链接。

# 此处<data_id>是你需要挂载的数据集的版本 ID ，由上一步数据集操作最终获得。如果你没有记下版本 ID ，可以通过网页端数据集页面“版本”查看并复制版本 ID 。这里<data_id>后的:data是用于指定挂载名称，数据目录会挂载到系统的 /input/挂载名称 的目录下，这里就是 /input/data 下。

$ russell run --mode jupyter --data <data_id>:data

```

由于我们使用的是 jupyter 模式，成功运行项目后将会自动打开网页端 Jupyter NoteBook 。

![网页端查看并复制数据集版本ID](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-datasetID.png)

![成功运行项目](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-projectrunsuccess.png)

* 使用 Jupyter Notebook 操作

打开 Jupyter Notebook 之后我们可以做很多方便的修改，可以上传 UPLOAD ，甚至可以运行终端。如果你有一些依赖的包忘记在上传的 requirements 文件中写了的话，可以在这里运行终端使用 pip 安装。下面是演示。

![Jupyter Notebook的强大操作](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-jupyternew.png)

![Jupyter Notebook运行终端命令](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-jupyternewterminal.png)

然后我们启动我们 code 中的 IPython NoteBook 代码来看看吧！直接点击这个 analysis_titanic.ipynb 文件即可。

![Jupyter Notebook启动IPython NoteBook代码](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-jupyterrun.png)

Jupyter Notebook 提供了极其丰富的功能，大家多多探索吧，这里就不再赘述了~

* 使用完毕后，使用 russell-cli 的stop命令结束

jupyter 模式下，任务不会自动关闭而是一直运行，为了资源利用以及省下大家的银子，千万不要忘记关了哦~提交 stop 请求后可以使用 status 命令检查是否关闭成功。

```bash

russell stop <run_id>

russell status <run_id>

```

![task请求stop并用status命令查看task状态](https://github.com/LovegoodStudy/kaggle_titanic/raw/master/.img/kaggle-titanic-taskstop.png)

大功告成！







