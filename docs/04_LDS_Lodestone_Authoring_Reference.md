---
title: LDS Lodestone Authoring Reference
document_id: LDS-04
version: 0.9
status: Review
last_updated: 2026-07-30
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

### 3.2 Phase 3共通検証環境

本書で非表示／展開表示、画像、DB表示挙動、
正常なタグの入れ子を `Verified` とする場合は、
個別に記載がない限り次の条件で確認した。

- 確認日：2026-07-30
- 環境：Windows PC、Lodestone PC版
- 編集：リッチ編集モード
- 背景：黒
- 方法：UIまたは既存のOfficial構文から入力し、エディタ内プレビュー、
  下書き保存後の表示、再読込、再編集時の構文保持を確認
- CSS viewport：`1920×1080`、4Kディスプレイの150%表示相当となる
  論理 `2560×1440`
- device pixel ratio：`1920×1080` は検証単位により約`1.58`または約`2.37`、
  `2560×1440` は約`1.58`

両viewportで対象記事の本文幅は620pxとなり、
本文と文書全体に横方向オーバーフローは発生しなかった。

`1920×1080` は論理viewportの再現であり、
物理Full HD環境の想定DPR `1`、色、精細度、OS描画品質は検証していない。
スマートフォン版と背景白へも一般化しない。

### 3.3 Phase 5共通検証環境

本書で現在の編集モード、リッチ編集toolbar、公開範囲、
保存後の編集モード保持を `Verified` とする場合は、
個別に記載がない限り次の条件で確認した。

- 確認日：2026-07-30
- 環境：Windows PC、Lodestone PC版
- 対象：新規日記作成画面、保存済み下書きと公開済み日記の再編集画面
- 背景：リッチ編集のUI検証は黒。新規日記作成画面の既定値は白
- CSS viewport：`1920×1079`、4Kディスプレイの150%表示相当となる
  論理 `2560×1440`
- device pixel ratio：約`1.58`
- visual viewport scale：`1`

両viewportでリッチ編集toolbarの16controlと公開範囲の5選択肢が表示され、
toolbarと文書全体に横方向オーバーフローは発生しなかった。

`1920×1079` は論理viewportの再現である。
物理Full HD環境の想定DPR `1`、色、精細度、OS描画品質、
スマートフォン版へは一般化しない。

---

## 4. 日記編集モード

### 4.1 シンプル編集モード

**Feature evidence:** Verified

**Saved-mode behavior evidence:** Verified

**Verification note:** 3.3の環境で、新規作成画面と専用下書きの保存後を確認した。

現在の新規日記作成画面では、
シンプル編集モードとリッチ編集モードを選択でき、
既定値はシンプル編集モードである。

シンプル編集モードでは、タイトル、画像選択、plain textarea、
文字数counterが表示される。
リッチ編集toolbarと背景色選択は表示されない。

シンプル編集で保存した下書きは、
再編集画面でもシンプル編集の入力領域を保持した。
保存後の編集モード変更については4.4で扱う。

### 4.2 リッチ編集モード

**Current feature evidence:** Verified

**Historical feature evidence:** Official

**Verification note:** 3.3の環境で、現在の新規日記作成画面に表示される
全toolbar controlを実機確認した。

Lodestoneには、文字装飾、リンク、非表示、画像挿入、動画挿入などを利用できる
リッチ編集モードが存在する。

現在のリッチ編集toolbarには次の16controlが表示される。

- 文字サイズ小、中、大、極大
- 文字色
- 太字
- 斜体
- 下線
- 取消線
- 左に配置
- 中央に配置
- 右に配置
- リンク
- 隠す
- 画像挿入
- 動画挿入

文字色paletteには42色が表示された。
動画挿入はcontrolの存在だけを確認しており、
正確な構文と保存後挙動は未検証である。

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

**Saved-mode behavior evidence:** Verified

**Conversion behavior evidence:** Unknown

**Verification note:** 3.3の環境で、シンプル編集下書き1件、
リッチ編集下書き1件、リッチ編集の公開済み日記2件を再編集して確認した。

対象とした再編集画面では、
保存時の編集モードが保持され、編集モード選択UIは表示されなかった。
シンプル編集ではリッチ編集toolbarが表示されず、
リッチ編集では16controlのtoolbarが表示された。

現在のUIでは別の編集モードへ変更するcontrolを確認できなかったため、
変換時の警告、構文変換、内容保持または拒否の挙動は実行していない。
UI外の操作や将来の仕様まで変更不能とは断定しない。

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

### 共通検証環境

本章で `Verified` とする構文と挙動は、次の条件で確認した。

