# Git

## 配置

```java
$ git config --global user.name "Soma1224"
$ git config --global user.email "250763424@qq.com"

```

## 初始化一个新的git仓库

1.新建一个test文件夹

![1541070922987](.\picture\6734672.png)

2.在文件内初始化git（==创建git仓库==）

![1541071128298](.\picture\3242647.png)

## 向仓库中添加文件

1创建a1.php文件

![1541071286450](.\picture\1541071286450.png)



2.添加到暂存区

![1541071459829](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541071459829.png)



3.将文件从暂存区提交到仓库

![1541072156282](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541072156282.png)



## 修改文件

![1541073265668](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541073265668.png)

![1541073589410](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541073589410.png)

## 删除文件

1.删除a1.php

2.在暂存区里面删除a1.php

3.把删除命令提交到仓库

![1541073937514](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541073937514.png)



## Git管理远程仓库

![1541074189531](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541074189531.png)















## 报错的解决方式

![1541076162667](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541076162667.png)









## Git与SVN的区别

- SVN是集中式的version control，Git是分布式的version control
- SVN每次存储的是变化，而Git存储的是完整的文件，如果没有变化的话，是通过指针指向前一个snapshot

![1541118077228](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541118077228.png)







每一次commit后面都会有一串字符串，这个是sha，是一个40位的不可逆的校验和，可以做文件恢复

![1541118301627](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541118301627.png)



sha保证文件的完整性

![1541119063127](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541119063127.png)





# Github

## SSH

很多朋友在用github管理项目的时候，都是直接使用https url克隆到本地，当然也有有些人使用 SSH url 克隆到本地。然而，为什么绝大多数人会使用https url克隆呢？

这是因为，使用https url克隆对初学者来说会比较方便，复制https url 然后到 git Bash 里面直接用clone命令克隆到本地就好了。而使用 SSH url 克隆却需要在克隆之前先配置和添加好 SSH key 。

因此，如果你想要使用 SSH url 克隆的话，你必须是这个项目的拥有者。否则你是无法添加 SSH key 的。

 

https 和 SSH 的区别：

1、前者可以随意克隆github上的项目，而不管是谁的；而后者则是你必须是你要克隆的项目的拥有者或管理员，且需要先添加 SSH key ，否则无法克隆。

2、https url 在push的时候是需要验证用户名和密码的；而 SSH 在push的时候，是不需要输入用户名的，如果配置SSH key的时候设置了密码，则需要输入密码的，否则直接是不需要输入密码的。

 

### 在 github 上添加 SSH key 的步骤：

#### 1、首先需要检查你电脑是否已经有 SSH key 

运行 git Bash 客户端，输入如下代码：

```
$ cd ~/.ssh
$ ls
```

这两个命令就是检查是否已经存在 id_rsa.pub 或 id_dsa.pub 文件，如果文件已经存在，那么你可以跳过步骤2，直接进入步骤3。

 

#### 2、创建一个 SSH key 

```
$ ssh-keygen -t rsa -C "your_email@example.com"
```

代码参数含义：

-t 指定密钥类型，默认是 rsa ，可以省略。
-C 设置注释文字，比如邮箱。
-f 指定密钥文件存储文件名。

以上代码省略了 -f 参数，因此，运行上面那条命令后会让你输入一个文件名，用于保存刚才生成的 SSH key 代码，如：

```
Generating public/private rsa key pair.
# Enter file in which to save the key (/c/Users/you/.ssh/id_rsa): [Press enter]
```

当然，你也可以不输入文件名，使用默认文件名（推荐），那么就会生成 id_rsa 和 id_rsa.pub 两个秘钥文件。

 

接着又会提示你输入两次密码（该密码是你push文件的时候要输入的密码，而不是github管理者的密码），

当然，你也可以不输入密码，直接按回车。那么push的时候就不需要输入密码，直接提交到github上了，如：

```
Enter passphrase (empty for no passphrase): 
# Enter same passphrase again:
```

接下来，就会显示如下代码提示，如：

```
Your identification has been saved in /c/Users/you/.ssh/id_rsa.
# Your public key has been saved in /c/Users/you/.ssh/id_rsa.pub.
# The key fingerprint is:
# 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com
```

当你看到上面这段代码的收，那就说明，你的 SSH key 已经创建成功，你只需要添加到github的SSH key上就可以了。

 

#### 3、添加你的 SSH key 到 github上面去

a、首先你需要拷贝 id_rsa.pub 文件的内容，你可以用编辑器打开文件复制，也可以用git命令复制该文件的内容，如：

```
$ clip < ~/.ssh/id_rsa.pub
```

