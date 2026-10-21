# CodeStep ポートフォリオ

**公開・動作確認状況（2026年10月21日更新）**

CodeStepは、プログラミング初学者が短いコード問題を解き、正誤判定と解説で学ぶWebアプリです。講座の最終課題として制作しました。

[アプリ本体のPR #3](https://github.com/bonbabo108/codestep/pull/3)を`main`へマージし、VercelのProductionへ反映済みです。**本番の新規登録・ログイン、正解した問題の進捗保存、同一アカウントでのPC・Android間の復元、管理者による問題作成・編集・削除は、2026年10月21日に制作者本人が実機で検証済みと報告しました。** これらは本人の確認結果であり、README改訂時にAIが本番操作やDBログを独立に再検証した結果ではありません。

**[本番アプリを開く](https://codestep-two.vercel.app)** ・ **[登録不要の学習・管理デモ](https://codestep-two.vercel.app/demo)** ・ **[アプリ本体のGitHub](https://github.com/bonbabo108/codestep)**

## アプリ概要と対象者

仕事や日常生活と両立しながらプログラミングを学ぶ初学者を想定しています。教材を探し回る負担を減らし、問題を1問ずつ解き、その場で答えと説明を確認できることを重視しました。この対象者像は設計上の仮説であり、調査による実測結果ではありません。

## サイトイメージ

![登録不要の体験デモ（2026年10月19日、ローカル実画面）](https://raw.githubusercontent.com/bonbabo108/codestep/53a5d4360e7c7c22a98997a9fc6d083818b7397c/docs/screenshots/final-20261019/demo-desktop.jpg)

[スマートフォン幅の画面](https://raw.githubusercontent.com/bonbabo108/codestep/53a5d4360e7c7c22a98997a9fc6d083818b7397c/docs/screenshots/final-20261019/demo-mobile.jpg) / [制作途中の学習画面原本](./docs/app-learning.png)

※画像は撮影時点の表示例です。本番の認証・DB保存を証明する画像ではありません。

## サイトURL・コード

- **本番アプリ：** https://codestep-two.vercel.app
- **登録不要デモ：** https://codestep-two.vercel.app/demo
- **アプリ本体リポジトリ：** https://github.com/bonbabo108/codestep
- **PRとマージ履歴：** https://github.com/bonbabo108/codestep/pull/3

## 主な機能と確認状況

| 機能 | できること・検証 |
| --- | --- |
| 新規登録・ログイン・ログアウト | Supabase Authによるメールアドレス・パスワード認証。新規登録・ログインは本番で本人が確認済み |
| 学習と解答 | DBの問題を読み込み、コードを入力して正誤判定・解説を確認 |
| 学習進捗の保存と復元 | ログインした本人の正解済み進捗を保存。同一アカウントでPC・Android間の復元を本人が本番確認済み |
| 管理者による問題CRUD | 管理者が問題の作成・一覧・編集・削除を実施。本番の一連操作を本人が確認済み |
| 権限・データ保護 | 管理者フラグ、RLS、列権限、削除用RPC、本人進捗の一意制約を利用。設定適用は既存の本番記録で確認 |
| 登録不要のデモ | 架空の問題で学習・問題管理を体験。ブラウザ内メモリだけを使い、実際のAuth・DBには書き込まない |

**検証の区別：** 自動テスト・検証用DB（staging）の実測・本人の本番実機確認はそれぞれ異なる種類の証拠です。本番の主要操作の最新判定は[Week11「現行検証_20261021」タブ](https://docs.google.com/spreadsheets/d/1E865kqwo83lWGgH0s1bbIIAs0FKfpGfzHbQTKxKiDqQ/edit#gid=648476743)を参照してください。

## 使い方（メンタリングでの実演）

1. [登録不要デモ](https://codestep-two.vercel.app/demo)で回答・正誤判定・解説を確認します。
2. デモの「問題管理を体験」から、サンプル問題の追加・編集・削除、削除取消、初期化を試せます。デモは実DBを更新しません。
3. [本番アプリ](https://codestep-two.vercel.app)で通常の学習・ログイン・本人進捗の保存を確認できます。
4. 管理者による実問題管理は、権限を持つ本人が[管理者入口](https://codestep-two.vercel.app/admin/login)からログインして操作します。管理者パスワードや管理者権限を第三者へ配布しません。

**解答判定の仕様：** 入力の前後空白を除いた文字列一致（大文字・小文字は区別）です。コード自体の実行、あらゆる別解の判定は行いません。

## 使用技術・構成

- **フロントエンド：** Next.js（App Router）、React、TypeScript、Tailwind CSS
- **認証・データベース：** Supabase Auth、PostgreSQL、Row Level Security（RLS）
- **問題・進捗：** publicの`questions`、`profiles`、`user_progress`の3テーブル。利用者認証はSupabase Auth側で管理し、独自のパスワード保存テーブルを作成していません。
- **デプロイ：** Vercel（GitHub連携）
- **ソース管理：** Git、GitHub、ブランチ、Pull Request
- **テスト・デバッグ：** Chrome DevTools、モック・staging実DB/API・本人実機での確認
- **CI：** GitHub ActionsでESLint、型検査、77件の自動テスト、ダミー接続ビルドを実施し成功を確認。CI成功を実DB試験の代わりとは扱いません。
- **CD：** ブランチpushでPreviewを更新し、[PR #3](https://github.com/bonbabo108/codestep/pull/3)のmainマージ後にVercel Productionへ反映しています。

## 要件定義・設計資料（Week 9）

- [Week9 要件定義・設計シート](https://docs.google.com/spreadsheets/d/1l6_wH24I4Cq1jhvHi1VtDjarj5fr8KK6jS0g7HTAtds/edit)
- **[現行設計との差分・2026年10月21日更新](https://docs.google.com/spreadsheets/d/1l6_wH24I4Cq1jhvHi1VtDjarj5fr8KK6jS0g7HTAtds/edit#gid=1446831800)**
- [ワイヤーフレーム原本](./docs/wireframe.png) / [ER図の画像原本](./docs/er-diagram.png)
- [詳細設計・現在の構成を説明する文書](https://github.com/bonbabo108/codestep/blob/main/docs/final-design.md)

**資料の読み方：** 制作初期のシート・図・GitHub文書は当時の設計や変更履歴も残しています。現行の3テーブル構成、管理画面URL、Authによる認証、本人進捗、管理者権限・削除RPCは、上記「現行設計との差分」と本READMEの更新日を優先して参照してください。Googleスプレッドシートは2026年10月21日に更新済みです。

## テスト・修正・検証資料（Week 11）

- [Week11 テスト設計＆実施シート](https://docs.google.com/spreadsheets/d/1E865kqwo83lWGgH0s1bbIIAs0FKfpGfzHbQTKxKiDqQ/edit)
- **[最新の合格・検証記録（現行検証_20261021）](https://docs.google.com/spreadsheets/d/1E865kqwo83lWGgH0s1bbIIAs0FKfpGfzHbQTKxKiDqQ/edit#gid=648476743)**
- [開発中の自動・staging検証履歴](https://github.com/bonbabo108/codestep/blob/main/docs/test-plan.md)
- [GitHub Actions実行記録](https://github.com/bonbabo108/codestep/actions/runs/39031564825) / [PR #3の品質確認とマージ](https://github.com/bonbabo108/codestep/pull/3)

旧v0プレビューの試験記録は制作経過として保持し、現在の主要な本番操作は本人の検証完了を受けて合格に更新しました。自動・staging・本番の検証条件は混同しません。

## 改善と今後の案（Week 12）

- [Week12 プログラムの改善シート](https://docs.google.com/spreadsheets/d/1flOiRudAh9wCJgjQoD1CQQVqrHq9n_bBH-agpPvHmLQ/edit)
- **[実施した改善と将来案（改善履歴_20261021）](https://docs.google.com/spreadsheets/d/1flOiRudAh9wCJgjQoD1CQQVqrHq9n_bBH-agpPvHmLQ/edit#gid=705317382)**

| 実施済みの改善 | 狙い・確認内容 |
| --- | --- |
| 問題管理UIとデモの共通化 | 通常管理と体験デモで画面・確認操作を共通化。データの保存先は実DBとメモリに分離 |
| 認証画面の入力・案内 | ダーク系配色での入力視認性、パスワード表示、戻り先・期限切れ案内などを改善 |
| 保存・更新・削除処理 | 0件返却を成功扱いしない、重複送信防止、削除前の確認、異常時の案内 |
| 進捗と権限制御 | 本人進捗・RLS・管理者用の権限を整備し、stagingと本番の記録を分離 |
| スマホ向け確認 | PC/390px幅の画面・デモを確認し、本人のAndroidからの操作感も確認 |

**提出後の改善候補（未実装）：** AIの危険操作を学ぶ問題、ヒントの段階表示、カテゴリ選択、達成率表示、AI作業前のチェックリスト。提案段階の機能を実装済みとは表示しません。

## 制約・未実装・今後の検討

- 新規登録・ログインは動作する構成ですが、**本番は`Confirm email OFF`、独自SMTPなし**です。メールアドレスを入力した人がその所有者かどうかの確認は行わず、改善候補として明記しています。
- OAuth、独立した生成AI API、ライブコード実行、画像・音声入力は今回の提出対象外です。採点表の最高評価をすべて満たしたという意味ではありません。
- 緊急停止・復旧の一部の異常系試験は未完了です。過去の本番DB移行・安全検証記録と、主要機能の本番実機確認は別項目として扱います。
- [本番移行・公開までの判断履歴（過去時点の未適用・未公開記載を含む）](https://github.com/bonbabo108/codestep/blob/main/docs/release-readiness.md)は時系列の履歴です。過去の「未公開」「未適用」を2026年10月21日時点の現在地として読まないでください。

## 生成AIの利用・提出補足

- **ChatGPT：** 要件・設計・提出条件の整理、資料作成とレビューの補助。
- **v0：** 初期UIプロトタイプの検討・画面確認。
- **Codex：** アプリの実装、修正案・SQLレビュー、テスト、安全性と設計の照合。

生成AIの作業結果と、制作者本人が本番で確認した結果を区別しています。

Week12のChrome DevTools課題は、アプリ画面とDevToolsのスクリーンショットをWorX AIへ提出済みです。GitHub Actions（ESLint）の課題は証拠画像の不足を修正して再提出済みですが、再採点結果は未確認です。

アプリ本体は別リポジトリ（[CodeStep](https://github.com/bonbabo108/codestep)）で管理しています。[プログラム格納場所の説明](./CodeStep/プログラム格納場所.md)も参照できます。このリポジトリのREADMEをメンターへの提出・共有の入口としています。