- 確認日：2026-07-30
- 環境：Windows PC、Lodestone PC版
- 編集：リッチ編集モード
- 背景：白
- 方法：UIが生成した構文を記録し、下書き保存後の表示と再編集時の構文保持を確認

スマートフォン版、背景黒での視覚的妥当性、複数段落、複合タグは、
個別に記載がない限り未検証である。

### 6.1 太字

**Feature evidence:** Official

**Syntax evidence:** Verified

**Behavior evidence:** Verified

**Verification note:** 共通検証環境で、保存後に太字として表示され、再編集時も構文が保持された。

検証済み構文：

```bbcode
[b]本文[/b]
```

未検証：

- 空行を含む複数段落
- 他タグとの最大入れ子深度

---

### 6.2 斜体

**Feature evidence:** Official

**Syntax evidence:** Verified

**Behavior evidence:** Verified

**Verification note:** 共通検証環境で、保存後に斜体として表示され、再編集時も構文が保持された。

検証済み構文：

```bbcode
[i]本文[/i]
```

フォント差、スマートフォン表示、背景黒での視認性は未検証。

---

### 6.3 下線

**Feature evidence:** Official

**Syntax evidence:** Verified

**Behavior evidence:** Verified

**Verification note:** 共通検証環境で、保存後に下線として表示され、再編集時も構文が保持された。

検証済み構文：

```bbcode
[u]本文[/u]
```

---

### 6.4 取消線

**Feature evidence:** Official

**Syntax evidence:** Verified

**Behavior evidence:** Verified

**Verification note:** 共通検証環境で、保存後に取消線として表示され、再編集時も構文が保持された。

検証済み構文：

```bbcode
[s]本文[/s]
```

---

### 6.5 文字サイズ

**Feature evidence:** Official

**Syntax evidence:** Verified

**Behavior evidence:** Verified

**Verification note:** 共通検証環境で、UIの4段階と保存後の表示サイズを確認した。任意値は対象外。

公式UIには次の4段階がある。

- 極大
- 大
- 中
- 小

現在のUIと生成構文の対応は次の通り。

| UI表記 | 生成値 | Evidence |
|---|---:|---|
| 小 | 10 | Verified |
| 中 | 12 | Verified |
| 大 | 18 | Verified |
| 極大 | 32 | Verified |

検証済み構文例：

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

**Syntax evidence:** Verified

**Behavior evidence:** Verified

**Verification note:** 共通検証環境で、UI上に42色のパレットが存在することを確認した。
3色の生成構文と、そのうち1色の保存後表示を検証した。
Phase 3共通検証環境では、`#FF99CC` を非表示領域と
3階層の正常な入れ子で保存し、背景黒での表示を確認した。
全パレット値と背景ごとのコントラストは未検証。

検証済み構文例：

```bbcode
[color=#FF99CC]本文[/color]
```

検証した3色では、6桁16進RGB形式のカラーコードが生成された。
UIパレット外の値を同形式で指定できる範囲は未検証。

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

**Syntax evidence:** Verified

**Behavior evidence:** Verified

2019年の公式更新情報で、
リッチ編集モードにテキストの表示位置を編集できるコードが追加された。

**Verification note:** 2026-07-30、Windows PC、Lodestone PC版、
リッチ編集モード、背景黒の下書きで、
UIが生成した構文、保存後の配置、再編集時の構文保持を確認した。

現在のUIと生成構文の対応は次の通り。

| UI | 検証済み構文 |
|---|---|
| 左寄せ | `[left]本文[/left]` |
| 中央寄せ | `[center]本文[/center]` |
| 右寄せ | `[right]本文[/right]` |

未検証：

- 複数段落への適用
- 左寄せ／右寄せと画像の組み合わせ
- 動画との組み合わせ
- 未検証の装飾タグとの入れ子

中央寄せと文字サイズ、中央寄せと画像の正常な入れ子は、
Phase 3共通検証環境で確認した。
詳細は「14. タグの入れ子」を参照する。

---

## 7. リンク

### 7.1 外部・内部URLリンク

**Feature evidence:** Official

**Syntax evidence:** Verified

**Behavior evidence:** Verified

**Verification note:** 2026-07-30、Windows PC、Lodestone PC版、リッチ編集モード、
背景白の下書きで、外部HTTPS URL 1件を確認した。
保存後のリンク先と再編集時の構文は入力値と一致した。
HTTP、Lodestone内部URL、日本語URLは未検証。

検証済み構文：

```bbcode
[url=https://example.com]リンク文字列[/url]
```

次を検証する。

- `http`
- Lodestone内部URL
- 日本語URL
- 外部リンク警告画面の有無
- 投稿後の `rel` や新規タブ挙動

