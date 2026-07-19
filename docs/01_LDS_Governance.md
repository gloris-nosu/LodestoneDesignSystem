---
title: LDS Governance
document_id: LDS-01
version: 0.7
status: Review
last_updated: 2026-07-20
owner: Lodestone Design System
---

# LDS Governance

## 1. 文書の目的

本書は、Lodestone Design System（LDS）を構成する文書・検証記録・テンプレート・事例研究を、
一貫した規則で作成、更新、参照、廃止するための管理方針を定める。

LDSの技術仕様は
[`04_LDS_Lodestone_Authoring_Reference.md`](04_LDS_Lodestone_Authoring_Reference.md)、
編集方法論は
[`03_LDS_Editorial_Methodology.md`](03_LDS_Editorial_Methodology.md)が扱う。

本書が扱うのは、次の問いである。

> LDSの正本はどこにあるか  
> 文書をどの名前で管理するか  
> 変更をどう記録するか  
> 何を確定仕様として扱うか  
> 実験結果をどの段階で本体へ反映するか

---

## 2. 適用範囲

### 2.1 管理対象成果物

本書は、LDSプロジェクト内の次の管理対象成果物に適用する。

- プロジェクト概要
- ガバナンス文書
- 編集方法論
- Lodestone技術リファレンス
- デザイン原則
- コンポーネント仕様
- 記事テンプレート
- 実機検証記録
- Case Study
- 参考記事評価
- 変更履歴
- 補助データ
- スクリーンショット

このうち、LDS-00からLDS-04までの5文書を基幹文書と呼ぶ。

### 2.2 対象外

- 公開済みLodestone日記そのもの
- 個々の記事の主張内容
- FINAL FANTASY XIV運営の公式仕様管理
- GitHubアカウント自体の管理規定

### 2.3 役割と権限

LDSでは、記事制作上の役割と文書管理上の役割を区別する。
同じ人物が複数の役割を兼ねる場合も、判断権限は役割ごとに扱う。

#### 記事著者

- 記事の主張、価値判断、結論、批判の方向性を決定する
- 記事著者固有の文体と声に関する最終判断を持つ
- LDS文書のStatusや技術仕様を、記事著者であることだけを根拠に確定しない

#### 編集者・編集支援

- 論理構造、情報分類、見出し、視覚表現、BBCode、可読性の改善を支援する
- 記事著者の主張、価値判断、結論を無断で変更しない
- LDSの未確認仕様や文書Statusを独自に確定しない

#### LDS maintainer

- 基幹文書と管理対象成果物の整合性を管理する
- 技術仕様と設計ルールの採否を判断する
- 文書Statusの変更とStable昇格を承認する
- Case Studyや検証結果を基幹文書または管理対象成果物へ反映するか判断する
- 公開範囲、ライセンス境界、変更履歴を管理する

LDS maintainerは、repository ownerまたはownerが明示的に権限を付与した者とする。

---

## 3. 正本

### 3.1 正本の所在

LDSの内容上の正本は、Gitリポジトリ内のMarkdownファイルとする。

既存ファイルを直接編集し、別形式のコピーを正本として並立させない。

### 3.2 GitとGitHub

ローカルGit作業フォルダーを編集環境として使用する。

GitHubは、次の情報を管理する正本とする。

- commit履歴
- 差分
- branchと共有状態
- push済みの版

リポジトリ外のコピー、一時ファイル、書き出しファイル、
他サービス上のコピーは正本として扱わない。

### 3.3 公開記事との関係

公開済みLodestone記事は、基幹文書または管理対象成果物の正本ではない。

公開記事は次のいずれかとして扱う。

- 適用例
- 検証対象
- Case Study
- 実画面上の証拠

---

## 4. 文書IDとファイル名

### 4.1 基本形式

LDSの基幹文書は、次の形式で命名する。

```text
NN_LDS_Document_Name.md
```

例：

```text
00_LDS_Project_Overview.md
01_LDS_Governance.md
02_LDS_Design_Principles.md
03_LDS_Editorial_Methodology.md
04_LDS_Lodestone_Authoring_Reference.md
```

### 4.2 番号

先頭番号は、表示順と論理階層を示す。

原則：

