# ハピベビ公式サイト（hapibebi.jp）

## 概要
個人開発者ブランド「ハピベビ」の公式サイト。アプリのサポートページ（App Store の「サポートURL」）、
アプリごとのプライバシーポリシー・利用規約を置く。最初のアプリは「そだち手帳」
（`../../app/母子手帳のようなダッシュボードアプリ/`）。2026-10-27 着手。

## 置き場所と公開のしかた
- 公開するファイルは `docs/` の中だけ（GitHub Pages で `docs/` を公開する設定にする）。この CLAUDE.md など、
  `docs/` の外のファイルはサイトに出ない
- GitHub：組織 `hapibebi`（持ち主は Yukiさんの個人アカウント `yy-devlog`）の公開リポジトリ `hapibebi.jp`
- ドメイン：**hapibebi.jp**（本命）。`docs/CNAME` に書いてある。hapibebi.com は .jp へ転送する予定（未設定）。
  ドメインとメールの詳細は `../../app/母子手帳のようなダッシュボードアプリ/20261025_資産台帳.md`
- **GitHub に送る（push）＝外に公開する操作**。送る前に、変更内容を Yukiさんに見せて承認を得る
- 変更の記録（コミット）の名前・メールは、このリポジトリだけ `yy-devlog` と GitHub の非公開アドレス
  （`…+yy-devlog@users.noreply.github.com`）に設定してある。本名や個人のメールを載せないため

## ページ
| アドレス | ファイル | 中身 |
|---|---|---|
| / | `docs/index.html` | ブランドの紹介、アプリの一覧 |
| /support/ | `docs/support/index.html` | 問い合わせ先（Googleフォーム・support@hapibebi.jp）、医療相談には答えられない旨と #8000・119、よくある質問、動作環境 |
| /sodachi/privacy/ | `docs/sodachi/privacy/index.html` | そだち手帳のプライバシーポリシー |
| /sodachi/terms/ | `docs/sodachi/terms/index.html` | そだち手帳の利用規約 |

- ほかのアプリを出すときは `/アプリの短い名前/privacy/` のように、アプリごとにフォルダを足す
- プライバシーポリシー・利用規約は、2026-09-23 制定の Artifact（claude.ai）の文面を移したもの。
  変えたのは連絡先（メールを追加）と「最終改定日」だけ。**Artifact は、古いビルドのアプリがリンクしているため消さない**
- ポリシーや規約を変えたら「最終改定日」を直す。アプリの機能（集める情報）が変わったら、ポリシーも必ず見直す

## 作りの方針
- 素の HTML・CSS だけ（共通の見た目は `docs/assets/style.css`）。ライブラリ・外部のスクリプト・Webフォントは使わない
- **アクセス解析・Cookie・広告は入れない**（プライバシーポリシーの「データを集めない」と矛盾させないため）
- 文字の大きさと色は `../../app/文字サイズ・読みやすさガイド.md` に合わせる。読ませたい文は16px、補足は13px以上。
  灰色・リンクの色は、背景の上で 4.5:1 以上（リンク #a84d40 は 5.2:1。そだち手帳の #d16f60 は 3.21:1 で足りないので文字には使わない）
- スマホで見るのが第一。ダークモードにも対応
- 確認：`python3 -m http.server 8765 --directory docs` で表示し、幅390pxで撮影して見る

## 開発進捗
- 2026-10-27：4ページと共通のCSSを作り、パソコンの中で表示を確認（ライト・ダーク）。組織 `hapibebi` を作成済み（Yukiさん）
- 次にやること：
  1. 【Yuki】中身の確認（とくにトップの紹介文、サポートページの文）
  2. 【ChatGPT】プライバシーポリシー・サポートページの review（任意）
  3. 【Claude】Yukiさんの承認後、GitHub にリポジトリを作って送り、GitHub Pages を有効にする
  4. 【Yuki】エックスサーバーの DNS に GitHub Pages 用の行を追加、GitHub で組織のドメインの確認（乗っ取り防止）
  5. 【Claude＋Yuki】HTTPS を有効にして表示を確認
  6. 【Yuki】App Store Connect のサポートURL・プライバシーポリシーURL を変える
  7. 【Claude】アプリ内のリンク（`SettingsView.swift` の `privacyPolicyAndTerms`）を次のビルドで新しいアドレスに
  8. 【Claude＋Yuki】hapibebi.com → hapibebi.jp の転送（急がない）
