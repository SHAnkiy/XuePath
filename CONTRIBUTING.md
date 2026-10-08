# XuePath 协作手册

这份手册供团队成员查阅日常 Git 与 PR 操作。[AGENTS.md](AGENTS.md) 维护项目背景与 AI 协作规则；本手册解释操作流程，不另设一套项目规则。两份文件涉及同一约定时应保持一致，约定调整也通过 PR 审阅。

## 1. 开始一项工作

先阅读 [README.md](README.md)，明确这次要解决的问题，检查工作区，保留自己和他人已有的修改。若有未提交内容，先妥善提交或暂存，再切换分支。

首次克隆使用组织地址：

```sh
git clone https://github.com/Xue-Path/XuePath.git
```

已有本地仓库仍使用旧地址时，更新一次：

```sh
git remote set-url origin https://github.com/Xue-Path/XuePath.git
```

每项新工作从最新 main 建立工作分支，例如：

```sh
git fetch origin --prune
git switch main
git pull --ff-only origin main
git switch -c docs/interview-questions
```

分支名简要描述任务，可使用 `docs/`、`feat/`、`fix/` 前缀。不要直接在 main 上提交；同一分支尽量只处理一个主题。如果同步失败或出现分叉，先检查原因，不用强推或重置覆盖修改。

## 2. 提交并创建 PR

修改后检查内容和链接。目前项目只有文档，执行 `git diff --check`，并确认候选想法没有被写成已实现功能、未确认事项没有被写成决定。原始 PDF 和原文转录副本的处理遵循 AGENTS.md。

只暂存本次任务涉及的文件，再查看将提交的差异：

```sh
git add <本次修改的文件路径>
git diff --cached
git diff --cached --check
git commit -m "docs: describe interview questions"
git push -u origin docs/interview-questions
```

在 GitHub 创建以 main 为目标的 PR，按模板说明修改原因、内容和验证结果。尚未完成的工作可先开 Draft PR，准备好后再标记为可审阅。请另一位有写入权限的成员审阅。

公开仓库中不要提交密码、API Key、学生个人资料或未公开敏感内容。使用 AI 时，提交者仍负责核对内容，并按当次授权控制提交、推送与合并。

## 3. 审阅、记录决定与合并

审阅者检查内容是否准确、范围是否清楚、是否与已有文档一致，以及验证是否充分。意见写在 PR 中；有修改要求时先处理，再批准。

main 当前启用强制 PR 审阅：至少 1 位其他协作者批准，新提交会撤销旧批准，合并前须解决全部审阅讨论。规则未配置绕过名单，管理员也按同一流程操作；main 禁止强推和删除。实际生效设置以 [GitHub Rules](https://github.com/Xue-Path/XuePath/rules) 为准。

推送到同一工作分支会更新原 PR。处理意见后，在 PR 中说明调整内容并请审阅者重新检查。解决讨论表示意见已处理，不代替批准。

如果讨论形成产品或协作决定，把决定、日期和依据写入对应文档，再让审阅者检查。PR 合并只表示本次修改被接受；候选方案是否成为产品决定，应在正文中明确标注，不能只从合并状态推断。

获得批准、处理完讨论并确认差异后，由团队成员合并。AI 不因创建了文件或 PR 就自动获得合并授权。

## 4. 合并后收尾

仓库已开启合并后自动删除工作分支。确认 PR 已合并后，同步本地：

```sh
git switch main
git pull --ff-only origin main
git fetch origin --prune
git branch -d docs/interview-questions
```

若 `git branch -d` 拒绝删除，先检查是否有未保留的提交；使用 squash 或 rebase 合并也可能导致 Git 无法按祖先关系判断。核对 PR 和提交内容后再处理，不直接改用强制删除。

下一项任务重新从最新 main 建分支，避免复用已经合并的旧分支。
