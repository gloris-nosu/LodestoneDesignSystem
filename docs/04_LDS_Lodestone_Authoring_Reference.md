---
title: LDS Lodestone Authoring Reference
document_id: LDS-04
version: 0.5
status: Review
last_updated: 2026-07-20
owner: Lodestone Design System
---

# LDS Lodestone Authoring Reference

## 1. 文書の目的

この文書は、FINAL FANTASY XIV Lodestoneの日記機能における、
記述方法・編集機能・表示機能・専用コード・既知の制約を整理する技術リファレンスである。

LDSのデザイン原則や編集方法論ではなく、

> ロドストで何ができるか  
> どの記法が使えるか  
> 何が未検証か

を管理する。

---

## 2. 適用範囲

本書の主対象は次の通り。

- Lodestoneの日記
- リッチ編集モード
- 日記本文内の文字装飾
- 画像・動画挿入
- 非表示／展開表示
- エオルゼアデータベース埋め込みコード
- 日記の公開・検索関連機能
- PC版／スマートフォン版の差異
- LDSによる実機検証結果

技術情報のEvidence区分は
[`01_LDS_Governance.md`](01_LDS_Governance.md) に従う。
編集上の推奨、代替表現、適用手順は
[`03_LDS_Editorial_Methodology.md`](03_LDS_Editorial_Methodology.md) が扱う。

次は本書の主対象外とする。

- 一般的な文章作法
- LDSの配色・組版ルール
- 記事ジャンル別テンプレート
- LDS文書のリポジトリ管理規約
- FINAL FANTASY XIVゲーム内チャットの記法
- Lodestone以外のBBCode実装

---

## 3. Evidenceの記録

各技術情報には、
[`01_LDS_Governance.md`](01_LDS_Governance.md) が定めるEvidence区分を付与する。

文書ライフサイクルの `Status` と区別するため、
本書では技術情報の根拠を `Evidence` と表記する。

### 3.1 記録原則

- 機能の存在と正確な構文を、根拠なく同じEvidenceで扱わない。
- 表示挙動のEvidenceが異なる場合は、機能や構文と分けて記録する。
- `Feature evidence`、`Syntax evidence`、`Behavior evidence` など、対象を示すラベルを使用する。
- 古さ、適用範囲、再検証の必要性は `Verification note` として記録する。
- `Official` は公式ページが対象の事実を直接裏付ける場合に限定する。
- `Verified` は確認日と確認環境を記録する。
- `Community` だけを根拠に仕様を断定しない。
- 未検証事項は推測で埋めず、`Unknown` として残す。

---

## 4. 日記編集モード

### 4.1 通常編集モード

**Evidence:** Unknown

通常編集モードの現在の機能範囲については、
LDSとしてまだ体系的に実機確認していない。

確認対象：

- 使用可能な文字装飾
- 画像添付
- 本文内画像挿入
- 埋め込みコード
- リッチ編集モードへの変更可否
- PC版とスマートフォン版の差異

### 4.2 リッチ編集モード

**Feature evidence:** Official

Lodestoneには、文字装飾、リンク、非表示、画像挿入、動画挿入などを利用できる
リッチ編集モードが存在する。

公式の2015年1月20日更新情報では、
新規日記作成時にリッチ編集モードを選択する仕様として案内されている。

同じ公式情報では、次の機能が列挙されている。

- 文字サイズ極大
- 文字サイズ大
- 文字サイズ中
- 文字サイズ小
- 太字
- 斜体
- 下線
- 取消線
- 文字色
- リンク
- 隠す
- 画像挿入
- 動画挿入

### 4.3 スマートフォン版

**Feature evidence:** Official

**Verification note:** 2015年時点の情報であり、現在の挙動は再検証が必要。

リッチ編集モード追加時の公式案内では、
スマートフォン版Lodestoneではリッチ編集モードを利用できないとされている。

ただし、この情報は2015年時点のものである。
2026年現在のスマートフォン表示・PC版表示切替を含めた挙動は、
LDSで改めて検証する必要がある。

