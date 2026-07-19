---
title: LDS Project Overview
document_id: LDS-00
version: 0.6
status: Draft
last_updated: 2026-07-19
owner: Lodestone Design System
---

# Lodestone Design System

## 1. プロジェクト概要

Lodestone Design System（LDS）は、FINAL FANTASY XIV Lodestoneの日記機能を対象とした、
編集・組版・情報デザインの体系である。

目的は記事を派手に装飾することではない。

**文章の論理構造、情報の役割、読者の視線、技術的制約を統合し、
長文でも内容を追いやすい記事を設計すること**を目的とする。

---

## 2. LDSが解決する問題

Lodestoneの日記には、一般的なWeb制作環境とは異なる制約がある。

- 任意のCSSを使用できない
- 利用できる編集機能や専用コードが限定される
- PC版とスマートフォン版で挙動が異なる場合がある
- 黒背景を前提に色とコントラストを設計する必要がある
- 長文では論点、根拠、分析、結論の位置を見失いやすい
- 技術的に可能な表現と、読みやすい表現が一致するとは限らない

LDSは、これらの制約を前提として再利用可能な判断基準と編集手順を提供する。

---

## 3. 基本的な考え方

LDSは、意味と読みやすさを装飾より優先する。

概要として、次の考え方を採用する。

- 見た目より先に論理構造を整理する
- 情報の役割を一貫した視覚表現で示す
- 流し読みと精読の両方に対応する
- 技術的に可能なことと、LDSが推奨することを分離する
- 実際のLodestone表示とCase Studyから継続的に改善する

設計判断の価値基準と優先順位は、
[`02_LDS_Design_Principles.md`](02_LDS_Design_Principles.md)を正本とする。

---

## 4. 設計対象

LDSが扱う主な領域：

- 論理構造
- 情報分類
- 段落
- 見出し階層
- Typography
- Color
- Emphasis
- Spacing
- Lists
- Disclosure / Folding
- Images
- Links
- BBCode
- 読者の視線誘導
- PC／スマートフォン差
- 記事テンプレート
- Case Study
- 実機検証

---

## 5. 基幹文書

LDSの基幹文書は次の5つで構成する。

| ID | File | Role |
|---|---|---|
| LDS-00 | [`00_LDS_Project_Overview.md`](00_LDS_Project_Overview.md) | プロジェクトの入口、目的、全体構成 |
| LDS-01 | [`01_LDS_Governance.md`](01_LDS_Governance.md) | 正本、命名、状態、変更、文書ライフサイクル |
| LDS-02 | [`02_LDS_Design_Principles.md`](02_LDS_Design_Principles.md) | 設計判断の価値基準と優先順位 |
| LDS-03 | [`03_LDS_Editorial_Methodology.md`](03_LDS_Editorial_Methodology.md) | 記事へLDSを適用する編集手順 |
| LDS-04 | [`04_LDS_Lodestone_Authoring_Reference.md`](04_LDS_Lodestone_Authoring_Reference.md) | Lodestoneの技術仕様、記法、制約、検証状態 |

### 5.1 文書間の関係

基幹文書の番号は入口から詳細へ進む基本的な参照順を示す。
一方、実際の責務と依存関係は単純な直列ではない。

```text
Project Overview     ── プロジェクトの入口
Governance           ── すべての管理対象成果物に適用
Design Principles    ── 設計判断の価値基準
Authoring Reference  ── 技術的事実と制約

Design Principles + Authoring Reference
                    ↓
Editorial Methodology
                    ↓
Article Application → Visual Verification → Case Study → System Revision
```

文書管理はGovernance、設計判断はDesign Principles、
技術的事実はAuthoring Reference、具体的な編集手順はEditorial Methodologyを正本とする。

---

## 6. 記事制作とLDS管理の役割

同じ人物が複数の役割を兼ねることはできるが、判断権限は役割ごとに区別する。

### 6.1 記事著者

記事著者が決定する領域：

- 記事の主張
- 価値判断
- 結論
- 批判の方向性
- 著者固有の文体と声

### 6.2 編集者・編集支援

編集者・編集支援が担当する領域：

- 論理構造の解析
- 情報の分類
- 段落整理
- 見出し設計
- 強調候補の選定
- 配色
- 余白
- 折り畳み候補の抽出
- BBCode変換
- 用語統一
- 実画面を前提とした改善提案

編集者・編集支援は、記事著者の主張、価値判断、結論を無断で変更しない。

### 6.3 LDS maintainer

LDS maintainerは、LDS文書体系を管理する役割である。

- 基幹文書と管理対象成果物の整合性確認
- 技術仕様と設計ルールの採否判断
- 文書Statusの変更
- Case StudyからLDS本体へ反映する知見の承認
- 公開範囲と変更履歴の管理

詳細な権限と変更手続きは、
[`01_LDS_Governance.md`](01_LDS_Governance.md)を参照する。

---

## 7. 標準編集フロー

```text
原文
↓
論理構造の解析
↓
情報分類
↓
段落と見出し
↓
Typography
↓
Emphasis
↓
Color
↓
Disclosure / Folding
↓
BBCode
↓
Lodestone実画面確認
↓
Case Study
↓
LDS更新
```

詳細な手順は
[`03_LDS_Editorial_Methodology.md`](03_LDS_Editorial_Methodology.md)を参照する。

---

## 8. 品質評価

LDSでは、正確性、論理の追跡可能性、誤読の防止、可読性を美観より優先する。
記事設計の価値基準と標準設計レビューは
[`02_LDS_Design_Principles.md`](02_LDS_Design_Principles.md)、
記事へ適用する編集手順は
[`03_LDS_Editorial_Methodology.md`](03_LDS_Editorial_Methodology.md)を参照する。

実装後は、PC／スマートフォン差を含む実際のLodestone表示で確認する。

---

## 9. 記事ファミリー

将来的に、共通原則を維持しながら記事目的別のテンプレートを整備する。

- LDS Essay
- LDS Guide
- LDS Proposal
- LDS Patch Notes
- LDS Diary
- LDS Review
- LDS Case Study

記事ファミリーは独立したデザインシステムではなく、
LDSの原則とコンポーネントを用途別に組み合わせたものとする。

---

## 10. 継続的改善

正本、命名、文書Status、バージョン、変更履歴、廃止方法は、
[`01_LDS_Governance.md`](01_LDS_Governance.md)が定める。

LDSは固定された完成品ではなく、記事への適用、実画面確認、Case Studyから得た証拠を
文書体系へ戻すことで継続的に改善する。
正式な改善サイクルと変更手続きはGovernanceを参照する。

---

## 11. Revision History

| Version | Date | Changes |
|---|---|---|
| 0.1 | 2026-07-19 | Initial LDS overview and basic philosophy. |
| 0.2 | 2026-07-19 | Rebuilt as the project entry document. Added canonical document architecture, scope, workflow, quality criteria, editor responsibilities, and project phase. |
| 0.3 | 2026-07-19 | Updated the source-of-truth model from Google Drive to repository Markdown with GitHub-managed history and diffs. |
| 0.4 | 2026-07-19 | Updated the current phase after restructuring Editorial Methodology around staged authoring and revision. |
| 0.5 | 2026-07-19 | Generalized author and editor responsibilities and removed internal work-state tracking from the public overview. |
| 0.6 | 2026-07-19 | Clarified document relationships, separated article and LDS governance roles, and delegated normative rules to Governance and Design Principles. |
