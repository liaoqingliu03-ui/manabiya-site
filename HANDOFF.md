# HANDOFF：学び屋 紹介サイト

## 作ったもの
- `index.html` / `style.css`（script.js なし。ビルドツール・フレームワーク・外部フォント・外部画像なし）
- 構成：ヒーロー → 発売中2点 → 無料サンプル（note） → ご利用の流れ（4ステップ） → フッター（BOOTH / note）
- 装飾はCSSとインラインSVGのみ。モバイルファースト（1カラム、720px以上で2カラム）。
- 掲載したのは BRIEF の事実のみ（商品2点・価格・ページ数・指定URL）。

## 検証結果（生の出力）
| 項目 | 結果 |
|---|---|
| `python3 -m http.server` + curl | index.html → 200、style.css → 200 |
| 全リンクが指定URLと完全一致 | href は BOOTHショップ(2)、商品2件、note、無料サンプル記事の5種＋`style.css`のみ。他URLなし（grep） |
| 個人情報（青柳／遼／明治） | index.html 0件、style.css 0件 |
| レスポンシブ | `<meta name="viewport" content="width=device-width, initial-scale=1">` あり、`@media (min-width:720px)` で拡張（基本はモバイル1カラム） |
| 外部画像・外部読み込み | `<img>`・`src=` なし、CSSに `url()`/http なし |

## 未実施・注意
- 実機/ブラウザでの目視（スクリーンショット）確認は未実施。上記はコード・grep・HTTPステータスのみの検証。
- 商品2の「3〜6歳向け・A4」はBRIEFに記載がないため書いていない（全10ページのみ記載）。
- 商品カードのイラスト（顔・「あ」・「123」）は雰囲気用の装飾で、実際のプリント内容を示すものではない。差し替え要否はSunny判断。
- 「購入→ダウンロード→A4印刷→遊ぶ」の各説明文（色えんぴつやクレヨン等）は一般的な使い方の文面。実態と合うか要確認。
- git commit はしていない（git管理外ディレクトリ）。

---

# 追加発注（2026-11-06：検索対策）の結果

## 実装
- `sitemap.xml` 新規：トップ1URL（https://liaoqingliu03-ui.github.io/manabiya-site/）、lastmod 2026-11-06。
- `robots.txt` 新規：`User-agent: *` / `Allow: /` / `Sitemap: …/sitemap.xml`。
- `index.html` head に追加：canonical、og:title / og:description / og:type=website / og:url、twitter:card=summary。meta keywords なし、description は既存のまま。
- 語の確認と最小補正（変更は2か所のみ）：
  - `<title>`：「学び屋｜3〜6歳の幼児向け知育プリント｜ぬりえ・ひらがな練習でおうち学習」（旧：おうちで印刷してすぐ遊べる、3〜6歳の知育プリント）。og:title も同文。
  - 商品セクションの h2：「発売中のプリント」→「発売中の知育プリント」。
  - 既存本文で足りていた語：知育プリント、ぬりえ、ひらがな練習。「3歳・4歳・5歳・6歳」は「3〜6歳」で表現済みのため個別には追加せず（詰め込み回避）。「幼児」「おうち学習」はタイトルにのみ追加。本文には入れていない。

## 検証（生の出力）
| 項目 | 結果 |
|---|---|
| `python3 -m http.server` + curl | index.html 200 / style.css 200 / sitemap.xml 200 / robots.txt 200 |
| sitemap.xml の整形式 | minidom で parse OK |
| head の追加タグ | canonical, og:title, og:description, og:type, og:url, twitter:card を目視で確認 |
| URL一覧（grep） | 新規サイトURL（canonical・og:url）＋従来の BOOTH/商品2件/note/無料サンプル記事のみ。他URLなし |
| 個人情報（青柳／遼／明治） | index.html / style.css / sitemap.xml / robots.txt すべて 0件 |
| 外部画像・読み込み | `<img>`・`src=`・`url()` 0件（従来維持） |

## 注意・未確認
- サイトURLは発注書記載の値をそのまま使用。実際にそのURLで公開されているか、GitHub Pagesが有効かは未確認（ローカル配信のみ検証）。
- og:image は未設定（発注に含まれず、外部画像直リンク禁止のため）。SNS共有時の画像は出ない。
- `index-standalone.html` は今回更新していない（head追加・title変更は未反映）。公開物として使うなら要同期。
- 検索順位・インデックス登録の効果は未確認（Search Consoleでのsitemap送信は遼の操作）。
- 冒頭の「git管理外」は古い記述。現在はgit管理下。git commit は今回もしていない。
