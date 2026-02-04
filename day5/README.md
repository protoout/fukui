# n8n を使って自動化ツールの開発に挑戦してみよう
特に海外で人気のあるワークフロー自動化ツール、n8n (エヌエイトエヌ) を使って、"フローグラマー(Flowgrammer)"に挑戦してみましょう。
今回は、動画作成から YouTube へのアップロードまでを自動化する方法を紹介します。

## 今日つくるもの
こんなワークフローをつくります。
「全体の画像」

> [!IMPORTANT]
> 今回の講義では以下の点を変更して実装します。完全版をつくるためのフローは資料で紹介しているので是非チャレンジしてみてください。
> - 動画生成 (Sora) → 画像生成 (DALL・E)
> - YouTube へのアップロード → Dropbox へのアップロード

## 目的
あなたが Gmail や Slack などのツール同士を連携させたいとき、どのようなイメージが沸くでしょうか？  
世界中で人気の高い自動化ツール n8n に触れ、ツールを連携させるための勘所を学びましょう。

---

# 準備の確認

以下にアクセスしてアカウント名を入力してサインインしてください。

https://app.n8n.cloud/login

アカウントがない場合やアカウント名が誤っている場合は以下のように表示されます。このようになってしまう方は教えて下さい。
「Errorの画像」

# n8n とは？
n8n はオープンソースのワークフロー自動化ツールです。プログラミング不要で、視覚的に Google Sheets や Slack、メール、データベース、生成 AI など普段使っているツール同士をつなげて面倒な作業を自動化できるソフトウェアです。  
パズルのようにツールをつなげられるサービスと考えてください。  

