---
layout: col-sidebar
title: OWASP Large Language Model Security Verification Standard
tags: llm, verification, ai, security
level: 2
type: documentation
pitch: 大規模言語モデルを使用するアプリケーションのセキュリティを設計、構築、検証するためのオープンスタンダード。
---

## 概要

OWASP 大規模言語モデルセキュリティ検証標準

OWASP 大規模言語モデルセキュリティ検証標準 (LLMSVS) は大規模言語モデルを使用するアプリケーションのためのセキュリティ要件のカタログです。アーキテクト、開発者、テスト担当者、セキュリティチームは LLM 機能において「検証済み」が何を意味するのかを合意するためにそれを使用します。これはアプリケーションの他の部分に関する OWASP アプリケーションセキュリティ検証標準を置き換えるものではありません。

**現行リリース:** [LLMSVS v2.0 (日本語)](LLMSVS-v2.0-ja.md)

**次期版ドラフト、レビュー用:** [LLMSVS v2.1 ドラフト](LLMSVS-v2.1-draft-ja.md)

このドラフトはリリース版ではありません。プロジェクトが新しい版を受諾するまで v2.0 を引用してください。


[![OWASP Incubator](https://img.shields.io/badge/owasp-incubator-blue.svg)](https://owasp.org/www-project-llm-verification-standard/)
[![Creative Commons License](https://img.shields.io/github/license/OWASP/www-project-llm-verification-standard)](https://creativecommons.org/licenses/by-sa/4.0/ "CC BY-SA 4.0")

## はじめに

OWASP 大規模言語モデルセキュリティ検証標準 (Large Language Model Security Verification Standard, LLMSVS) プロジェクトの主な目的は、人工知能と大規模言語モデルを活用するシステムのためにオープンなセキュリティ標準を提供することです。

この標準は、アーキテクチャ、モデルライフサイクル、モデルトレーニング、モデルの運用と統合、モデルの保存と監視に関する懸念事項を含む、堅牢な LLM をバックとするアプリケーションを設計、構築、テストするための基礎を提供します。

**バグを見つけたり、アイデアがある場合、[issue を記録](https://github.com/OWASP/www-project-llm-verification-standard/issues) してください。その後、その issue のディスカッションに基づいて [プルリクエストを開く](https://github.com/OWASP/www-project-llm-verification-standard/pulls) ようにおねがいすることがあります。**

## 分類 (Classification) と対象読者 (Audience)

**分類 (Classification):** ドキュメント (Documentation)

**対象読者 (Audience):**

* 開発者 (Builders)
* 解析者 (Breakers)
* 保守者 (Defenders)

## プロジェクトリーダー

このプロジェクトは [Vandana Verma Sehgal](https://github.com/vermava) と [Elliot Ward](https://github.com/mowzk) が主導しています。初版のレビュー担当者は本標準にクレジットされています。<!-- Supporters are listed in [SUPPORTERS.md](SUPPORTERS.md). -->

## 標準ドキュメント (マークダウン)

- **[LLMSVS v2.0 (日本語)](LLMSVS-v2.0-ja.md)** — 現行リリース。この版を引用してください。
- **[LLMSVS v2.1 ドラフト (日本語)](LLMSVS-v2.1-draft-ja.md)** — 次版の提案。リリースではありません。<!-- Kept in step with [`catalog/llmsvs-draft.json`](catalog/llmsvs-draft.json). -->
- **[LLMSVS v1.0 (日本語)](LLMSVS-v1.0-ja.md)** — 2024 年 2 月 **0.1** テキストのマークダウン版。ファイル名は 1.0 と示しており、要件番号は初版と一致しています。
- **[改訂履歴](https://github.com/OWASP/www-project-llm-verification-standard/blob/main/CHANGELOG.md)**
<!-- - **[Crosswalk](mappings/crosswalk.md)**, **[profiles](profiles/)**, and a **[worked assessment](examples/worked-assessment.md)** for the draft. -->

`main` には 2.0 リリースと作業中のドラフトをともに含みます。2.0 をフリーズしたままにしつつ、`main` でドラフトを継続するには、git タグを作成してください。

## リポジトリとコミュニティ <a name="repository-and-community"></a>

* [GitHub リポジトリ](https://github.com/OWASP/www-project-llm-verification-standard)
* [Releases (changelog)](https://github.com/OWASP/www-project-llm-verification-standard/releases)
* [OWASP Slack に参加する](https://owasp.org/slack/invite)
* [Slack の #project-llmvs](https://owasp.slack.com/messages/C06MDJG0KBK)

## 標準の目標

要件は以下の目標を念頭に置いて作成されました。

1. **セキュリティガイドラインを策定および改良する**: コミュニティの参加と標準の進化などの一般的な目標を、AI と LLM ベースのシステムのための包括的なセキュリティガイドラインセットに統合します。
2. **LLM 固有のセキュリティ課題に対処する**: 大規模言語モデルによってもたらされる固有の機能的および非機能的なセキュリティ課題に特に焦点を当てます。
3. **開発チームにセキュアプラクティスをガイドする**: LLM ベースのアプリケーションに堅牢なセキュリティ対策を実装するための詳細なガイダンスを開発チームに提供します。
4. **監査とペネトレーションテストでセキュリティチームを支援する**: セキュリティチームが LLM をバックとするシステムで効果的なセキュリティ監査とペネトレーションテストを実施するための方法論と標準を提供します。
5. **セキュリティベンチマークを確立および更新する**: AI とサイバーセキュリティの最新の進歩に合わせて、セキュリティベンチマークを作成し、定期的に更新します。
6. **LLM セキュリティのベストプラクティスを推進する**: LLM ベースのシステムのセキュリティ保護において、業界のベストプラクティスの採用を奨励します。
7. **利害関係者間でのセキュリティに対する期待を調整する**: 開発者、セキュリティ専門家、ベンダー、クライアントの間でセキュリティへの期待について共通認識を確立します。


## 貢献

[CONTRIBUTING.md](https://github.com/OWASP/www-project-llm-verification-standard/blob/main/CONTRIBUTING.md) をお読みください。要件変更はドラフトカタログに入ります。2.0 リリースファイルには入りません。貢献者は [OWASP 行動規範](https://owasp.org/www-policy/operational/code-of-conduct) に準拠してください。


## ライセンス

プロジェクトのコンテンツ全体は **[Creative Commons Attribution-Share Alike v4.0](LICENSE.md)** ライセンスの下にあります。
