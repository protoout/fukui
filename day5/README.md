# n8n を使って自動化ツールの開発に挑戦してみよう
特に海外で人気のあるワークフロー自動化ツール、**n8n (エヌエイトエヌ)** を使って、**"フローグラマー(Flowgrammer)"** に挑戦してみましょう。
今回は、動画作成から YouTube へのアップロードまでを自動化する方法を紹介します。

## 今日つくるもの
こんなワークフローをつくります。  
<a href="https://gyazo.com/4c1f37c03de873798f42c87cd5253967"><img src="https://i.gyazo.com/4c1f37c03de873798f42c87cd5253967.png" alt="Image from Gyazo" width="600px"/></a>

> [!IMPORTANT]
> 今回の講義では時間の都合上、以下の点を変更して実装します。完全版をつくるためのフローも資料では紹介しているので是非チャレンジしてみてください。  
> 変更点
> - 動画生成 (Sora) → 画像生成 (DALL・E)
> - YouTube へのアップロード → Dropbox へのアップロード

## 目的
あなたが Gmail や Slack などのツール同士を連携させたいとき、どのようなイメージが沸くでしょうか？  
世界中で人気の高い自動化ツール n8n に触れ、ツールを連携させるための勘所を学びましょう。
  
---
  
# 準備状況の確認

以下にアクセスしてアカウント名を入力してサインインしてください。

https://app.n8n.cloud/login

何かしらワークフローをスタートできそうな画面になっていれば OK です。例えば、このような画面から始まる人は `Start from scratch` から始めましょう。  
<a href="https://gyazo.com/75833048bbec2e28872856fd1b0c61a8"><img src="https://i.gyazo.com/75833048bbec2e28872856fd1b0c61a8.png" alt="Image from Gyazo" width="450px"/></a>  
  
> [!WARNING]
> アカウントがない場合やアカウント名が誤っている場合は以下のように表示されます。このようになってしまう方は教えて下さい。  

<a href="https://gyazo.com/f32050fca9df56ee2f451d49e76ce26a"><img src="https://i.gyazo.com/f32050fca9df56ee2f451d49e76ce26a.png" alt="Image from Gyazo" width="450px"/></a>  

# n8n とは？
n8n はオープンソースのワークフロー自動化ツールです。プログラミング不要で、視覚的に Google Sheets や Slack、メール、データベース、生成 AI など普段使っているツール同士をつなげて面倒な作業を自動化できるソフトウェアです。  
パズルのようにツールをつなげられるサービスと考えてください。  
  
<a href="https://gyazo.com/4949011962adbe4bac7920b0d22f5e3b"><img src="https://i.gyazo.com/4949011962adbe4bac7920b0d22f5e3b.png" alt="Image from Gyazo" width="450px"/></a>