### 4.4 編集モードの後変更

**Feature evidence:** Community

**Verification note:** 現在の公式仕様と実機挙動は未確認。

ユーザー記事には、
新規作成時にリッチ編集モードを選択し、
後から切り替えられない旨の報告がある。

現在の公式仕様としては未確認。

検証項目：

- 通常編集で保存した下書きをリッチ編集へ変更できるか
- 公開済み日記をリッチ編集へ変更できるか
- リッチ編集から通常編集へ戻せるか

---

## 5. 本文文字数

### 5.1 日記本文の上限

**Evidence:** Official

**Verification note:** 2015年時点の上限であり、現在の値は再検証が必要。

2015年のリッチ編集モード追加時に、
日記本文の入力文字数制限が10,000文字へ拡張された。

現在も同じ上限であるかは、LDSで実機確認する。

### 5.2 文字数カウンター

**Feature evidence:** Official

**Verification note:** 現在のカウント条件は再検証が必要。

同更新で、入力文字数カウンターが追加された。

確認項目：

- タグ文字列が文字数に含まれるか
- 改行が文字数に含まれるか
- DB埋め込みコードの数え方
- 絵文字の数え方
- 全角・半角による差
- 下書き保存時と投稿時の判定差

---

## 6. 対応文字装飾

### 6.1 太字

**Feature evidence:** Official

**Syntax evidence:** Observed

観測構文：

```bbcode
[b]本文[/b]
```

未検証：

- 空行を含む複数段落
- 他タグとの最大入れ子深度

---

### 6.2 斜体

**Feature evidence:** Official

**Syntax evidence:** Unknown

構文候補：

```bbcode
[i]本文[/i]
```

日本語環境での視認性、フォント差、スマートフォン表示は未検証。

---

### 6.3 下線

**Feature evidence:** Official

**Syntax evidence:** Unknown

構文候補：

```bbcode
[u]本文[/u]
```

---

### 6.4 取消線

**Feature evidence:** Official

**Syntax evidence:** Unknown

構文候補：

```bbcode
[s]本文[/s]
```

---

### 6.5 文字サイズ

**Feature evidence:** Official

**Syntax evidence:** Observed

公式UIには次の4段階がある。

- 極大
- 大
- 中
- 小

ユーザー記事では、次の数値が報告されている。

| UI表記 | 報告された値 | Evidence |
|---|---:|---|
| 小 | 10 | Community |
| 中 | 12 | Community |
| 大 | 18 | Community |
| 極大 | 32 | Community |

観測構文：

```bbcode
[size=18]本文[/size]
```

### 6.5.1 任意サイズ値

公開中のLodestone記事では、
`size=16` や `size=20` などUIプリセット以外の値が使用されている。

**Syntax evidence:** Observed

ただし、使用可能な最小値・最大値・整数以外の扱いは未検証。

### 6.5.2 検証項目

- 許容される最小値
- 許容される最大値
- 0、負数、小数
- 範囲外値の補正
- 長い日本語見出しの折り返し
- PC／スマートフォン表示差
- 行間への影響

---

### 6.6 文字色

**Feature evidence:** Official

**Syntax evidence:** Observed

観測構文：

```bbcode
[color=#CBB8E8]本文[/color]
```

16進RGB形式のカラーコード使用例が公開記事で確認できる。

### 6.6.1 検証項目

- 3桁HEX
- 6桁HEX
- 大文字・小文字
- `#` 省略
- 色名指定
- 不正値
- 実際の背景色とのコントラスト
- リンク文字への適用
- 既読リンクへの影響
- スマートフォン表示差

---

### 6.7 表示位置

**Feature evidence:** Official

**Syntax evidence:** Unknown

2019年の公式更新情報で、
リッチ編集モードにテキストの表示位置を編集できるコードが追加された。

公式ページのテキスト抽出からは、
具体的なタグ名・属性値を確認できていない。

確認対象：

- 左寄せ
- 中央寄せ
- 右寄せ
- 対応タグ
- 複数段落への適用
- 画像・動画との組み合わせ

---