### 7.2 URLだけを貼った場合の自動リンク

**Feature evidence:** Verified

**Syntax evidence:** Verified

**Behavior evidence:** Verified

**Verification note:** 2026-07-30、Windows PC、Lodestone PC版、
リッチ編集モード、背景黒の下書きで確認した。
286文字のHTTPS URLを装飾タグなしで入力すると自動的にリンク化され、
再編集時は入力した生のURLが保持された。

本文幅570pxでは4行へ折り返された。
CSS viewport `1280×720`、`1920×1080`、`2560×1440` の3条件で、
本文または文書全体の横方向オーバーフローは発生しなかった。

未検証：

- HTTP URL
- 日本語を含むURL
- Lodestone内部URL
- 末尾の句読点や括弧との境界
- 複数URLの連続入力

### 7.3 URLタグ内の装飾

**Syntax evidence:** Verified

**Behavior evidence:** Verified

**Verification note:** Phase 3共通検証環境で、
外部HTTPS URLの内側へ太字を配置し、
保存後のリンクと太字、再編集時の構文保持を確認した。
保存後のリンクには `rel="nofollow noopener"` が付与された。

検証済み構文：

```bbcode
[url=https://example.com][b]リンク[/b][/url]
```

太字の外側へURLを配置する逆順、
他の装飾、HTTP、内部URLとの組み合わせは未検証。

---

## 8. 非表示／展開表示

### 8.1 「隠す」機能

**Feature evidence:** Official

**Syntax evidence:** Verified

**Behavior evidence:** Verified

**Verification note:** Phase 3共通検証環境で、
UIが生成した構文、初期表示、開閉、再読込、
複数領域、複数行、空行、正常な入れ子を確認した。

検証済み構文：

```bbcode
[hb]非表示にする内容[/hb]
```

確認した挙動：

- 初期状態では内容を非表示にし、`クリックして表示` と表示する。
- 展開後は内容を表示し、操作文言を `クリックして隠す` へ切り替える。
- 再読込すると初期非表示へ戻る。
- 連続する非表示領域は個別に開閉できる。
- 複数行と空行を保持する。
- 1投稿で使用できる `hb` タグは最大5件である。
- 文字色、画像、DB itemコードを内側へ配置できる。

現在のUIでは任意ラベルを指定する入力欄を確認できなかった。
任意ラベル用の構文が存在しないとは断定せず、
正確な構文と挙動は `Unknown` とする。

### 8.2 編集上の扱い

折り畳みへ配置する情報の判断は、
[`03_LDS_Editorial_Methodology.md`](03_LDS_Editorial_Methodology.md) のPass 6を参照する。

### 8.3 検証項目

- 動画
- スマートフォン操作
- 検索インデックスへの含まれ方
- 任意ラベル指定構文の有無
- 不正な入れ子の補正
- 最大入れ子深度

---

## 9. 画像

### 9.1 画像挿入

**Feature evidence:** Official

**Syntax evidence:** Verified

**Behavior evidence:** Verified

**Verification note:** Phase 3共通検証環境で、
1024×576pxの不透明PNG 1件をアップロードし、
UIが生成した構文、保存後表示、元画像表示、
再編集時の構文保持を確認した。

検証済み構文：

```bbcode
[img=画像ID]
```

`画像ID` は、Lodestoneへアップロードした画像に割り当てられる数値である。

本文内では110×110pxのJPEGサムネイルとして表示され、
操作すると元画像をライトボックスで表示した。
サムネイルは元画像へのリンクを持ち、
検証した `img` 要素の `alt` は空文字だった。

### 9.2 現在の画像アップロードUI

**Upload UI evidence:** Verified

**Verification note:** Phase 3共通検証環境で、
現在の画像選択UIに表示された条件を記録した。
上限値の境界と全形式の実動作は確認していない。

UIには次が表示される。

- JPEG、GIF、PNG形式
- 1点につき30MB以内
- 同時に10枚までアップロード可能
- 一辺が1024pxを超える画像はリサイズし、JPEGへ変換
- 外部画像参照機能

検証時の画像選択ダイアログと投稿フォームでは、
サムネイルを別途指定するUIを確認できなかった。
この観察だけでサムネイル指定機能が存在しないとは断定しない。

### 9.3 画像の参照切れ

**Behavior evidence:** Observed

古い公開記事では、
参照先画像がHTTP通信であるため読み込めない旨の表示が確認できる。

これは、外部画像・過去仕様・HTTPS移行などが影響している可能性がある。

### 9.4 未確認事項

