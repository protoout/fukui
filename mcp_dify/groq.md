# Groqの設定方法

Groqとは、GPT-OSSなどのAIモデル（LLM）を高速に実行できるAI推論サービスです。  

一定の利用上限はありますが無料で試すことができ、Difyのモデルプロバイダーとしても利用できます。  
このページでは、GroqのAPIキーを取得し、Difyへ登録する方法を説明します。

## 1. Groqへログインする

1. [GroqCloud Console](https://console.groq.com/keys)を開きます。

2. Google、GitHub、SSO、メールアドレスのいずれかを選択してログインします。  
初めて利用する場合は、画面の案内に従ってアカウントを作成してください。

> <img src="https://i.gyazo.com/5d43c1966dae600553dfed3c80243416.png" width="450px"/>

## 2. APIキーを作成する

1. ログインすると、`API Keys`画面が表示されます。右側にある`Create API Key`ボタンをクリックします。

> <img src="https://i.gyazo.com/b3811e6012a6ed06560e33871b80f9df.png" width="650px"/>

2. APIキーの名前を入力する画面が表示された場合は、`dify-workshop`など用途が分かる名前を入力し、作成ボタンをクリックします。

3. APIキーが発行されたら、右側の`Copy`ボタンをクリックしてコピーします。  
コピーできたら`Done`をクリックします。

> <img src="https://i.gyazo.com/597769b98a0b40278657287fea825e8b.png" width="600px"/>

APIキーは、この画面を閉じると再表示できません。  
**必ず`Done`をクリックする前にコピーし、PCに搭載されているメモ帳やパスワード管理ツールなどへ保管しておきましょう。**

> APIキーはパスワードと同じように扱い、第三者へ共有したり、GitHubなどの公開場所へ登録したりしないでください。

## 3. Difyのモデルプロバイダーを設定する

Difyでは、モデルプロバイダーの画面からGroqCloudを追加できます。

1. [Dify](https://cloud.dify.ai/)へログインし、画面左側にある`連携`をクリックします。

2. `モデルプロバイダー`を選択し、検索欄に`groq`と入力します。

3. 検索結果に表示された`GroqCloud`の`インストール`ボタンをクリックします。

> <img src="https://i.gyazo.com/37b2b64e96eee9e13ee301bdf819ad1b.png" width="750px"/>

4. 確認画面が表示されたら、内容を確認して`インストール`ボタンをクリックします。

> <img src="https://i.gyazo.com/4b8a1f5579b212f2c1b410a8531972a5.png" width="450px"/>

5. インストールが完了すると、GroqCloudの設定欄が表示されます。  
右側にある`APIキーを追加`ボタンをクリックします。

> <img src="https://i.gyazo.com/5bf0c0c3d52e0cdffaee6dacf6d1e5ce.png" width="750px"/>

6. 表示されたメニューから、もう一度`APIキーを追加`をクリックします。

> <img src="https://i.gyazo.com/ca9a9f07f21289e1a9b2c478bb8b4c9c.png" width="350px"/>

7. APIキーの入力欄に、先ほどGroqCloudでコピーしておいたAPIキーを貼り付け、保存します。

8. GroqCloudの右側に緑色のマークと`API KEY 1`が表示されていれば、APIキーの登録は完了です。

> <img src="https://i.gyazo.com/178f2c9a653aa8299244ecfd0e426ad5.png" width="750px"/>

## 4. GroqCloudのモデルを選択する

1. Difyでアプリを開き、画面上部にあるモデル名をクリックします。

2. モデル一覧の`GroqCloud`から、使用するモデルを選択します。

以下の画像では、`gpt-oss-20b`を選択しています。

> <img src="https://i.gyazo.com/0dd3dc8de4c98b578ad92b5e259157fe.png" width="600px"/>

選択できるモデルは、GroqCloudやDifyの提供状況によって変わる場合があります。

以上で、GroqCloudのAPIキー取得とDifyへの登録は完了です。

---

[目次へ戻る](./readme.md)
