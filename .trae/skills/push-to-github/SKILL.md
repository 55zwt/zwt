---
name: push-to-github
description: Commit and push the whole wangyesheji project to GitHub repo 55zwt/zwt over SSH. Use when the user asks to 提交到github、push、同步到 GitHub、备份项目 or publish this portfolio. Do not use for ordinary code edits that were not asked to be committed.
---

# 提交并推送项目到 GitHub（55zwt/zwt）

把 `d:\wangyesheji` 整个项目提交并推送到 `git@github.com:55zwt/zwt.git`（SSH，公钥 `C:\Users\ROG\.ssh\id_ed25519.pub` 已配置到该账号）。按顺序执行以下步骤，中途失败先诊断再重试，不要盲目重复。

## 步骤

1. **检查仓库状态**：运行 `git status`。若 `git rev-parse --is-inside-work-tree` 失败（尚未初始化），执行 `git init -b main`。
2. **绑定远程**：`git remote -v` 查看现有远程。
   - 无 origin → `git remote add origin git@github.com:55zwt/zwt.git`
   - origin 指向其他地址 → `git remote set-url origin git@github.com:55zwt/zwt.git`
3. **确认提交身份**：`git config user.name` 与 `git config user.email`（仓库级或全局任一存在即可）。若两者都为空，仅设置仓库局部配置（不动全局）：
   - `git config user.name "赵婉彤"`
   - `git config user.email "55zwt@users.noreply.github.com"`
4. **SSH 预热**（避免首次连接的交互式 host key 确认卡住）：`ssh -o StrictHostKeyChecking=accept-new -T git@github.com`。期望输出含 `Hi 55zwt!`（认证成功，exit code 1 属正常）。失败则停止并提示检查公钥是否已添加到 GitHub 账号。
5. **暂存全部改动**：`git add -A`（本技能的语义就是提交整个项目）。
6. **提交**：先 `git log --oneline -5` 参考已有风格；仓库无历史或用户未指定时，使用 `git commit -m "课堂实践作品提交 <当天日期 YYYY-MM-DD>"`。若没有可提交的改动（工作区干净），跳过提交。
7. **推送**：`git push -u origin main`。
   - 若被拒（远端已有提交，如初始化时的 README）：`git pull --rebase origin main` 后重试 push。
   - 禁止 `--force` / `--no-verify`。
8. **验证**：`git status` 干净；`git log -1 --stat` 显示本次提交与文件清单；`git push` 后远程 origin/main 已包含最新提交。

## 注意事项

- 远端报 `Repository not found` → 用户尚未在 GitHub 创建仓库，停止并请用户到 github.com 上新建空的 `55zwt/zwt` 仓库后重试（SSH 无法自动建仓）。
- SSH 写 `C:\Users\ROG\.ssh\known_hosts` 可能被命令沙箱拦截；报权限错误时对该条命令使用 `dangerouslyDisableSandbox: true` 重试。
- 不提交敏感文件（.env、密钥等）；本项目当前没有，但 add 前留意 `git status` 输出。
- 文件名含中文与空格（如 `4-1 css2.html`），git 正常处理，无需额外配置。
- 提交完成后向用户报告：最新提交哈希、改动文件数、推送是否成功。
