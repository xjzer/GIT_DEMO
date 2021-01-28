

#### Git简单操作指南

使用工具 github1+Ubuntu18.04+git

#### 资料来源

- ```
  git 简明指南 https://www.runoob.com/manual/git-guide/
  
  图解git及原理 http://marklodato.github.io/visual-git-guide/index-zh-cn.html#checkout
  
  git使用教程 https://mubu.com/app/edit/home/1lxWcxIplm5#m
  
  配套视频 https://www.bilibili.com/video/BV1Mk4y1y7jR?p=7
  ```

#### 理论基础

- 三棵树

  ```
  工作区 暂存区 Git仓库
  ```

- Git管理的文件有三种状态

  ```
  已修改 modified
  已暂存 staged
  已提交 committed
  ```

  

#### 实用技巧

- 过程

  ```bash
  #彩色的 git 输出：
  git config color.ui true
  #内建的图形化 git：
  gitk
  #显示历史记录时，每个提交的信息只显示一行：
  git config format.pretty oneline
  #交互式添加文件到暂存区：
  git add -i
  ```




#### 准备工作

- 过程

  ```bash
  #配置提交人姓名
  git config --global user.name 姓名
  
  #配置提交人邮箱
  git config --global user.email 邮箱
  
  #查看配置信息
  git config --list
  ```


#### 基本操作

- 过程

  ```bash
  #初始化git仓库：在新建文件夹下会新建一个.git隐藏文件夹
  git init
  
  #查看文件状态
  git status
  
  #追踪文件：将想要被git管理的文件添加到暂存区中
  git add 文件
  #追踪所有文件
  git add . 
  
  #向仓库中提交代码：每次只包含一个功能，或者一个功能中包含bug的修改，便于恢复更改
  git commit -m 提交信息
  
  #查看提交记录
  git log
  ```



#### 撤销/删除

- 过程

  ```bash
  #删除暂存区和工作区的文件
  git rm filename
  
  #用暂存区中的文件覆盖工作目录中的文件（暂存区不受影响）
  #适用于 工作目录中的文件存在问题
  git checkout 文件名
  
  #将文件从暂存区中删除，工作区不受影响
  #适用于 将不想提交的临时文件从暂存区删除
  git rm --cached 文件名
  
  #将git仓库中指定的更新记录恢复出来，并且覆盖暂存区和工作目录，且在这条更新记录之后的提交也被删除
  #适用于 工作目录和仓库中的代码都存在问题，希望将更早的提交记录恢复，并且删除有问题的提交记录
  git reset --hard commitID
  ```

#### 分支

- 通俗理解

  复制了一份工作目录，但在git中实现的方法更加复杂

- 使用场景

  一个分支上开发新功能，另一个分支上修复之前的bug，并且互不影响

- 一般使用

  1. 主分支（master）

     保持稳定

  2. 开发分支（develop）

     基于master分支创建。

     开发分支功能累积到一定程度以后再合并到主分支

     也要保持最大程度的稳定性

  3. 功能分支（feature）

     作为开发具体功能的分支，基于开发分支创建。

     功能分支完成后将功能分支中的代码合并到开发分支，这时功能分支就可以删除了。

- 过程

  ```bash
  #查看分支 
  git branch
      git branch -a（查看本地和远程的所有分支）
      git branch -r（查看远程分支）
      结果*表示当前分支
      
  #创建分支
  git branch 分支名称
  	在哪个分支操作就是基于哪个分支创建副本
  	
  #切换分支
  #注意切换分支前将当前分支的工作要提交到仓库，防止将当前未提交的文件携带到其他分支，如果不想提交还想切换，查看第4点
  git checkout 分支名称
  	在切换分支之前，当前分区工作目录的文件一定要提交到git仓库中，保持当前分支工作区完全干净。
  
  #合并分支
  #使用场景 当前分支的工作已经完成，合并当前分支的工作成果
  git merge 来源分支
  	当前分支的工作已经完成，需要合并到其他分支，原来的分支依然存在，可以回去继续开发。
  	如果要把develop合并到master分支，先切换到master分支，然后输入合并命令。
  
  #删除分支
  git branch -d 分支名称 （分支被合并后才允许删除，-D强制删除）
  	某一分支工作哦已经完成，且不需要继续存在。
  	先切换到其他分支，才能删除当前分支。
  	如果要删除的分支不想合并，用D强制删除
  ```

#### 暂时保存更改

- 使用场景

  分支临时切换：当前正在开发分支写新功能，但要去别的分支修改bug，而新功能未写完不想提交到仓库。

- 过程

  ```bash
  #存储临时改动
  git stash
  
  #恢复改动
  git stash pop
  ```

