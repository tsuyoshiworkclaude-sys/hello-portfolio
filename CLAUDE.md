# 開発ルール

このリポジトリは1人開発でも「機能ごとに ブランチ → PR → マージ」を繰り返す。
PR の履歴がそのまま開発の記録（面接での説明材料）になるので、必ずこの流れを守る。

アプリ本体は `hello-portfolio/`（Vite + React + TypeScript）。

## Git の流れ

機能追加・修正を頼まれたら、特に指示がなくても以下の順で進める。`/feature-pr` でも同じ流れを実行できる。

1. `git switch main && git pull` で main を最新にする
2. `git switch -c feature/<機能名>` で作業ブランチを作る（main 上で直接作業しない）
   - 機能以外の変更は `fix/`・`chore/`・`docs/` を使う
3. 実装する
4. 確認する：`hello-portfolio/` で `npm run build` と `npx eslint src` を実行し、`git diff` の要点をユーザーに示す
5. `git add` → `git commit -m "変更内容"`（英語の命令形・1行で要約）
6. `git push -u origin <ブランチ名>` → `gh pr create`
7. **マージはしない。** ユーザーが GitHub 上で差分を見直してマージする

## PR の説明欄

以下の3点を短く書く（後で README の「AI駆動開発の進め方」を書く材料にする）。

```markdown
## 何を変えたか
- ...

## AIに任せたところ / 自分で判断・修正したところ
- AI: ...
- 自分: ...（ユーザーが指示・判断した内容。分からない部分は「（記入してください）」と残す）

## 動作確認
- ...（実行したコマンドと結果。ブラウザで確認していなければそう書く）
```

## コミットしてはいけないもの

- `.env` など APIキー・パスワードを含むファイル。`.gitignore` に入っていることを確認する
- コミット前に `git status` と `git diff --cached` を見て、秘密情報らしきもの（`API_KEY`、`SECRET`、`TOKEN` など）が含まれていたら止めてユーザーに確認する
- `node_modules/`・`dist/` などの生成物