- UI表示上限の境界値
- GIFのアップロードとアニメーション
- 透過PNG
- 一辺1024px超の実際のリサイズとJPEG変換
- アップロード後の圧縮品質
- EXIF情報を含む画像の処理
- 外部画像参照
- キャプション
- 代替テキストの指定
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

**Behavior evidence:** Verified

エオルゼアデータベースには、
Lodestone内で使用する専用埋め込みコードがある。

アイテム例：

```bbcode
[db:item=1db77e54e4d]コルドロンキングコート[/db:item]
```

投稿後、対応するコンテンツではツールチップとして表示される。

**Verification note:** Phase 3共通検証環境で、
itemコードの表示、リンク、ツールチップ、
再編集時の構文保持を確認した。
タグ内の表示名を1件変更しても、
変更後の表示名、同じitemへのリンク、ツールチップを保持した。
非表示領域の内側でも、展開後に同じ表示と操作が成立した。

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

- 言語切替時の表示
- 存在しないID
- 古いID
- 色・太字・サイズとの組み合わせ
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

**Behavior evidence:** Verified

**Verification note:** 2026-07-30、Windows PC、Lodestone PC版、
リッチ編集モード、背景黒の下書きで確認した。
エディタ内プレビュー、保存後の記事、再編集時の本文を比較した。

検証したCSS viewportは `1280×720`、`1920×1080`、
4Kディスプレイの150%表示相当となる論理 `2560×1440` である。
3条件とも記事本文幅は570pxで、本文の表示結果は一致した。

Markdownの段落規則や一般的なHTMLの空白処理ではなく、
現在のLodestoneリッチ編集モードで確認した挙動として扱う。

### 13.1 改行と空行

- 改行1回は、保存後に1個の改行要素として表示された。
- 1行の空行は、連続する2個の改行要素として保持された。
- 2行、3行の連続空行も、入力数に対応する連続改行として保持された。
- 再編集時の本文でも、入力した改行と空行は保持された。

### 13.2 空白とタブ

現在の記事本文は、検証環境で `white-space: pre-wrap` として表示された。

- 1個、2個、4個の連続半角スペースを保持した。
- 1個、2個、4個の連続全角スペースを保持した。
- 行頭と行末に置いた4個の半角スペースを保持した。
- 行頭と行末に置いた4個の全角スペースを保持した。
- タブ文字は保存後の表示と再編集時の本文で保持された。

タブの視覚幅は表示環境に依存する可能性がある。
保持されることは、LDSが記事組版での利用を推奨することを意味しない。

### 13.3 長い文字列の折り返し

現在の記事本文は、検証環境で
`overflow-wrap: break-word`、`word-break: normal` として表示された。

本文幅570pxで、次の文字列は横方向へはみ出さずに折り返された。

| 対象 | 検証文字数 | 表示行数 |
|---|---:|---:|
| 句読点を含む日本語 | 260 | 6 |
| 空白を含まない英数字列 | 248 | 4 |
| HTTPS URL | 286 | 4 |
| 連続する罫線文字 `─` | 96 | 3 |

`1280×720`、`1920×1080`、`2560×1440` の3つのCSS viewportで、
本文幅と折り返し行数は一致した。

### 13.4 未検証

次は引き続き未検証である。

- タグ直前・直後の改行
- 開始タグと本文間の改行
- 終了タグ前の改行
- 空タグ
- 大サイズ文字の行間
- 段落を表す専用要素の有無
- 背景白での視覚的妥当性
- スマートフォン表示
- 物理ディスプレイ固有の色、精細度、OS描画品質

---

## 14. タグの入れ子

### 14.1 基本形

Phase 3共通検証環境で、次の3階層を保存し、
表示と再編集時の構文保持を確認した。

**Syntax evidence:** Verified

**Behavior evidence:** Verified

```bbcode
[size=18][b][color=#FF99CC]本文[/color][/b][/size]
```

これはLodestone公式の必須順序またはLDSの推奨順序を示すものではない。

### 14.2 閉じタグ

後から開いたタグを先に閉じる正常な構文を、
保存後表示と再編集時の構文保持で確認した。

**Syntax evidence:** Verified

**Behavior evidence:** Verified

```bbcode
[size=18][b]本文[/b][/size]
```

不正例：

```bbcode
[size=18][b]本文[/size][/b]
```

不正な閉じ順序をLodestoneが自動補正するかは未検証。

### 14.3 検証マトリックス

| 外側 | 内側 | Evidence |
|---|---|---|
| size | b | Verified |
| size | color | Verified |
| b | color | Verified |
| color | size | Observed |
| url | b | Verified |
| hb | color | Verified |
| hb | img | Verified |
| hb | db:item | Verified |
| center | size | Verified |
| center | img | Verified |

