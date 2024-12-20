MMVC_Trainer
===
AIを使ったリアルタイムボイスチェンジャーのモデル学習用ツール

## Description
AIを使ったリアルタイムボイスチェンジャー「MMVC(RealTime-Many to Many Voice Conversion)」 で使用するモデルを学習するためのリポジトリです。  
Google Colaboratory (Google Colab) を用いることで、個人の環境に依存せず、かつ簡単に機械学習の学習フェーズを実行可能です。  

## Concept
「簡単」「だれでも」「好きな声に」「リアルタイムで」 

## Demo
v1.3.0.0は制作中だそうだ。
[v1.2.0.0](https://www.nicovideo.jp/watch/sm40386035)   

## ライセンス
[LICENSE](https://github.com/AIITScience/MMVC_Trainer/blob/main/LICENSE.md)

## Requirement
・Google アカウント

## セットアップ
2つのパターンがあります。
### アプリを頼る!!
アプリを頼れば、簡単にセットアップできます!!
1. [![Static Badge](https://img.shields.io/badge/%E3%82%A2%E3%83%97%E3%83%AA%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB-green)](https://github.com/AIITScience/MMVC_Trainer/releases)
2. アプリの指示に従って自分のGoogle Drive上にインストールしてください。
### アプリなんかに頼らねえ!!
#### Ph1. 自分の音声の録音と音声データの配置 及びターゲット音声データの配置
1. このリポジトリをクローンします。
   - [![image](https://github.com/user-attachments/assets/d2c17268-174d-4a5c-8964-5716884019bd)](http://colab.research.google.com/github/isletennos/MMVC_Trainer/blob/main/notebook/00_Clone_Repo.ipynb)(アプリではこちらを利用しています)→この場合、Googleドライブがディレクトリです。
   - gitを使ってクローンします。→この場合、クローンされた場所がディレクトリです。
2. 自分の声の音声データを録音します。方法:  
    - notebookディレクトリにある「00_Rec_Voice.ipynb」から自分の音声を録音します。(アプリではこちらを利用しています)
    - 自分のPCで録音してGoogle Drive上に配置します。[特別感謝のコーパス](https://github.com/AIITScience/MMVC_Trainer/blob/main/README.md#special-thanks%E3%82%B3%E3%83%BC%E3%83%91%E3%82%B9)や[MMVC用にテキストを分割したITAコーパス](https://drive.google.com/file/d/14oXoQqLxRkP8NJK8qMYGee1_q2uEED1z/view?usp=sharing)を台本にし、100文程度読み上げます。また、録音した音声は**24000Hz 16bit 1ch**である必要があります。
3. 録音した自分の声の音声データとその音声データに対応するテキスト、変換したい声の音声データとその音声データに対応するテキストを用意します。この時、用意する音声(自分の声の音声データ/変換したい声の音声データ共に)は**24000Hz 16bit 1ch**を強く推奨しております。
4. 下記のようなディレクトリ構成になるように音声データとテキストデータを配置します。  
    - textfulの直下には2ディレクトリになります。
    - 「00_Clone_Repo.ipynb」を利用した場合はこのように配置されていますのでそのままで大丈夫です。 
    (1205_zundamonディレクトリはずんだもんの音声データなのでずんだもん以外の声の場合無くても問題ありません)  
```
dataset
├── textful
│   ├── 00_myvoice
│   │   ├── text
│   │   │   ├── emoNormal_001.txt
│   │   │   ├── emoNormal_002.txt
│   │   │   ├── ...
│   │   └── wav
│   │        ├── emoNormal_001.wav
│   │        ├── emoNormal_002.wav
│   │        ├── ...
│   │── 01_target
│   │   ├── text
│   │   └── wav
│   │
│   └── 1205_zundamon
│       ├── text
│       │   ├── emoNormal_001.txt
│       │   ├── emoNormal_002.txt
│       │   ├── ...
│       └── wav
│            ├── emoNormal_001.wav
│            ├── emoNormal_002.wav
│            ├── ... 
│        
└── textless
```
#### Ph2. モデルの学習方法
1. 事前学習済みデータを配置します。  
    - 「00_Clone_Repo.ipynb」を利用しなかった場合や「fine_model」ディレクトリに下記ファイルが存在しなかった場合、以下の手順でファイルを配置してください。
        1. [「G_v13_20231020.pth」「D_v13_20231020.pth」をダウンロード](https://huggingface.co/MMVC/prelearned-model/tree/main)。
        2. 「G_v13_20231020.pth」「D_v13_20231020.pth」を「fine_model」ディレクトリに配置します。**(良く忘れるポイントなので要注意！)**  
2. notebookディレクトリにある「01_Create_Configfile.ipynb」をGoogle Colab 上で実行、学習に必要なconfigファイルを作成します。
3. configsに作成されたtrain_config.jsonの    
      - "eval_interval"  
        modelを保存する間隔です。
      - "batch_size"  
        colabで割り当てたGPUに合わせて調整してください。
    上記2項目を環境に応じて最適化してください。わからない方はそのままで大丈夫です。  
4. notebookディレクトリにある「02_Train_MMVC.ipynb」をgoogle colab 上で実行してください。 logs/にモデルが生成されます。
#### Ph3. 学習したモデルの性能検証
notebookディレクトリにある「03_MMVC_Interface.ipynb」をgoogle colab 上で実行してください。  

## MMVC_Client
### プロジェクトによるMMVC Client
[MMVCを実際に動かすClient software](https://github.com/isletennos/MMVC_Client)  

### 有志によるMMVC Client
[Voice Changer Trainer and Player](https://github.com/w-okada/voice-changer)  

様々な環境でMMVCを動かすように作成されたClient software。  

- 動作確認状況

| #   | os            | middle   | トレーニングアプリ | ボイスチェンジャー             |
| --- | ------------- | -------- | ------------------ | ------------------------------ |
| 1   | Windows       | Anaconda | 未                 | 未                             |
| 2   | Windows(WSL2) | Docker   | wsl2+ubuntuで確認  | wsl2+ubuntuで確認              |
| 3   | Windows(WSL2) | Anaconda | 未                 | ubuntuで確認                   |
| 4   | Mac(Intel)    | Anaconda | 未                 | 動作するが激重。(2019, corei5) |
| 5   | Mac(M1)       | Anaconda | 未                 | M1 MBA, M1 MBPで確認           |
| 6   | Linux         | Docker   | debianで確認       | debianで確認                   |
| 7   | Linux         | Anaconda | 未                 | 未                             |
| 8   | Colab         | Notebook | 確認済み           | 確認済み                       |


ある程度最近のものであればCPUでの稼働も可能です(i7-9700Kで実績あり。下記デモ参照)。  

- デモ動画
[Docker環境(GPU) デモ](https://twitter.com/DannadoriYellow/status/1588115075587768326?s=20&t=f-sduXYzrq2sCdOpjKbUjg), [Docker環境(CPU)デモ](https://twitter.com/DannadoriYellow/status/1588317790502801409?s=20&t=f-sduXYzrq2sCdOpjKbUjg), [Colab環境デモ](https://youtu.be/TogfMzXH1T0)  

## 有志によるチュートリアル動画
### v1.2.1.x
| 前準備編        | [ニコニコ動画](https://www.nicovideo.jp/watch/sm40415108) | [YouTube](https://www.youtube.com/watch?v=gq1Hpn5CARw&ab_channel=popi) |
| :-------------- | :-------------------------------------------------------- | :--------------------------------------------------------------------- |
| 要修正音声      | [ニコニコ動画](https://www.nicovideo.jp/watch/sm40420683) | [YouTube](https://youtu.be/NgzC7Nuk6gg)                                |
| 前準備編2       | [ニコニコ動画](https://www.nicovideo.jp/watch/sm40445164) | [YouTube](https://youtu.be/m4Jew7sTs9w)                                |
| 学習編_前1      | [ニコニコ動画](https://www.nicovideo.jp/watch/sm40467662) | [YouTube](https://youtu.be/HRSPEy2jUvg)                                |
| 学習編_前2      | [ニコニコ動画](https://www.nicovideo.jp/watch/sm40473168) | [YouTube](https://youtu.be/zQW59vrOSuA)                                |
| 学習編_後       | [ニコニコ動画](https://www.nicovideo.jp/watch/sm40490554) | [YouTube](https://www.youtube.com/watch?v=uB3YfdKzo-g&ab_channel=popi) |
| リアルタイム編  | [ニコニコ動画](https://www.nicovideo.jp/watch/sm40415108) | [YouTube](https://youtu.be/Al5DFCvKLFA)                                |
| 質問編          | [ニコニコ動画](https://www.nicovideo.jp/watch/sm40599514) | [YouTube](https://youtu.be/aGBcqu5M6-c)                                |
| 応用編_九州そら | [ニコニコ動画](https://www.nicovideo.jp/watch/sm40647601) | [YouTube](https://youtu.be/MEXKZoHVd-A)                                |
| 応用編_音街ウナ | [ニコニコ動画](https://www.nicovideo.jp/watch/sm40714406) | [YouTube](https://youtu.be/JDMlRz-PkSE)                                |

## Q&A
[FAQ](https://github.com/isletennos/MMVC_Trainer/wiki/FAQ)をご参考ください。  

## MMVCコミュニティサーバ(discord)
本家の開発の最新情報や、不明点のお問合せ、MMVCの活用法など[MMVCに関するコミュニティサーバ](https://discord.gg/2MGysH3QpD)です。    

## MMVC開発者問い合わせ(PIXIV FANBOX)
MMVCに関する疑問・質問等の本家の開発者への問い合わせは[PIXIV FANBOX](https://mmvc.fanbox.cc/posts/6858033)で受け付けています。  

## Special thanks(コーパス類)
- [JVS (Japanese versatile speech) corpus](https://sites.google.com/site/shinnosuketakamichi/research-topics/jvs_corpus)  
  contributors : 高道 慎之介様/三井 健太郎様/齋藤 佑樹様/郡山 知樹様/丹治 尚子様/猿渡 洋様     
- [ITAコーパス マルチモーダルデータベース](https://zunko.jp/multimodal_dev/login.php)  
  contributors : 金井郁也様/千葉隆壱様/齊藤剛史様/森勢将雅様/小口純矢様/能勢隆様/尾上真惟子様/小田恭央様  
  CharacterVoice : 東北イタコ(木戸衣吹様)/ずんだもん(伊藤ゆいな様)/四国めたん(田中小雪様)/九州そら(西田望見)     
- [つくよみちゃんコーパス](https://tyc.rei-yumesaki.net/material/corpus/)  
  contributor : 夢前黎様  
  CharacterVoice : つくよみちゃん(夢前黎様)     

## 本家が参考したもの
[Conditional Variational Autoencoder with Adversarial Learning for End-to-End Text-to-Speech](https://arxiv.org/abs/2106.06103)  
[vits](https://github.com/jaywalnut310/vits)  

## 本家のREADMEの著者
[Isle Tennos Twitter](https://twitter.com/IsleTennos)  

---
このファイルは、[本家のREADME](https://github.com/isletennos/MMVC_Trainer/blob/main/README.md)を一部編集したものです。
