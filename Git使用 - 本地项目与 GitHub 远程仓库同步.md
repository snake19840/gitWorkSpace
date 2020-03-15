# Git使用 - 本地项目与 GitHub 远程仓库同步

翻译[ithanmang](https://me.csdn.net/ithanmang) 最后发布于2018-07-01 19:33:40 阅读数 4992 收藏

展开

**具体步骤如下**

#### 1 安装 Git

地址：https://git-scm.com/
![这里写图片描述](D:\图片\TyporaImage\20180630193828239.png)

#### 2 配置 Git

安装后在桌面任意位置右键选择，`Git bash Here` 打开Shell。
**window 配置**
![这里写图片描述](D:\图片\TyporaImage\20180630194230782.png)
命令输入以下两行代码：

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com
12
```

具体的详细步骤大家可以去[廖雪峰官网](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000)去查看，本篇文章，只涉及如何将 `本地项目` 同`远程仓库`同步。

#### 3 创建 SSH key

+ 首先，在用户主目录`C:\Users\wangzhongjie`这是我的目录，查看是否有`.ssh`目录。
  ![这里写图片描述](D:\图片\TyporaImage\20180630195254178.png)
  若有的话，查看此目录下是否有`id_rsa`和`id_rsa.pub`两个文件，这两个是密匙对，`id_rsa`是私匙，不能泄露出去，`id_rsa.pub`公匙。，如果有的话请进行下一步，若没有请 打开 Git Bash 输入以下命令来创建 ssh key。

```
ssh-keygen -t rsa -C "youremail@example.com"
1
```

然后就会在`用户主目录`生成`.ssh`目录和那两个文件。

#### 4 添加 GitHub SSH Key

+ 点击设置
  ![这里写图片描述](D:\图片\TyporaImage\20180630200435165.png)
+ 点击 `SSH and GPG keys`
  ![这里写图片描述](D:\图片\TyporaImage\20180630201021952.png)
+ 创建 `SSH key`
  把 `用户主目录`下的那个 公匙 文件中的内容复制。
  ![这里写图片描述](D:\图片\TyporaImage\20180630201424806.png)
+ 添加`SSH Key`成功。

#### 5 创建远程仓库

+ 步骤1
  ![这里写图片描述](D:\图片\TyporaImage\20180630201823600.png)
+ 步骤2
  ![这里写图片描述](D:\图片\TyporaImage\20180630202245431.png)
+ 步骤3
  创建仓库完成
  ![这里写图片描述](D:\图片\TyporaImage\20180630202455812.png)

#### 6 创建本地仓库

在本地任意目录创建一个测试文件夹。
![这里写图片描述](D:\图片\TyporaImage\20180630203042116.png)
我这里是在`D:\workSpace`下创建了一个`test`目录，并初始化为`Git`仓库。

#### 7 将本地仓库和远程仓库建立连接

回到 刚才在`GitHub`上创建的那个 `test`库，复制 `SSH`。
![这里写图片描述](D:\图片\TyporaImage\20180630203501836.png)
回到`Git Bash`，输入以下代码。

```
 git remote add origin git@github.com:ithanmang/test.git

12
```

注意将`git@github.com:ithanmang/test.git` 改为你自己的。
此时 远程库就与本地库建立了连接。

+ 然后在，本地库新建一个测试文件`hello.txt`。
  ![这里写图片描述](D:\图片\TyporaImage\20180630204026141.png)
+ `add`和 `commit`
  ![这里写图片描述](D:\图片\TyporaImage\20180630204328254.png)

#### 8 把本地仓库的文件同步到远程库

输入代码
`$ git push -u orgin master`
会发现拒绝合并
![这里写图片描述](D:\图片\TyporaImage\20180630204741278.png)
这是因为在刚开始创建远程仓库的时候，默认创建了 `README.md`文件。
![这里写图片描述](D:\图片\TyporaImage\20180630204929521.png)
因此，在`push`之前需要先 `pull`一下，让本地库与远程库同步。
输入以下代码
`$ git pull origin master`
**origin**：是本地库的别名
**master**：分支名
`git pull origin master`：将远程库的内容，更新到本地。
![这里写图片描述](D:\图片\TyporaImage\20180701192410129.png)
此时本地库与远程的内容是一致的，所以，可以将本地添加的文件同步到远程库了。
然后在执行：`git push -u orgin master`命令，将本地库的内容推送到远程库中去。
![这里写图片描述](D:\图片\TyporaImage\20180701193042799.png)
刷新远程库，发现 `hello.txt`已经上传。
![这里写图片描述](D:\图片\TyporaImage\20180701193144871.png)