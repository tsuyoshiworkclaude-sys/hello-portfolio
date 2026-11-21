---
name: feature-pr
description: 機能ごとに「main更新 → ブランチ作成 → 実装 → 確認 → コミット → push → PR作成」までを自動で行う。機能追加・修正を頼まれたとき、または /feature-pr <やりたいこと> で使う。
---

# feature-pr

引数: やりたいこと（例: `/feature-pr カウンターにリセットボタンを付ける`）。
ルールの詳細はリポジトリ直下の `CLAUDE.md` に従う。

## 手順

1. **main を最新にする**
   - 未コミットの変更があれば止めてユーザーに確認する
   - `git switch main && git pull --ff-only`
2. **ブランチを作る**
   - やりたいことから英語の短い名前を決める（例: `feature/counter-reset`）
   - `git switch -c feature/<機能名>`（修正なら `fix/`、設定なら `chore/`、文書なら `docs/`）
3. **実装する**
4. **確認する**
   - `cd hello-portfolio && npm run build && npx eslint src`
   - 失敗したら直す。直せなければ止めて報告する
   - `git diff --stat` と変更の要点をユーザーに示す
5. **コミットする**
   - `git status` で意図しないファイル（`.env`、秘密情報、生成物）がないか確認する。あれば止める
   - 変更したファイルを `git add` し、英語の命令形1行でコミットする
6. **PR を出す**
   - `git push -u origin <ブランチ名>`
   - `gh pr create --base main` で、説明欄は CLAUDE.md の3点テンプレート（何を変えたか / AIに任せたところと自分で判断・修正したところ / 動作確認）
   - 「自分で判断・修正したところ」はユーザーの指示内容から書き、分からない部分は「（記入してください）」と残す
7. **マージはしない**
   - PR の URL を伝え、「GitHub上で差分を見直してマージしてください」と案内して終わる
