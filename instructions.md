plugins/odekake-scout/skills/orchestrator/SKILL.md の「フェーズ1: イベント調査」のprofile読み込み部分を以下に書き換えてください。



\### フェーズ1: イベント調査



まず最初に、以下のコマンドを実行してprofile.ymlを読み込むこと。これは必須ステップである。



cat profile.yml



このコマンドでファイルの内容が表示されたら、その内容を家族プロフィールとして使用する。



ファイルが見つからない場合は、以下のメッセージを表示して処理を停止する:

「profile.yml が見つかりません。カレントディレクトリに profile.yml を作成してください。書き方の例は README.md の「カスタマイズ」セクションを参照してください。」



デフォルト値は使用しない。必ず profile.yml から読み込むこと。



（検索戦略以降はそのまま残す）



同様に、他のスキル（scout, rating, planner, advance-scout）のSKILL.mdからもデフォルト値のyamlブロックを削除し、同じ方式（profile.ymlが必須、なければエラー）に変更してください。

