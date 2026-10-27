# らくらくシフト登録 画面プロトタイプ（HTML/CSS）ユースケース改訂版対応

ユースケース記述（207-3、22件）とユースケース図②（drawio）とプロジェクト計画書をもとに作成した静的プロトタイプです。
JavaScript は使っていません。ダイアログ・代替フローの表示は CSS の `:target`、日付のタップ選択は CSS のチェックボックスで動きます。

## VS Code での開き方
1. VS Code で `rakuraku-shift` フォルダを開く
2. 拡張機能「Live Server」を入れる
3. `login.html` を右クリック →「Open with Live Server」
4. 「管理者としてログイン」は管理者画面選択へ、「従業員としてログイン」は従業員メニューへ進みます

**代替フローの確認**：各画面の下の「代替フローの表示確認」のリンクを押すと、エラー・警告・確認ダイアログが表示されます。

## ユースケースと画面の対応

| ユースケース | アクター | 画面（基本フローの順） |
|---|---|---|
| ログイン | 管理者・従業員 | login.html → （管理者）admin/select.html／（従業員）employee/menu.html |
| サインアップ | 管理者 | login.html「サインアップ」→ signup.html → login.html（登録完了の表示） |
| 本人確認 | 管理者・従業員 | login.html「パスワードを忘れた場合」→ verify.html → verify-otp.html |
| パスワード変更 | 管理者・従業員 | password-change.html → login.html（変更完了の表示） |
| 管理者画面選択 | 管理者 | admin/select.html → 管理者メニュー／従業員メニュー |
| 管理者メニュー | 管理者 | admin/menu.html |
| 従業員メニュー | 従業員 | employee/menu.html |
| ログアウト | 管理者・従業員 | 各画面の「ログアウト」→ login.html |
| 管理者・従業員登録 | 管理者 | employee-new → employee-registered →（続けて登録／一覧へ） |
| 従業員情報変更 | 管理者 | employee-list（区分・スキルで絞り込み）→ employee-edit → employee-updated → 一覧へ |
| 従業員削除 | 管理者 | employee-list → employee-delete（元に戻せない旨）→ employee-deleted → 一覧へ |
| 勤務希望登録（休日希望を含む） | 従業員 | employee/request → request-done（期限後は request-closed） |
| 勤務条件設定 | 管理者 | conditions → conditions-done |
| シフト自動作成 | 管理者 | shift-generate（結果・充足率・不足枠）→ shift-view |
| 出勤催促メール | システム | シフト自動作成の結果から自動送信（画面は reminder-result で確認） |
| 出勤催促メールの結果確認 | 管理者 | reminder-result → 催促承認へ／シフト修正へ |
| 従業員出勤催促承諾 | 従業員 | employee/offer → offer-done（承認待ち） |
| 催促承認 | 管理者 | approval → approval-approve／approval-reject（確認）→ shift-view／approval |
| シフト確認 | 管理者・従業員 | admin/shift-view（作成中も可）、employee/shift（確定・公開済みのみ） |
| シフト修正 | 管理者 | shift-edit → shift-edit-done（確定後は確認ダイアログ） |
| シフト確定 | 管理者 | shift-view「確定へ進む」→ shift-confirm（確定確認）→ shift-confirmed |
| シフト表出力 | 管理者 | shift-export（期間・Excel/PDF） |

## ユースケース図②との照合結果
- 図のユースケースは22個（重複の楕円を除く）で、記述シート22件と名前がすべて一致しました。
- 画面は、アクターの権限を**記述シートに合わせて**作っています。図と記述で食い違う点は次のとおりです（どちらかの修正が必要です）。

| 点 | 図 | 記述 | 画面での扱い |
|---|---|---|---|
| 従業員 → 管理者・従業員登録、従業員情報変更、従業員削除、サインアップ | 線あり | アクターは管理者のみ | 管理者だけが使える画面にしています |
| 従業員 → 管理者画面選択 | 線あり | アクターは管理者のみ | 管理者だけ |
| 「従業員情報変更」の楕円 | 2つ | 1件 | 1つにまとめています |
| 「出勤催促メールの結果確認」の楕円 | 2つ（どちらも管理者と接続） | 1件 | 1つにまとめています |

## 要件の整理（確認済み）
- **CSV取込**と**催促加算（給与アップ・加算額）**は、システムの範囲から外しました。画面にも含めていません。
- 改訂履歴と非機能要件の、CSV関連の行は削除します（ユースケース記述・プロジェクト計画書側の修正は、各ファイルで行ってください）。

## 確定した前提（記述にないため、プロトタイプで決めた内容）
- 勤務希望登録の時間帯の選択肢：「早番／遅番／どちらでもよい」
- パスワードの形式：8文字以上、英字と数字を含む
- シフト確認画面（管理者）の「確定へ進む」ボタンから、確定確認画面へ進む
- サンプルデータ（従業員名、時間帯、必要人数、日付）は仮の値です。後で差し替えてください。

## フォルダ構成
```
rakuraku-shift/
├─ login.html／signup.html／verify.html／verify-otp.html／password-change.html
├─ css/style.css
├─ admin/       管理者の画面（22画面）
└─ employee/    従業員の画面（スマホ優先・7画面）
```
