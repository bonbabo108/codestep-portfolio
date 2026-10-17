# CodeStep ポートフォリオ

## アプリ概要

CodeStepは、プログラミング初学者が短いコーディング問題に回答し、正誤判定と解説を通して学べるWebアプリです。学習者の正解・進捗を保存・復元する仕組みや、管理者による問題管理機能を備えています。

**公開状況について：** 下記のProduction URLは旧版（`main`）です。作業ブランチで実装・staging検証した最新の管理者権限制御、本人の進捗保存・復元、学習履歴に関連する問題削除などは、Productionにはまだ反映していません。最新機能の完成・公開実績と混同しないでください。

## サイトイメージ

![CodeStepの学習画面（以前の版）](./docs/app-learning.png)

※画像は以前の画面です。最新作業ブランチの画面・動作を示す証跡ではありません。

## アプリURL

- [公開アプリ（Production・旧版）](https://codestep-two.vercel.app)
- [最新実装の作業ブランチ](https://github.com/bonbabo108/codestep/tree/codex/admin-rls-portfolio)（最新の非本番版。一般公開用URLではありません）

## アプリ本体GitHub

- [CodeStepアプリ本体](https://github.com/bonbabo108/codestep)
- [最新検証・公開準備記録](https://github.com/bonbabo108/codestep/blob/codex/admin-rls-portfolio/docs/release-readiness.md)

## 使用技術

- フロントエンド：Next.js（App Router）、React、TypeScript、Tailwind CSS
- 認証・データベース：Supabase Auth、PostgreSQL、RLS
- デプロイ：Vercel
- バージョン管理：Git、GitHub
- テスト・デバッグ：Chrome DevTools（Consoleの確認）、単体・モック・staging実DB/APIでの検証

- CI：GitHub Actions（ESLint自動実行） — [成功したワークフローの実行履歴](https://github.com/bonbabo108/codestep/actions/runs/39031564825)（作業ブランチ `codex/admin-rls-portfolio`、コミット `d950f3f`）

## 機能一覧

**最新作業ブランチ・stagingで検証した主な機能（Productionへの反映前）**

- ユーザー登録・ログイン・ログアウト（Supabase Auth）
- データベースからの学習問題表示、解答入力、正誤判定、解説表示
- ログインした本人の正解・学習進捗の保存と復元
- 管理者専用ログイン入口・管理画面、一般ユーザーの管理操作制限
- 管理者による問題作成・一覧表示・編集・削除（関連する進捗がある問題の削除を含む）

※各機能の検証範囲と未検証項目は、[アプリ本体のテスト記録](https://github.com/bonbabo108/codestep/blob/codex/admin-rls-portfolio/docs/test-plan.md)を参照してください。

## 設計ドキュメント

- [Week9 要件定義・設計スプレッドシート](https://docs.google.com/spreadsheets/d/1l6_wH24I4Cq1jhvHi1VtDjarj5fr8KK6jS0g7HTAtds/edit)
- [ワイヤーフレーム](./docs/wireframe.png)
- [ER図](./docs/er-diagram.png)

※設計原本には旧仕様が含まれます。最新の認証・権限・削除方法と完全一致するとは限りません。

## テスト・修正の設計及び実施書（Week11）

- [Week11 テスト設計＆実施書](https://docs.google.com/spreadsheets/d/1E865kqwo83lWGgH0s1bbIIAs0FKfpGfzHbQTKxKiDqQ/edit)
- [最新作業ブランチのテスト記録](https://github.com/bonbabo108/codestep/blob/codex/admin-rls-portfolio/docs/test-plan.md)

Week11シートにはv0プレビュー段階の確認結果と「未検証」の項目が残っています。別途実施したstaging実DB/API・認証・画面の検証結果を、同じ条件で実施したものと誤認しないよう区別しています。

## アプリ改善案（Week12）

- [提出済みのWeek12改善案シート](https://docs.google.com/spreadsheets/d/1flOiRudAh9wCJgjQoD1CQQVqrHq9n_bBH-agpPvHmLQ/edit)

今後の改善構想として、AI利用時の情報漏洩・危険操作を学ぶ問題、段階的なヒント、問題・カテゴリ選択、達成率表示、AI作業前の簡易リスク確認チェックリストを挙げています。**これら5件は提案段階で、まだ実装していません。**

## 生成AIツールの活用用途

- ChatGPT：要件・提出条件の整理、仕様の検討、READMEや課題資料の作成補助
- v0：初期プロトタイプと画面構成の作成・確認
- Codex：実装・SQLレビュー、修正案の作成、テスト・安全性検証、既存設計との照合
- Cline、GitHub Copilot等：過去の開発・ドキュメント作業での補助（実際の使用範囲に基づき必要に応じて見直す）

生成AIの出力をそのまま動作保証とはみなさず、検証内容と未検証項目を分けて記録しています。

## 備考・今後の課題

- Week12の「DevToolsの確認」は、アプリとDevToolsの画面を含むスクリーンショットをWorX AIへ提出済みです。
- GitHub Actions（ESLint）は作業ブランチで実行・成功を確認済みです：[実行履歴](https://github.com/bonbabo108/codestep/actions/runs/39031564825)。WorX AIへの課題は、初回の証拠画像不足を修正して再提出済みです（再採点結果は未確認）。
- Productionへの最新機能反映、本番DB/Auth移行は未実施です。本番DBの権限変更・データ保全には個別の確認が必要です。
- このリポジトリはポートフォリオ提出用です。アプリ本体のコードは上記の別リポジトリで管理しています。
