---
title: LDS General Article Template
version: 0.2
status: Draft
last_updated: 2026-08-05
owner: Lodestone Design System
---

# LDS General Article Template

## 1. 目的

Lodestone日記の内容を置き換えるだけで、
見出し、本文、結論、補足、参考資料の区別を維持できる汎用テンプレートである。

文字色や文字サイズの知識がなくても使えること、
装飾より文章構造と読みやすさを優先することを目的とする。

本テンプレートは現在 `Draft` である。
初版の適用範囲は背景黒のWindows PC版Lodestoneとする。
背景黒のlocal previewと視覚レビューは完了しているが、
保存後表示とFull HD / 4Kでの最終確認は完了していない。

## 2. 設計方針

- 記事のtitleはLodestoneのtitle fieldへ入力し、本文で重複させない。
- 本文はLodestoneの既定文字サイズと既定文字色を使用する。
- 4色版は既定本文色、Section Heading、Conclusion、Noteで構成する。
- 5色版では、意味が明確な `重要：` だけを追加する。
- 色だけで役割を示さず、文字サイズ、太字、label、空行を併用する。
- Noteを10pxへ縮小せず、本文と同じ既定サイズを使用する。
- 見出しと段落の間、段落同士の間には空行を1行置く。
- 本文は左寄せを維持し、初版では中央寄せや装飾罫線を使用しない。
- link textにはURLだけでなく、遷移先を説明する名称を使う。

## 3. Component

| Component | Lodestone表現 | 役割 |
|---|---|---|
| Article Title | title field | 記事の主題を示す |
| Lead | 既定size・既定color | 誰に何を伝える記事かを示す |
| Section Heading | 18px・太字・Heading color | 大きな話題の境界を示す |
| Subsection Heading | 既定size・太字 | Section内の小区画を示す |
| Body | 既定size・既定color | 説明、根拠、経緯を記述する |
| Important | 5色版のみ。太字・`重要：`・Important color | 読む前に必要な要点を示す |
| Conclusion | 太字・`結論：`・Conclusion color | 記事の着地点を示す |
| Note | `補足：`・Note color | 本筋を妨げず補助情報を示す |
| Source | `参考資料：`・説明的link text | 出典または関連情報を示す |

## 4. Active color profile

初版では背景黒profileだけをActiveとする。

| Profile | Role | Color | Measured background | Calculated contrast |
|---|---|---:|---:|---:|
| Black | Section Heading | `#73CFE0` | `#262626` | 8.45:1 |
| Black | Important | `#8FD18B` | `#262626` | 8.40:1 |
| Black | Conclusion | `#E2B477` | `#262626` | 7.95:1 |
| Black | Note | `#999999` | `#262626` | 5.31:1 |

contrastは候補選定のscreening値であり、
Lodestone記事全体のWCAG適合を示すものではない。
上記色は未保存local previewでの展開と視覚レビューを完了している。
保存後表示と再編集時保持は未検証である。

背景黒用の色を背景白へ流用してはならない。

## 5. 背景黒・4色template

Lodestoneのbase colorで「黒」を選択して使用する。

```bbcode
{この記事で扱う内容と、想定する読者を1～2段落で記述する。}

[size=18][b][color=#73CFE0]{Section Heading}[/color][/b][/size]

{本文を記述する。話題が変わる場合は段落間に空行を1行置く。}

[b]{Subsection Heading}[/b]

{補足する本文を記述する。}

[b][color=#E2B477]結論：{記事の着地点を短く記述する。}[/color][/b]

[color=#999999]補足：{本筋と分離した補助情報を記述する。}[/color]

参考資料：
[url={URL}]{遷移先を説明する資料名}[/url]
```

## 6. 背景黒・5色template

`重要：` を独立して示す必要がある記事で使用する。

```bbcode
{この記事で扱う内容と、想定する読者を1～2段落で記述する。}

[size=18][b][color=#73CFE0]{Section Heading}[/color][/b][/size]

{本文を記述する。話題が変わる場合は段落間に空行を1行置く。}

[b][color=#8FD18B]重要：{記事を読む前に必要な要点を短く記述する。}[/color][/b]

[b]{Subsection Heading}[/b]

{補足する本文を記述する。}

[b][color=#E2B477]結論：{記事の着地点を短く記述する。}[/color][/b]

[color=#999999]補足：{本筋と分離した補助情報を記述する。}[/color]

参考資料：
[url={URL}]{遷移先を説明する資料名}[/url]
```

## 7. 背景白profileの状態

背景白profileは `Parked` とする。

contrast計算だけでなく複数の高彩度色、文字サイズ、太字、部分color labelを比較したが、
ImportantとNoteで背景黒と同等の視認性を確保できなかった。
主要な記事著者が背景黒を使用するため、背景白の完成を初版の公開条件にしない。

次のいずれかが生じた場合に再開する。

- 背景白で記事を作成する具体的な予定が生じる。
- 利用者から背景白profileへの需要が確認される。
- 文字色以外を含む、Lodestoneで実装可能な有効な設計案が見つかる。

## 8. 使用方法

1. Lodestoneのbase colorで「黒」を選択する。
2. `重要：` が不要なら4色版、必要なら5色版を選ぶ。
3. code block内をLodestoneのリッチ編集モード本文へコピーする。
4. `{...}` のplaceholderを記事内容へ置き換える。
5. 不要なComponentを削除する。
6. Sectionが複数ある場合は、Section Headingと本文の組を複製する。
7. previewで見出し、本文、重要、結論、補足、linkを確認する。
8. 記事内容と視覚階層が一致していることを確認してから保存する。

## 9. 適用範囲と制約

- 背景黒のWindows PC版Lodestoneを初期対象とする。
- 背景白profileはParkedであり、初版の適用範囲に含めない。
- スマートフォン版はParkedであり、初版の適用範囲に含めない。
- 動画、画像、DB埋め込み、複雑な比較、FAQ、折り畳みは初版に含めない。
- 候補色の保存後表示とFull HD / 4K確認は今後実施する。
- 記事目的に合わないComponentは無理に使用しない。
- 色を変更する場合も、文字サイズ、太字、labelによる識別を残す。

## 10. Design references

- [LDS Design Principles](../docs/02_LDS_Design_Principles.md)
- [LDS Editorial Methodology](../docs/03_LDS_Editorial_Methodology.md)
- [LDS Lodestone Authoring Reference](../docs/04_LDS_Lodestone_Authoring_Reference.md)
- [WCAG 2.2 Understanding: Contrast (Minimum)](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum)
- [WCAG 2.2 Understanding: Use of Color](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color)
- [WCAG 2.2 Understanding: Headings and Labels](https://www.w3.org/WAI/WCAG22/Understanding/headings-and-labels)
- [Requirements for Japanese Text Layout](https://www.w3.org/TR/jlreq/?lang=en)

## 11. Revision History

| Version | Date | Changes |
|---|---|---|
| 0.1 | 2026-08-04 | Created the first research-grounded general article template with shared structure and provisional black/white color profiles. |
| 0.2 | 2026-08-05 | Limited the active first release to the black background, added four- and five-color variants, and parked the white profile with explicit restart conditions. |
