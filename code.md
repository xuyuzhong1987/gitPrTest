# Code

> 常用命令和操作一览

## fork

准备上游代码库，并 fork 这个代码库，例如，代码库地址为：<git@github.com:xuyuzhong1987/gitPrTest.git>，这个原始的代码库称之为上游代码库（upstream）。

- 原始仓库：xuyuzhong1987/gitPrTest
- fork 后的仓库：djyuning/gitPrTest

克隆 djyuning/gitPrTest 到本地电脑，并设置 remote。

```bash
# 显示设置 origin
$ git remove set-url origin git@github.com:djyuning/gitPrTest.git

# 然后设置 upstream
$ git remove set-url upstream git@github.com:xuyuzhong1987/gitPrTest.git

# 查看设置
$ git remote -v
# origin  git@github.com:djyuning/gitPrTest.git (fetch)
# origin  git@github.com:djyuning/gitPrTest.git (push)
# upstream        github-xyz1987:xuyuzhong1987/gitPrTest.git (fetch)
# upstream        github-xyz1987:xuyuzhong1987/gitPrTest.git (push)
```

在以后的协作中，每次提交代码前，我们需要拉取上游代码：

```bash
git fecth upstream
```

这会把上游的代码拉取到一个名为 upstream/master 的分支中，然后，我们使用本地 master 分支 rebase 到 upstream/master 分支。

```bash
# 切换到 master 分支
$ git checkout master

# 变基到 upstream/master 分支
$ git rebase upstream/master
```

## Pull request

使用 Github 的 Pull request 可以把 fork 出来的代码库请求合并到上游代码库，也就是所谓的贡献代码。

我们本地的代码提交后，可以基于我们的最新代码创建一个 Pull request。

上游仓库的代码管理者，会对 PR 的代码进行 Review 操作，如果存在冲突，Review 的时候需要先解决冲突，最后使用 【rebase and merge】，不要使用默认的【Marge and commit】，通常这会多出一条无意义 commit。

```bash
git rebase -i HEAD~2
```

## 冲突设置

fork 的代码库刚刚同步了上游代码库的修改，还没来得及提交，我们的上游代码库又做了新的修改，这次还涉及到了相同的文件修改。
