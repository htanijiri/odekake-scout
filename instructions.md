以下の2ファイルの交通手段に関する記述を修正してください。



■ 1. plugins/odekake-scout/skills/orchestrator/SKILL.md



交通手段の判断ロジックを以下に書き換え:



profile.ymlのtransport設定に基づいて判断する。

\- primary: メインの交通手段（車 or 電車）

\- secondary: サブの交通手段（省略可）

\- prefer\_secondary\_when: サブに切り替える条件



secondaryが設定されている場合、prefer\_secondary\_whenの条件に該当すればsecondaryを使用する。

secondaryがない場合は常にprimaryを使用する。



■ 2. plugins/odekake-scout/skills/planner/SKILL.md



同様に、交通手段の判断ロジック部分を上記と同じ方式に書き換えてください。

「prefer\_train\_when」という記述があれば「prefer\_secondary\_when」に変更してください。



修正後、git add -A \&\& git commit -m "fix: transport構造をprimary/secondary/prefer\_secondary\_whenに変更" \&\& git push origin main を実行してください。

