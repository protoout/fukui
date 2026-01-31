# 事前準備
## n8n のアカウント作成をお願いいたします
**n8n (エヌエイトエヌ)** は様々なサービス同士をつないで自分で自動化ツールを作成することができるサービスです。  
イメージはこんな感じ。
  
<a href="https://gyazo.com/fe60c3c17874b585da86d4416f037297"><img src="https://i.gyazo.com/fe60c3c17874b585da86d4416f037297.png" alt="Image from Gyazo" width="450px"/></a>
  
このサービスの詳細は講義で紹介しますので、まずはアカウントをつくってみましょう。
  
> [!TIP]
> n8n にはクラウド版とローカルホスト版があります。  
> 今回使うのはクラウド版です。本来は[最安プラン](https://n8n.io/pricing/)で20ユーロ/月の費用が掛かりますが、今回はトライアル期間を使って無料で利用します。トライアル期間が過ぎても自動で有料プランに移行することはないのでご安心ください (クレジットカード登録もしません)。
> 
> ローカルホストとは、ソースコードが入ったプロジェクトを自分の PC やサーバー上にインストールし使うことを指します。技術的にややハードルが高い方法です。  
> クラウド版と同様に AI を稼働させる費用は掛かりますが、ライセンスは無料で使用することができます。参考までに、この資料の最後にローカルホストするためのプロジェクトデータのリンクを載せておきます。

---

## 手順  ( 所要時間：8分 )

**1. 以下のリンクから `Get started` に進みましょう**

https://n8n.io/

右上にボタンがあります。  
<a href="https://gyazo.com/e8f6c39a959d6dcb8bc85d2ae8b9e77e"><img src="https://i.gyazo.com/e8f6c39a959d6dcb8bc85d2ae8b9e77e.png" alt="Image from Gyazo" width="450px"/></a>

> [!NOTE]
> もし`Sign in` を選んでしまった場合は `Start a free trial` に進んでください。

<a href="https://gyazo.com/cd7358db86590e64d35575a05a6ada74"><img src="https://i.gyazo.com/cd7358db86590e64d35575a05a6ada74.png" alt="Image from Gyazo" width="450px"/></a>

**2. メールアドレスの登録**

Company e-mail を要求されますが普段使っているメールアドレスで大丈夫です。  
  
<a href="https://gyazo.com/dc24782a1c8db15200bcfa78510d1814"><img src="https://i.gyazo.com/dc24782a1c8db15200bcfa78510d1814.png" alt="Image from Gyazo" width="450px"/></a>  

入力したメールアドレス宛てに送られるコードを入力するか、メールに記載のリンク (`Verify my email`) にアクセスし検証を完了します。
  
<a href="https://gyazo.com/dba322e85fcfaf5aa992019e225d06a5"><img src="https://i.gyazo.com/dba322e85fcfaf5aa992019e225d06a5.jpg" alt="Image from Gyazo" width="450px"/></a>
  
**3. ユーザー名などを入れていきます**

任意のユーザー名(Full name)、パスワード、アカウント名を入力して、`Start free 14-day trial` に進みます。  
※アカウント名は既に誰かが使っている場合、入力をし直すよう指示があります。その際は別の名前にしてください。  
  
<a href="https://gyazo.com/f84193f0fcaf9a7c0c4449816ed4c742"><img src="https://i.gyazo.com/f84193f0fcaf9a7c0c4449816ed4c742.png" alt="Image from Gyazo" width="450px"/></a>

> [!IMPORTANT]
> アカウント名、パスワード、メールアドレスはサインイン時に使うので、手元に控えておいてください。
  
**4. あとはアンケートに回答すればOKです**
  
簡単なアンケートに答えます。    
  
<a href="https://gyazo.com/a136d5aaea3b6f4372ee035a3f960221"><img src="https://i.gyazo.com/a136d5aaea3b6f4372ee035a3f960221.png" alt="Image from Gyazo" width="450px"/></a>
  
回答例は以下の通りです。  
- What is the size of your company?: Only me
- What team are you on?: Support
- Have you built something yourself in the past ?: Not yet
- Which of these do you feel comfortable doing?: Writing JavaScript functions
- How did you hear about n8n?: Google

最後にチームをワークスペースに招待するかを聞かれますが、`Skip`で問題ありません
  
<a href="https://gyazo.com/fc1109b42cc6450fa7b42c12f410c070"><img src="https://i.gyazo.com/fc1109b42cc6450fa7b42c12f410c070.png" alt="Image from Gyazo" width="450px"/></a>

**5. これでアカウント作成は完了です**

英語ですが[チュートリアル動画](https://youtu.be/4cQWJViybAQ?si=UwpnnRzyUWSk-VXN)もあるので、気になる方はチェックしてください。
  
<a href="https://gyazo.com/b4539523a7f08eb2563e6a7a5a97638c"><img src="https://i.gyazo.com/b4539523a7f08eb2563e6a7a5a97638c.png" alt="Image from Gyazo" width="450px"/></a>

`Start automating` で進みましょう。このような画面になればOKです。  
<a href="https://gyazo.com/c50fc53c1d1f238d0f57046444968511"><img src="https://i.gyazo.com/c50fc53c1d1f238d0f57046444968511.png" alt="Image from Gyazo" width="450px"/></a>

これで登録は終了です。お疲れまでした。

---

## 参考  

- ローカルホスト版の環境をつくるための GitHub プロジェクト

https://github.com/n8n-io/self-hosted-ai-starter-kit

ソースコードがおいてあるだけでなく、やり方も丁寧に紹介されています。本格的に使う際はこちらを使うのがおすすめです。

---