## 7. リンク

### 7.1 外部・内部URLリンク

**Feature evidence:** Official

**Syntax evidence:** Unknown

構文候補：

```bbcode
[url=https://example.com]リンク文字列[/url]
```

次を検証する。

- `https`
- `http`
- Lodestone内部URL
- 長いURL
- 日本語URL
- URLだけを貼った場合の自動リンク
- 装飾タグとの入れ子
- 外部リンク警告画面の有無
- 投稿後の `rel` や新規タブ挙動

### 7.2 URLタグ内の装飾

**Syntax evidence:** Unknown

候補：

```bbcode
[url=https://example.com][b]リンク[/b][/url]
```

```bbcode
[b][url=https://example.com]リンク[/url][/b]
```

両者の挙動を実機比較する。

---

## 8. 非表示／展開表示

### 8.1 「隠す」機能

**Feature evidence:** Official

公式UIには「隠す」機能が存在する。

ユーザー記事では、`hb` タグとして報告されている。

報告例：

```bbcode
[hb]非表示にする内容[/hb]
```

**Syntax evidence:** Community

公開後は、読者が操作して内容を表示する形式になる。

### 8.2 編集上の扱い

折り畳みへ配置する情報の判断は、
[`03_LDS_Editorial_Methodology.md`](03_LDS_Editorial_Methodology.md) のPass 6を参照する。

### 8.3 検証項目

- 展開ボタンの表示文言
- 任意ラベル指定の可否
- 複数段落
- 画像
- 動画
- DB埋め込みコード
- 入れ子
- 複数連続配置
- スマートフォン操作
- 展開状態の保持
- 検索インデックスへの含まれ方

---

## 9. 画像

### 9.1 画像挿入

**Feature evidence:** Official

リッチ編集モードでは、日記本文中へ画像を挿入できる。

ユーザー記事では、画像IDを使う `img` タグが報告されている。

報告形式：

```bbcode
[img=画像ID]
```

または実装上類似する形式。

**Syntax evidence:** Community

**Verification note:** 正確な属性形式と現在の挙動は未確認。

### 9.2 画像の参照切れ

**Behavior evidence:** Observed

古い公開記事では、
参照先画像がHTTP通信であるため読み込めない旨の表示が確認できる。

これは、外部画像・過去仕様・HTTPS移行などが影響している可能性がある。

### 9.3 未確認事項

- アップロード可能枚数
- 1枚あたりの容量
- 対応形式
- 最大解像度
- 自動リサイズ
- 圧縮
- EXIF情報
- 透過PNG
- GIFアニメーション
- 本文内での配置
- キャプション
- 代替テキスト
- 削除時の本文リンク
- サムネイル選択
- 公開後の差し替え

---

## 10. 動画

### 10.1 動画挿入

**Feature evidence:** Official

リッチ編集モードには動画挿入機能がある。

### 10.2 対応サービス

公式更新履歴では、当初YouTubeに対応し、
2019年にTwitchが追加されたとされている。

| サービス | Evidence |
|---|---|
| YouTube | Official |
| Twitch | Official |
| その他 | Unknown |

### 10.3 タグ

**Syntax evidence:** Unknown

ユーザー記事では `video` や `iframe` に関する表示が見られるが、
現在の正確な構文は未確認。

外部の任意iframeを許可しているとは限らないため、
一般HTMLのiframe埋め込みと同一視しない。

---

## 11. エオルゼアデータベース埋め込みコード

### 11.1 概要

**Feature evidence:** Official

**Syntax evidence:** Official

エオルゼアデータベースには、
Lodestone内で使用する専用埋め込みコードがある。

アイテム例：

```bbcode
[db:item=1db77e54e4d]コルドロンキングコート[/db:item]
```

投稿後、対応するコンテンツではツールチップとして表示される。

公式説明では、次が明記されている。

- エオルゼアデータベース内の投稿
- リッチモード日記
- イベント

などで利用できる。

- Lodestone専用コードである
- 他サイトでは利用できない
- コンテンツによってツールチップが表示されない場合がある

