---
name: submit-project
description: 使用 git commit 并 push 将当前项目提交推送到 Gitee 远程仓库 whalefox/yl2。当用户要求提交项目、提交并推送代码、同步到 Gitee 或上传代码时使用。不适用于仅查看 git 状态、回滚或撤销操作。
---

# 提交项目

将当前项目（课程作品集，学生袁磊）提交（commit）并推送（push）到 Gitee 远程仓库 `https://gitee.com/whalefox/yl2.git`。

仓库已配置完成：远程 `origin` 指向上述地址，工作分支为 `master`，无需重新 init 或添加 remote。

## 步骤

1. 在项目根目录 `f:\高级网页设计\site\1` 运行 `git status` 查看变更。如果没有变更（无修改、无未跟踪文件），不创建空提交，直接告知用户已是最新状态。
2. 暂存全部变更：`git add -A`。本项目为静态课程作品集，所有文件均需提交，包括 yuan_prompt.md（提示词日志）。
3. 生成提交信息并提交。要求：
   - 中文，简洁描述本次变更（参考历史风格，如 `更新：提交项目文件`）
   - 可阅读 yuan_prompt.md 最近几条记录了解本次变更意图
   - 提交信息通过 HEREDOC 格式传递
4. 推送：`git push origin master`
5. 如果推送被拒绝（远程有新提交），运行 `git pull --rebase origin master` 解决后再重试推送；禁止 force push。
6. 完成后向用户报告提交摘要与推送结果。

## 注意

- 用户说"提交项目"即触发本技能，直接执行，无需再确认。
- 认证失败时提示用户检查 Gitee 凭据（账号密码或私人令牌），不要反复重试。
