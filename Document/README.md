# OWASP 大規模言語モデルセキュリティ検証標準

[![OWASP Incubator](https://img.shields.io/badge/owasp-incubator-blue.svg)](https://owasp.org/www-project-llm-verification-standard/)
[![Creative Commons License](https://img.shields.io/github/license/OWASP/www-project-llm-verification-standard)](https://creativecommons.org/licenses/by-sa/4.0/ "CC BY-SA 4.0")

## はじめに

OWASP 大規模言語モデルセキュリティ検証標準 (Large Language Model Security Verification Standard, LLMSVS) プロジェクトの主な目的は、人工知能と大規模言語モデルを活用するシステムのためにオープンなセキュリティ標準を提供することです。

この標準は、アーキテクチャ、モデルライフサイクル、モデルトレーニング、モデルの運用と統合、モデルの保存と監視に関する懸念事項を含む、堅牢な LLM をバックとするアプリケーションを設計、構築、テストするための基礎を提供します。

多大な時間を割いて、あるいは資金面でプロジェクトを支援してくださった団体に "[Supporters](SUPPORTERS.md)" ページで感謝の意を表します。

**バグを見つけたり、アイデアがある場合、[issue を記録](https://github.com/OWASP/www-project-llm-verification-standard/issues) してください。その後、その issue のディスカッションに基づいて [プルリクエストを開く](https://github.com/OWASP/www-project-llm-verification-standard/pulls) ようにおねがいすることがあります。**

## 分類 (Classification) と対象読者 (Audience)

**分類 (Classification):** ドキュメント (Documentation)

**対象読者 (Audience):**

* 開発者 (Builders)
* 解析者 (Breakers)
* 保守者 (Defenders)

## プロジェクトリーダーとワーキンググループ

このプロジェクトは二人のプロジェクトリーダー [Vandana Verma Sehgal](https://github.com/vermava) と [Elliot Ward](https://github.com/mowzk) が主導しています。

## 標準ドキュメント (マークダウン)

- **[LLMSVS v2.0 (日本語)](LLMSVS-v2.0-ja.md)** — 日本語 2.0 リリースのマークダウン版。

- **[LLMSVS v1.0 (日本語)](LLMSVS-v1.0-ja.md)** — 以前の **0.1** 公開トラック (2024 年 2 月) に適合するマークダウン版。コミュニティ PDF と同じ要件番号付けをしています。

## バージョン 2.0 は 6 月 15 日にリリース予定

このブランチのマスターブランチは常に "bleeding edge version" であり、進行中の変更や他の編集が開いているかもしれません。

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


## [貢献](https://github.com/OWASP/www-project-llm-verification-standard/blob/main/CONTRIBUTING.md)

OWASP 大規模言語モデルセキュリティ検証標準 (Large Language Model Security Verification Standard, LLMSVS) プロジェクトへの貢献に関心を寄せていただき、ありがとうございます。あらゆる貢献を歓迎するとともに、プロジェクトの改善に向けた皆様の取り組みに感謝します。

### 始め方

1. OWASP Slack ワークスペースと `#project-llmvs` チャンネルに参加します。上記の [リポジトリとコミュニティ](#repository-and-community) にあるリンクを使用します。
2. プロジェクトの目標と目的をよく理解します。
3. リポジトリをフォーク氏、ローカルマシンにクローンします。
4. 必要な依存関係をインストールし、開発環境をセットアップします。
5. 変更を行い、ローカルでテストし、期待したように動作することを確認します。
6. 変更を含むプルリクエストを送信します。

### プルリクエストガイドライン

プルリクエストを送信する前に、以下を確認してください。

1. 変更はプロジェクトの目標や目的に沿っていること。
2. 変更は適切に文書化されており、プロジェクトのコーディング規約に準拠していること。
3. 変更は新たなバグを混入したり、既存の機能を損なうことがないこと。
4. 適用できる場合、変更にはテストを付属していること。
5. プルリクエストには行った変更の明確かつ簡潔な説明を含むこと。

### 行動規範

OWASP プロジェクトのすべての貢献者には [行動規範](https://owasp.org/www-policy/operational/code-of-conduct) の遵守をお願いしています。この規範はプロジェクトコミュニティ内での行動に関する指針を示し、すべての貢献者にとって歓迎的かつ包括的な環境を維持するために役立ちます。

OWASP プロジェクトへの貢献に関心を寄せていただき、ありがとうございます。プロジェクトの改善と発展に寄与する皆様の取り組みに感謝します。


## ライセンス

プロジェクトのコンテンツ全体は **[Creative Commons Attribution-Share Alike v4.0](LICENSE.md)** ライセンスの下にあります。
