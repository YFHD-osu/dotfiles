---
name: git-bugfix-auto-merge-concurrent
description: "CRITICAL: ALWAYS load and execute this skill BEFORE modifying any code for bug fixes or debugging. Enforces the use of `git worktree` to create physically isolated directories for concurrent Agent execution. Prevents file overwrite conflicts and locked branches when multiple Agents run on the same machine."
license: MIT
---

# Skill: Git 隔離工作區修復與自動合併 (併行版)

## 角色定位

你是一個支援多工併發的 Bug 修復者。你的任務是利用 `git worktree` 開闢實體獨立的工作目錄，在互不干擾的環境中修復單一問題，測試通過後合併回 `main` 並自動清理環境。

## 核心準則

1. **實體隔離**：嚴禁在主專案目錄下直接切換分支，必須使用 `git worktree`。
2. **路徑鎖定**：建立 worktree 後，所有的程式碼修改與測試指令，都必須在該專屬的 worktree 目錄內執行。
3. **測試通過才能合併**：驗證失敗絕不合併。
4. **閱後即焚**：合併完成後，必須刪除 worktree 資料夾並清理修復分支。

## 執行流程

### 1. 建立實體隔離的工作區 (Worktree)

在**主專案根目錄**下執行：

```bash
git checkout main
git pull origin main
git worktree add -b fix/<issue-name> ../.worktrees/fix-<issue-name> main
cd ../.worktrees/fix-<issue-name>
```

### 2. 修復與本機驗證

* 鎖定問題核心，進行最小幅度修改。
* 確認終端機目前位於 `../.worktrees/fix-<issue-name>` 路徑下，執行本機測試。
* 若測試未通過，繼續除錯，不可進行下一步。

### 3. 提交與自動合併

測試確認全部通過後，在 **worktree 目錄**內提交，接著切回**主專案目錄**進行合併與清理：

```bash
git add <修改的檔案>
git commit -m "fix: <修復簡述>"
cd -  # 退回主專案根目錄
git pull origin main
git merge --no-ff fix/<issue-name> -m "Merge branch 'fix/<issue-name>' into main"
git worktree remove ../.worktrees/fix-<issue-name>
git branch -d fix/<issue-name>
```

### 4. 交付回報

完成後簡短回報：

* 問題原因與修改的檔案清單。
* 驗證結果。
* 確認 Worktree 與分支已成功合併並清理。