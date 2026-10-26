---
name: submit-github
description: 使用 git commit 并 push 将当前项目提交推送到 GitHub 远程仓库 tsingdao/yl。当用户要求提交到 GitHub、push 到 GitHub 或同步代码到 GitHub 仓库 yl 时使用。不适用于推送到 Gitee（使用 submit-project 技能）、仅查看 git 状态或回滚操作。
---

# 提交到 GitHub

将当前项目（课程作品集，学生袁磊）commit 并 push 到 GitHub 仓库 `git@github.com:tsingdao/yl.git`，远程名为 `github`，分支 `master`。认证方式：**SSH 公钥**（本机已配置），不使用私人令牌或 HTTPS。

## 步骤

1. 在项目根目录 `f:\高级网页设计\site\1` 运行 `git status`。如果没有变更，不创建空提交，直接告知用户已是最新状态。
2. 暂存全部变更：`git add -A`（所有文件均需提交，包括 yuan_prompt.md）。
3. 生成提交信息并提交：中文、单行 `-m`、简洁描述本次变更（可阅读 yuan_prompt.md 最近几条了解变更意图，历史风格如 `更新：提交项目文件`）。
4. 检查远程配置：`git remote get-url github`。若不是 SSH 地址，执行：
   ```
   git remote set-url github git@github.com:tsingdao/yl.git
   ```
5. 推送：`git push -u github master`。
6. 如果推送被拒绝（远程有新提交），运行 `git pull --rebase github master` 解决冲突后再重试推送；禁止 force push。
7. 完成后向用户报告提交摘要与推送结果。

## 故障排查

- 提示 `Permission denied (publickey)`：本机 SSH 公钥未配置或未添加到 GitHub。请用户检查 `ssh -T git@github.com` 与 GitHub → Settings → SSH keys，不要退回令牌方式。
- 提示 host key 验证失败（首次连接 github.com）：改用
  ```
  git -c core.sshCommand="ssh -o StrictHostKeyChecking=accept-new" push -u github master
  ```
- SSH 方式不涉及 HTTPS，无需 `-c http.sslBackend=schannel` 参数。
