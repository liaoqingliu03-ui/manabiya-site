# 指示書：学び屋 紹介サイト構築

あなたはAI同盟の実行席（Claude Code）です。議長Sunnyからの発注として、以下を自律的に構築し、自己検証まで完了させてください。git commitはしないこと（検証後にSunnyが行います）。

## 作るもの
「学び屋」の紹介用1ページサイト（ランディングページ）。静的サイト：`index.html` + `style.css`（必要なら最小限の `script.js`）。ビルドツール・フレームワーク禁止。frontend-design スキルの流儀で、保護者がスマホで見て温かみと信頼感を持つデザインにすること。モバイルファースト。

## 学び屋とは（事実のみ、ここに無い実績は書かない）
- おうちで印刷して使える、3〜6歳向け知育プリントの小さなダウンロードショップ
- 販売はBOOTH、読み物と無料サンプルはnoteで公開

## 掲載商品（発売中はこの2点のみ。それ以外の商品・価格を invent しない）
1. ぬりえ＋ひらがな練習 あいうえお おともだち編｜3〜6歳向け・印刷して使えるA4 PDF（全13ページ）— ¥100
   https://manabiya.booth.pm/items/9060017
2. クリスマスぬりえ＋かずあそび（全10ページ）— ¥200
   https://manabiya.booth.pm/items/9076817

## リンク（完全一致で使うこと）
- BOOTHショップ: https://manabiya.booth.pm
- note: https://note.com/manabiya_print
- 無料サンプル記事: https://note.com/manabiya_print/n/na28b91ef5f6b

## ページ構成
1. ヒーロー：学び屋の名前と「おうちで印刷してすぐ遊べる、3〜6歳の知育プリント」という一文、BOOTHへのボタン
2. 商品紹介：上記2点（タイトル・ページ数・価格・BOOTH商品ページへのボタン）
3. 無料サンプル：noteで無料サンプルを配布中であることと、その記事へのリンク
4. 使い方：購入→ダウンロード→A4印刷→おうちで遊ぶ、の3〜4ステップ
5. フッター：BOOTHとnoteへのリンク

## 禁止事項（厳守）
- 運営者の個人情報（氏名・学校名・年齢・学年）を一切書かない。「学び屋」という屋号のみ
- 売上件数・レビュー・お客様の声など、存在しない実績を書かない
- 上記以外のURLを invent しない
- 外部画像の直リンク禁止。装飾はCSSとインラインSVGで作る

## 自己検証（実施して結果を HANDOFF.md に書く）
- `python3 -m http.server` で配信し、`curl` で index.html が 200 で返ること
- ページ内の全リンクが上記URLのいずれかと完全一致すること（grepで確認）
- 個人情報が含まれないこと（「青柳」「遼」「明治」でgrepして0件）
- レスポンシブ確認：viewportメタタグとモバイル向けレイアウトが入っていること

## 成果物
- index.html / style.css（/ script.js）
- HANDOFF.md：作ったもの、検証結果、判断に迷った点があれば明記

## 追加発注（2026-11-06：検索対策）
サイトURL: https://liaoqingliu03-ui.github.io/manabiya-site/
以下を実装し、自己検証して結果を HANDOFF.md に追記すること。ページの見た目と既存の文章は基本変えない。
1. sitemap.xml を新規作成（トップページ1URLのみ、lastmod は 2026-11-06）。
2. robots.txt を新規作成（全許可＋sitemapの場所を記載）。
3. index.html の head に追加：
   - canonical リンク（上記URL）
   - OGP（og:title / og:description / og:type=website / og:url）と twitter:card=summary
   - meta keywords は不要。description は既存のままでよい。
4. 検索で使われる語（知育プリント・ぬりえ・ひらがな練習・3歳・4歳・5歳・6歳・幼児・おうち学習）を、既存の本文の範囲で自然に確認し、タイトルと見出しに不足があれば最小限だけ補う（キーワードの詰め込み、不自然な繰り返しは禁止）。
5. 検証：sitemap.xml と robots.txt がローカル配信で 200 で返ること、head の追加タグが入っていること、リンクと個人情報の再チェック（従来分も維持）。
6. git commit はしない（Sunnyが行う）。