- `00`：プロジェクト概要
- `01`：ガバナンス
- `02`：設計原則
- `03`：編集方法論
- `04`：Lodestone技術リファレンス
- `05`以降：詳細仕様、コンポーネント、テンプレート、検証文書

番号は内容の依存関係を優先して決める。

### 4.3 文書ID

各基幹文書にはYAMLフロントマターで文書IDを付与する。

```yaml
document_id: LDS-01
```

規則：

- ファイル番号と文書IDを一致させる
- 文書IDは原則変更しない
- ファイル名変更後も文書IDを維持する
- 分割した場合は新しいIDを付与する
- 統合した場合も履歴に旧IDを記録する

### 4.4 ファイル名の安定性

ファイル名は、正本として参照されるURLやリンクの安定性を考慮し、
頻繁に変更しない。

変更が必要な例：

- 内容と名称が明確に不一致
- 番号体系の誤り
- 重大なスペルミス
- 文書の役割変更

単なる表現の好みでは変更しない。

---

## 5. 文書状態

各文書は、次の状態のいずれかを持つ。

| Status | 意味 |
|---|---|
| Draft | 作成・検討中 |
| Review | 内容確認中 |
| Stable | 現行の標準として利用可能 |
| Experimental | 検証目的の暫定仕様 |
| Deprecated | 新規利用を推奨しない |
| Archived | 履歴保存のみ |
| Superseded | 別文書に置き換え済み |

### 5.1 Draft

- 未確定の内容を含む
- 構成変更があり得る
- 他文書から参照する場合は暫定であることを示す

### 5.2 Review

- 初稿が完成している
- 内容、整合性、証拠、用語を確認する段階
- 大幅な追加より、修正と確認を優先する

### 5.3 Stable

- LDSの現行標準として使用できる
- 主要な未検証事項が明示されている
- 他文書との重大な矛盾がない
- 変更履歴が記録されている

Stableへの昇格は、関連文書との整合性と根拠を確認した上で、LDS maintainerが承認する。

### 5.4 Experimental

- 実験的なコンポーネントや手法
- 本番記事で使う場合は検証前提
- 成功しても自動的にStableへ昇格しない

### 5.5 Deprecated

- 過去には有効だった
- 現在は新規利用を推奨しない
- 代替先を記載する

### 5.6 Archived / Superseded

- `Archived`：歴史的記録として保存
- `Superseded`：後継文書が存在する

削除ではなく、原則として履歴を残す。

---

## 6. バージョン管理

### 6.1 バージョン形式

文書バージョンは次の形式とする。

```text
MAJOR.MINOR
```

例：

```text
0.1
0.2
1.0
1.1
```

### 6.2 0.x

`0.x` は設計中・運用確立前を示す。

- 構成変更が可能
- 用語変更が可能
- 文書分割・統合が可能

### 6.3 1.0

次を満たした文書は `1.0` 候補とする。

- 目的と適用範囲が明確
- 用語が整理済み
- 主要規則が確定
- 実運用で検証済み
- 重大な未解決事項が明示済み
- 関連文書との整合性確認済み

### 6.4 MAJOR更新

次の場合はMAJORを上げる。

- 文書の責務が大きく変わる
- 既存ルールとの互換性が失われる
- 大規模な構成変更
- 用語体系の全面変更
- 適用方法が変わる

### 6.5 MINOR更新

次の場合はMINORを上げる。

- 新しい節を追加
- 新しいルールを追加
- 検証結果を反映
- 既存規則を明確化
- 例や表を追加
- 軽微な構成整理

誤字修正のみの場合は、
必要に応じてバージョンを維持してよい。

---

## 7. 更新履歴

各基幹文書の末尾に、Revision Historyを置く。

推奨形式：

```markdown
## Revision History

| Version | Date | Changes |
|---|---|---|
| 0.1 | 2026-07-19 | Initial draft. |
```

変更履歴には、単なる「更新」ではなく、
何を変更したかを記載する。

良い例：

```text
Added Evidence definitions and verification workflow.
```

悪い例：

```text
Updated document.
```

---

## 8. 変更の分類

変更は次のいずれかに分類する。

### 8.1 Editorial Change

- 誤字修正
- 表現の明確化
- 見出し調整
- 重複除去
- 内容の意味を変えない整理

