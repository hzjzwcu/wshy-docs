# GIT 命令

# 常见指令

- 只拉取指定分支代码
  - `git clone --single-branch -b 分支名 仓库链接`
  - `git clone -b <branch-name> --single-branch <repository-url>`
- 查看所有分支
  - `git branch -r`

-   创建并切换分支
    -   `git checkout -b 分支名`
-   回到指定版本
    -   `git reset --hard 版本号`
-   使用某分支强制覆盖
    -   `git reset --hard origin/分支名`
-   合并分支到 master
    -   `git checkout master`
    -   `git merge 分支名` 也可 `git merge --no-commit 分支名`从而部分合并
    -   `git push origin master`
-   删除远程分支
    -   `git fetch -p origin`（如果不能删除的话）
    -   `git push origin --delete 分支名`
-   删除本地分支
    -   `git branch -d 分支名`

## 统计数据

-   查询单人提交某段时间所有记录
    -   `git log --since ==2021-01-01 --until=2021-05-31 --author="weisheng" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "新增： %s , 移除： %s , 总计： %s \n ", add, subs, loc }'`
-   查询单人提交所有记录
    -   `git log --author="weisheng" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "新增: %s, 移除 %s, 总计: %s\n", add, subs, loc }'`

## 保存修改并拉取代码

在使用 Git 时，如果你想拉取（`pull`）最新的代码，同时又不想影响到你当前已经更改但尚未提交（`commit`）的内容，你可以使用以下几种方法：

`git stash` 可以临时保存你的工作进度，让你的工作目录回到最近一次 `commit` 的状态。之后你可以安全地拉取最新的代码，然后再应用（`apply`）你之前保存的更改。

步骤如下：

1. **保存当前更改**：

   ```
   bashCopy code
   git stash
   ```

   或者，为你的 stash 创建一个有意义的名字：

   ```
   bashCopy code
   git stash save "你的描述信息"
   ```

2. **拉取最新代码**：

   ```
   bashCopy code
   git pull
   ```

3. **应用之前保存的更改**：

   ```
   bashCopy code
   git stash apply
   ```

   如果你创建了多个 stash，你可以通过 `git stash list` 查看所有的 stash，并通过 `git stash apply stash@{n}` 应用指定的 stash，其中 `n` 是你想要应用的 stash 的编号。

### 注意事项

- 在使用这些命令之前，确保你的工作目录是干净的，即除了你想要保留的更改之外，没有其他未提交的更改。这可以通过 `git status` 命令来检查。
- 如果你使用 `git stash` 并且在 `git stash apply` 之后发现有冲突，你需要手动解决这些冲突。解决冲突后，不要忘记使用 `git add` 将解决后的文件标记为已解决，然后继续你的工作。
- 使用 `git pull --rebase` 时，如果遇到冲突，同样需要手动解决冲突，并使用 `git rebase --continue` 继续 rebase 过程。

选择哪种方法取决于你的具体情况和个人偏好。在处理较大的更改或多个分支时，`git stash` 可能是更安全的选择。对于较小的更改，`git pull --rebase` 可能更方便快捷。

## 本地仓库关联远程

- `git init` 初始化
- `git remote add origin 仓库链接` 关联仓库
- `git fetch origin 分支名`（不填分支名会全部拉取）
- `git checkout -b 分支名 origin/分支名` 新建并关联分支

## hosts

```
140.82.112.3 github.com
199.232.69.194 github.global.ssl.fastly.net
185.199.108.153 assets-cdn.github.com
185.199.109.153 assets-cdn.github.com
185.199.110.153 assets-cdn.github.com
185.199.111.153 assets-cdn.github.com
```

