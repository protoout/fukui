# 応用：GitHub CodespacesでMCPを公開しよう

今回MCP ServerのURLを使ったと思いますが、こちらの工程は事前に講師側で準備していました。   
ここでは、自分でもできるようにGitHub Codespacesを使って、MCP Serverを起動・公開する手順を紹介します。  

GitHub Codespacesを使えば、パソコンへ開発ツールをインストールしなくても、ブラウザ上に用意された開発環境を操作できます。  
実際に自分の手でMCP Serverを動かしながら、MCPがどのように公開されているのかを試してみましょう。

## 1. 事前準備：GitHubアカウントの作成と持続時間設定

1. GitHubアカウントを持っていない場合は、[GitHubアカウントの作成手順](https://zenn.dev/protoout/articles/50-howto-github-setup)の次の手順を見ながらアカウントを作成しましょう。

2. [GitHub Codespacesの持続時間を延ばす手順](https://zenn.dev/protoout/articles/77-github-codespaces-restart#2.-github-codespaces%E3%81%AE%E6%8C%81%E7%B6%9A%E6%99%82%E9%96%93%E3%82%92%E5%BB%B6%E3%81%B0%E3%81%99)の手順を参考に、GitHub Codespacesの持続時間を最大の240分へ変更しておきましょう。

## 2. ハンズオン：GitHub CodespacesでMCPを公開しよう

### 2-1. GitHub Codespacesを作成する

1. [デジタル庁 行政手続データ分析MCP](https://github.com/digital-go-jp/administrative-procedures-mcp)を開き、リポジトリ画面右上の `Code` ボタンをクリックします。  
`Codespaces` タブを選択し、`Create codespace on main` ボタンをクリックします。

> <img src="https://i.gyazo.com/b1a84a3f05f460b7c7ed48b7f16bc606.png" width="450">

2. 別のタブで、開発環境が起動するため画面が表示されるまで、そのまま待ちましょう。  
「このフォルダー内のファイルの作成者を信頼しますか？」と表示されたら、`フォルダーを信頼して続行` ボタンをクリックします。

> <img src="https://i.gyazo.com/05a12e7990515fb8e6ae570b23c586cb.png" width="300">

3. 画面下部のターミナルに入力待ちの記号 `$`が表示されていればOKです。

> <img src="https://i.gyazo.com/3faa1f757d0de40152384f9ea2e906bf.png"  width="450">

### 2-2. セットアップし、MCP Serverを起動する

1. ターミナルへ次のコマンドをコピーして貼り付け、Enterキーを押します。

> [!NOTE]
> ターミナルの行頭に表示されている `$` は入力しません。`./setup.sh` の部分だけを入力してください。

```bash
./setup.sh
```

> <img src="https://i.gyazo.com/9599d4125cd950de6795c4f079c255a7.png" width="450">

2. クリップボードへのアクセス許可を求められた場合は、`許可する` をクリックします。

> <img src="https://i.gyazo.com/c1de593101d0414dfe37ef17b967b5ec.png" width="250">

3. 「セットアップを進めますか？」と表示されたら、`y` を入力してEnterキーを押します。

> <img src="https://i.gyazo.com/be074d6657adc00f2bc6df583e4469e4.png" width="450">

4. 依存パッケージのインストールを進めるか確認されたら、`y` を入力してEnterキーを押します。

> <img src="https://i.gyazo.com/8f9fe27239d98088e68043ff8660a3ba.png" width="450">

5. 調査結果データを取得するか確認されたら、`y` を入力してEnterキーを押します。

> <img src="https://i.gyazo.com/74e07bf3a5f887177229e9cdda5692d7.png" width="450">

6. 「セットアップ完了」と表示され、ターミナルへ入力待ちの記号が戻ればセットアップは完了です。

> <img src="https://i.gyazo.com/86da414211d031de9d351bd7c6be9616.png" width="450">

7. 続けて、次のコマンドを1行で実行します。  
（$は入力しません。）

```bash
$ ADMIN_PROCEDURES_HOST=0.0.0.0 ADMIN_PROCEDURES_PORT=8000 uv run python -m admin_procedures
```

> <img src="https://i.gyazo.com/e8dbd6efcddf6912decd34a13db3b253.png" width="450">

### 2-3. ポートを公開する

1. 画面下部の `ポート` タブを開きます。    
ポート8000の行にある表示範囲の `Private` を右クリックし、`ポートの表示範囲` を選択します。

> <img src="https://i.gyazo.com/f51e93f1427fed33952e7113bd311765.png" width="450">

2. ポートの表示範囲を `Public` に設定します。

> <img src="https://i.gyazo.com/d32da13eb55d627b30395f3cd5c2b649.png" width="450">

3. `転送されたアドレス` に表示されたURLのコピーアイコンをクリックします。

> <img src="https://i.gyazo.com/a4661edf992c411d919fd7f65f93b26c.png" width="450">

4. MCP Server URLは、コピーしたURLの末尾へ `/mcp` を追加したものです。

```text
https://<CODESPACE_NAME>-8000.app.github.dev/mcp
```

これでMCP Serverを利用することができました。

## 3. まとめ

ここまでできたら、作成したMCP Server URLをDifyへ接続して使用していきましょう。

最後に試し終わったら、ポートの表示範囲を`Private` へ戻し、Codespacesも停止しておきましょう。

---

[目次へ戻る](./readme.md)