### 8.2 Specification Change

- 新規ルール
- 既存ルール変更
- 技術仕様の更新
- 状態区分の変更
- 推奨手法の変更

### 8.3 Evidence Change

- 実機検証結果
- 公式情報の追加
- 参考記事の追加
- Evidence区分またはVerification noteの変更

### 8.4 Structural Change

- 文書分割
- 文書統合
- ファイル名変更
- 文書ID追加
- 章構成の大幅変更

---

## 9. 証拠と確定ルール

### 9.1 証拠区分

Lodestone技術仕様と設計検証には、次のEvidence区分を使用する。
文書ライフサイクルの `Status` と区別するため、技術情報には `Evidence` と記載する。

| Evidence | 意味 |
|---|---|
| Official | スクウェア・エニックスの公式情報が対象の事実を直接裏付けている |
| Verified | LDSが実機で再現し、確認日と確認環境を記録している |
| Observed | 公開中のLodestone記事または表示結果で観測したが、再現条件を確定していない |
| Community | ユーザー記事などの二次情報だけで確認している |
| Provisional | 複数情報から妥当と推定するが、直接確認していない |
| Unknown | 判断に十分な証拠がない、または現在の仕様が不明である |

古さ、適用範囲、再検証の必要性、廃止情報はEvidenceへ混在させず、
Verification noteとして記録する。

同じ機能でも、機能の存在、正確な構文、表示挙動でEvidenceが異なる場合は、
項目を分けて記録する。

[`04_LDS_Lodestone_Authoring_Reference.md`](04_LDS_Lodestone_Authoring_Reference.md) は、
この区分をLodestoneの技術情報へ適用する。

### 9.2 方法論への採用条件

LDSの標準ルールとして採用する場合は、
原則として次のいずれかを満たす。

- 公式仕様である
- LDS実機検証で再現できる
- 複数のCase Studyで有効性が確認できる
- 明確な目的と制約が説明できる

単一の参考記事で使われているだけでは、
LDS標準へ自動採用しない。

### 9.3 観測と推奨の分離

次を区別する。

- Lodestoneで可能である
- LDSで推奨する
- 特定記事で有効だった
- 実験中である

技術的に可能でも、LDSで推奨しない場合がある。

---

## 10. 変更ワークフロー

### 10.1 標準フロー

```text
Issue / Observation
↓
Draft Change
↓
Evidence Check
↓
Cross-document Review
↓
Practical Test
↓
Revision History Update
↓
Status Decision
↓
Git差分確認
↓
Commit / Push
```

### 10.2 Issue / Observation

変更の起点：

- 実画面で問題を発見
- 新しいLodestone仕様を確認
- 既存文書間に矛盾
- Case Studyから知見を抽出
- 新しい表現手法を発見
- ユーザーが改善案を提示

### 10.3 Evidence Check

確認する事項：

- 公式情報か
- 実機確認済みか
- 単一記事だけの観測か
- 古い情報ではないか
- PC／スマートフォン差があるか
- 再現条件が明確か

### 10.4 Cross-document Review

最低限、次の整合性を確認する。

- [Project Overview](00_LDS_Project_Overview.md)
- [Governance](01_LDS_Governance.md)
- [Design Principles](02_LDS_Design_Principles.md)
- [Editorial Methodology](03_LDS_Editorial_Methodology.md)
- [Lodestone Authoring Reference](04_LDS_Lodestone_Authoring_Reference.md)
- 関連コンポーネント仕様
- 関連Case Study

### 10.5 Practical Test

デザインルールは、可能であればLodestone下書きまたは公開記事で確認する。

確認例：

- 読みやすさ
- 色
- 折り返し
- 空行
- スマートフォン表示
- タグの動作
- 見出し階層
- 折り畳み

### 10.6 Git差分と履歴

変更を履歴へ反映する前に次を行う。

- ファイル名を確認
- YAMLメタデータ更新
- バージョン更新
- `last_updated` 更新
- Revision History更新
- 関連文書の参照先確認
- Git差分とcommit対象の確認

commitとpushは、必要な確認が完了した後に行う。
文書Statusの変更とStable昇格を含む場合は、LDS maintainerの承認を記録する。

---

## 11. 文書間の責務