`Verified` の組み合わせは、
Phase 3共通検証環境で正常な閉じ順序、
保存後表示、再編集時の構文保持を確認した。
不正な閉じ順序、自動補正、最大入れ子深度は未検証。

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

**Behavior evidence:** Verified

**Verification note:** 2026-07-30、PC版、リッチ編集モード、
背景黒、本文幅570pxで、96個の罫線文字 `─` が3行へ折り返され、
横方向へはみ出さないことを確認した。

例：

```text
￣￣￣￣￣￣￣￣￣￣￣￣￣￣
```

---

## 16. 日記の公開範囲

### 16.1 現在の選択肢

**Current options evidence:** Verified

**Historical FC-option evidence:** Official

**Verification note:** 3.3の環境で、新規作成画面と保存済み記事の
再編集画面を確認した。

2015年の更新で、
公開範囲に「フリーカンパニーのみ公開」が追加された。

現在のLodestone PC版では、次の5種類を選択できる。

- 公開
- フレンドのみ公開
- フリーカンパニーのみ公開
- PvPチームのみ公開
- 下書き

新規日記作成画面の既定値は「公開」である。
UIでは「下書き」を自分のみ閲覧できる状態として説明している。

### 16.2 設定保持と未検証範囲

**Setting behavior evidence:** Verified

保存済み下書きでは「下書き」、
公開済み日記では「公開」が再編集画面でも保持され、
どちらも16.1の5選択肢を表示した。

次の挙動は未検証である。

- フレンド、フリーカンパニー、PvPチームの第三者アカウントからの閲覧
- 公開範囲を変更して保存した後のアクセス制御
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
| 太字 | `[b]本文[/b]` | Verified | 2026-07-30、PC版、背景白。複数段落と最大入れ子深度は未確認 |
| 斜体 | `[i]本文[/i]` | Verified | 2026-07-30、PC版、背景白。フォント差とスマートフォン表示は未確認 |
| 下線 | `[u]本文[/u]` | Verified | 2026-07-30、PC版、背景白 |
| 取消線 | `[s]本文[/s]` | Verified | 2026-07-30、PC版、背景白 |
| 文字サイズ | `[size=18]本文[/size]` | Verified | UIプリセットは10、12、18、32。任意値は未検証 |
| 文字色 | `[color=#FF99CC]本文[/color]` | Verified | 42色中3色の構文と1色の背景白表示を検証 |
| URLリンク | `[url=https://example.com]リンク[/url]` | Verified | 外部HTTPS URL 1件だけを検証 |
| URL自動リンク | `https://example.com` | Verified | 装飾タグなしの長いHTTPS URLで保存、リンク化、折り返し、再編集時の保持を検証 |
| 左寄せ | `[left]本文[/left]` | Verified | PC版、背景黒でUI、保存後配置、再編集時の保持を検証 |
| 中央寄せ | `[center]本文[/center]` | Verified | PC版、背景黒でUI、保存後配置、再編集時の保持を検証 |
| 右寄せ | `[right]本文[/right]` | Verified | PC版、背景黒でUI、保存後配置、再編集時の保持を検証 |
| URL内太字 | `[url=https://example.com][b]リンク[/b][/url]` | Verified | 外部HTTPS URL 1件で保存後表示と構文保持を検証 |
| 非表示 | `[hb]本文[/hb]` | Verified | PC版、背景黒で初期非表示、開閉、再読込、最大5件を検証 |
| 画像 | `[img=画像ID]` | Verified | 不透明PNG 1件で110pxサムネイル、元画像表示、構文保持を検証 |
| DB埋め込み | `[db:item=1db77e54e4d]表示名[/db:item]` | Official | Itemの表示、リンク、ツールチップはVerified。Item以外は未確認 |
| 動画 | 未確定 | Unknown | 対応サービスの機能情報とは分離する |

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
| 0.6 | 2026-07-30 | Verified current rich-editor syntax and saved-draft behavior for basic text decoration, UI size presets, representative color values, and one external HTTPS link. |
| 0.7 | 2026-07-30 | Verified alignment syntax, line breaks, whitespace preservation, long-string wrapping, bare HTTPS URL auto-linking, and rule-character behavior across desktop viewport conditions. |
| 0.8 | 2026-07-30 | Verified disclosure syntax and behavior, image insertion and saved display, DB item display behavior, and supported normal tag nesting across desktop viewport conditions. |
| 0.9 | 2026-07-30 | Verified current simple and rich editor surfaces, saved-mode retention and change-control absence, publication options and retained settings, and desktop editor layout coverage. |