- 注意事项

  **请勿在其他分支上恢复，不然就会将文件携带到其他分支**

#### github

1. 注册、创建远程仓库（省略）
2. 程序员A推送本地仓库到远程仓库

   ```bash
   #将本地分支的更新，推送到远程仓库。
   git push 远程仓库地址 分支名称
   	WIN10将用户名和密码存储在控制面板-凭据管理器-windows凭据中
   #简化 为远程仓库创建别名
   git remote add 远程仓库地址别名 远程仓库地址
   	别名一般写作 origin，之后推送到远程仓库直接写作
   git push origin 分支名称
   
   #再次简化
   git push -u 远程仓库地址别名 分支名称
   	记住远程仓库别名和分支名称，下次提交只需要git push即可
   ```

3. 程序员B将远程仓库克隆到本地进行开发

   ```bash
   #不需要身份验证
   git clone 仓库地址
   ```

   初始程序员A邀请B共同开发，从而B也可以将更新的代码上传到远程仓库，否则B只能克隆到本地开发。

   ```
   github项目界面-settings-寻找到邀请collaborators-输入其用户名即可
   ```

4. 程序员A从远程仓库获取最新的版本

   ```bash
   #获取指定分支
   git pull 远程仓库地址 分支名称
   #获取所有分支
   git pull -all
   ```

5. 注意事项

   - git clone 只在第一次加入开发时使用
   - 如果本地版本低于远程仓库，不能直接向远程仓库推送，要把远程仓库先pull到本地，然后再推送

#### 解决冲突之团队协作

- 使用场景

  程序员A和B属于统一开发团队，并且修改了代码的同一处地方，一方A提交到远程仓库后，另一方B提交会失败。

  此时B需要先将远程仓库的内容先拉取到本地。

  拉取成功后会提示存在冲突(conflict)，然后去指定文件处理冲突。

  <<<<<<表示冲突的开始，>>>>>>表示冲突的结束。

  处理完毕后再次上传即可。

#### 解决冲突之非团队协作

- 使用场景 

  程序员A和B不属于同一开发团队，B提交代码后，由仓库管理者A审核通过后才能生效。

- B如何提交

  ```bash
  #B将A的仓库复制一份到自己的仓库
  	在该仓库页面点击fork
  
  #B将自己的那一份克隆到本地(没有测试将A克隆到本地)
  
  #B对代码进行修改，上传
  
  #B向A发出修改请求
  	在B的github仓库界面 ==》Pull request ==》New pull request ==》 Create ==》写好主题与描述
  ```

- A如何审核

  ```bash
  #A查看请求
  	点击合并请求(Pull request)可以查看会话(Conversation)，提交项(Commit)，改变的内容
  #A同意请求
  	点击会话,在下方点击Merge pull request ==》添加描述(与-m的作用一样) ==》确认
  #A
  	此时，
  ```

#### ssh免登陆上传

- 认证方式 

  公钥+私钥

  公钥相当于门锁，放在github的账户中。

  私钥相当于钥匙，放在本地

  上传时，ssh认证成功即可完成上传。

- 私钥生成

  ```bash
  #输入命令
  ssh-keygen
  (会提示需要保存到的目录)直接使用默认值，一路回车即可
  
  #根据刚才的路径找到公钥和私钥
  公钥名称：id_rsa.pub
  私钥名称：id_rsa
  ```

- github设置

  ```bash
  #将公钥放在github中
  	打开公钥文件全选复制 ==》头像 ==》settings ==》SSH and GPG keys ==》粘贴到key中提交
  
  #设置仓库
  	头像 ==》Your repositories ==》选择仓库 ==》 code ==》ssh ==》复制
  ```

- 使用ssh免登录上传

  ```bash
  #起别名
  git remote add origin_ssh git@github.com:xjzer/GIT_DEMO.git
  #上传
  git push origin_ssh 分支
  ```

#### Git忽略清单

- 使用场景

  将不需要被git管理的文件名字添加到此文件中，在执行git命令的时候，git就会忽略这些文件。

- 过程

  ```bash
  #创建忽略清单
  touch .gitignore
  
  #添加想要忽略的文件或文件夹
  	将文件或文件夹的名称写入，每行一个
  	
  #测试
  git add .
  	发现刚才被忽略的内容没有放到暂存区
  ```

#### 为仓库添加详细说明

- 过程

  ```bash
  #方法1
  项目根目录 ==》vi readme.md ==》写入说明(可以使用专门的编辑器Typora打开) ==》保存上传
  #方法2
  github仓库页面 ==》ADD A README
  ```

  

