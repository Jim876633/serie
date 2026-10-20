# serie（個人 fork）

這是 [lusingander/serie](https://github.com/lusingander/serie) 的個人 fork，只給自己用，不對 upstream 發 PR。

## Remote 與分支

- `origin`：`github.com/Jim876633/serie`（fork）
- 自訂改動放在 `feat/compact-graph-and-copy-branch`，`master` 保持跟 upstream 一致
- 同步 upstream：
  ```
  git remote add upstream https://github.com/lusingander/serie.git   # 只需一次
  git fetch upstream
  git switch master && git merge --ff-only upstream/master
  git switch feat/compact-graph-and-copy-branch && git rebase master
  ```

## 安裝

本機的 `serie` 指令是從這份原始碼裝的（`~/.cargo/bin/serie`），不是 brew 版。改完 code 後重新安裝：

```
cargo install --path . --locked
```

## 檢查（同 CI `build.yml`）

```
cargo fmt --all -- --check
cargo clippy --all-targets --all-features -- -D warnings
cargo test
cargo sort-derives --check   # 需先 cargo install --locked cargo-sort-derives
```

## Fork 的自訂改動

- graph 欄寬依畫面上可見的 commit 決定（只在 `graph.row_image_width = "compact"` 時生效，`fixed` 維持整張圖寬度）：`GraphImageManager::visible_graph_cell_width`
- commit list 按 `b`（`branch_copy`）複製選取 commit 的 branch name，優先序為 HEAD、local、去掉 remote 前綴的 remote：`CommitListState::selected_commit_branch_name`
- 新增 keybind 時要同步更新 `assets/default-keybind.toml`、`src/event.rs`、`src/view/help.rs`、`config.schema.json`、`docs/src/keybindings/index.md`
