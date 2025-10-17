---
title: "Amazon Q Developer for GitHub で PR を日本語レビューしてもらう"
emoji: "🍒"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["github", "amazonq", "aws", "コードレビュー", "ai"]
published: false
---

:::message
**注意（2025-10-17 時点）**  
Amazon Q Developer for GitHub はプレビュー中です。利用前に最新のガイドラインを確認してください。

* プレビューのため仕様は変更される可能性があります。
* サービス向上のためにお客様のコンテンツを利用することはありません。今後そのような利用を可能にする場合は、適切な通知とオプトアウト手段が提供されます。  

ref. <https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/amazon-q-for-github.html>
:::

こんにちは。jkkitakitaです。

最近はコードレビューを Claude Code Actions / Copilot / Bugbot などの AI にお願いすることが増えてきました。
この記事では、意外と情報が少ない Amazon Q Developer for GitHub で PR を日本語レビューさせるための Tips を紹介します。

## 結論：`.amazonq/rules/` に Markdown を置けば日本語レビューモードになる

リポジトリ直下に `.amazonq/rules/language.md`（ファイル名は任意）を追加します。中身はたとえばこれだけでOK。

```markdown
すべての説明・提案・レビューコメントは日本語で書いてください。
````

ディレクトリ構成例：

```
.
├─ .amazonq/
│  └─ rules/
│     └─ language.md
└─ ...
```

> PR を作成・再オープンすると、以降のレビューコメントが日本語寄りになります。

## Amazon Q Developer for GitHub とは

GitHub のワークフロー上で **Amazon Q Developer** の機能（コードレビューや Coding Agent）を使える GitHub App です。
この記事では **コードレビュー** に絞って紹介します。Amazon Q 全体像は下記がまとまっています。
[https://zenn.dev/issy/articles/zenn-q-overview](https://zenn.dev/issy/articles/zenn-q-overview)

セットアップは **GitHub Marketplace の App をインストール**するだけ。
[https://github.com/marketplace/amazon-q-developer](https://github.com/marketplace/amazon-q-developer)

連携が完了すると、次のタイミングで **PR に自動レビュー**が走ります。

* 新しいプルリクエストを作成したとき
* クローズ済み PR を再オープンしたとき

## 使い方：PR を作るだけ（＋ルールファイル）

前述の `rules` を追加して PR を作ると、こんな感じでレビューが出ます。

* まず **概要**（変更点の要約や気になる点）

![overview](/images/1e984caafadc8d/overview.png)

* さらに **インラインのコードコメント**

![inline](/images/1e984caafadc8d/inline.png)

## さいごに

Amazon Q Developer for GitHub のレビューは、Claude Code Actions や Copilot と比べるとやや
指摘が細かくて“おせっかい”に感じる場面もありますが（笑）
他ツールが見落としがちな箇所を拾ってくれる印象もあるので
用途やチームの好みに合わせて 併用していくのが良さそうだなと思っています。
ぜひ活用してもらえると良いかなと思います！
