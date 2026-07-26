---
title: OWASP Large Language Model Security Verification Standard
lang: ja
version: '1.0'
status: release
---

# OWASP 大規模言語モデルセキュリティ検証標準 (Large Language Model Security Verification Standard, LLMSVS)

**バージョン:** 1.0 (日本語)  
**出版年:** 2024  

このドキュメントは OWASP LLMSVS 日本語リリースのマークダウン版です。バージョン 0.1 の公式 PDF と同じ技術内容を含み、ウェブレンダリング、バージョン管理、派生ビルド向けに整理されています。

## 目次

- [扉](#frontispiece)
  - [本標準について](#about-the-standard)
  - [著作権およびライセンス](#copyright-and-license)
  - [プロジェクトリーダー](#project-leads)
  - [他の貢献者およびレビュー担当者](#other-contributors-and-reviewers)
  - [主なサポータおよびスポンサー](#major-supporters-and-sponsors)
- [序文](#preface)
- [LLMSVS の活用](#utilizing-the-llmsvs)
  - [セキュリティ検証レイヤ](#security-verification-layers)
  - [想定](#assumptions)
- [監査と認証](#assessment-and-certification)
  - [LLMSVS 認証と認証マークに対する OWASP の見解](#owasps-stance-on-llmsvs-certifications-and-trust-marks)
  - [認証機関のためのガイダンス](#guidance-for-certifying-organizations)
- [V1. 安全な構成と保守 (Secure configuration and maintenance)](#v1-secure-configuration-and-maintenance)
- [V2. モデルのライフサイクル (Model lifecycle)](#v2-model-lifecycle)
- [V3. リアルタイム学習 (Real time learning)](#v3-real-time-learning)
- [V4. Model memory and storage](#v4-model-memory-and-storage)
- [V5. Secure LLM integration](#v5-secure-llm-integration)
- [V6. Agents and plugins](#v6-agents-and-plugins)
- [V7. Dependency and component](#v7-dependency-and-component)
- [V8. Monitoring and anomaly detection](#v8-monitoring-and-anomaly-detection)
- [Appendix A: Glossary](#appendix-a-glossary)

---

## 扉 <a name="frontispiece"></a>

### 本標準について <a name="about-the-standard"></a>

大規模言語モデルセキュリティ検証標準は、アーキテクト、開発者、テスト担当者、セキュリティ専門家、ツールベンダー、および消費者によって、安全な LLM 駆動型アプリケーションを定義、構築、テスト、検証するために使用できる、特定の AI および LLM セキュリティ要件やテストのリストです。

### 著作権およびライセンス <a name="copyright-and-license"></a>

Copyright © 2008–2024 The OWASP Foundation. このドキュメントは [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/) の下でリリースされています。再使用または配布する場合は、他者に対し本著作物のライセンス条項を明らかにする必要があります。

### プロジェクトリーダー <a name="project-leads"></a>

- Vandana Verma Sehgal
- Elliot Ward

### 他の貢献者およびレビュー担当者 <a name="other-contributors-and-reviewers"></a>

| 氏名 | 組織 |
| ---- | ------------ |
| Eric Allen | Lakera |
| Frawa Vetterli | Lakera |
| Rory McNamara | Snyk |
| Raul Onitza-Klugman | Snyk |
| Moshe Ben-Nehemia | Snyk |
| Sam Watts | Lakera |

クレジットが上記の 0.1 クレジットリストから漏れている場合には、今後の 0.x アップデートで反映されるために GitHub にチケットを登録してください。

大規模言語モデルセキュリティ検証標準は Snyk Security Labs チームが 2023 年に実施した LLM セキュリティに関する初期研究に基づいて構築されています。LLMSVS の概念、構造、定型、ツールの多くは OWASP ASVS プロジェクトから採用されています。OWASP ASVS にこれまで関わってこられた皆様に感謝します。

### 主なサポータおよびスポンサー <a name="major-supporters-and-sponsors"></a>

この取り組みはスポンサーの皆様の支援と提供されたリソースなくしては実現できませんでした。下記の皆様の支援に謝意を表します。

#### Snyk

LLMSVS プロジェクトは Snyk Security Labs チーム内での AI および LLM プロジェクトに関する研究から得られた知見を共有する方法として設立されました。初期要件の策定およびプロジェクトの設立に尽力した Snyk に感謝します。

#### Lakera

開発者が安全な生成 AI アプリケーションを自信を持って構築できるよう支援するセキュリティ企業 Lakera は、本標準の初期草案をレビューおよび校正し、モデルのライフサイクルセキュリティや安全な LLM 統合の専門知識に基づくガイダンスを提供しました。

---

## 序文 <a name="preface"></a>

OWASP 大規模言語モデルセキュリティ検証標準 (Large Language Model Security Verification Standard, LLMSVS) の最初のアルファ版へようこそ。これは大規模言語モデル (LLM) を統合したアプリケーションやシステムを評価するためのフレームワークを提供します。

LLMSVS は、不変的に適用する明確で実践的なガイドラインを提供し、開発者、アーキテクト、セキュリティ専門家、ベンダー、研究者が LLM を活用したシステムを保護することを支援します。

LLMSVS はさまざまな分野にわたる専門家の知見を集めた共同作業の成果です。これは LLM によってもたらされる特有のセキュリティ課題に対処するものであり、機能的および非機能的なセキュリティの側面に焦点を当てています。このアルファ版は、継続的なフィードバックや LLM の動態の変化、新たな人工知能 (Artificial Intelligence, AI) 技術、サイバーセキュリティの進歩によって形作られて適用していくガイドラインの基盤となります。

このリリースは検証標準を議論して改善するための出発点となります。この標準は最終版ではなく、コミュニティからの貢献と当該分野の進歩に基づいて進化するでしょう。特に AI のような新興分野では、ワンサイズですべてにフィットするセキュリティソリューションは存在しないことを認識しており、定期的な更新と改良が必要になると見込んでいます。

このアルファ版は LLMSVS を開発して向上するために幅広いコミュニティに参加していただくためのものです。私たちは各参加者がこのプロジェクトにもたらす多様な視点と専門知識を高く評価しています。この標準が有意義かつ実用的であり続けるには、皆様のフィードバックや貢献が不可欠です。

貴重な意見を寄せていただいた貢献者の皆様に感謝するとともに、LLMSVS の開発での皆様の継続的な支援と関与を心待ちにしています。

---

## LLMSVS の活用 <a name="utilizing-the-llmsvs"></a>

OWASP LLMSVS は主に以下の目的に仕えます。

- **開発チームの支援:** セキュアな LLM 搭載アプリケーションを開発および保守するチームをガイドします。
- **セキュリティチーム向けのフレームワーク:** LLM 搭載システムに対する要件の策定、セキュリティ監査のガイド、ペネトレーションテストの実施においてセキュリティチームを支援します。
- **セキュリティベンチマークの整合:** セキュリティサービスプロバイダ、ベンダー、クライアントにセキュリティの期待に関する共通基盤を確立します。

### セキュリティ検証レイヤ <a name="security-verification-layers"></a>

LLMSVS はセキュリティ検証を三つの異なるレベルに分類しており、それぞれが異なるレベルのセキュリティ保証に適合しています。

1. **LLMSVS レベル 1 — 基本的なセキュリティ:** このレベルはセキュリティリスクが低めのアプリケーションを対象としており、あらゆる LLM 搭載システムの基本的なセキュリティコントロールに焦点を当てています。

2. **LLMSVS レベル 2 — 中程度のセキュリティ:** このレベルは機密データを扱うアプリケーションに最適であり、多くのアプリケーションのニーズを満たすバランスの取れたセキュリティアプローチを提供します。これらのアプリケーションには、パーソナルアシスタント、顧客データを処理する API、社内データを処理するシステムなどがあります。

3. **LLMSVS レベル 3 — 高保証のセキュリティ:** このレベルは、機密データや高価値取引を伴う極めて重要なアプリケーションに対して、最も広範なセキュリティ対策を提供します。これらのアプリケーションには、業務遂行に不可欠な基幹業務アプリケーション、金融取引を扱うシステム、患者データや医療データを処理するシステムなどの特定の業界規制に該当するシステムがあります。

LLMSVS の各レベルは一連の具体的なセキュリティ要件を提供し、それらを堅牢な LLM 搭載アプリケーションの構築と運用に必要なセキュリティ機能やプラクティスにマップしています。このアプローチは、開発者、アーキテクト、セキュリティ専門家に実践的かつ実行可能なガイドラインを身につけます。これらのアプリケーションのセキュリティを構築、強化、評価するいずれにおいても、LLMSVS は LLM 搭載システムのライフサイクルに関わるすべての利害関係者に明確なロードマップを提示します。

### 想定 <a name="assumptions"></a>

LLMSVS を活用する際、以下の想定を念頭に置くことが重要です。

- LLMSVS は、セキュアコーディングやセキュアソフトウェア開発ライフサイクル (Secure Software Development Life Cycle, SSDLC) といった、セキュアな開発ベストプラクティスに準拠することに置き換わるものではありません。これらのプラクティスは開発の取り組み全体に不可欠なものとして採用されるべきであり、LLMSVS は LLM 搭載アプリケーション向けにそれらを補強するのに役立ちます。

- LLMSVS は包括的なリスク評価や詳細なセキュリティレビューに代わるものではありません。どちらかといえば、LLM 搭載アプリケーション特有の潜在的なセキュリティ脆弱性に対処するためのガイドとして役立ちます。リスクのより徹底した評価や緩和を実現するためには、LLMSVS を採用することは、これらの重要なセキュリティプラクティスを補完すべきものであり、置き換わるものではありません。

LLMSVS は LLM 搭載アプリケーションのセキュリティを強化するための包括的なフレームワークを提供しますが、完全なセキュリティを保証するものではありません。それはセキュリティ要件の基本セットとみなすべきであり、特定の LLM リスクや脅威を緩和するには、必要に応じて追加の保護策を講じる必要があります。

---

## 監査と認証 <a name="assessment-and-certification"></a>

### LLMSVS 認証と認証マークに対する OWASP の見解 <a name="owasps-stance-on-llmsvs-certifications-and-trust-marks"></a>

OWASP はベンダ中立の非営利組織であり、ベンダ、検証者、ソフトウェアの認証は行っていません。

こうした保証の表明、認証マーク、認証はいずれも OWASP によって公式に審査、登録、認証されたものではないため、そうした見解を信頼する組織は、(LLM)SVS 認証を謳う第三者や認証マークについて、その信頼性に注意する必要があります。

これは、OWASP の公式な認証であると主張しない限り、組織がこうした保証サービスを提供することを妨げるものではありません。

### 認証機関のためのガイダンス <a name="guidance-for-certifying-organizations"></a>

大規模言語モデルセキュリティ検証標準 (Large Language Model Security Verification Standard, LLMSVS) への準拠には、「オープンブック」レビューが推奨されます。システムアーキテクト、開発者、プロジェクトドキュメント、ソースコード、認証済みインタフェース (各ユーザーロールについて少なくとも一つのアカウントへのアクセスを含む) といった重要なリソースへのアクセスを、評価者に許可します。

LLMSVS は LLM の使用および統合に関連するセキュリティ要件のみをカバーしていることに留意することが重要です。LLM 搭載システムに特有ではない一般的なアプリケーションセキュリティコントロール (ウェブサービスなど) をカバーしていません。その他のシステムや非 LLM 属性については、[OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/) などの適切な標準に基づいて検証を行う必要があります。

認証レポートには、検証範囲を明確に定義し、特に除外を注記し、合格および不合格となったテストの両方について、結果の詳細と、不合格事項への対処についてのガイダンスを含めて、まとめる必要があります。業界標準の慣行として、検証プロセスの詳細なドキュメントを求められます。これには、作業記録、スクリーンショット、問題再現用スクリプト、プロキシログなどの電子的なテスト記録を含みます。自動化ツールの結果だけでは不十分であり、すべてのコントロールに対して徹底的かつ厳格なテストを裏付ける決定的な証拠をドキュメントで提示しなければなりません。異議申し立てがあった場合に、それぞれの検証コントロールが実際にテストされたことを実証するのに十分な証跡が必要となります。

---

## V1. 安全な構成と保守 (Secure configuration and maintenance) <a name="v1-secure-configuration-and-maintenance"></a>

### 管理目標

モデルプロバイダにホストされている LLM やセルフホストされている LLM が、不正アクセスや機密情報の漏洩を防ぐために、安全に構成および保守されていることを確保します。

| # | 要件        | L1 | L2 | L3 |
| - | ----------- | -- | -- | -- |
| 1.1 | ホストされている LLM やベクターデータベースなどのサードパーティシステムの API キーなどのシークレットを保存するコンポーネントを特定し、OWASP ASVS のセクション V2.10 「サービス認証」に従って、これらのクレデンシャルを安全に処理することを確保します。 | | ✓ | ✓ |
| 1.2 | セルフホストされている LLM の場合、そのようなアクセスが必要でない限り、エンドユーザーに直接公開されることを防ぐために、ネットワーク内で適切に分割されていることを確保します。 | | ✓ | ✓ |
| 1.3 | すべての LLM インスタンスの最新のインベントリを維持し、セルフホストされているモデルに定期的なアップデートとパッチを適用します。 | | | ✓ |
| 1.4 | LLM を搭載したシステムに関連する構成設定について定期的な構成レビューを実施して文書化します。 | | | ✓ |

---

## V2. モデルのライフサイクル (Model lifecycle) <a name="v2-model-lifecycle"></a>

### 管理目標

LLM を搭載したシステム内で使用されるモデルの機械学習 (Machine Learning, ML) が、データセットのキュレーション、モデルのトレーニング、バリデーションによるさまざまなセキュリティ脅威を考慮していることを確保します。

| # | 要件        | L1 | L2 | L3 |
| - | ----------- | -- | -- | -- |
| 2.1 | 機械学習モデルのライフサイクルが既存のセキュアソフトウェア開発ライフサイクル (Secure Software Development Lifecycle, SSDLC) に統合されるように確保します。定義されたプロセスが存在し、ML モデルのライフサイクルの各ステージにおいて利用できる必要があります。 | | ✓ | ✓ |
| 2.2 | 新しく作成される ML モデルの要件とユースケースを定義するユーザーストーリーを文書化します。 | | ✓ | ✓ |
| 2.3 | モデルのトレーニングリソースとデータセットが信頼できるソースから取得され、正確性を検証しているか、悪意のあるデータがないことを確保します。 | ✓ | ✓ | ✓ |
| 2.4 | モデルのトレーニングリソースとデータセットが取得後に不正な変更から適切に保護されていることを確保します。 | | ✓ | ✓ |
| 2.5 | トレーニングリソースとデータセットのソースが文書化されていることを確保します。 | | | ✓ |
| 2.6 | 内部脅威によるデータポイズニングのリスクを軽減するために、オリジナルのトレーニングリソースに対するデータクリーニングやその他の変更が追跡され、監査可能であることを確保します。 | | | ✓ |
| 2.7 | 潜在的なライセンスや著作権侵害の問題を回避するために、モデルのトレーニングリソースとデータセットの知的財産権をチェックしていることを確保します。このプロセスが文書化され、監査可能であることを確保します。 | ✓ | ✓ | ✓ |
| 2.8 | モデルのトレーニングリソースが機密データ (個人情報、社内データなど) について監査され、モデルのレスポンスにおける機密データの露出を軽減するために、トレーニング前にクリーニングされていることを確保します。 | | ✓ | ✓ |
| 2.9 | 基本モデルや事前トレーニング済みモデルの安全な取得と保管を確保します。 | ✓ | ✓ | ✓ |
| 2.10 | 可能であれば、PyTorch の Pickle 形式などの安全でないシリアライゼーションを使用する形式よりも SafeTensors などの安全なモデル形式を選択します。 | ✓ | ✓ | ✓ |
| 2.11 | モデルのパフォーマンス低下につながる可能性のある無関係なデータポイントを制限するために、基本モデルをファインチューニングされることを確保します。 | | ✓ | ✓ |
| 2.12 | モデルのトレーニングデータを取扱いおよび処理する際のコンプライアンスを確保するための規制上の義務を確認します。 | | ✓ | ✓ |
| 2.13 | ML 部品表 (Bill-of-Materials, BOM) がモデルごとに作成されることを確保します。 | | | ✓ |
| 2.14 | モデル窃取が懸念される場合やモデルの出力を識別可能にする必要がある場合は、モデルレスポンスの電子透かし技法を検討します。 | | | ✓ |
| 2.15 | バイアスを検出し、公平性を確保するためのツールが ML モデルのライフサイクルに統合されていることを確保します。 | | ✓ | ✓ |
| 2.16 | インジェクション攻撃、脱獄の試み、その他の悪用などの LLM の脆弱性を検出するセキュリティツールが ML モデルのライフサイクルに統合されていることを確保します。 | | ✓ | ✓ |
| 2.17 | モデルがデプロイメントを完了する前に、徹底的なリスク評価を実施して、潜在的なセキュリティリスク、倫理リスク、運用リスクを把握します。この評価はモデルのデプロイメントに関する意思決定のプロセスの指針となります。 | | | ✓ |
| 2.18 | 使用されなくなったモデルを廃止するための明確な計画があることを確保します。これは、不正アクセスや悪用を防ぐために、データ、モデルパラメータ、モデルに関連する機密情報を安全に消去することを含みます。 | | | ✓ |

---

## V3. リアルタイム学習 (Real time learning) <a name="v3-real-time-learning"></a>

### 管理目標

LLM システム内でのリアルタイム学習に関連するリスクを軽減するためのコントロールを確立します。ここでは、リアルタイムでのユーザーインタラクションに基づいてモデルを継続的にファインチューニングします。

| # | 要件        | L1 | L2 | L3 |
| - | ----------- | -- | -- | -- |
| 3.1 | モデルとインタラクションするための明確な使用条件とガイドラインを定義し、許容できる振る舞いと許容できない振る舞いをユーザーに認識させます。 | ✓ | ✓ | ✓ |
| 3.2 | モデルのパフォーマンスとインタラクションの継続的な監視を確保します。これには、すべての入力と出力を (必要に応じて、データの潜在的な機密性を考慮して) リアルタイムでログ記録し、不適切な振る舞いと予期しない振る舞いを迅速に特定して対処することが含まれます。 | | ✓ | ✓ |
| 3.3 | モデルが望ましくない振る舞いを示し始めた場合に即座に介入するための明確なプロトコルを作成します。これには必要に応じてシステムを迅速にオフラインにする機能を含める必要があります。 | | | ✓ |
| 3.4 | ユーザーインタラクションを定期的に分析して、モデルを不適切な振る舞いに操作しようとする試みを特定して軽減します。 | | | ✓ |
| 3.5 | 人間の承認を得てモデルを段階的に更新できる増分学習アプローチの使用を検討します。 | | | ✓ |

---

## V4. Model memory and storage

### Control objective

Ensure that mechanisms which allow for “memory” or additional knowledge that was not included in the training phase is safely handled.

| # | Requirement | L1 | L2 | L3 |
| - | ----------- | -- | -- | -- |
| 4.1 | Ensure that mechanisms that implement “Conversational memory” do not mistakenly mix up prior prompts for other users. | ✓ | ✓ | ✓ |
| 4.2 | Ensure that mechanisms which support “long-term” storage appropriately segregate user data to ensure it is not possible to retrieve data pertaining to other users, or inject false records for other users. | ✓ | ✓ | ✓ |
| 4.3 | Ensure that controls exist to detect leakage of sensitive data from internal knowledge bases provided as additional context to the LLM. It should not be possible to coerce the LLM into leaking the contents of the knowledge base. | | ✓ | ✓ |
| 4.4 | Ensure that external storage components such as vector databases and caches require authentication for consumers. | ✓ | ✓ | ✓ |
| 4.5 | Enforce the principle of least privilege for accessing production storage components, such as vector databases and caches. | | ✓ | ✓ |
| 4.6 | When updating embeddings within a knowledge base, ensure that an adversary is not able to inject arbitrary documents or otherwise insert false information into the knowledge base. | ✓ | ✓ | ✓ |

---

## V5. Secure LLM integration

### Control objective

Establish controls that enable safe interactions and operations between application components and LLMs.

| # | Requirement | L1 | L2 | L3 |
| - | ----------- | -- | -- | -- |
| 5.1 | Ensure that prompts to LLMs are issued from a trusted server-side component. | ✓ | ✓ | ✓ |
| 5.2 | Ensure that prompts to LLMs are constructed server-side, rather than accepting the complete prompt directly from the client. | ✓ | ✓ | ✓ |
| 5.3 | Consider the use of redundant LLM accounts and providers to avoid single points of failure and ensure application availability. | | | ✓ |
| 5.4 | Ensure that credentials for LLM providers are securely handled according to section V2.10 “Service Authentication” of the OWASP ASVS. | | ✓ | ✓ |
| 5.5 | Ensure that the output format and properties of the data returned from the LLM match the expected structure and properties. Specifically, when a response is expected in JSON, the result should not only be in valid JSON format, but also undergo schema validation to ensure it contains all the expected JSON fields and does not include any unnecessary or extraneous properties. | ✓ | ✓ | ✓ |
| 5.6 | Ensure that the output language of the LLM response matches the expected language. | | ✓ | ✓ |
| 5.7 | Consider using canary tokens in LLM prompts and check whether LLM completions contain the canary word to detect prompt leakage attacks. | | | ✓ |
| 5.8 | Check the entropy of LLM responses to detect encoded data which aims to circumvent additional checks, such as bypassing canary tokens. | | | ✓ |
| 5.9 | Perform length checks on LLM completions to verify that the response length is within an expected range. For example, a response that is significantly longer than the normal output length might indicate the completion is including additional, unexpected data. | | | ✓ |
| 5.10 | Ensure that the application properly suppresses any exceptions and error messages when interacting with the LLM. LLM errors may inadvertently leak the prompt and should not be visible to the client. | ✓ | ✓ | ✓ |
| 5.11 | Ensure that appropriate LLM guards are used to scan prompts and compilations to help detect potential prompt injection attacks. | | ✓ | ✓ |
| 5.12 | Ensure that all prompts are considered to be untrusted and subjected to any deployed security controls. Reflecting stored data, data from third-party APIs, or the response from previous prompt compilations may lead to indirect prompt injections and must be subjected to the same controls as prompts containing direct user input. | | ✓ | ✓ |
| 5.13 | Ensure that the output of LLM completions is considered to be untrusted by any subsequent system. For example, if using the LLM response within a SQL query, the query should not be constructed by concatenating parts of the LLM response but should follow section V5.3.4 of the OWASP ASVS and use parameterized queries. | ✓ | ✓ | ✓ |
| 5.14 | Ensure that systems that result in LLM calls have appropriate API rate limiting to avoid excessive calls to LLMs, which may result in unexpected and excessive LLM costs. | | ✓ | ✓ |
| 5.15 | Ensure that cost alerts are active within LLM provider configurations to be alerted when costs exceed expectations. | ✓ | ✓ | ✓ |
| 5.16 | Define baselines for normal LLM interactions and monitor and alert when abnormal LLM interactions are detected. | | | ✓ |
| 5.17 | Ensure any functionality that allows anonymous users to preview features is properly restricted to allow only the necessary features. | | ✓ | ✓ |

---

## V6. Agents and plugins

### Control objective

The autonomous nature of agent-based systems presents new risks and can increase the impact of attacks such as prompt injection. These controls aim to reduce the risk associated with autonomous LLM components to an acceptable level.

| # | Requirement | L1 | L2 | L3 |
| - | ----------- | -- | -- | -- |
| 6.1 | Ensure that agent based solutions only expose access to the agent tools and plugins required for the current task. When multiple agent supported tasks exist, it should not be possible for a given task to leverage tools or plugins used by another task. | ✓ | ✓ | ✓ |
| 6.2 | Ensure that custom plugins and agent tools follow existing SSDLC processes. | | ✓ | ✓ |
| 6.3 | Ensure third-party plugins and toolkits are properly vetted according to existing Third-party risk management processes. | | ✓ | ✓ |
| 6.4 | Ensure that the parameters for agent tools and plugins are validated prior to execution. Typical checks should include type checks at minimum, in addition to any more specific validation. | | ✓ | ✓ |
| 6.5 | Ensure that credentials for third-party services consumed by agent tools and plugins are securely handled according to section V2.10 “Service Authentication” of the OWASP ASVS. | | ✓ | ✓ |
| 6.6 | Ensure that agent and plugin frameworks contain hooks that allow the raw prompts and completions to be intercepted, enabling LLM guards to operate, and enabling proper monitoring, troubleshooting, and auditing. | | ✓ | ✓ |
| 6.7 | Ensure that custom built plugins consider the scope of the currently authenticated principal. Plugins should not be able to access more than what the current principal is authorized to access. | | ✓ | ✓ |
| 6.8 | Ensure that the host that executes agent tools and plugins is appropriately segregated from other internal components. Certain internal services might need to be queried, but firewall rules should enforce that unrelated services are not reachable. | | | ✓ |
| 6.9 | Ensure that the host that executes agent tools and plugins is appropriately restricted from making arbitrary egress network requests. Only traffic for required APIs and services should be allowed to help increase the difficulty of data exfiltration from autonomous agents. | | | ✓ |
| 6.10 | Ensure that API tokens for third-party services are scoped to the minimum required by the agent or plugin. For example, an agent designed to read messages from a specific Slack channel should not be able to read messages from other channels or post messages. | | ✓ | ✓ |
| 6.11 | Consider manual approval, sometimes referred to as “human in the loop,” for sensitive operations before autonomous agents can continue execution. | | | ✓ |
| 6.12 | Ensure that agents are executed in a sand-boxed ephemeral environment to reduce the risk of agent prompts which result in code execution due to software defects. | | | ✓ |

---

## V7. Dependency and component

### Control objective

Ensure that third-party components and dependencies are safely handled to reduce supply chain risk.

| # | Requirement | L1 | L2 | L3 |
| - | ----------- | -- | -- | -- |
| 7.1 | Utilize Software Composition Analysis (SCA) tools to identify and remediate known vulnerabilities within third-party components used in LLM-powered applications. | | ✓ | ✓ |
| 7.2 | Ensure that all third-party LLM components are acquired from a trusted source. | ✓ | ✓ | ✓ |
| 7.3 | Ensure a defined vulnerability and patch management process exists for third-party components. | | ✓ | ✓ |
| 7.4 | Ensure that a Software Bill of Materials (SBOM) exists cataloging third-party components, licenses, and versions. | | ✓ | ✓ |
| 7.5 | Where unsafe PyTorch models are required, ensure the model is scanned for potentially dangerous Python imports. | | ✓ | ✓ |
| 7.6 | When hosting LLM components within private package registries, ensure the setup is not susceptible to Dependency Confusion attacks. | | ✓ | ✓ |

---

## V8. Monitoring and anomaly detection

### Control objective

Continuously monitor the use of LLM-powered applications to detect anomalous behavior or outputs that could indicate security incidents or system misuse.

| # | Requirement | L1 | L2 | L3 |
| - | ----------- | -- | -- | -- |
| 8.1 | Continuously monitor the usage patterns of LLM applications for anomalies that could indicate security incidents, such as unexpected spikes in usage or deviations from typical output patterns. | | ✓ | ✓ |
| 8.2 | Establish logging and alerting mechanisms for events that could suggest prompt leaks, such as the appearance of canary tokens (see 5.7) in logs or unexpected language patterns. | | ✓ | ✓ |

---

## Appendix A: Glossary

- **Large Language Model (LLM)** — A type of artificial intelligence model designed to understand, generate, and interact with human language, based on vast amounts of text data. LLMs can perform a variety of language tasks like translation, summarization, and question answering.

- **Prompt Injection** — A technique where an attacker intentionally crafts inputs (or “prompts”) to manipulate or exploit the behavior of an LLM. This can involve inserting misleading, biased, or malicious information in a prompt to influence the model’s output.

- **LLM Agent** — A software entity or bot that utilizes a Large Language Model to perform tasks, answer queries, or interact in conversations, often designed to automate certain functions or provide user assistance.

- **Model Poisoning** — A malicious attempt to influence or corrupt a machine learning model’s training data, causing it to learn incorrect, biased, or harmful behaviors.

- **Natural Language Processing (NLP)** — The field of computer science and artificial intelligence focused on enabling computers to understand, interpret, and generate human language.

- **Transformer Architecture** — A neural network architecture used in many modern LLMs. It is known for its ability to handle sequential data and its effectiveness in tasks involving natural language.

- **Tokenization** — The process of converting text into smaller units (tokens), such as words, characters, or subwords, which can be used as input for language models.

- **Fine-Tuning** — The process of taking a pre-trained model and further training it on a specific dataset to specialize it for particular tasks or domains.

- **Data Privacy** — Concerns related to the handling, processing, and storage of sensitive or personal information by language models, especially when dealing with user inputs.

- **Bias in AI** — The phenomenon where AI models, including LLMs, exhibit biased behavior, often as a result of biased training data or algorithms.

- **Adversarial Attack** — A strategy where attackers create inputs to deceive AI models into making errors. This is particularly concerning in security-sensitive applications of LLMs.

- **Principle of Least Privilege** — A security concept that involves granting users or systems the minimal level of access or permissions necessary to perform their tasks. This principle helps minimize potential damage from accidents or malicious attacks by limiting access rights for users to the bare minimum necessary to complete their duties.
