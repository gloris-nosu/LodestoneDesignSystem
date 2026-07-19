# Lodestone Design System

Lodestone Design System（LDS）は、FINAL FANTASY XIV Lodestone日記を
一貫した品質で継続的・再利用可能に制作するためのMarkdownベースの文書体系です。

記事を派手に装飾することではなく、文章の論理構造、情報の役割、読者の視線、
Lodestone固有の技術的制約を統合して設計することを目的とします。

## Source of Truth

- リポジトリ内のMarkdownファイルを内容上の正本とします。
- GitHubをcommit履歴、差分、共有状態の正本として使用します。
- Versionは各文書のYAML Front Matterで管理します。

## Canonical Documents

| ID | Document | Role |
|---|---|---|
| LDS-00 | [`docs/00_LDS_Project_Overview.md`](docs/00_LDS_Project_Overview.md) | プロジェクトの入口、目的、全体構成 |
| LDS-01 | [`docs/01_LDS_Governance.md`](docs/01_LDS_Governance.md) | 正本、命名、状態、変更、文書ライフサイクル |
| LDS-02 | [`docs/02_LDS_Design_Principles.md`](docs/02_LDS_Design_Principles.md) | 設計判断の価値基準と優先順位 |
| LDS-03 | [`docs/03_LDS_Editorial_Methodology.md`](docs/03_LDS_Editorial_Methodology.md) | 記事へLDSを適用する編集手順 |
| LDS-04 | [`docs/04_LDS_Lodestone_Authoring_Reference.md`](docs/04_LDS_Lodestone_Authoring_Reference.md) | Lodestoneの技術仕様、記法、制約、検証状態 |

## Working Rules

- 既存Markdownを直接編集し、不要な複製文書を作りません。
- ファイル名を固定し、バージョン番号をファイル名へ含めません。
- 文書責務、用語、相互参照、Governanceとの整合性を確認します。
- 変更はGitのcommit履歴と差分で管理します。

## Repository Scope

このリポジトリには、公開可能なLDS仕様と一般向け文書だけを置きます。
内部の作業記録、調査メモ、引継ぎ情報、公開可否が未確認の資料は含めません。

## License

特記がない限り、このリポジトリでLodestone Design System contributorsが作成した文書は、
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International](LICENSE.md)
（CC BY-NC-SA 4.0）で提供します。

非営利目的での共有・改変を認めます。利用時はLodestone Design Systemを表示し、
改変の有無を示し、改変物にも同一または互換ライセンスを適用してください。
商用利用には、該当する権利者からの個別許可が必要です。

FINAL FANTASY XIVの名称、商標、ロゴ、スクリーンショット、ゲーム内容、公式サイトの内容など、
Square Enixまたはその他の第三者が権利を持つ素材は、このライセンスの対象外です。
該当素材を利用する場合は、
[ファイナルファンタジーXIV 著作物利用条件](https://support.jp.square-enix.com/rule.php?id=5381&la=0&tag=authc)
など、権利者が定める最新の条件に従ってください。

本プロジェクトはSquare Enixによる公式プロジェクトではなく、同社との提携または承認を示すものではありません。