### 11.2 対象カテゴリ

**Item evidence:** Official

**Other category evidence:** Unknown

アイテム以外のカテゴリについては、
各データベースページの埋め込みコードを確認する必要がある。

候補：

- アイテム
- クエスト
- コンテンツ
- アチーブメント
- 製作手帳
- 採集手帳
- ショップ
- テキストコマンド
- アクション
- エモート
- マウント
- ミニオン

### 11.3 検証項目

- 表示名の改変可否
- 言語切替時の表示
- 存在しないID
- 古いID
- 色・太字・サイズとの組み合わせ
- 非表示領域内
- ツールチップ非対応画面
- スマートフォン表示

---

## 12. Unicode・絵文字・特殊文字

### 12.1 Unicode絵文字

**Feature evidence:** Official

公式更新履歴では、
Patch 5.1以降に入力されたUnicode絵文字を表示できるようになったとされている。

### 12.2 検証項目

- 絵文字の入力・保存・再編集
- 複合絵文字
- 肌色修飾
- ZWJシーケンス
- 国旗
- 機種依存表示
- PC／スマートフォン差
- 文字数カウント
- 検索対象
- タイトルでの利用
- タグ名での利用

### 12.3 ゲーム内特殊文字

**Evidence:** Unknown

ゲーム内チャットで利用される特殊記号が、
日記本文・タイトル・コメントでどのように扱われるかは未整理。

---

## 13. 改行・空白・段落

**Evidence:** Unknown

**Verification note:** 改行、空白、段落を体系的に実機検証する必要がある。

Markdownの段落規則やHTMLの空白処理を前提にしない。

検証対象：

- 改行1回
- 空行1行
- 連続空行
- 行頭半角スペース
- 行頭全角スペース
- 連続半角スペース
- 連続全角スペース
- タブ
- タグ直前・直後の改行
- 開始タグと本文間の改行
- 終了タグ前の改行
- 空タグ
- 大サイズ文字の行間
- 罫線文字の折り返し
- 長い英数字列
- URLの折り返し

---

## 14. タグの入れ子

### 14.1 基本形

公開中のLodestone記事では、次の入れ子が観測されている。

**Syntax evidence:** Observed

```bbcode
[size=18][b][color=#CBB8E8]本文[/color][/b][/size]
```

これはLodestone公式の必須順序またはLDSの推奨順序を示すものではない。

### 14.2 閉じタグ

公開記事では、後から開いたタグを先に閉じる構文が観測されている。

**Syntax evidence:** Observed

```bbcode
[size=18][b]本文[/b][/size]
```

不正例：

```bbcode
[size=18][b]本文[/size][/b]
```

不正な閉じ順序をLodestoneが自動補正するかは未検証。

**Behavior evidence:** Unknown

### 14.3 検証マトリックス

| 外側 | 内側 | Evidence |
|---|---|---|
| size | b | Observed |
| size | color | Observed |
| b | color | Observed |
| color | size | Observed |
| url | b | Unknown |
| hb | color | Unknown |
| hb | img | Unknown |
| hb | db:item | Unknown |
| alignment | size | Unknown |
| alignment | img | Unknown |

---

## 15. リスト・引用・表・罫線

### 15.1 リスト

**Feature evidence:** Unknown

公式のリッチ編集機能一覧には、
リストが明示されていない。

一般的なBBCodeの `[list]` が使えるとは断定しない。

未確認機能の代替表現は、
[`03_LDS_Editorial_Methodology.md`](03_LDS_Editorial_Methodology.md) のPass 7に従う。

### 15.2 引用

**Feature evidence:** Unknown

公式の機能一覧に引用は明示されていない。

`[quote]` の対応可否は実機検証が必要。

### 15.3 表

**Feature evidence:** Unknown

**Verification note:** 対応を示す証拠はなく、現在は未確認。

一般的なMarkdown表やHTMLテーブルが使えるとは確認できていない。

未確認機能の代替表現は、
[`03_LDS_Editorial_Methodology.md`](03_LDS_Editorial_Methodology.md) のPass 7に従う。