### 11.1 Project Overview

```text
00_LDS_Project_Overview.md
```

扱う内容：

- LDSの目的
- 全体像
- 基本理念
- 主要成果物
- プロジェクトの入口

詳細ルールは持たせない。

### 11.2 Governance

```text
01_LDS_Governance.md
```

扱う内容：

- 正本
- 命名
- 状態
- バージョン
- 変更
- 証拠管理
- 文書ライフサイクル
- 役割と権限
- ライセンスと公開境界

### 11.3 Design Principles

```text
02_LDS_Design_Principles.md
```

扱う内容：

- 設計判断の価値基準
- 品質評価の優先順位
- 情報デザインの原則
- 複数の設計案から選ぶための判断基準

具体的な編集手順やLodestoneの技術仕様は持たせない。

### 11.4 Editorial Methodology

```text
03_LDS_Editorial_Methodology.md
```

扱う内容：

- 編集手順
- 情報分類
- 視線設計
- Typography
- Color
- Spacing
- Folding
- 品質評価の実施手順

### 11.5 Lodestone Authoring Reference

```text
04_LDS_Lodestone_Authoring_Reference.md
```

扱う内容：

- Lodestoneで可能なこと
- タグ
- UI機能
- 制約
- 実機検証
- 技術的事実

「何を推奨するか」ではなく、
「何ができるか」を主に扱う。

---

## 12. Case Study

### 12.1 目的

Case Studyは、
LDSルールを実際の記事へ適用した記録である。

単なる完成記事の保存ではなく、
判断と結果を残す。

### 12.2 必須項目

- Case Study ID
- 対象記事
- 日付
- 適用前の問題
- 採用したLDSルール
- 実装内容
- 実画面結果
- 問題点
- 修正履歴
- 基幹文書または管理対象成果物へ反映する知見
- 証拠画像

### 12.3 昇格条件

Case Studyの知見を基幹文書または管理対象成果物へ反映する場合は、
次を確認する。

- 他の記事でも再利用できるか
- 特定テーマに依存しすぎていないか
- 読みやすさが実際に改善したか
- 既存ルールと矛盾しないか
- 技術的に安定しているか

---

## 13. 実験的コンポーネント

新しいコンポーネントは、
最初からStableとして扱わない。

推奨フロー：

```text
Idea
↓
Experimental Spec
↓
Test Article
↓
Case Study
↓
Review
↓
Stable または Rejected
```

Rejectedになった場合も、
理由を記録する。

例：

- 色が強すぎた
- スマートフォンで崩れた
- 文章構造を誤認させた
- タグが不安定だった
- 再利用性がなかった

---

## 14. 廃止と置換

### 14.1 廃止条件

- Lodestone仕様変更
- より良い手法への置換
- アクセシビリティ上の問題
- 読者テストで悪影響
- 文書間の重複
- 実装不可能

### 14.2 廃止時の記録

Deprecated文書またはルールには、次を記載する。

- 廃止理由
- 廃止日
- 代替先
- 影響範囲
- 過去記事への扱い

### 14.3 削除

原則として即時削除しない。

削除候補：

- 完全な重複
- 誤って作成された空ファイル
- 機密情報
- 法的・安全上の問題
- 正本でない一時ファイル

---

## 15. 編集支援と自動化

### 15.1 基本原則

編集支援ツールや自動化は、LDS文書に対して次を行える。

- 構成整理
- 重複検出
- 用語統一
- 矛盾確認
- 草稿作成
- 差分提案
- Revision History作成
- Case Study整理
- 技術仕様と方法論の分離

### 15.2 禁止事項

編集支援ツールや自動化は、根拠なく次を行わない。

- 未確認仕様を確定扱い
- 記事著者の意図を変更
- 参考記事を公式仕様扱い
- 文書状態をStableへ自動昇格
- 証拠なしの最適値断定
- 既存ルールを黙って変更

### 15.3 直接更新

編集支援ツールや自動化がMarkdownを直接更新する場合は、
変更対象と目的を明確にする。

ユーザーの未commit変更を保全し、
無関係な差分を変更しない。

大規模変更では、
更新前に草稿または差分を確認する。

軽微な修正では、
直接更新後に変更内容を報告してよい。

---

## 16. セキュリティと共有

