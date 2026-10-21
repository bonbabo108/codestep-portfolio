# CodeStep

## アプリ概要

CodeStepは、プログラミング初学者向けのコード学習Webアプリです。

学習問題にコードを入力し、正誤判定と解説を確認できます。ログインしたユーザーは正解した問題の学習進捗を保存でき、別の端末からも学習を再開できます。

## サイトイメージ

![CodeStepの体験デモ画面](https://raw.githubusercontent.com/bonbabo108/codestep/53a5d4360e7c7c22a98997a9fc6d083818b7397c/docs/screenshots/final-20261019/demo-desktop.jpg)

[スマートフォン表示例](https://raw.githubusercontent.com/bonbabo108/codestep/53a5d4360e7c7c22a98997a9fc6d083818b7397c/docs/screenshots/final-20261019/demo-mobile.jpg)

## サイトURL

**公開アプリ**

https://codestep-two.vercel.app

**登録不要の体験デモ**

https://codestep-two.vercel.app/demo

**アプリ本体のGitHubリポジトリ**

https://github.com/bonbabo108/codestep

## 使用技術

- フロントエンド：Next.js、React、TypeScript、Tailwind CSS
- 認証：Supabase Auth
- データベース：Supabase（PostgreSQL、RLS）
- デプロイ：Vercel
- バージョン管理：Git、GitHub
- テスト・デバッグ：Chrome DevTools
- CI/CD：GitHub Actions、Vercel

## 設計ドキュメント

[Week 9：要件定義・設計書（Googleスプレッドシート）](https://docs.google.com/spreadsheets/d/1l6_wH24I4Cq1jhvHi1VtDjarj5fr8KK6jS0g7HTAtds/edit)

設計資料の図は、次のリンクから確認できます。

- [ER図](https://github.com/bonbabo108/codestep-portfolio/blob/main/docs/er-diagram.png)
- [ワークフロー図（画面遷移図）](https://github.com/bonbabo108/codestep-portfolio/blob/main/docs/workflow.md)

## 機能一覧

- メールアドレスとパスワードによるユーザー登録・ログイン
- 学習問題の表示、コード入力、正誤判定、解説表示
- 正解した問題の学習進捗の保存・復元
- 同一アカウントによるPC・スマートフォン間の進捗同期
- 管理者による問題の作成・閲覧・編集・削除（CRUD）
- 登録不要で学習機能と問題管理を試せる体験デモ

体験デモではサンプルデータを使用し、実際のデータベースは変更しません。

## テスト・修正の設計及び実施書

- [Week 11：テスト設計・実施書（Googleスプレッドシート）](https://docs.google.com/spreadsheets/d/1E865kqwo83lWGgH0s1bbIIAs0FKfpGfzHbQTKxKiDqQ/edit)
- [自動テスト・開発中の検証記録（GitHub）](https://github.com/bonbabo108/codestep/blob/main/docs/test-plan.md)

自動テスト77件が成功しています。また、ユーザー登録・ログイン、学習進捗の保存・端末間復元、管理者による問題管理など、主要機能の本番動作を確認済みです。

最新の検証結果はWeek 11の「現行検証_20261021」タブに記録しています。

## アプリの改善案

- [Week 12：プログラム改善案（Googleスプレッドシート）](https://docs.google.com/spreadsheets/d/1flOiRudAh9wCJgjQoD1CQQVqrHq9n_bBH-agpPvHmLQ/edit)

**リアルタイムプレビュー機能（未実装）**

当初は、入力・変更したコードが画面上にリアルタイムで反映され、コードと表示結果の関係を視覚的に理解できる学習機能を構想していました。

現状は正誤判定と解説表示が中心のため、この機能は今後の改善案として残っています。

その他の改善案や実施済みの修正はWeek 12の資料に整理しています。

## 備考

**GitHub Actions**

- ESLint、TypeScriptの型チェック、自動テストなどを実施
- [GitHub Actionsの実行結果](https://github.com/bonbabo108/codestep/actions/runs/39031564825)

**活用した生成AIと用途**

- ChatGPT：要件定義、設計、仕様の検討、資料の整理
- v0：初期画面のプロトタイプ作成
- Codex：プログラムの実装・修正、テスト、コードレビュー

**現在の仕様上の制約**

- 解答は文字列一致で判定し、入力したコード自体は実行しません。
- 新規登録時のメールアドレス所有確認は未実装です。