### 15.4 水平線

**Feature evidence:** Unknown

専用の水平線タグは未確認。

公開記事では、
罫線文字を連続させた視覚的区切りが利用されている。

**Representation evidence:** Observed

例：

```text
￣￣￣￣￣￣￣￣￣￣￣￣￣￣
```

---

## 16. 日記の公開範囲

### 16.1 フリーカンパニー限定

**Feature evidence:** Official

**Verification note:** 現在利用可能な公開範囲は再検証が必要。

2015年の更新で、
公開範囲に「フリーカンパニーのみ公開」が追加された。

現在利用可能な公開範囲の全一覧は未整理。

### 16.2 確認対象

- 公開
- フレンド限定
- フリーカンパニー限定
- 非公開
- 下書き
- その他グループ限定
- 公開後の変更
- 検索結果への反映
- 共有URLへのアクセス挙動

---

## 17. 日記検索

### 17.1 現在確認できる検索条件

**Feature evidence:** Observed

Lodestoneの日記検索画面では、次の条件が確認できる。

- キーワード
- タグ
- 関係があるグループ
  - フレンド
  - フリーカンパニー
  - リンクシェル
  - クロスワールドリンクシェル
  - PvPチーム
  - フォロー
- データセンター／ホームワールド
- 使用言語
  - 日本語
  - 英語
  - ドイツ語
  - フランス語
- 除外キーワード

関係グループ検索は、ログイン時のみ利用可能と表示される。

### 17.2 注目の日記

**Feature evidence:** Observed

現在の日記ページでは、
直近30日間の「いいね」数が多い日記を注目の日記として扱う旨の説明がある。

ただし、

- 作成から30日を経過した日記
- 一定以上の閲覧数に満たない日記

は除外されると表示される。

選定アルゴリズムの詳細は不明。

---

## 18. タグ

**Feature evidence:** Official

**Verification note:** 現在の日記検索でも利用可能であることを観測済み。

日記には定型タグが存在する。

2015年の公式更新で定型タグ追加が案内されている。

現在の日記検索では、タグによる検索が可能。

未確認事項：

- 一記事あたりの上限
- 自由入力タグと定型タグの区別
- 大文字・小文字
- 同義語
- 編集後の検索反映
- タグの並び順
- 新規タグの作成可否
- 廃止タグ
- 言語別タグ

---

## 19. いいね・コメント・閲覧数

**Feature evidence:** Observed

**Verification note:** 各数値の意味と更新条件は未整理。

公開日記では、いいね数とコメント数が表示される。

検索・一覧画面では、閲覧数または反応数に相当する数値表示も確認できるが、
各数値の意味と更新条件は未整理。

確認対象：

- 自分でいいねできるか
- いいね取消
- コメント公開範囲
- コメント削除
- コメント文字数上限
- コメント内の装飾
- コメント内のDBコード
- 閲覧数の更新条件
- 自分の閲覧
- ログアウト閲覧
- ボット・クローラーの扱い

---

## 20. ソーシャルサービス自動投稿

**Feature evidence:** Official

**Verification note:** 2015年時点の情報であり、現在の提供状況は未確認。

2015年の公式案内では、
リッチ編集モード利用時にソーシャルサービス自動投稿機能を利用できないとされている。

現在、その自動投稿機能自体が提供されているか、
連携対象サービスが存在するかは未確認。

過去仕様と現在仕様を分離して扱う。

---

## 21. 技術上の前提と未確認範囲

現時点では、次の互換性や適用範囲が未確認または条件付きである。

- 一般的なMarkdown、HTML、CSSとの互換性は確認されていない
- 一般的なBBCodeタグがすべて使えることは確認されていない
- タグ構文はLodestone固有実装として個別に確認する必要がある
- PC版とスマートフォン版の編集機能が同一であるかは未確認範囲を含む
- 古い公式情報の現在における有効性は、個別のVerification noteを参照する
- 外部画像・動画の表示は、外部サービスとLodestone双方の仕様に依存する
- DB埋め込みコードはLodestone外では機能しない
- ツールチップは表示場所によって利用できない場合がある

