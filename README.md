# git_basic-operation
**Git基本操作**
- [一、拉取代码及代码推送](https://github.com/nichan-13/git_basic-operation/blob/master/README.md#一拉取代码及代码推送)
- [二、分支操作](https://github.com/nichan-13/git_basic-operation/blob/master/README.md#二分支操作)
- [三、修改已提交的commit注释](https://github.com/nichan-13/git_basic-operation/blob/master/README.md#三修改已提交的commit注释)

------------------------------


## Git基本操作

### 一、拉取代码及代码推送

- 拉取远程仓库代码

  ```
  $ git clone https://github.com/xxxx/xxxx.git
  ```

- 查看当前状态

  ```
  $ git status
  ```

  ​	

- 添加本地仓库所有修改或增加的文件 / 指定文件

  ```
  $ git add .    /    $ git add xxx.md
  ```

- 提交修改

  ```
  $ git commit -m "说明文字"
  ```

- 推送代码至远程仓库

  ```
  $ git push
  ```

- 拉取远程仓库最新代码至本地仓库

  ```
  $ git pull
  ```

  ​	

### 二、分支操作

- **本地分支操作**

  - 查看本地分支

    ```
    $ git branch
    ```

  - 本地仓库新建分支,切换分支 / 新建并切换至新分支

    ```
    $ git branch test         // 新建 test 分支
    $ git checkout test       // 从主分支切换至 test 分支
    $ git checkout -b test    // 创建 test 分支并切换至 test 分支
    ```

    - 此时可向 `test` 分支添加文件并提交

      ```
      $ git add .
      $ git commit -m "test"
      ```

      ​	

    - 将本地分支推送至远程仓库（远程仓库不存在该分支）

      ```
      $ git push --set-upstream origin test
      ```

    - 将 `test` 分支与主分支 `master` 合并

      ```
      $ git checkout master    // 切换至主分支
      $ git merge test         // 内容合并至主分支
      ```

    - 删除分支 / 强制删除分支

      ```
      $ git branch -d test    /    $ git branch -D test
      ```

    - 此时可向远程仓库推送代码

      ```
      $ git push
      ```

    - 删除远程分支

      ```
      $ git push origin --delete test
      ```

      ​	

- **远程分支与本地分支操作**

  - 查看分支

    ```
    $ git branch -r    // 查看所有远程分支
    $ git branch -a    // 查看所有远程和本地分支
    ```

  - 拉取远程分支并创建本地分支（本地分支名称可与远程分支名称不一致）
  
    - 方法一
  
      在本地新建分支 `dev` 并切换至改本地分支 `dev` 
      
      采用此种方法建立的本地分支会和远程分支建立映射关系
      
      ```
      $ git checkout -b 本地分支名dev origin/远程分支名dev
      ```
  
    - 方法二

      在本地新建分支 `dev` ，但是不会切换至该本地分支，需手动checkout

      采用此种方法建立的本地分支不会和远程分支建立映射关系

      ```
      $ git fetch origin 远程分支名dev:本地分支名dev
      ```
    
  - 此时可向 `dev` 分支添加文件并提交
    
    ```
    $ git add .
    $ git commit -m "update dev"
    ```
    
  - 将分支代码合并到主分支并推送
    
    ```
    $ git checkout master       // 切换至主分支
    $ git merge dev             // 将 dev 分支合并到主分支
    $ git push origin master    // 将代码推送至远程仓库
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
      $ git branch -u origin/分支名
      ```

      ```
      $ git branch --set-upstream-to origin/分支名
      ```

    - 撤销本地分支与远程分支的映射关系

      ```
      $ git branch --unset-upstream
      ```

      之后可以再次用 `git branch -vv` 查看本地分支和远程分支映射关系
      
      ​	

### 三、修改已提交的commit注释

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

       