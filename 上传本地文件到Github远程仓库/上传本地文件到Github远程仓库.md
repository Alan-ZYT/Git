# 上传本地文件到Github远程仓库

#### 环境：windows10 64位

前提要求：已经有了github账号，已经安装了[Git](https://git-scm.com/) (Git安装很简单,一路默认即可.)

## 一：创建Github repository(仓库)

#### 勾选 Initialize this repository with a README

1、假如你已经有了[Github](https://github.com/)账号，没有的话去才注册一个，很简单。

2、点击头像旁边的+号，New repository 如下图所示 : 

![1561293220347.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561293220347.png?raw=true)

3、创建仓库（注意：在README处勾选框，这样的话在你的github仓库中会为你自动生成一个README.md）

![1561293839064.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561293839064.png?raw=true)

4、最后创建仓库后的页面效果如下:

![创建仓库后的页面.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/%E5%88%9B%E5%BB%BA%E4%BB%93%E5%BA%93%E5%90%8E%E7%9A%84%E9%A1%B5%E9%9D%A2.png?raw=true)

------

## 二、为Github账户添加SSH key

### 了解ssh key 基础知识：

加密传输的算法有好多，git使用rsa，rsa要解决的一个核心问题是，如何使用一对特定的数字，使其中一个数字可以用来加密，而另外一个数字可以用来解密。这两个数字就是你在使用git和github的时候所遇到的public key也就是公钥以及private key私钥。

其中，公钥就是那个用来加密的数字，这也就是为什么你在本机生成了公钥之后，要上传到github的原因。从github发回来的，用那公钥加密过的数据，可以用你本地的私钥来还原。

如果你的key丢失了，不管是公钥还是私钥，丢失一个都不能用了，解决方法也很简单，重新再生成一次，然后在github.com里再设置一次就行。

------

#### 一、本地生成 ssh key

准备工作：绑定用户和邮箱

在项目文件目录右键 Git Bash Here，然后绑定用户名和邮箱

```bash
git config --global user.name "Alan-ZYT"
git config --global user.email "17717874203@163.com"
```

![在项目目录中右键点击Git Bash Here.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/%E5%9C%A8%E9%A1%B9%E7%9B%AE%E7%9B%AE%E5%BD%95%E4%B8%AD%E5%8F%B3%E9%94%AE%E7%82%B9%E5%87%BBGit%20Bash%20Here.png?raw=true)

Tips：用户名和邮箱作为你的唯一标识，--global 这个参数，表示这台机器上的所有Git仓库都会使用这个配置，也可以指定仓库用不同的用户名和邮箱

1、首先检查本地是否已经有秘钥了

（因为我之前生成过秘钥，所以本地是有的）

![1561294906843.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561294906843.png?raw=true)

2、如果没有的话，执行以下指令生成秘钥：

```bash
ssh-keygen -t rsa -C "你的邮箱"

example:
ssh-keygen.exe -t rsa -C "17717874203@163.com"
```

3、然后去按照上条方式查看以下有没有生成。

4、去C:\Users\Administrator.ssh里找到id_rsa.pub，用记事本打开，Ctrl+A，Ctrl+C 得到ssh key公钥。

------

#### 二、为github账号设置ssh key

1、进入github，点击settings

![1561295211988.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561295211988.png?raw=true)



2、然后打开SSH keys菜单，Add SSH key新增秘钥，填上标题（随意，建议跟repository一致），然后将id_rsa.put文件中的key粘贴，然后Add key生成秘钥。


![这里写图片描述](https://img-blog.csdn.net/2018072320353470?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlaW11MjQ=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

到此，github账号与本地的SSH key配置完成

------

## 三、上传本地文件到github上

#### 一、Git 基础知识补充

```bash
1、git init #把这个目录变成Git可以管理的仓库

2、git add README.md #本地README.md文件添加到远程仓库

3、git add . #不但可以跟单一文件，还可以跟通配符，更可以跟目录。一个点就把当前目录下所有未追踪的文件全部add了，注意空格

4、git commit -m “注释” #把文件提交到仓库

5、git remote add origin git@github.com:Alan-ZYT/cryptography.git #本地关联远程仓库

6、git push -u origin master #把本地库的所有内容推送到远程库上（第一次需要加-u，后面就不用加了）
```



------

#### 二、接下来的目标就是把 Go语言基础文件夹 上传到Github仓库

> Tips：切换到Go语言基础文件夹 git是不能管理空文件夹的，也就是说文件夹了必须有文件才能add

依次执行以下指令

```bash
1、git init .  #初始化
```

之后你会发现文件夹下多了一个隐藏文件夹.git，这个目录是Git用来跟踪管理版本库的，不要修改
![1561295745094.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561295745094.png?raw=true)

```bash
2、git add . # 将所有文件添加到仓库，注意空格
3、git commit -m "提交说明注释" # 注释内容自行修改

# 本地文件远程关联github仓库
4、git remote add origin git@github.com:Alan-ZYT/Golang-Language-Base-Document.git
```

Tips：后面的地址请自行修改，地址怎么来的，见下图。
![1561296002440.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561296002440.png?raw=true)

```bash
5、git push -u origin master # 上传本地代码

$ git push -u origin master
Connection reset by 52.74.223.119 port 22
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

错误原因: 没有权限,重新生成 ssh key
$ ssh-keygen.exe -t rsa -C "17717874203@163.com"
参考文档: https://blog.csdn.net/Leolu007/article/details/79129446
```

![1561297049760.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561297049760.png?raw=true)



然后你会发现又[出错了](https://www.jianshu.com/p/835e0a48c825)？如上所示 

错误原因：github中的README.md文件没有download到本地代码目录中

解决方案：执行以下指令

```bash
git pull --rebase origin master
```

这个时候查看本地代码目录，会发现多了个README.md文件
![1561297242393.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561297242393.png?raw=true)

此时再次执行以下语句，上传代码

```
git push -u origin master
```

![1561297285934.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561297285934.png?raw=true)

然后去github仓库查看，成功 ! ! !   如下图：

![1561297347869.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561297347869.png?raw=true)

===============================================================================

### *Try Again*

然后我们接着在本地新建一个文件heelo.go，再次上传。直接执行以下指令

```
1、git add .
2、git commit -m "hello"
3、git push origin master #只有第一次需要加 -u，以后可以不加
```

查看效果

![1561297686678.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561297686678.png?raw=true)

![1561297713335.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561297713335.png?raw=true)

------

#### 总结：

上述步骤在新建repository的时候，由于初始化了README.md，所以出了错，后来成功解决了这个问题。

如果在新建repository的时候，不勾选的?不初始化README.md呢？

效果如下：
![1561298063065.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561298063065.png?raw=true)

里面是空的，什么都没有，只有提示消息，也没有README.md 

哈哈~~~ 其实细心的小伙伴会发现下图中 官网已经告诉了使用Git命令上传文件的方式.

![1561298119283.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561298119283.png?raw=true)

上传文件，没有报错，直接成功，

（因为错误就是因为远程仓库的README.md没有download到本地，现在远程仓库没有该文件，
所以本地就不需要download，就不报错了）
![1561298375791.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561298375791.png?raw=true)

最后的效果

![1561298403128.png](https://github.com/Alan-ZYT/Git/blob/master/%E4%B8%8A%E4%BC%A0%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6%E5%88%B0Github%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/1561298403128.png?raw=true)

Tips：
README.md是属于仓库的说明书，建议是要有的。
1、你可以在github新建README.md，这个时候如果本地上传文件，你同样需要把README.md给download到本地
2、你可以在本地新建README.md文件，然后 git add README.md 上传到仓库
总之不管怎么样，远程仓库没有，本地就可以不要，远程仓库有，本地就必须有，保持一致

------

#### 参考链接：

参考文档: https://www.cnblogs.com/specter45/p/github.html

github入门到上传本地项目



Git 提示fatal: remote origin already exists 错误解决办法:

参考文档: http://blog.csdn.net/top_code/article/details/50381432



解决failed to push some refs to git：

参考文档: http://www.jianshu.com/p/835e0a48c825



$ git push -u origin master  推送代码到GitHub报错解决方法
Connection reset by 52.74.223.119 port 22
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

错误原因: 没有权限,重新生成 ssh key
$ ssh-keygen.exe -t rsa -C "17717874203@163.com"
参考文档: https://blog.csdn.net/Leolu007/article/details/79129446

