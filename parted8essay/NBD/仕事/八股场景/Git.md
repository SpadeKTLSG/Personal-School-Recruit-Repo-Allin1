‍

‍

# 概念

‍

### Git常用命令

以下是一些常用的 Git 命令及其用途：

1. **克隆仓库**：

    ```sh
    git clone <repository_url>
    ```
2. **查看当前状态**：

    ```sh
    git status
    ```
3. **添加文件到暂存区**：

    ```sh
    git add <file_name>
    ```
4. **提交更改**：

    ```sh
    git commit -m "commit message"
    ```
5. **查看提交历史**：

    ```sh
    git log
    ```
6. **查看分支**：

    ```sh
    git branch
    ```
7. **创建新分支**：

    ```sh
    git branch <new_branch_name>
    ```
8. **切换分支**：

    ```sh
    git checkout <branch_name>
    ```
9. **合并分支**：

    ```sh
    git merge <branch_name>
    ```
10. **拉取远程仓库的更改**：

     ```sh
     git pull
     ```
11. **推送更改到远程仓库**：

     ```sh
     git push
     ```
12. **查看远程仓库**：

     ```sh
     git remote -v
     ```
13. **添加远程仓库**：

     ```sh
     git remote add <name> <url>
     ```
14. **删除分支**：

     ```sh
     git branch -d <branch_name>
     ```
15. **强制删除分支**：

     ```sh
     git branch -D <branch_name>
     ```
16. **查看变更**：

     ```sh
     git diff
     ```

‍

‍

‍

## Git基础操作

‍

‍

### 删除除了master之外的所有分支

```text
git branch | grep -v "master" | xargs git branch -D
```

**注意点**

* 执行前需要切换到master分支执行
* 当前分支未做修改

‍

### 删除指定分支

#### 删除本地分支

```text
git branch -d 分支名（remotes/origin/分支名）
```

#### 强制删除本地分支

```text
git branch -D 分支名
```

#### 删除远程分支

```text
git push origin --delete 分支名（remotes/origin/分支名）
```

‍

‍

### 提交所有变化

```java
git add .

git commit -m'commit message'

git push
```

‍

### 提交指定文件

```text
git status

// 修改的文件

git commit filepath1 -m'commit message'

```

‍

‍

### git pull冲突解决

原因：其他人修改了某一文件的内容，而本地文件也被修改了，pull代码的时候就会产生冲突。

解决：贮存更改

操作步骤：

* git stash：将工作区恢复到上次提交的内容，同时备份本地修改
* git pull
* git stash pop：弹出最近保存的内容，查看对应文件，解决冲突

‍

‍

### 暂存

‍

‍

‍

## 软件开发模型

软件开发模型有很多种，比如瀑布模型（Waterfall Model）、快速原型模型（Rapid Prototype Model）、V 模型（V-model）、W 模型（W-model）、敏捷开发模型。其中最具有代表性的还是 **瀑布模型** 和 **敏捷开发**

**瀑布模型** 定义了一套完成的软件开发周期，完整地展示了一个软件的的生命周期。

‍

**敏捷开发模型** 是目前使用的最多的一种软件开发模型

像现在比较常见的一些概念比如 **持续集成**、**重构**、**小版本发布**、**低文档**、**站会**、**结对编程**、**测试驱动开发** 都是敏捷开发的核心。

‍

‍

# 大块

‍

‍

‍

# 高级

‍
