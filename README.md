# firebase-sample
DBの環境を構築し、Firebaseにデプロイするまでの一連の流れをまとめたREADME
（下記記述は参考資料2から引用しつつ、VersionUpによって表示が変わったものを修正しています）
※WebサイトからDBに値を入れる方法は参考資料3を参考にしてね！

## Datebase
ローカルPCの適当な場所にサンプルプログラム用のディレクトリを作って
Firebase SDKをインストールする。
```
mkdir firestore-test && cd $_
npm init -f
npm install --save firebase-admin@^5.7.0
```

### 権限の設定
1.プロジェクトのダッシュボードから 歯車アイコン -> ユーザーと権限 をクリックする
2.タブのサービスアカウントをクリックする
3.クリックした画面下の秘密鍵を作成 をクリックする
4.サービスアカウントの秘密鍵が入ったJSONファイルがダウンロードされる。
  このJSONファイルを先ほど作ったディレクトリに配置しておく。

### プロジェクトの作成  
下記のテストコードをディレクトリ下に作成する。[SERVICE ACCOUNT JSON FILE] の部分を先ほどダウンロードしたサービスアカウントのJSONファイル名に書き換える。
```
index.js
const admin = require('firebase-admin');

var serviceAccount = require("./[SERVICE ACCOUNT JSON FILE]");

admin.initializeApp({
  credential: admin.credential.cert(serviceAccount)
});

var db = admin.firestore();

var docRef = db.collection('users').doc('alovelace');

var setAda = docRef.set({
    first: 'Ada',
    last: 'Lovelace',
    born: 1815
});
```

### 実行する
```
node index.js
```


### 参考サイト
①：データベースをどれを選択するか
https://tomokazu-kozuma.com/difference-between-cloud-firestore-and-firebase-realtime-database/
②：Firebase Cloud Firestore使い方
https://qiita.com/bathtimefish/items/164d2b0cd268f209db9b
③：FirestoreにWebサイトからデータを追加する手順
https://www.virment.com/writedata-from-webapp-to-firestore/

