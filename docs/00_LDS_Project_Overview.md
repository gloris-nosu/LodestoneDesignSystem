---
title: LDS Project Overview
document_id: LDS-00
version: 0.5
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

## 3. 基本方針

LDSは次の原則を採用する。

- 本文の論旨、価値判断、結論は著者が決定する
- 編集支援は原則として著者ではなく編集者として機能する
- 色は重要度だけでなく情報の役割を示す
- 見た目より先に論理構造を整理する
- 同じ意味には同じ視覚表現を使う
- 強調は限定的に使う
- 流し読みと精読の両方に対応する
- 技術仕様とデザイン上の推奨を分離する
- 実際のLodestone表示を最終判断とする
- 検証結果とCase StudyをLDS本体へ循環させる

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
| LDS-00 | `00_LDS_Project_Overview.md` | プロジェクトの入口、目的、全体構成 |
| LDS-01 | `01_LDS_Governance.md` | 正本、命名、状態、変更、文書ライフサイクル |
| LDS-02 | `02_LDS_Design_Principles.md` | 設計判断の価値基準と優先順位 |
| LDS-03 | `03_LDS_Editorial_Methodology.md` | 記事へLDSを適用する編集手順 |
| LDS-04 | `04_LDS_Lodestone_Authoring_Reference.md` | Lodestoneの技術仕様、記法、制約、検証状態 |

### 5.1 文書間の関係

```text
Project Overview
↓
Governance
↓
Design Principles
↓
Editorial Methodology
↓
Lodestone Authoring Reference
```

実際の作業では、Design PrinciplesとEditorial Methodologyが
Authoring Referenceに記録された技術的制約を参照する。

---

## 6. 著者と編集者の役割

編集者が担当する領域：

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
- 文書間の整合性確認
- Case Study整理
- 実画面を前提とした改善提案

著者が決定する領域：

- 著者の主張
- 価値判断
- 結論
- 批判の方向性
- 未検証仕様の確定
- 文書のStable昇格

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

詳細な手順は `03_LDS_Editorial_Methodology.md` を参照する。

---

## 8. 品質評価

LDSの記事設計は次の順序で評価する。

1. 内容が正確である
2. 論理を追跡できる
3. 誤読しにくい
4. 長文でも読み続けられる
5. 情報の役割を視覚的に判別できる
6. 表現が一貫している
7. PC／スマートフォン差に耐えられる
8. 再利用できる
9. 美観が保たれている

美観は重要だが、意味や読みやすさより優先しない。

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

## 10. 正本と運用

LDSの内容上の正本は、Gitリポジトリ内のMarkdownファイルとする。

GitHubはcommit履歴、差分、共有状態の正本として使用する。
Google Drive上のコピーは正本として扱わない。

文書の命名、状態、バージョン、変更履歴、廃止方法については
`01_LDS_Governance.md` を参照する。

LDSは固定された完成品ではない。

```text
Specification
↓
Design
↓
Application
↓
Visual Verification
↓
Case Study
↓
Revision
```

この循環により継続的に改善する。

---

## 11. Revision History

| Version | Date | Changes |
|---|---|---|
| 0.1 | 2026-07-19 | Initial LDS overview and basic philosophy. |
| 0.2 | 2026-07-19 | Rebuilt as the project entry document. Added canonical document architecture, scope, workflow, quality criteria, editor responsibilities, and project phase. |
| 0.3 | 2026-07-19 | Updated the source-of-truth model from Google Drive to repository Markdown with GitHub-managed history and diffs. |
| 0.4 | 2026-07-19 | Updated the current phase after restructuring Editorial Methodology around staged authoring and revision. |
| 0.5 | 2026-07-19 | Generalized author and editor responsibilities and removed internal work-state tracking from the public overview. |
