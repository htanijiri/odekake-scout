■ このプロジェクトの全体像

「おでかけスカウト」は4つのSkillが連鎖して自走するAIエージェントです。

1\. scout：イベント調査（Web検索）

2\. rating：おすすめ選定（スコアリング）

3\. planner：おでかけプラン作成

4\. output：最終レポート出力



今作るのは1番のscoutだけです。



■ scoutの設計方針

\- ユーザーに毎回聞き取りはしない

\- 代わりに profile.yml から家族情報を読み込む

\- ユーザーは「今週末のおでかけ調べて」と言うだけで、あとは自走する

\- Web検索を使って実際のイベント情報を収集する



■ plugins/odekake-scout/skills/scout/SKILL.md を以下の仕様で書き直してください：



フロントマター:

&#x20; name: scout

&#x20; description: >

&#x20;   子連れ家族向け週末イベントの自動調査。

&#x20;   「おでかけ調べて」「今週末のイベント」などで起動。

&#x20;   家族プロフィールを元にエリア別・興味別にWeb検索し、

&#x20;   結果が少なければクエリを変えてリトライする自律型スキル。

&#x20; user-invocable: true



内容に含めること:

\- 役割：家族プロフィールを読み込み、今週末のイベントをWeb検索で自律的に収集する

\- profile.ymlの場所：${CLAUDE\_PLUGIN\_ROOT}/data/profile.yml

\- profile.ymlがまだない場合のデフォルト値：

&#x20; home\_area: 葛飾区

&#x20; children:

&#x20;   - name: 長男, age\_group: 小学生, interests: \[マインクラフト, ポケモン]

&#x20;   - name: 次男, age\_group: 保育園児, interests: \[]

&#x20; search\_areas: \[東京23区, 千葉県, 埼玉県, 茨城県南部, 神奈川県]

&#x20; max\_travel\_time: 片道2時間

&#x20; transport:

&#x20;   primary: 車

&#x20;   prefer\_train\_when: \[都内の近場, 駐車場が不安な場所, 荷物が少ない時]

\- 検索戦略：

&#x20; 1. まずエリア別に「○○ 子ども イベント 今週末」で検索

&#x20; 2. 次に興味別に「マインクラフト イベント 関東」等で検索

&#x20; 3. 結果が5件未満ならクエリを変えてリトライ

&#x20; 4. 各イベントの日時・場所・対象年齢・料金・申込要否・URLを構造化

\- 出力：イベント一覧をMarkdown形式で出力

\- 完了後：「続けてrating Skillを実行してイベントを評価します」と表示する

\- ルール：

&#x20; - 実在するイベントのみ（架空のイベントを作らない）

&#x20; - 検索結果をそのまま信頼せず、日付が今週末かどうかを確認する

&#x20; - 結果が少ない場合は最低3回はクエリを変えてリトライする



■ 合わせて以下も確認・修正してください：

\- .claude-plugin/marketplace.json にodekake-scoutプラグインが登録されているか

\- plugins/odekake-scout/.claude-plugin/plugin.json が存在するか