## 特徴
- 利用できるサービスが豊富
約8千ものテンプレートが用意されているので普段使っている主要なサービスは連携できると思います。
参考:  
  - [こちら](https://n8n.io/integrations/)から自分が知っているサービスを検索してみましょう。
  - [こちら](https://n8n.io/workflows/)からどのような自動化ができるかを調べることもできます。
  
<a href="https://gyazo.com/e9387409a1951d6023808f7d1698af66"><img src="https://i.gyazo.com/e9387409a1951d6023808f7d1698af66.png" alt="Image from Gyazo" width="450px"/></a>  

- セルフホスト
[事前準備の資料](https://github.com/protoout/fukui-day4-5/blob/main/day5/preparation.md#n8n-%E3%81%AE%E3%82%A2%E3%82%AB%E3%82%A6%E3%83%B3%E3%83%88%E4%BD%9C%E6%88%90%E3%82%92%E3%81%8A%E9%A1%98%E3%81%84%E3%81%84%E3%81%9F%E3%81%97%E3%81%BE%E3%81%99)にも記載しましたが、自身のPC(ローカル)の環境やサーバー環境に構築し使用することができます。今回はクラウド版を利用しますが、組織で使う際など、セルフホストできる点が n8n を利用する大きなメリットです。


> [!NOTE]
> あと、英語ですが頑張っていきましょう！

# 実装

## まずはノードを並べる
このような完成図を目指します。まずは細かい編集はせずに必要なノードを並べていきます。  
  
<a href="https://gyazo.com/0030e70ba7e6d7d397b535254b13dbe4"><img src="https://i.gyazo.com/0030e70ba7e6d7d397b535254b13dbe4.png" alt="Image from Gyazo" width="600px"/></a>
  
**1. n8n Form**
  
初めは `Add first Step` を選び右側の検索バーからノードを探します。  

<a href="https://gyazo.com/7485f01f9727818784565b0de7f150bf"><img src="https://i.gyazo.com/7485f01f9727818784565b0de7f150bf.png" alt="Image from Gyazo" width="450px"/></a>  

まずはユーザーが入力するフォームを作成します。
「Form」と入力し、`n8n Form` から `On new n8n Form event` を選択しフォームをつくりましょう。  

<a href="https://gyazo.com/81326076061cd37f020e7a2b5d4c2182"><img src="https://i.gyazo.com/81326076061cd37f020e7a2b5d4c2182.png" alt="Image from Gyazo" width="450px"/></a>  

できたら、色々と入力する画面が出てきますが「×」で閉じます。

> [!NOTE]
> 一番初めに置くノードをトリガーと言い、他にも「9時になったら」「データがアップロードされたら」「メールが来たら」など様々な条件を起点にすることができます。  

**2. Data Transformation**  

続いて、フォームに入力されたデータを加工するノードを準備します。
今つくったノードの右側の「＋」を押してフローをつなげることができます。  
  
<a href="https://gyazo.com/ce0311512e893bc8465f4cbb9a0da6b7"><img src="https://i.gyazo.com/ce0311512e893bc8465f4cbb9a0da6b7.png" alt="Image from Gyazo" width="450px"/></a>  

「＋」を押して、`Data Transformation`(既に候補に出てきていると思います) から `Edit Fields` を選択します。(もしくは `Edit Fields` を検索してください)
  
<a href="https://gyazo.com/b1156c0d4d2cf8c864de4fedd58630eb"><img src="https://i.gyazo.com/b1156c0d4d2cf8c864de4fedd58630eb.png" alt="Image from Gyazo" width="450px"/></a>  

ノードを出せたら「×」で閉じます。    
  
**3. OpenAI**
続いて、加工したデータを生成 AI に渡します。
ノードをつなげて、`OpenAI` から `Generate an image` を選びます。
  
<a href="https://gyazo.com/dd179b43d38198f29a04ab308ec402bf"><img src="https://i.gyazo.com/dd179b43d38198f29a04ab308ec402bf.png" alt="Image from Gyazo" width="450px"/></a>
   
ノードを出せたら「×」で閉じます。  
  
> [!NOTE]
> 動画を生成するときは `Generate a video` を選びます。

**4. Dropbox**  
最後です。  
`Dropbox` から `Upload a file` を選択します。

<a href="https://gyazo.com/809f46217fc43e19cde2e6e9af767df9"><img src="https://i.gyazo.com/809f46217fc43e19cde2e6e9af767df9.png" alt="Image from Gyazo" width="450px"/></a>
  
ノードを出せたら「×」で閉じます。  
  
> [!NOTE]
> これ以外にも Google Drive や YouTube など様々なサービスにデータをアップロードできます。

ひとまず必要なものは揃いました。ではそれぞれを設定していきましょう。

<a href="https://gyazo.com/0030e70ba7e6d7d397b535254b13dbe4"><img src="https://i.gyazo.com/0030e70ba7e6d7d397b535254b13dbe4.png" alt="Image from Gyazo" width="600px"/></a>
  
---

## 1. On form submission (On new n8n Form event) 
ノードをダブルクリックすると詳細を編集する画面が立ち上がります。  

編集する部分を以下に記載します。  
  
<a href="https://gyazo.com/89398134b805a01b132f389e24754c51"><img src="https://i.gyazo.com/89398134b805a01b132f389e24754c51.png" alt="Image from Gyazo" width="450px"/></a>  
  
- `Form Title`: 画像作成
- `Form Description`: つくりたい画像のテーマを入力してください
  
`Add Form Element` を押します。
- `Label`: 画像のテーマ
- `Element Type`: Text input
  
さらに、`Add Attribute` を押します。
- `Custom Field Name`: imageTheme
- `Placeholder`: 例：ラッパを吹いている猫

データのやり取りで重要なのは`Element Type`と`Custom Field Name`です。間違えがないようにしましょう。

## 2. Edit Fields
続いて `Edit Fields` を設定していきます。
ここで画面上部の `Execute step` もしくは画面左側の `Execute Previous nodes` を押してみましょう。ワークフローが実行されて先ほど作成したフォームが別のフォームが立ちあがります。

<a href="https://gyazo.com/2212b90d72da2f211eadc7ae10e2e5b0"><img src="https://i.gyazo.com/2212b90d72da2f211eadc7ae10e2e5b0.png" alt="Image from Gyazo" width="450px"/></a>  
  
何か入力して `Submit` しましょう。
すると`imageTheme`、`submittedAt`、`form Mode`という名前の3つの変数が出来上がります。  
これらを真ん中の`Drag input fields here or Add Field`に順々にドラッグ&ドロップしましょう。  
  
<a href="https://gyazo.com/4e985ff135f3587b9911323cab0ee675"><img src="https://i.gyazo.com/4e985ff135f3587b9911323cab0ee675.png" alt="Image from Gyazo" width="450px"/></a>  
  
> [!NOTE]
> 途中であってもワークフローの実行(`Execute workflow`や`Execute step`)は積極的に行って問題ありません。
> 前のノードでつくったものをドラッグ&ドロップで使えるほか、直前のノードまでどのようなデータが来ているかを確認することができるので、どんどん実行しましょう。

それぞれ、`{{ $json.imageTheme }}`のような値が入ります。

もう一度 `Execute step` を押してみましょう。右側の `OUTPUT` に3つの値が入っていればOKです。
  
<a href="https://gyazo.com/0024b5971c52a953f9a7b699192f684f"><img src="https://i.gyazo.com/0024b5971c52a953f9a7b699192f684f.png" alt="Image from Gyazo" width="450px"/></a>
  
> [!NOTE]
> `{{ }}` に囲まれた内容は、「変数として扱う」という明示的な指示となります。

## 3. Generate an Image (OpenAI)

> [!IMPORTANT]
> `Credidential to connect with`という項目に何も表示されていない場合は、
> 中央上部にある `Claim credits` をクリックして OpenAI の API を一定量無料で使えるクレジットを入手します。

設定はほとんど必要ありません。以下のようになっているか確認します。  
  
- `Credidential to connect with`: n8n free OpenAI API credits
- `Resource`: image
- `Operation`: Generate an Image
- `Model`: DALL・E 3 

そして、プロンプト(`Prompt`)を編集します。
左側の Input から`Edit Fields`の`imageTheme`を`Prompt`のボックスにドラッグ&ドロップします。  
`{{ $json.imageTheme }}` となります。
  
<a href="https://gyazo.com/654c3d8e767f4e6380a85c10d8210425"><img src="https://i.gyazo.com/654c3d8e767f4e6380a85c10d8210425.png" alt="Image from Gyazo" width="450px"/></a>  
  
ここでも `Execute step` を押してみましょう。今度は時間がかかりますね。  
`OUTPUT`に 「data」 というカードが現れたら `View` を押してみましょう。生成された画像が見えたら OK です。

<a href="https://gyazo.com/b6247381df2bd86bba132edac536dcc9"><img src="https://i.gyazo.com/b6247381df2bd86bba132edac536dcc9.png" alt="Image from Gyazo" width="450px"/></a>
  

## 4. Upload a file (Dropbox)
仕上げにつくった画像を Dropbox にアップロードしましょう。地味ですがここが一番難しいです。  

### Dropbox と API 連携する  
  
まず、ワークフローから移動します。
画面左上の`Personal`に移動し、`Credentials`(認証情報) タブを選択します。  
  
<a href="https://gyazo.com/6f63aa4ef7d6aff44523d2d9541b5d1b"><img src="https://i.gyazo.com/6f63aa4ef7d6aff44523d2d9541b5d1b.png" alt="Image from Gyazo" width="450px"/></a>  
  
<a href="https://gyazo.com/9b7a5e8f2755a90c0e5db93d384b6c33"><img src="https://i.gyazo.com/9b7a5e8f2755a90c0e5db93d384b6c33.png" alt="Image from Gyazo" width="450px"/></a>
  
> [!NOTE]
> 既に n8n free OpenAI API credits があると思います。もし自分のアカウントの OpenAI の API Key を使う際もこの `Credentials` から追加します。

右上の `Create credentials` から `Dropbox API` を選びましょう。  

<a href="https://gyazo.com/d8aa43e36cfd8111d370c5500dc22299"><img src="https://i.gyazo.com/d8aa43e36cfd8111d370c5500dc22299.png" alt="Image from Gyazo" width="450px"/></a>
  
**Access Token に、講義中にお知らせする値をコピーして貼り付けてください。**

その他は編集不要です。`Save` を押して保存しましょう。
「Connection tested successfully」という文字が出てきたらOKです。
  
<a href="https://gyazo.com/52d8732d5634d9699cc581a1904a96ed"><img src="https://i.gyazo.com/52d8732d5634d9699cc581a1904a96ed.png" alt="Image from Gyazo" width="450px"/></a>  
  
### ワークフロー設定の続き
Workflows タブから再び自分がつくったワークフローを開きます。
以下の箇所を設定します。 
  
<a href="https://gyazo.com/c55459bc20bcebb6c42fc0d210e74b69"><img src="https://i.gyazo.com/c55459bc20bcebb6c42fc0d210e74b69.jpg" alt="Image from Gyazo" width="450px"/></a>  

- `Credential to connect with`: 先ほど作った認証情報(「Dropbox  accout」などの名前になっていると思います)
- `File Path`: {{ '/fukui_hands-on/'+ $('Edit Fields').item.json.imageTheme +'.png'}}
- `Binary File`: オンにする(トグルスイッチ)

> [!NOTE]
> `File Path` の中身は変数が入っていて少しわかりにくいですが、「フォルダ名＋画像のテーマ+拡張子(png)」の順番になっています。

仕上げに `Execute step` を押してみましょう。`OUTPUT` に出力がでたらOKです。

<a href="https://gyazo.com/19590538b7745cc4555534f1ce92e236"><img src="https://i.gyazo.com/19590538b7745cc4555534f1ce92e236.png" alt="Image from Gyazo" width="450px"/></a>  

これで画像生成からアップロードまでの一連の流れを組むことができました。お疲れ様でした。
  
<a href="https://gyazo.com/7271729a6da2afc880313c0c9902d5ce"><img src="https://i.gyazo.com/7271729a6da2afc880313c0c9902d5ce.png" alt="Image from Gyazo" width="600px"/></a>  

皆さんがつくった画像は以下のリンクかスマホでQRコードを読んでいただくと閲覧できます。    
https://www.dropbox.com/scl/fo/gna6572rcxw2hngqjr5m5/ACxwNHwmCnhU4ReiSstdphw?rlkey=m35atup0twf1epy61kzej3vks&st=i0kxwsvu&dl=0  
  
<a href="https://gyazo.com/eba946fd03b8e2321ad60d085bb2ee7a"><img src="https://i.gyazo.com/eba946fd03b8e2321ad60d085bb2ee7a.png" alt="Image from Gyazo" width="250px"/></a>  

  
---  

# さらにつくってみたい人へ
さて、YouTube 動画の自動生成のフローをつくってみましょう。

## ノードの配置
`Generate an image` の手前のノードを切り、以下の3つを追加します。  
  
- `OpenAI` > `Generate a video`
- `Data Transformation` > `Edit Fields`
- `YouTube` > `Upload a video`

このような状態になれば OK です。
  
<a href="https://gyazo.com/f99334e90c2a927065d346e236f87356"><img src="https://i.gyazo.com/f99334e90c2a927065d346e236f87356.png" alt="Image from Gyazo" width="450px"/></a>  
  
## SORA を使うには
動画生成には SORA を使います。

https://sora.chatgpt.com/explore

残念ながら画像生成に使った `n8n free OpenAI API credits` は動画の生成に使うことができません。  
まずは OpenAI のアカウントをつくり API Key を取得します。  
アカウント作成や API Key のつくり方については、ChatGPT やインターネット記事で調べてみてください。大量に見つかるはずです。
  
<a href="https://gyazo.com/df9400ee6db597966eaba05b63e09241"><img src="https://i.gyazo.com/df9400ee6db597966eaba05b63e09241.png" alt="Image from Gyazo" width="450px"/></a>  
  
> [!WARNING]
> SORA で動画をつくる際、従量課金で費用が掛かります。そのため支払方法の登録が必要です。  
> 詳しくは[プライスリスト](https://openai.com/ja-JP/api/pricing/)を参照してください。
> <a href="https://gyazo.com/10b7c83c8d75b94f81b6fa7b897fb958"><img src="https://i.gyazo.com/10b7c83c8d75b94f81b6fa7b897fb958.png" alt="Image from Gyazo" width="400px"/></a>

API Key をコピーし n8n の認証情報に追加します。  
`Create Credentials` から　`OpenAi` を選択します。  

<a href="https://gyazo.com/5cbbd27c46df1656f9d123f5c856b544"><img src="https://i.gyazo.com/5cbbd27c46df1656f9d123f5c856b544.png" alt="Image from Gyazo" width="450px"/></a>

`API Key`に取得したキーを貼り付けて `Save` し認証情報の作成は完了です。

ワークフローに戻り、`Generate a video` を設定していきます。
- `Credential to connect with`: 先ほど作った認証情報(「OpenAi account」などの名前になっていると思います)
- `Model`: SORA-2
- `Prompt`: {{ $json.imageTheme }} (左側の Schema から `imageTheme` をドラッグ&ドロップしましょう)

`Second` (動画の時間)や `Size` はお好みで。

<a href="https://gyazo.com/66810b6dace5b519ebdbda9c4368d346"><img src="https://i.gyazo.com/66810b6dace5b519ebdbda9c4368d346.jpg" alt="Image from Gyazo" width="450px"/></a>

ここまでで `Execute step` してみましょう。画像生成よりもさらに時間がかかります。気長に待ちましょう。
`OUTPUT`にデータカードが出現したら成功です。`View` からどんな画像ができたか確かめて見ましょう。  
  
<a href="https://gyazo.com/9d907b8e1ed25b21cf10e9d4d03e2231"><img src="https://i.gyazo.com/9d907b8e1ed25b21cf10e9d4d03e2231.png" alt="Image from Gyazo" width="450px"/></a>
 
## YouTube の自動アップロード
### Edit Fields
動画投稿のためのメタデータを準備していきます。要するに YouTube をアップする際に YouTube が求めている情報やデータ形式に加工していくということです。`Edit Fields` は二度目ですね。  
  
<a href="https://gyazo.com/42b6684737e6cb787a9011c761a7c8ee"><img src="https://i.gyazo.com/42b6684737e6cb787a9011c761a7c8ee.png" alt="Image from Gyazo" width="450px"/></a>
  
`Add Field` を押して以下の3つを準備してください。
- `title`: {{ $('Edit Fields').item.json.imageTheme }} (`Edit Fields`からドラッグ&ドロップしてきます)
- `description`: {{ 'この動画はSORAがつくった「' +  $('Edit Fields').item.json.imageTheme +'」です。'}}
  - 動画の概要欄になります。今回はタイトルの内容に「この動画はSORAがつくった～」などと追記しています。
- `videoData`:
  - デフォルトのデータ形式が `String` になっていますが **`Binary`** にしてください。
  - {{ $('Generate a video').item.binary.data}}

最後の `videoData` の設定が特に重要です。

`Execute step`で確認しておきましょう。`OUTPUT` にバイナリー (Binary) データがあればOKです。

### Upload a video (YouTube)
またまた、認証情報を取得します。ここが山場です。

#### Credentials 

`Credentials` から`Create credentials`を選び、**`YouTube OAuth2 API`** を検索します。  

<a href="https://gyazo.com/325822a9ecbe88574d704713448aa20d"><img src="https://i.gyazo.com/325822a9ecbe88574d704713448aa20d.png" alt="Image from Gyazo" width="450px"/></a>  
  
必要なのは `Client ID` と `Client Secret` です。
  
<a href="https://gyazo.com/1cb0537e42d0714b7d722632fcbff125"><img src="https://i.gyazo.com/1cb0537e42d0714b7d722632fcbff125.png" alt="Image from Gyazo" width="450px"/></a>
  
この２つは GCP (Google Cloud Platform) で認証を取得します。
こちらも調べるとたくさん出てくるので調べてみてください。
[こちら](https://youtu.be/kbB2TfAQRH0?si=SuA5SI-hJ3Y3BlLL)に参考動画を用意しました。  

1. Google Cloud Console で プロジェクトを作成
2. APIs Services から OAuth を設定  
<a href="https://gyazo.com/f4444ba946cbb1c2524ab543811537ca"><img src="https://i.gyazo.com/f4444ba946cbb1c2524ab543811537ca.png" alt="Image from Gyazo" width="450px"/></a>
3. YouTube Data API (v3) を有効にする  
<a href="https://gyazo.com/40cb404766fb8b0d7cf52c9ed269a9c6"><img src="https://i.gyazo.com/40cb404766fb8b0d7cf52c9ed269a9c6.png" alt="Image from Gyazo" width="450px"/></a>
4. n8nで サインイン(Sign in with Google)  
<a href="https://gyazo.com/4532a095f64d4f48e741ebd2530802a0"><img src="https://i.gyazo.com/4532a095f64d4f48e741ebd2530802a0.png" alt="Image from Gyazo" width="450"/></a>  

`Client ID` と `Client Secret` を入れて Google アカウントでサインインして完了です。
<a href="https://gyazo.com/16e173033a2d7e71636205d3d1cafeac"><img src="https://i.gyazo.com/16e173033a2d7e71636205d3d1cafeac.png" alt="Image from Gyazo" width="450px"/></a>


#### ワークフローの設定
- `Credential to connect with`:  先ほど作った認証情報(「YouTube account」などの名前になっていると思います)
- `Title`: {{ $json.title }} (左側の Schema から `title` をドラッグ&ドロップしましょう)
- `Region Code`: Japan - JP
- `Category Name or ID`: Education
- `Input Binary Field`: videoData

`Options` でフィールドを追加します。
- `Description`：{{ $json.description } (左側の Schema から `description` をドラッグ&ドロップしましょう)
- `Privacy Status`
  - `Public`
  - 公開動画にしたくない場合は `Private` を選んでください。

これで完成です！実行してみましょう。

自身の YouTube アカウントに動画が追加されたらOKです。(n8n のワークフローが完了してから YouTube にアップされるまでに時間差があります)  
<a href="https://gyazo.com/7d91de28168e401b5e053a7fed91673e"><img src="https://i.gyazo.com/7d91de28168e401b5e053a7fed91673e.png" alt="Image from Gyazo" width="450px"/></a>




--- 

## Tips 紹介
### API Keyって？
### 自分のDropboxと連携したいとき
### n8n の AI 機能について
