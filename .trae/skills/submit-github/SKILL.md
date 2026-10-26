---
name: submit-github
description: 使用 git commit 并 push 将当前项目提交推送到 GitHub 远程仓库 tsingdao/lei。当用户要求提交到 GitHub、push 到 GitHub 或同步代码到 GitHub 仓库 lei 时使用。不适用于推送到 Gitee（使用 submit-project 技能）、仅查看 git 状态或回滚操作。
---

# 提交到 GitHub

将当前项目（课程作品集，学生袁磊）commit 并 push 到 GitHub 仓库 `https://github.com/tsingdao/lei`，远程名为 `github`，分支 `master`。

## 步骤

1. 在项目根目录 `f:\高级网页设计\site\1` 运行 `git status`。如果没有变更（无修改、无未跟踪文件），不创建空提交，直接告知用户已是最新状态。
2. 暂存全部变更：`git add -A`（所有文件均需提交，包括 yuan_prompt.md）。
3. 生成提交信息并提交：中文、单行 `-m`、简洁描述本次变更（可阅读 yuan_prompt.md 最近几条了解变更意图，历史风格如 `更新：提交项目文件`）。
4. 检查远程配置：`git remote get-url github`。若远程 `github` 不存在，执行：
   ```
   git remote add github https://tsingdao:<私人令牌>@github.com/tsingdao/lei.git
   ```
   `<私人令牌>` 必须由用户提供，或从本机已有的 `.git/config` / 凭据管理器中读取。禁止使用他人的令牌。
5. 推送：`git -c http.sslBackend=schannel push github master`。
   本机 OpenSSL 缺少 CA 证书包，所有访问 github.com 的 git 网络命令（push/pull/ls-remote）都必须加 `-c http.sslBackend=schannel` 参数，改用 Windows 原生证书存储。
6. 如果推送被拒绝（远程有新提交），运行 `git -c http.sslBackend=schannel pull --rebase github master` 解决冲突后再重试推送；禁止 force push。
7. 完成后向用户报告提交摘要与推送结果。

## 安全注意

- 私人令牌（GitHub PAT）是敏感凭据：不得写入任何仓库内的文件（包括 SKILL.md、yuan_prompt.md、AGENTS.md 等），不得在回复正文中完整展示，只能保存在 `.git/config`（远程 URL）或凭据管理器中。
- 若认证失败（401/403），提示用户检查令牌是否已过期或被吊销，必要时请用户重新提供新令牌并更新远程 URL，不要反复重试。
- 用户在对话中粘贴过的令牌存在泄露风险，建议适时提醒其在 GitHub 上轮换（regenerate）该令牌。