これらは対応機能を断定する一覧ではない。
個別機能と構文のEvidenceは、各節の記録を優先する。

可読性と実画面確認の手順は、
[`03_LDS_Editorial_Methodology.md`](03_LDS_Editorial_Methodology.md) が定める。

---

## 22. 構文クイックリファレンス

以下は本書で扱う構文例と、正確な構文に対する現在のEvidenceをまとめたものである。
LDSでの推奨または標準利用可否を示す一覧ではない。

| 機能 | 構文例 | Syntax evidence | Verification note |
|---|---|---|---|
| 太字 | `[b]本文[/b]` | Observed | 複数段落と最大入れ子深度は未確認 |
| 斜体 | `[i]本文[/i]` | Unknown | 機能の存在はOfficial |
| 下線 | `[u]本文[/u]` | Unknown | 機能の存在はOfficial |
| 取消線 | `[s]本文[/s]` | Unknown | 機能の存在はOfficial |
| 文字サイズ | `[size=18]本文[/size]` | Observed | UIプリセット値との対応はCommunity |
| 文字色 | `[color=#CBB8E8]本文[/color]` | Observed | HEX形式の許容範囲は未確認 |
| URLリンク | `[url=https://example.com]リンク[/url]` | Unknown | 機能の存在はOfficial |
| 非表示 | `[hb]本文[/hb]` | Community | 正確な構文と現在の挙動は未確認 |
| 画像 | `[img=画像ID]` | Community | 正確な属性形式は未確認 |
| DB埋め込み | `[db:item=1db77e54e4d]表示名[/db:item]` | Official | Item以外のカテゴリは未確認 |
| 動画 | 未確定 | Unknown | 対応サービスの機能情報とは分離する |
| 表示位置 | 未確定 | Unknown | 機能の存在はOfficial |

標準利用の判断は、
[`03_LDS_Editorial_Methodology.md`](03_LDS_Editorial_Methodology.md) のPass 7に従う。

---

## 23. 情報源

### Official

- [Lodestone更新情報：リッチ編集モード追加、2015-01-20](https://jp.finalfantasyxiv.com/lodestone/special/update_log/1/)

- [Lodestone更新情報：Unicode絵文字、表示位置コード、Twitch動画対応](https://jp.finalfantasyxiv.com/lodestone/special/update_log/2/)

- [Lodestone日記検索](https://jp.finalfantasyxiv.com/lodestone/blog/)

- [エオルゼアデータベース埋め込みコード例](https://jp.finalfantasyxiv.com/lodestone/playguide/db/item/1db77e54e4d/)

### Community / Observed

- [リッチ編集モードの日記](https://jp.finalfantasyxiv.com/lodestone/character/6908566/blog/2067326)

- [見る人が見やすいロドストの日記を書こう（タグ有り版）](https://jp.finalfantasyxiv.com/lodestone/character/12671540/blog/5322264/)

- [読みやすい日記を書きたい！](https://jp.finalfantasyxiv.com/lodestone/character/12176107/blog/4544267)

- [リッチ編集モードへの入り方](https://jp.finalfantasyxiv.com/lodestone/character/789701/blog/4526654/)

---

## 24. Revision History

| Version | Date | Changes |
|---|---|---|
| 0.1 | 2026-07-19 | 公式情報・公開記事を基に初版作成。未検証事項と実機検証計画を分離。 |
| 0.2 | 2026-07-19 | 旧Google Drive運用への参照を除去し、リポジトリ管理規約へ一般化。 |
| 0.3 | 2026-07-19 | 内部の実機検証計画と優先度付きバックログを公開技術リファレンスから分離。 |
| 0.4 | 2026-07-19 | Applied Governance-defined Evidence, separated feature and syntax claims, removed editorial recommendations, and replaced standard candidates with an evidence-labeled syntax reference. |
| 0.5 | 2026-07-20 | Generalized unresolved platform assumptions, aligned display terminology, completed the cross-document consistency review, and advanced the document to Review. |
