# 職場概要
私達の職場は金型を使って、自動車部品の製造をしています。

金型は規定回数使用したら定期的に金型メンテナンス部署に点検をしてもらわなければなりません。

金型は突発的に壊れることがあり、その場合も金型メンテナンス部署に修理を行ってもらいます。

しかし、金型の数が数十個とあり、下記の問題があります。

* どの金型をいつまでに点検・修理しなければならないのか？
* どれだけの金型が点検・修理待ちなのか？

# サービス概要
金型のメンテナンス状況が把握できない人に

金型のメンテナンス状況を可視化する

Webアプリケーションサービスです。

# 登場人物
* エンドユーザー
  * 金型使用者
  * 金型部署作業者

* 管理者
  * 金型使用者の管理職
  * 金型メンテンナンス作業者の管理職

# ユーザーが抱える問題
  * 金型の修理状況がわからない
  * 金型の修理優先順位がわからない
  * 金型の定期点検間近のものがわからない

# 解決方法
  * 修理中、依頼中の金型を一覧で表示し、金型の修理状況を可視化する
  * 金型修理時に次回使用時の日時を設定し、修理依頼中の金型を次回使用日時が早いものから、並び替え表示し、優先順位を可視化する
  * 金型一覧の使用数を表示し、定期点検に近いものは、色付けなどし、可視化する
  
# 解決後の効果
 * 金型修理待ち時間０
 * 定期点検遅れ金型０

# プロダクト
金型のメンテナンス状況を可視化できるWebアプリケーション

# マーケット
金型使用部署・金型メンテナンス部署
自職場で運用予定

# 各画面説明
画面遷移図

https://xd.adobe.com/view/8014a3c1-223a-44d7-a941-95c25aef02e5-d547/

# TOPページ（ログインページ）
* ログインフォーム
  * 名前
  * パスワード
* ユーザー新規作成ページへのリンク

ログイン後は金型一覧ページへリダイレクト

# 金型一覧ページ
* 全金型の使用数累計、修理・点検状態を可視化
  * 金型の使用数が定期点検設定数の8割を超えているものは黄色。10割を超えているものは赤色。など
    * 金型の使用数は定期点検アクションでリセット。表示数は前回の定期点検から現在の使用数の累計を表示
  * 金型の状態を見える化（金型の状態：使用可・修理依頼中・修理中・修理完）
* 各金型は金型詳細ページへのリンク

# 金型詳細ページ
* 金型使用数入力履歴を日時の降順で表示（最新が一番上にくる）

* 前回の修理から現在までの加工数累計を表示

* 前回の定期点検から現在までの加工数累計を表示

* 新規入力で金型使用数入力ページへリダイレクト

# 金型使用数入力ページ
* 金型使用数入力フォーム
  * 作業者（ログイン中のユーザー）
  * 使用日（現在時刻）
  * 使用数
  * 材料情報
  * 備考（空欄の場合あり）
  * 修理状態（修理なしor修理or定期点検　デフォルトで修理なし）

    ### 修理依頼入力フォーム
    修理項目が修理or定期点検時のみ入力
    * 修理内容
    * 次回使用予定日

    ### 修理作業者入力フォーム
    修理金型一覧ページからのリンクでメンテナンス作業者が修理開始時に入力
    * 修理状況 修理依頼が入力された時点で修理待ち。修理を開始したら修理中。終了したら修理完。
    * 修理完了予定は見積が取れ次第入力。未入力の場合は見積中。
    * 実施修理内容は修理後に入力。このカラムが入力されて登録されたら、修理状況カラムを修理完にする。
    * 修理完了時刻も上記のカラムが入力された時点で登録

確認画面のあとに送信。
* 修理項目が修理なしの場合、入力情報が金型詳細ページへ追加
* 修理項目が修理or定期点検の場合、入力情報が修理金型一覧へ追加

# 修理金型一覧ページ
* 修理依頼中・修理中の金型一覧（次回使用日が近いものから降順で表示）
* 修理内容
* 次回使用予定日
* 修理状況
* 修理完了予定日

各項目は金型使用詳細ページ（金型使用数入力フォーム詳細）へリダイレクト

# ユーザー新規作成ページ
* ユーザー新規作成フォーム
  * 名前
  * パスワード
  * パスワード確認
  * 所属部署（リスト）

# 追加仕様
* エクセルへの出力
* 他Webアプリ（DIEMS）の入力フォームへパラメーター送信（修理数累計・修理内容）
  * DIEMS [![Image from Gyazo](https://i.gyazo.com/6469861ca90f68ff7107554bedf710da.png)](https://gyazo.com/6469861ca90f68ff7107554bedf710da)
  * 上記アプリは会社サーバーにあり、ログイン必須でセッションが切れるのが早いので厳しい？
* 修理アクションでメンテナンス作業者に通知・修理完了アクションで使用者に通知
* 入力項目はなるべく少なくor簡単に入力させたい
  * 音声入力
  * Lineの選択入力（例：ヤマト運輸の日時指定のような）
