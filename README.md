# git_basic-operation
[**Git概述**](https://github.com/nichan-13/git_basic-operation#git%E6%A6%82%E8%BF%B0)

- [一、Git简介](https://github.com/nichan-13/git_basic-operation#%E4%B8%80git%E7%AE%80%E4%BB%8B)
- [二、Git代码托管](https://github.com/nichan-13/git_basic-operation#%E4%BA%8Cgit%E4%BB%A3%E7%A0%81%E6%89%98%E7%AE%A1)
- [三、Git工作流程](https://github.com/nichan-13/git_basic-operation#%E4%B8%89git%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B)

[**Git基本操作**](https://github.com/nichan-13/git_basic-operation#git%E5%9F%BA%E6%9C%AC%E6%93%8D%E4%BD%9C)

- [一、常用操作](https://github.com/nichan-13/git_basic-operation/blob/master/README.md#一常用操作)
- [二、分支操作](https://github.com/nichan-13/git_basic-operation/blob/master/README.md#二分支操作)
- [三、解决冲突](https://github.com/nichan-13/git_basic-operation/blob/master/README.md#三解决冲突)
- [四、修改已提交的commit注释](https://github.com/nichan-13/git_basic-operation/blob/master/README.md#四修改已提交的commit注释)

[**Git commit 规范**](https://github.com/nichan-13/git_basic-operation#git-commit-%E8%A7%84%E8%8C%83)

[**参考文档**](https://github.com/nichan-13/git_basic-operation#参考文档)

------------------------------

## Git概述

### 一、Git简介

Git是分布式版本控制系统（Distributed Version Control System，简称 DVCS） ，分为两种类型的仓库：
**本地仓库**和**远程仓库**。

- 本地仓库：是在开发人员自己电脑上的Git仓库
- 远程仓库：是在远程服务器上的Git仓库

 <img src="http://mms2.baidu.com/it/u=1539200278,1497704057&fm=253&app=138&f=PNG&fmt=auto&q=75?w=508&h=500" alt="流程图" style="zoom:50%;" />

> Clone：克隆，将远程仓库复制到本地
> Push：推送，将本地仓库代码上传到远程仓库
> Pull：拉取，将远程仓库代码下载到本地仓库

​		

### 二、Git代码托管

常用的Git代码托管平台有GitHub、码云(Gitee)、GitLab等。

- gitHub（ 地址：https://github.com/ ）是一个面向开源及私有软件项目的托管平台，因为只支持Git 作为唯一的版本库格式进行托管，故名 GitHub

- 码云（地址： https://gitee.com/ ）是国内的一个代码托管平台，由于服务器在国内，所以相比于GitHub，码云速度会更快

- GitLab （地址： https://about.gitlab.com/ ）是一个用于仓库管理系统的开源项目，使用Git作为代码管理工具，并在此基础上搭建起来的web服务

  ​		

### 三、Git工作流程

1. 从远程仓库中克隆代码到本地仓库
2. 从本地仓库中切换分支然后进行代码修改
3. 在提交前先将代码提交到暂存区
4. 提交到本地仓库,本地仓库中保存修改的各个历史版本
5. 修改完成后,将代码push到远程仓库

 ![Git常用命令](https://img-blog.csdnimg.cn/img_convert/774e705851446e315a780e04405dc417.png)

​		

​		

## Git基本操作

### 一、常用操作

- 创建本地库

  本地库(**Repository**)是一个目录，这个目录里面的所有文件都可以被Git管理起来，Git跟踪目录中每个文件的修改和删除，以便在将来某个时刻可以“还原”。

  ```
  # 在当前目录新建一个Git代码库
  $ git init
   
  # 新建一个目录，将其初始化为Git代码库
  $ git init [project-name]
  ```

  

- 复制远程仓库代码

  使用 **git clone** 从现有 Git 仓库中拷贝代码到本地库，在本地库创建完成之后，就可以使用 Git 命令来对本地库进行修改和管理分支

  > git基于多种传输协议，其中最常用的就是https和ssh。都是为了数据传输安全，设置ssh密钥的目的是为了节省输入用户名密码的过程，同时保证传输安全。并不是必须设置。

  ```
  $ git clone [url]
  ```

  

- 添加新文件

  git add 命令用于增加 Git 追踪的内容，把内容加入到本地代码库的暂存区

  ```
  # 添加所有文件
  $ git add .  /  git add -A
  
  # 添加指定文件
  $ git add [file1] [file2]
  
  # 取消文件暂存
  $ git reset [file]
  ```

  ​		

- 删除文件

    ```
    # 删除工作区文件，并且将这次删除放入暂存区
    $ git rm [file1] [file2] ...
    
    # 停止追踪指定文件，但该文件会保留在工作区
    $ git rm --cached [file]
    
    # 改名文件，并且将这个改名放入暂存区
    $ git mv [file-original] [file-renamed]
    ```

    ​	

- 将暂存区的文件修改提交到本地仓库

  提交内容到本地仓库，使用 -m 为该次提交添加说明

  > Git 每次提交代码，都要写 Commit message（提交说明），否则就不允许提交。一般来说，commit message 应该清晰明了，说明本次提交的目的。

  ```
  $ git commit -m "提交说明"
  ```

  ​	  

- 本地仓库关联远程仓库

  首次提交必须关联远程仓库后才能提交成功

  ```
  $ git remote add origin [url]
  ```

  ​		 

- 推送代码至远程仓库

  > `-u ` 会把本地的 master 分支和远程的 master 分支关联起来，在以后的推送或者拉取时就可以简化命令

  ```
  $ git push -u origin master
  ```

  ​		 

- 拉取远程仓库最新代码至本地仓库

  ```
  $ git pull
  ```

  ​		  

- 查看当前文件状态

    ```
    $ git status
    ```

​	

- 查看文件修改后的差异

  ```
  $ git diff [files]
  ```

  ​	

### 二、分支操作

几乎所有的版本控制系统都以某种形式支持分支。 使用分支意味着可以把自己的工作从开发主线上分离开来，以免影响开发主线。Git 的 master 分支并不是一个特殊分支， 它跟其它分支没有区别。

master 主分支应该非常稳定，用来发布新版本，一般情况下不允许在上面工作，工作一般情况下在新建的 dev 分支上工作，dev 分支代码稳定后可以合并到主分支 master 上来。

- 查看分支

  ```
  # 查看所有本地分支
  $ git branch
  
  # 查看所有远程分支
  $ git branch -r  
  
  # 查看所有远程和本地分支
  $ git branch -a
  ```

  ​		

- 本地仓库新建分支及切换分支

  ```
  # 新建分支
  $ git branch [branch-name]         
  
  # 从主分支切换至指定分支
  $ git checkout [branch-name] 
  
  # 创建分支并切换至该分支
  $ git checkout -b [branch-name]	
  ```



- 拉取远程分支并创建本地分支（本地分支名称可与远程分支名称不一致）

  - 方法一

    在本地新建分支 `dev` 并切换至改本地分支 `dev` 

    采用此种方法建立的本地分支会和远程分支建立映射关系

    ```
    $ git checkout -b 本地分支dev origin/远程分支dev
    ```

  - 方法二

    在本地新建分支 `dev` ，但是不会切换至该本地分支，需手动checkout

    采用此种方法建立的本地分支不会和远程分支建立映射关系

    ```
    $ git fetch origin 远程分支dev:本地分支dev
    ```

​	

- 本地分支和远程分支建立映射关系的作用

  建立本地分支与远程分支的映射关系（或者为跟踪关系track）

  这样使用 `git pull` 或者 `git push` 时就不必每次都要指定从远程的哪个分支拉取合并和推送到远程的哪个分支了

    - 查看所有与远程仓库具有映射关系的本地分支

      ```
      $ git branch -vv 
      ```

    - 手动建立映射关系 
      `origin` 为**git地址**的标志，可以建立当前分支与远程分支的映射关系

      ```
      $ git branch -u origin/[branch-name]  /  
      $ git branch --set-upstream-to origin/[branch-name]
      ```
      
    - 撤销本地分支与远程分支的映射关系
  
      ```
      $ git branch --unset-upstream
      ```
  
      之后可以再次用 `git branch -vv` 查看本地分支和远程分支映射关系
  
      ​		
  
- 将本地分支推送至远程仓库

  ```
  # 远程仓库不存在该分支
  $ git push --set-upstream origin [branch-name]
  
  $ git push origin master
  ```

  ​		

- 分支合并

  ```
  # 先切换至主分支
  $ git checkout master   
  
  # 将指定分支内容合并至主分支
  $ git merge [branch-name] 
  ```

  ​		

- 删除分支

  ```
  # 删除分支 
  $ git branch -d [branch-name]
  
  # 强制删除分支
  $ git branch -D [branch-name]
  
  # 删除远程分支
  $ git push origin --delete [branch-name]  /  $ git branch -dr [remote/branch]
  ```


​		

### 三、解决冲突
> 多人开发时显示代码有冲突无法操作
> error: Your local changes to 'c/environ.c' would be overwritten by merge.  Aborting.Please, commit your changes or stash them before you can merge.

1. 暂存当前本地代码
    ```
    $ git stash
      
    # 查看暂存列表
    $ git stash list
    
    # 暂存添加注释
    $ git stash save "XXX"
    
    # 将当前暂存弹出，并应用到当前分支对应的工作目录上
    $ git stash pop
      
    # 删除指定暂存
    $ git stash drop + 名称
      
    # 清除所有暂存
    $ git stash clear
    
    # 查看最新暂存和当前目录的差异
    $ git stash show
    
    # 查看指定暂存和当前目录的差异
    $ git stash show stash@{1}
    # 查看详细的不同
    $ git stash show -p
    ```
   
2. 拉取代码
    ```
    $ git pull
    ```
    
3. 还原暂存内容
    ```
    ### 还原暂存并从暂存列表删除暂存
    $ git stash pop stash@{id}
    ### 还原暂存不从列表删除暂存
    $ git stash apply stash@{id}
    ```
    > 系统提示如下类似的信息：
    > Auto-merging c/environ.c
    > CONFLICT (content): Merge conflict in c/environ.c
    > 意思就是系统自动合并修改的内容，但是其中有冲突，需要解决其中的冲突。
    
4. 与本地代码比较，手动解决冲突，完成这一步即可正常提交代码
   
   - `Updated upstream` 和 ===== 之间的内容是指主分支修改的内容
   - ==== 和 `stashed changes` 之间的内容就是本地分支修改的内容




### 四、修改已提交的commit注释

> 把最新的版本从远程仓库pull下来，按照以下步骤修改完成后，强制push到远程仓库
>
> **注：保证在修改注释之前没有其他人提交代码，因为修改注释需要强制push，如果在push之前有其他人提交了新的代码到远程仓库，然后又强制push，那么会被强制更新覆盖**

- 修改最后一次注释

  1. 进入最后一次注释提交

     ```
     $ git commit --amend
     ```

  2. 修改注释

     - vscode会自动弹窗显示，第一行为注释，修改后关闭窗口即可
     - 编辑方式：`i` --- 进入编辑模式，修改注释， `Esc键 ` --- 退出编辑模式， `:wq` --- 保存退出

  3. 强制提交

     ```
     $ git push -f
     ```

     ​	

- 修改已提交的某次注释

  1. 进入倒数n次注释提交

     ```
     $ git rebase -i HEAD~2
     ```

     - HEAD~n  表示显示倒数的n次注释

  2. 将要修改的注释前的 `pick` 改为 `edit`（可以修改多条）

     - vscode会直接弹出窗口显示，把 `pick` 改为 `edit` ，关闭窗口即可
     - 编辑方式：`i` --- 编辑，把 `pick` 换成 `edit` ， `Esc键` --- 退出编辑，`:wq` --- 保存退出

  3. 按照提示输入

     ```
     $ git commit --amend
     ```

     - vscode依旧会直接弹出窗口，修改注释后关闭窗口即可
     - 编辑方式：依旧修改注释后保存退出

  4. 按照提示输入

     ```
     $ git rebase --continue
     ```

     > 修改多个注释重复多遍步骤3和步骤4，直至修改完所有注释

  5. 强制提交

     ```
     $ git push -f
     ```

    ​	

## Git commit 规范

代码规范提交可以很好的保存代码修改日志，规范提交日志对于定位问题或代码回退具有极大意义。

现在主流的 commit message 规范就是 Angular 团队所用的准则，继而衍生了 [Conventional Commits specification](https://www.conventionalcommits.org/en/v1.0.0/) ,很多工具也是基于此规范。

每次提交，Commit message 都包括三个部分：header，body 和 footer，其中 header 有一个特殊的格式，包括了 type、scope、subject。

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

其中 header 是必选的，但是 header 里的 scope 是可选的，另外提交的 message 长度不要超过 100 个字符，太长了不易阅读。一般来说只要把 header 部分规范基本就能满足绝大部分需求。

- ##### type

  type 指明 git commit 的类别，应该使用以下类型

  - 『feat』: 新增功能

  - 『fix』: 修复 bug

  - 『docs』: 仅仅修改了文档，比如 README, CHANGELOG 等等

  - 『test』: 增加/修改测试用例，包括单元测试、集成测试等

  - 『style』: 修改了空行、缩进格式、引用包排序等等（不改变代码逻辑）

  - 『perf』: 优化相关内容，比如提升性能、体验、算法等

  - 『refactor』: 代码重构，「没有新功能或者 bug 修复」

  - 『chore』: 改变构建流程、或者增加依赖库、工具等

  - 『revert』: 回滚到上一个版本

  - 『merge』: 代码合并

    

- ##### scope（可选）

  scope 用于说明 commit 影响的范围，根据不同项目有不同层次描述。若没有特殊规定，也可以描述影响的哪些功能等。

  ​	

- ##### subject

  subject 是 commit 目的的简短描述，不超过 50/80 个字符，一般 git 提交的时候会有颜色提示。

  - 若英文用不惯，那么推荐使用中文

  - 若是开源代码，一律推荐统一英文，英文不行可以翻译软件用起来

  - 若是开源代码，可以再附加对应的 issue 地址

  - 结尾不加标点符号

    

- ##### 工具：Commitizen

  Commitizen 是一个撰写合格 Commit message 的工具，用于代替 git commit 指令，而 cz-conventional-changelog 适配器提供 conventional-changelog 标准（约定式提交标准）。基于不同需求，也可以使用不同适配器。

  [Commit message 和 Change log 编写指南](https://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)

  [规范提交git commitizen conventional-changelog-cli](https://www.cnblogs.com/mengfangui/p/12634845.html)

  

## 参考文档

- [Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)

- [常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)
