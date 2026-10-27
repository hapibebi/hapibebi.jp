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
- プライバシーポリシー・利用規約は、2026-09-23 制定の Artifact（claude.ai）の文面がもと。2026-10-27 に ChatGPT の review
  （`handoff/responses/20261027_2133_review-hapibebi-site.md`）を受け、本人が選んだ指摘を反映：全面免責をやめる、TestFlight で
  名前・メールが見えることを書く、問い合わせ（Googleフォーム・iCloudメール）の保存は**対応が終わってから1年以内に削除**、
  運営者の氏名・住所は**求めに応じて回答**（Webには載せない）、開示・削除などの請求窓口、規約の変更は民法548条の4に沿う、
  料金は無料と明記、「Apple Account」に統一。Apple のガイドライン 5.1.3(ii)（健康情報の iCloud 保存）は Apple の回答待ちで文面は変えていない。
  **Artifact は、古いビルドのアプリがリンクしているため消さない**（Artifact の文面は古いまま）
- ポリシーに書いた運用は、書いたとおりに行う：問い合わせは対応後1年以内に削除（年に1〜2回まとめて）、不具合の中身は
  個人の情報を抜いて開発のメモに残す
- ポリシーや規約を変えたら「最終改定日」を直す。アプリの機能（集める情報）が変わったら、ポリシーも必ず見直す

## 作りの方針
- 素の HTML・CSS だけ（共通の見た目は `docs/assets/style.css`）。ライブラリ・外部のスクリプト・Webフォントは使わない
- **アクセス解析・Cookie・広告は入れない**（プライバシーポリシーの「データを集めない」と矛盾させないため）
- 文字の大きさと色は `../../app/文字サイズ・読みやすさガイド.md` に合わせる。読ませたい文は16px、補足は13px以上。
  灰色・リンクの色は、背景の上で 4.5:1 以上（リンク #a84d40 は 5.2:1。そだち手帳の #d16f60 は 3.21:1 で足りないので文字には使わない）
- スマホで見るのが第一。ダークモードにも対応
- 確認：`python3 -m http.server 8765 --directory docs` で表示し、幅390pxで撮影して見る

## 開発進捗
- 2026-10-27：4ページと共通のCSSを作り、パソコンの中で表示を確認（ライト・ダーク）。トップの見出しは本人の希望で
  やわらかい色の丸ゴシック・句点なし（パソコン1行、スマホは「、」で2行）。サポートから #8000・119 の文は削除（本人判断）
- 2026-10-27：組織 `hapibebi` を作成、組織でドメイン hapibebi.jp を確認済み（`_github-pages-challenge-hapibebi` の TXT）。
  公開リポジトリ `hapibebi/hapibebi.jp` に送り、GitHub Pages（main の `/docs`）と独自ドメインを設定。
  エックスサーバーの DNS に A 4行（185.199.108〜111.153）と `www` CNAME（hapibebi.github.io）を追加、21:59 に3台へ反映
- 2026-10-27 夜の時点：**HTTPS の証明書がまだ発行されていない**（`gh api repos/hapibebi/hapibebi.jp/pages` の
  `https_certificate` が null）。本人の家の回線は「行き先なし」の古い答えを覚えていて、22:45ごろまで開けなかった
- 次にやること：
  1. 【Claude】証明書の状態を確認。できていれば `gh api -X PUT repos/hapibebi/hapibebi.jp/pages -F https_enforced=true` で
     「Enforce HTTPS」をオン。できていなければ、独自ドメインを一度外して付け直す（GitHub の Settings → Pages）
  2. 【Claude＋Yuki】https://hapibebi.jp の4ページが鍵マーク付きで開けるか確認
  3. 【ChatGPT】review の依頼済み（`handoff/requests/20261027_2133_review-hapibebi-site.md`）。回答を見て直す
  6. 【Yuki】App Store Connect のサポートURL・プライバシーポリシーURL を変える
  7. 【Claude】アプリ内のリンク（`SettingsView.swift` の `privacyPolicyAndTerms`）を次のビルドで新しいアドレスに
  8. 【Claude＋Yuki】hapibebi.com → hapibebi.jp の転送（急がない）