### 16.1 リポジトリアクセス

GitHubリポジトリの公開範囲と書き込み権限は、
所有者が必要性を確認して設定する。

- collaboratorは必要最小限とする
- 不特定多数へ書き込み権限を与えない
- 公開範囲を変更する場合は、機密情報が含まれないことを確認する
- 自動化されたcommitやpushには、所有者の明示的な承認を必要とする

### 16.2 機密情報

LDS文書に次を含めない。

- アカウント認証情報
- 非公開個人情報
- APIキー
- セッショントークン
- 非公開メールアドレス
- 無許可の第三者情報

### 16.3 ライセンスと第三者権利

特記がない限り、公開リポジトリでLodestone Design System contributorsが作成した文書には、
Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International
（CC BY-NC-SA 4.0）を適用する。

利用者は、ライセンス条件に従って非営利目的で文書を共有・改変できる。
改変物を共有する場合は、Lodestone Design Systemを表示し、変更の有無を示し、
同一または互換ライセンスを適用する。

次の素材は、LDSのライセンス対象に含めない。

- FINAL FANTASY XIVの名称、商標、ロゴ
- ゲーム内または公式サイトのスクリーンショット、画像、文章、データ
- Square Enixまたはその他の第三者が権利を持つ素材

第三者素材を公開成果物へ追加する場合は、公開前に利用条件を確認し、
必要な権利表記と出典を付け、LDS独自文書とのライセンス境界を明示する。
FINAL FANTASY XIV素材には、その時点で最新の
[公式著作物利用条件](https://support.jp.square-enix.com/rule.php?id=5381&la=0&tag=authc)を適用する。

将来、プログラムコードを追加する場合は、文書ライセンスを自動適用せず、
コードに適したライセンスと適用範囲を別途決定する。

---

## 17. 品質確認チェックリスト

文書更新前に確認する。

- [ ] 文書の目的と責務に合っている
- [ ] ファイル名と文書IDが一致している
- [ ] YAMLメタデータが更新されている
- [ ] Statusが妥当
- [ ] Versionが妥当
- [ ] `last_updated` が更新されている
- [ ] Revision Historyがある
- [ ] 技術的事実と推奨が分離されている
- [ ] Evidence区分が適切
- [ ] 他文書と矛盾していない
- [ ] 重複が過剰でない
- [ ] 用語が統一されている
- [ ] 未検証事項が明示されている
- [ ] ライセンスと第三者権利の境界が明示されている
- [ ] Git差分とcommit対象を確認している

---

## 18. 運用方針

LDSは、次の循環で成熟させる。

```text
Design Principles + Authoring Reference
                  ↓
Editorial Methodology
                  ↓
Component Design
                  ↓
Article Application
                  ↓
Visual Verification
                  ↓
Case Study
                  ↓
Evidence Review → System Revision
```

Governanceはこの循環の一段階ではなく、すべての段階へ適用する管理規則である。

LDSは固定された完成品ではなく、
実際の記事作成と検証を通じて更新される設計システムである。

---

## 19. Revision History

| Version | Date | Changes |
|---|---|---|
| 0.1 | 2026-07-19 | Initial governance draft. Defined source of truth, naming, status, versioning, evidence, change workflow, Case Study lifecycle, assisted editing, and security policy. |
| 0.2 | 2026-07-19 | Replaced the former Google Drive source-of-truth model with repository Markdown and Git/GitHub history management. Updated workflow, assisted editing, access, and quality checks accordingly. |
| 0.3 | 2026-07-19 | Generalized tool-specific editing rules and removed internal work planning from the public governance document. |
| 0.4 | 2026-07-19 | Established CC BY-NC-SA 4.0 for original LDS documentation and defined the boundary for Square Enix and other third-party materials. |
| 0.5 | 2026-07-19 | Defined article and maintainer roles, standardized document terminology, restored Design Principles to the responsibility model, and separated governance from the improvement cycle. |
| 0.6 | 2026-07-19 | Established Governance as the canonical owner of Evidence categories, separated technical Evidence from document Status, and required verification notes and aspect-specific evidence. |
| 0.7 | 2026-07-20 | Standardized role and managed-artifact terminology, completed the cross-document consistency review, and advanced the document to Review. |
