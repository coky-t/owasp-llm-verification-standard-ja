# OWASP 大規模言語モデルセキュリティ検証標準

[![OWASP Incubator](https://img.shields.io/badge/owasp-incubator-blue.svg)](https://owasp.org/www-project-llm-verification-standard/)
[![Creative Commons License](https://img.shields.io/github/license/OWASP/www-project-llm-verification-standard)](https://creativecommons.org/licenses/by-sa/4.0/ "CC BY-SA 4.0")

## はじめに

OWASP 大規模言語モデルセキュリティ検証標準 (Large Language Model Security Verification Standard, LLMSVS) プロジェクトの主な目的は、人工知能と大規模言語モデルを活用するシステムのためにオープンなセキュリティ標準を提供することです。

この標準は、アーキテクチャ、モデルライフサイクル、モデルトレーニング、モデルの運用と統合、モデルの保存と監視に関する懸念事項を含む、堅牢な LLM をバックとするアプリケーションを設計、構築、テストするための基礎を提供します。

多大な時間を割いて、あるいは資金面でプロジェクトを支援してくださった団体に "[Supporters](SUPPORTERS.md)" ページで感謝の意を表します。

**バグを見つけたり、アイデアがある場合、[issue を記録](https://github.com/OWASP/www-project-llm-verification-standard/issues) してください。その後、その issue のディスカッションに基づいて [プルリクエストを開く](https://github.com/OWASP/www-project-llm-verification-standard/pulls) ようにおねがいすることがあります。**

## プロジェクトリーダーとワーキンググループ

このプロジェクトは二人のプロジェクトリーダー [Vandana Verma Sehgal](https://github.com/vermava) と [Elliot Ward](https://github.com/mowzk) が主導しています。

## 初期ドラフトバージョン - 0.1

最初の安定バージョンはバージョン 0.1 (2024 年 2 月付け) で、以下にあります。

* [OWASP Large Language Model Security Verification Standard 0.1 English (PDF)](https://github.com/OWASP/www-project-llm-verification-standard/releases/tag/0.1)

このブランチのマスターブランチは常に "bleeding edge version" であり、進行中の変更や他の編集が開いているかもしれません。

## 標準の目標

要件は以下の目標を念頭に置いて作成されました。

1. **セキュリティガイドラインを策定および改良する**: コミュニティの参加と標準の進化などの一般的な目標を、AI と LLM ベースのシステムのための包括的なセキュリティガイドラインセットに統合します。
2. **LLM 固有のセキュリティ課題に対処する**: 大規模言語モデルによってもたらされる固有の機能的および非機能的なセキュリティ課題に特に焦点を当てます。
3. **開発チームにセキュアプラクティスをガイドする**: LLM ベースのアプリケーションに堅牢なセキュリティ対策を実装するための詳細なガイダンスを開発チームに提供します。
4. **監査とペネトレーションテストでセキュリティチームを支援する**: セキュリティチームが LLM をバックとするシステムで効果的なセキュリティ監査とペネトレーションテストを実施するための方法論と標準を提供します。
5. **セキュリティベンチマークを確立および更新する**: AI とサイバーセキュリティの最新の進歩に合わせて、セキュリティベンチマークを作成し、定期的に更新します。
6. **LLM セキュリティのベストプラクティスを推進する**: LLM ベースのシステムのセキュリティ保護において、業界のベストプラクティスの採用を奨励します。
7. **利害関係者間でのセキュリティに対する期待を調整する**: 開発者、セキュリティ専門家、ベンダー、クライアントの間でセキュリティへの期待について共通認識を確立します。

## ライセンス

プロジェクトのコンテンツ全体は **[Creative Commons Attribution-Share Alike v4.0](LICENSE.md)** ライセンスの下にあります。
