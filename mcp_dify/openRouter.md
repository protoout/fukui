# OpenRouterを設定してみよう

OpenRouterとは、1つのAPIキーを使って、OpenAI、Anthropic、Googleなどの多様なAIモデル（LLM）をまとめて利用できるようにするAIゲートウェイ（中継サービス）です。  

一定の利用上限はありますが無料である程度試すことができ、さまざまなAIモデルを比較して使ってみたい場合にも便利です。  
このページでは、OpenRouterの設定方法を進めていきます。

## 1. OpenRouterへログインする

1. [OpenRouter](https://openrouter.ai/)を開き、「Sign Up」を選びます。

> <img src="https://i.gyazo.com/1c03fa09c3cb1e4f39bad75ca8004afd.png" width="450px"/>

2. いずれかでログインをします。

> <img src="https://i.gyazo.com/7508cc62486bf3205850dd5bf69315b8.png" width="250px"/>

## 2. APIキーを作成する

1. `Get API Key`ボタンをクリックします。

> <img src="https://i.gyazo.com/340f50902a0a0862bcfece08b43a2572.png" width="450px"/>

2. `+ New Key`ボタンをクリックします。

> <img src="https://i.gyazo.com/fabf08ffd68ecedebf4dbb0e6baa2f7b.png" width="450px"/>

3. Nameを`dify-workshop`など用途が分かる文字を入力し、Expirationでは`1day`と有効期限を選びます。  
入力できたら`Create`ボタンをクリックします。

> <img src="https://i.gyazo.com/c1db3476cfadac456ccd6541e3bfd085.png" width="250px"/>

4. APIキーが発行されたら右側の`コピー`アイコンをクリックしてコピーし、PCに搭載されているメモ帳などに保管しておきましょう。

> <img src="https://i.gyazo.com/b0b4c00780e058a0b125be13902d39c9.png" width="450px"/>


## 3. Difyのモデルプロバイダーの設定をする

Difyはモデルプロバイダーという画面から各種AIモデルを追加できます。  

1. [Dify](https://cloud.dify.ai/)にログインし、画面左にある`連携`→`モデルプロバイダー`を選びます。

> <img src="https://i.gyazo.com/7e378c169bffaec81a9fa0fedd4c12f0.png" width="450px"/>

2. 検索バーで`openrouter`と検索し、OpenRouterのモデルプロバイダーをインストールします。

> <img src="https://i.gyazo.com/ef717dba9935baa84585ffb7d7f15422.png" width="450px"/>

> <img src="https://i.gyazo.com/30a4c11e7dcd9620dbd90285a67e4fef.png" width="300px"/>


3. 右側にある`APIキーを追加`→`APIキーを追加`ボタンをクリックします。  

> <img src="https://i.gyazo.com/3a721be1860ad01c9627799012b3803d.png" width="450px"/>

> <img src="https://i.gyazo.com/c18e9e9b40b68c9697e5a3bf18ff4c17.png" width="300px"/>


4. API Keyの欄に、先ほどメモ帳に保管しておいた文字列をコピーして貼り付け、`保存`ボタンをクリックします。

> <img src="https://i.gyazo.com/3bc6138ad1a7efa7b0977481c08376ad.png" width="250px"/>

5. 以下のような表示になっていればAPIキー登録完了です。

> <img src="https://i.gyazo.com/ee0670ebd6815c7fe600aebf9e118d5f.png" width="450px"/>

---
[目次へ戻る](./readme.md)
