## 三、为Github账户设置SSH key

**3.1、 生成ssh key**

首先检查是否已生成密钥 cd ~/.ssh，ls如果有3个文件，则密钥已经生成，id_rsa.pub就是公钥

 ![img](https://img2018.cnblogs.com/blog/774824/201907/774824-20190711145416020-932560671.png)

 

如果没有，输入: ssh-keygen -t rsa -C "你的邮箱"

![img](https://img2018.cnblogs.com/blog/774824/201907/774824-20190711155135006-458973993.png)

 

**3.2、复制ssh key**

 方法1: 输入 clip < ~/.ssh/id_rsa.pub  会自动复制ssh key，可以直接粘贴

![img](https://img2018.cnblogs.com/blog/774824/201907/774824-20190711150857630-1321965671.png)

 方法2:在c/Users/Administrator/.ssh/id_rsa)文件找到直接复制

![img](https://img2018.cnblogs.com/blog/774824/201907/774824-20190711150932612-1478161474.png)

 

 

**3.3、连接github，打开GitHub 进入setting找到ssh key并新建**

![img](https://img2018.cnblogs.com/blog/774824/201907/774824-20190711151830920-877566481.png)

![img](https://img2018.cnblogs.com/blog/774824/201907/774824-20190711152017912-1651603673.png)

![img](https://img2018.cnblogs.com/blog/774824/201907/774824-20190711152242633-1972966452.png)

 

**3.4、然后测试连接是否成功**

输入: ssh -T git@github.com 

![img](https://img2018.cnblogs.com/blog/774824/201907/774824-20190711152508736-450105130.png)

 

**3.5、进入本地要提交项目文件的的所在位置右键点击打开Git Bash Here 或者在当前命令窗口 执行 cd F:\test 进入目录。**

 然后依次执行

　1、git init  

  2、git add .

  3、git commit -m "提交描述"

  4、git remote add origin https://github.com/MyJoanna/test.git  （这里的 https://github.com/MyJoanna/test.git 是你的仓库地址）

  5、git push -u origin master  

![img](https://img2018.cnblogs.com/blog/774824/201907/774824-20190711154006660-1638758494.png)

 

最后我们就可以在GitHub的仓库上看到我们提交上去的代码了