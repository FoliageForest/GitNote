# 可用命令

* `git init <文件名>`  
* `git init`  
* `git clone [url]`  
* `git clone [url] <name>`  
* `git config --global user.name "FoliageForest@LAPTOP-PCTGUH7L"`  
* `git config --global user.email "123456@qq.com"`
* `git config user.name "FoliageForest@LAPTOP-PCTGUH7L"`
* `git config user.email "123456@qq.com"`
* `git config --global core.quotepath false`
* `git config core.quotepath false` （解决 `git status` 中文文件名无法正常显示的问题）
* `git config core.editor nano`  
* `git config core.editor vim`  
* `git diff` (如果在上一次提交后修改了文件, 用此命令可查询修改的行)  
* `git add <file>...`  
* `git reflog`  
* `git log --oneline --decorate --graph --all`  
* `git log`  
* `git log --oneline` 简洁的提交历史  
* `git log --pretty=oneline`  
* `git log -p`  
* `git log -2`  
* `git log -p -2`  
* `git restore --staged <file>...` (一个文件修改后用了 git add, 但我后悔 使用 git add, 可以用该命令)  
* `git -p -2 --pretty=oneline`  
* `git rm --cached <file>...`  
* `git reset --hard HEAD^^`  
* `git reset --hard HEAD~2`
* `git reset --hard <commit id>`  
* `git restore <name>`  
* `git remote -v` 查看当前仓库所对应的远程仓库的别名和地址  
* `git commit -m <message>`  
* `git commit -a`  
* `git branch` 查看分支  
* `git branch -avv` 查看分支  
* `git branch <name>` 创建一个新的分支但是不切换到新创建的分支  
* `git branch -m new-branch-name` 把当前分支名修改为 new-branch-name  
* `git checkout <name>` 切换当前分支  
* `git checkout -b <your-branch-name>` 创建一个新的分支同时切换到新创建的分支  
* `git merge <name>`  
* `git commit <commit id>`  
* `git stash`  
* `git stash pop`  

快速初始化仓库并完成配置（需替换 `<仓库名>`）：  

``` bash
git init <仓库名> && cd <仓库名> && git config user.name "FoliageForest@LAPTOP-PCTGUH7L" && git config user.email "123456@qq.com"
```

快速创建提交：

``` bash
nano README.md && git add . && git commit -m "commit"
```

命令 `git restore <文件名>` 和 `git restore --staged <文件名>` 的使用。  
命令 `git restore <文件名>`：**用暂存区的** `<文件名>` **文件覆盖工作区的** `<文件名>` **文件**。一个例子：  

1. 初始化本地仓库及其状态：  

``` shell
$ git init learnGit
$ cd learnGit/
$ git config user.name "Admin@LAPTOP"
$ git config user.email "Admin@email.LAPTOP"
$ git config core.editor nano
$ nano README.md
$ cat README.md
A

$ git add README.md
$ git commit -m "First commit"
$ nano README.md
$ cat README.md
AB

$ git add README.md
$ nano README.md
$ cat README.md
ABC

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md
```

2. 使用 `git restore --staged <file>...` 命令  

``` shell
$ git restore --staged README.md
$ cat README.md
ABC
$ git status
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

3. 当暂存区无文件时的 `git restore <file>...`  

``` shell
$ git restore README.md
$ cat README.md
A

$ git status
On branch master
nothing to commit, working tree clean
```

4. 当暂存区有文件时的 `git restore <file>...`  

``` shell
$ nano README.md
$ cat README.md
AB

$ git add README.md
$ nano README.md
$ cat README.md
ABC

$ git restore README.md
$ cat README.md
AB
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md
```

2. 将文件 `README.md` 的内容修改为 `AB`  

3. 运行 **`git restore README.md`**。该命令会**用暂存区的** `README.md` **文件覆盖工作区的** `README.md` **文件**  

# SSH key 生成

> 来源: 掘金社区字节跳动课程 PPT  
> 
> SSH 可以通过公私钥的机制, 将生成公钥存放在服务端, 从而实现免密访问  
> 目前的 Key 的类型四种, 分别是 dsa, rsa, ecdsa, ed25519  
> **默认使用的是 rsa**, 由于一些安全问题, 现在已经不推荐使用 dsa 和 rsa 了, 优先推荐使用 ed25519  
> `ssh-keygen -t ed25519 -C "your_email@example.com"`  
> 密钥默认存储在 ~/.ssh/id_ed25519.pub  

使用 `ssh -T git@github.com` 测试连接

# 上传本地已有仓库

```bash
git remote add origin https://github.com/guyibang/TEST2.git
```

```bash
git push -u origin master # 首次提交, 远程仓库为空
git push origin master # 已有远程仓库, 不是第一次提交
```

# 查看远程仓库

```bash
git remote -v
```

# Windows 更新 git

> `git update-git-for-windows # Windows更新Git`  
> 来源: <https://github.com/seven-innovation-base/Git2Github-practice/tree/main/%E8%87%B4%E5%A4%A7%E4%B8%80>  

# 重命名 git 分支

法一: checkout 到需要重命名的分支 (`git checkout branch-name`) 后, 使用 `git branch -m new-branch-name`  
法二: checkout 到 master/main 分支中后, 使用 `git branch -m old-branch new-branch`  