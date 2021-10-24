# Git 学习

## Git & Version Control

- Git：开源、免费的版本控制系统（Version Control）

> Git 和 GitHub的区别：Git是一个版本控制系统，是一个软件。GitHub是一个网站，是一个存储通过Git进行版本控制的软件代码的仓库，可以通过该网站进行多人协作软件开发工作。

- Version Control：保存对于代码的每一次修改，因此可以随时查看以往的代码，便于进行软件开发。

## 常见词汇

- CLI：命令行界面

- Repository：项目，或是保存项目的文件夹

## Git命令

- clone：下载GitHub网站上的代码到本地

- add：向Git中保存对于文件的修改（增删改等）

- commit：将文件保存到Git中

- push：将Git中的修改过的文件上传到GitHub等远程仓库中

- pull：将GitHub中被他人修改过的文件下载到本地

## SSH Keys

> 在Linux（Ubuntu）系统环境操作。具体看https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agenthttps://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

1. 生成公私密钥
   
   - 在命令行中输入：
     
     ```shell
     $ ssh-keygen -t ed25519 -C "your_email@example.com"
     或
     $ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
     ```
     
     > [your_email@example.com] 是注册GitHub账户时所使用的邮箱
   
   - 给所生成的密钥对命名。该名称包含路径，若不指明路径，则在当前目录下保存。按回车以括号内默认名命名
     
     ```shell
     > Enter a file in which to save the key (/home/you/.ssh/key): [Press enter]
     ```
   
   - 给私钥添加密码。按回车表示空密码
     
     ```shell
     > Enter passphrase (empty for no passphrase): [Type a passphrase]
     > Enter same passphrase again: [Type passphrase again]
     ```

2. 添加SSH Keys到ssh-agent
   
   - 启动ssh客户端
     
     ```shell
     $ eval "$(ssh-agent -s)"
     > Agent pid 59566
     ```
   
   - 添加之前生成的私钥
     
     ```shell
     $ ssh-add ~/.ssh/key
     ```

3. 将SSH Keys添加到GitHub账户
   
   - 查看公钥密码，并复制其值（ssh-rsa也要复制）
     
     ```shell
     $ cat ~/.ssh/key.pub
     ```
   
   - 在GitHub网站，点击自己头像下拉框 - settings - SSH and GPG keys。点击 SSH Keys 旁 **New SSH Key**，粘贴公钥值，完成添加

## 在VSCode上使用Git

> 本地Git讲解：在本地Git项目文件夹中，会有一个 .git 文件夹，该文件夹保存有对于该项目的所有修改。

1. 创建Git Repository
   
   - 从GitHub上直接导入已有Repository
     
     - 复制GitHub项目链接地址 github_address
     
     - 在VSCode命令行中输入，敲击回车。下载完成后即完成创建
       
       ```shell
       $ git clone github_address
       ```
   
   - 本地创建Git Repository并连接到GitHub上
     
     - 在GitHub上创建一个新的空项目，并复制其链接地址 github_address
     
     - 用VSCode打开项目文件夹，在命令行中输入下列语句以完成Git项目的创建
       
       ```shell
       $ git init
       ```
     
     - 在命令行中输入下列语句，完成与GitHub的连接
       
       ```shell
       $ git remote add origin github_address
       ```
     
     - 在命令行中输入下列语句，检测该项目所连接的GitHub
       
       ```shell
       $ git remote -v 
       ```

2. 查看Git状态
   
   - 在命令行中输入下列语句，查看该Git项目中所作的修改
     
     ```shell
     $ git status
     ```

3. add命令
   
   - add命令用于向Git说明要记录哪些文件的修改（每次修改后都要使用add进行说明）
   
   - 使用 add + 文件夹或文件名，表示使用Git对于该文件夹或文件的修改进行记录
     
     ```shell
     $ git add dir/filename
     ```
   
   - 使用 add . 表示对于当前文件夹内所有内容的修改进行记录
     
     ```shell
     $ git add .
     ```

4. commit命令
   
   - 使用 commit 命令向Git说明保存修改记录，使用方法如下：
     
     ```shell
     $ git commit -m "changes" -m "description"
     ```
   
   - -m：message，消息
   
   - 第一个 -m 后，双引号内写上所进行的修改，如添加了某个文件，或修改了某个文件
   
   - 第二个 -m 后，双引号内写上对于此修改所做的具体描述，可以不写第二个 -m 及以后内容
   
   > 使用下列命令，可以同时进行 add 和commit 操作，但仅限于被修改过的文件，而不可用于新增文件
   > 
   > ```shell
   > $ git commit -am "xxx" -m "description"
   > ```

5. push命令
   
   - 使用push命令用于将本地Git中的内容上传到GitHub中
   
   - 完全版：
     
     ```shell
     $ git push origin main
     ```
     
     - origin：
     
     - main：所要保存到的GitHub项目的分支（brunch），默认为main或master
   
   - 简化版：
     
     - 指明默认保存的分支
       
       ```shell
       $ git push -u origin main
       ```
     
     - 简化命令
       
       ```shell
       $ git push
       ```

6. pull命令
   
   - 使用pull命令下载GitHub中指定分支的内容(main 为所要下载的分支)
     
     ```shell
     $ git pull origin main
     ```

## Git brunch

- 查看当前所有分支
  
  ```shell
  $ git branch
  ```

- 创建新分支
  
  ```shell
  $ git checkout -b branchname
  ```

- 删除分支
  
  ```shell
  $ git branch -d branchname
  ```

- 切换分支
  
  ```shell
  $ git checkout branchname
  ```

- 查看两个分支间的不同：查看branchname分支与当前分支的不同
  
  ```shell
  $ git diff branchname
  ```

- 上传分支
  
  ```shell
  $ git push origin branchname
  ```

- 创建PR分支：主要在GitHub上进行可视化操作，依循指示即可。
  
  > PR分支主要是用于向外公布，人们可以对于当前项目进行评论、提建议，甚至可以对于某一行具体代码进行建议。当收集到足够的建议后，开发者可以选择将PR分支合并到主分支中，合并完成后PR分支将关闭。

- 合并分支：将branchname合并到当前分支
  
  ```shell
  $ git merge branchname
  ```

- 处理分支冲突：主要存在与多人同时对主分支进行修改时，此时可能代码的同一行会存在多个不同的修改，造成冲突。

## Git撤销

- 取消上一步的add命令
  
  ```shell
  $ git reset
  ```

- 取消上一步的commit命令
  
  ```shell
  $ git reset HEAD~1
  ```

- 查看commit记录，将会以最近修改为顺序展示修改记录，按空格键翻页。每个记录会有一个特定的hash值
  
  ```shell
  $ git log
  ```

- 取消到指定的commit命令，复制从log中查到的指定记录的hash值commit_hash
  
  ```shell
  $ git reset commit_hash
  ```

- 取消并恢复代码到指定的commit命令，复制从log中查到的指定记录的hash值commit_hash
  
      $ git reset --hard commit_hash