## 特徴
- 利用できるサービスが豊富
約8千ものテンプレートが用意されているので普段使っている主要なサービスは連携できると思います。
参考:  
  - [こちら](https://n8n.io/workflows/)から自分が知っているサービスを検索してみましょう。
  - [こちら](https://n8n.io/integrations/)からどのような自動化ができるかを調べることもできます。

- セルフホスト
[事前準備の資料](https://github.com/protoout/fukui-day4-5/blob/main/day5/preparation.md#n8n-%E3%81%AE%E3%82%A2%E3%82%AB%E3%82%A6%E3%83%B3%E3%83%88%E4%BD%9C%E6%88%90%E3%82%92%E3%81%8A%E9%A1%98%E3%81%84%E3%81%84%E3%81%9F%E3%81%97%E3%81%BE%E3%81%99)にも記載しましたが、自身のPC(ローカル)の環境やサーバー環境に構築し使用することができます。今回はクラウド版を利用しますが、組織で使う際など、セルフホストできる点が n8n を利用する大きなメリットです。


> [!NOTE]
> あと、英語ですが頑張っていきましょう！

# 実装

## まずはノードを並べる
このような完成図を目指します。まずは細かい編集はせずに必要なノードを並べていきます。
  
**1. n8n Form**
初めは `Add first Step` を選び右側の検索バーからノードを探します。  
まずはユーザーが入力するフォームを作成します。
「Form」と入力し、`n8n Form` から `On new n8n Form event` を選択しフォームをつくりましょう。
できたら、色々と入力する画面が出てきますが「×」で閉じます。

> [!NOTE]
> 一番初めに置くノードをトリガーと言い、他にも「9時になったら」「データがアップロードされたら」「メールが来たら」など様々な条件を起点にすることができます。  

**2. Data Transformation**
続いて、フォームに入力されたデータを加工するノードを準備します。
今つくったノードの右側の「＋」を押してフローをつなげることができます。
「＋」を押して、`Data Transformation`(既に候補に出てきていると思います) から `Edit Fields` を選択します。

**3. OpenAI**
続いて、加工したデータを生成 AI に渡します。
ノードをつなげて、`OpenAI` から `Generate an image` を選びます。

> [!NOTE]
> 動画を生成するときは `Generate a video` を選びます。

**4. Dropbox**  
最後です。  
`Dropbox` から `Upload a file` を選択します。

> [!NOTE]
> これ以外にも Google Drive や YouTube など様々なサービスにデータをアップロードできます。

ひとまず必要なものは揃いました。ではそれぞれを設定していきましょう。

---

## 1. On form submission (On new n8n Form event) 
ノードをダブルクリックすると詳細を編集する画面が立ち上がります。  

編集する部分を以下に記載します。
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
ここで画面上部の `Execute step` もしくは画面左側の `Execute Previous nodes` を押してみましょう。ワークフローが実行されて先ほど作成したフォームが別のフォームが立ちあがります。何か入力して `Submit` しましょう。
すると`imageTheme`、`submittedAt`、`form Mode`という名前の3つの変数が出来上がります。これらを真ん中の`Drag input fields here or Add Field`に順々にドラッグ&ドロップしましょう。
  
> [!NOTE]
> 途中であってもワークフローの実行(`Execute workflow`や`Execute step`)は積極的に行って問題ありません。
> 前のノードでつくったものをドラッグ&ドロップで使えるほか、直前のノードまでどのようなデータが来ているかを確認することができるので、どんどん実行しましょう。

それぞれ、`{{ $json.imageTheme }}`のような値が入ります。

もう一度 `Execute step` を押してみましょう。右側の `OUTPUT` に3つの値が入っていればOKです。

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
  
ここでも `Execute step` を押してみましょう。今度は時間がかかりますね。  
`OUTPUT`に 「data」 というカードが現れたら `View` を押してみましょう。生成された画像が見えたら OK です。


## 4. Upload a file (Dropbox)
仕上げにつくった画像を Dropbox にアップロードしましょう。地味ですがここが一番難しいです。  

### Dropbox と API 連携する
まず、ワークフローから移動します。
画面左上の`Personal`に移動し、`Credentials`(認証情報) タブを選択します。

> [!NOTE]
> 既に n8n free OpenAI API credits があると思います。もし自分のアカウントの OpenAI の API Key を使う際もこの `Credentials` から追加します。

右上の `Create credentials` から `Dropbox API` を選びましょう。
**Access Token に、講義中にお知らせする値をコピーして貼り付けてください。**

その他は編集不要です。`Save` を押して保存しましょう。
「Connection tested successfully」という文字が出てきたらOKです。

### ワークフロー設定の続き
Workflows タブから再び自分がつくったワークフローを開きます。
以下の箇所を設定します。

- `Credential to connect with`: 先ほど作った認証情報(「Dropbox  accout」などの名前になっていると思います)
- `File Path`: {{ '/fukui_hands-on/'+ $('Edit Fields').item.json.imageTheme +'.png'}}
- `Binary File`: オンにする(トグルスイッチ)

> [!NOTE]
> `File Path` の中身は変数が入っていて少しわかりにくいですが、「フォルダ名＋画像のテーマ+拡張子(png)」の順番になっています。

仕上げに `Execute step` を押してみましょう。`OUTPUT` に出力がでたらOKです。

これで画像生成からアップロードまでの一連の流れを組むことができました。お疲れ様でした。

---  

# さらにつくってみたい人へ
さて、YouTube 動画の自動生成のフローをつくってみましょう。

## ノードの配置
`Generate an image` の手前のノードを切り、以下の3つを追加します。
- `OpenAI` > `Generate a video`
- `Data Transformation` > `Edit Fields`
- `YouTube` > `Upload a video`

このような状態になれば OK です。

## SORA を使うには
動画生成には SORA を使います。

https://sora.chatgpt.com/explore

残念ながら画像生成に使った `n8n free OpenAI API credits` は動画の生成に使うことができません。  
まずは OpenAI のアカウントをつくり API Key を取得します。  
アカウント作成や API Key のつくり方については、ChatGPT やインターネット記事で調べてみてください。大量に見つかるはずです。

> [!WARNING]
> SORA で動画をつくる際、従量課金で費用が掛かります。詳しくは[プライスリスト](https://openai.com/ja-JP/api/pricing/)を参照してください。

API Key をコピーし n8n の認証情報に追加します。  
`Create Credentials` から　`OpenAi` を選択します。  
`API Key`に先ほど取得したキーを貼り付けて `Save` し認証情報の作成は完了です。

ワークフローに戻り、`Generate a video` を設定していきます。
- `Credential to connect with`: 先ほど作った認証情報(「OpenAi account」などの名前になっていると思います)
- `Model`: SORA-2
- `Prompt`: {{ $json.imageTheme }} (左側の Schema から `imageTheme` をドラッグ&ドロップしましょう)

`Second` (動画の時間)や `Size` はお好みで。

ここまでで `Execute step` してみましょう。画像生成よりもさらに時間がかかります。気長に待ちましょう。
`OUTPUT`にデータカードが出現したら成功です。`View` からどんな画像ができたか確かめて見ましょう。
 
## YouTube の自動アップロード
### Edit Fields
動画投稿のためのメタデータを準備していきます。要するに YouTube をアップする際に YouTube が求めている情報やデータ形式に加工していくということです。

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
必要なのは `Client ID` と `Client Secret` です。

この２つは GCP (Google Cloud Platform) で認証を取得します。
こちらも調べるとたくさん出てくるので調べてみてください。
[こちら](https://youtu.be/kbB2TfAQRH0?si=SuA5SI-hJ3Y3BlLL)に参考動画を用意しました。  

1. Google Cloud Console で プロジェクトを作成
2. APIs Services から OAuth を設定
3. YouTube Data API (v3) を有効にする
4. n8nで サインイン(Sign in with Google)

#### ワークフローの設定
- `Credential to connect with`:  先ほど作った認証情報(「YouTube account」などの名前になっていると思います)
- `Title`: {{ $json.title }} (左側の Schema から `title` をドラッグ&ドロップしましょう)
- `Region Code`: Japan - JP
- `Input Binary Field`: videoData

`Options` でフィールドを追加します。
- `Description`：{{ $json.description } (左側の Schema から `description` をドラッグ&ドロップしましょう)
- `Privacy Status`
  - `Public`
  - 公開動画にしたくない場合は `Private` を選んでください。

これで完成です！実行してみましょう。

  <img width="1741" height="533" alt="image" src="https://github.com/user-attachments/assets/95b15b45-1c95-48b4-a431-c9aa2000e401" />



--- 

## Tips
### API Keyって？
### 自分のDropboxと連携したいとき
### n8n の AI 機能について