b、登录你的github账号，从又上角的设置（ [Account Settings](https://github.com/settings) ）进入，然后点击菜单栏的 SSH key 进入页面添加 SSH key。

c、点击 Add SSH key 按钮添加一个 SSH key 。把你复制的 SSH key 代码粘贴到 key 所对应的输入框中，记得 SSH key 代码的前后不要留有空格或者回车。当然，上面的 Title 所对应的输入框你也可以输入一个该 SSH key 显示在 github 上的一个别名。默认的会使用你的邮件名称。

 

#### 4、测试一下该SSH key

在git Bash 中输入以下代码

```
$ ssh -T git@github.com
```

当你输入以上代码时，会有一段警告代码，如：

```
The authenticity of host 'github.com (207.97.227.239)' can't be established.
# RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
# Are you sure you want to continue connecting (yes/no)?
```

这是正常的，你输入 yes 回车既可。如果你创建 SSH key 的时候设置了密码，接下来就会提示你输入密码，如：

```
Enter passphrase for key '/c/Users/Administrator/.ssh/id_rsa':
```

当然如果你密码输错了，会再要求你输入，知道对了为止。

注意：输入密码时如果输错一个字就会不正确，使用删除键是无法更正的。

密码正确后你会看到下面这段话，如：

```
Hi username! You've successfully authenticated, but GitHub does not
# provide shell access.
```

如果用户名是正确的,你已经成功设置SSH密钥。如果你看到 “access denied” ，者表示拒绝访问，那么你就需要使用 https 去访问，而不是 SSH 。



### 使用Https向github发送文件

==先克隆远程仓库，再往里面写==，记得一定要进入复制仓库的文件夹目录下面

![1541077382077](E:\Typora文件 公司电脑\图片\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541077382077.png)



如何push自己的文件夹，例如笔记文件夹

https://blog.csdn.net/Rong_Toa/article/details/80577410

整体思路是：

1. 在你的工程的上一个文件目录下面git init一下（git bash here）
2. git clone github上的https或者是ssh的地址，然后就会在此文件目录下创建一个同名的文件夹
3. 在同名文件夹里面年粘贴你想push的文件夹
4. 进入这个同名文件夹，然后git bash here（git bash here）
5. git add .
6. git commit -m"first commit"
7. git push





### 使用ssh向github发送文件

参考这个

https://blog.csdn.net/p10010/article/details/51336332

思路：

在你的电脑已经生成ssh的key并且添加到github上之后，在你想要放文件的地方Git Bash Here，然后

- git init 
- git remote add origin 你github上文件的ssh地址
- git pull origin  master
  - 表示将远程origin主机的master分支拉取过来和本地的**当前分支**进行合并。











## 删除已经在github远程仓库下的文件夹和文件

- 首先**进入你的master文件夹**下, Git Bash Here ，打开命令窗口

- $ git pull origin master 将远程仓库里面的项目拉下来

- $ dir  查看有哪些文件夹

- $ git rm -r --cached Photo\ albums  删除Photo albums文件夹(这里的文件夹名有空格命令行需要用"\ "来拼接）

- $ git commit -m '删除了Photo albums文件夹t'  提交，添加操作说明

- $ git push -u origin master 将本次更改更新到GitHub项目上去



注:本地项目中的Photo albums文件夹不收操作影响,删除的只是远程仓库中的Photo albums, 可放心删除

每次增加文件或删除文件，都要commit 然后直接 git push -u origin master，就可以同步到GitHub上了。



![1553148697040](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1553148697040.png)



## 修改github上的文件

- git init  
- git remote add origin 你github上文件的ssh地址
- git pull origin master
- git add .
- git commit -m "first edit"
- git push -u origin master





常用命令大全：



![1553170246861](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1553170246861.png)







## Git fetch和git pull的区别:

- 都可以从远程获取最新版本到本地

1.Git fetch:只是从远程获取最新版本到本地,不会merge(合并)

```
$:git fetch origin master   //从远程的origin的master主分支上获取最新版本到origin/master分支上
$:git log -p master..origin/master //比较本地的master分支和origin/master分支的区别
$:git merge origin/master          //合并123
```

2.Git pull:从远程获取最新版本并merge(合并)到本地

```
$:git pull origin master  //相当于进行了 git fetch 和 git merge两部操作1
```

- 实际工作中,可能`git fetch`更好一些, 因为在`merge`前,可以根据实际情况决定是否`merge`

------

**再说导致报错:error: You have not concluded your merge (MERGE_HEAD exists).的原因可能是在以前pull下来的代码自动合并失败**



**解决办法一:保留本地的更改,中止合并->重新合并->重新拉取**

```
$:git merge --abort
$:git reset --merge
$:git pull123
```

**解决办法二:舍弃本地代码,远端版本覆盖本地版本(慎重)**

```
$:git fetch --all
$:git reset --hard origin/master
$:git fetch123
```