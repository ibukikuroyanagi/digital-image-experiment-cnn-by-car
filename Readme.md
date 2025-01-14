* windows10 64bit version 1909 (OSビルド 18363.476)
* python 3.7.3
* keras 2.3.1

### このリポジトリのデータはkaggleの ```carvana-image-masking-challenge``` からデータを取得しています。
全ての画像データを取得したい場合はkaggleのアカウントを作成し、 ```carvana-image-masking-challenge``` コンペから```metadata.csv, train.zip, test.zip```を取得してください。


一部のデータで十分であるならば、  
```git clone https://github.com/ibukikuroyanagi/digital-image-experiment-cnn-by-car.git ```   
で問題ありません。  

本コードの解説は [僕のブログ](https://ibuki-study.net/keras1) にしています。  
是非、参考にしてみてしてください！  



## 使用にあたって
* ファイル番号順に実行をしていくことですべてのコードを実行することが可能です。
* git cloneによってダウンロードされた方は、その時点でファイル3以降のコードから実行することが可能です。
* ファイル1, ファイル2はselected_picturesディレクトリ作成のためのコードなので、データの前処理をどのように行っているのかを確認したい方は実行をしてみて下さい。

macOSで実行する場合は、コードの最初に
```os.environ['KMP_DUPLICATE_LIB_OK']='True'```
こちらを加える必要がある場合があります。


### picturesディレクトリについて
kaggle competitionからダウンロードした車の画像データ(train.zip, test.zip)を一つのディレクトリに合体させたもののこと。

### selected_picturesディレクトリについて
400クラス分類のモデルを作成するための、大量のデータで学習をする際にのみ用いる。  
データが巨大なためCPUでは実行を終えることが困難である。そのため、GPUを使用できる場合にのみ使用をすすめる。  
なお本チュートリアルでは使用していない。

### mini_picturesディレクトリについて
データの基本となるディレクトリ。
基本的に全てのコードはこのディレクトリがあれば実行が可能。  
小さいデータセットでの学習をするために作成する。  
このサイズでもCPUでは学習に５～６時間要するので実行には注意が必要である。  

### ImageDataGeneratorの扱いについて
画像をバッチで学習を進めて行くにあたり、画像フォルダの配置に注意をしなければならない。  
ImageDataGeneratorはディレクトリ名を参照し自動でone-hotラベルを付与するからである。  
以下のように配置することで、正解ラベルを生成せずとも自動で認識をしてくれる。  
* 注意 pythonコードでディレクトリ生成を行うと大文字と小文字の区別がされず「すでにフォルダが生成されています」といったエラーが出される場合があるので、前処理としてラベル名が大文字と小文字で一致するものがないようにする。  


├─mini_pictures  
│  ├─test  
│  │  ├─Audi-a3  
│  │  ├─Audi-a5  
│  │  ├─Audi-q5  
│  │  ├─BMW-1-series  
│  │  ├─BMW-4-series  
│  │  ├─BMW-x3  
│  │  ├─Honda-pilot  
│  │  ├─Jeep-wrangler  
│  │  ├─Mazda-mazda5  
│  │  ├─Mercedes-Benz-gla  
│  │  ├─Mercedes-Benz-glk  
│  │  ├─MINI-clubman  
│  │  ├─MINI-countryman  
│  │  ├─Mitsubishi-outlander  
│  │  ├─Nissan-370z  
│  │  ├─Nissan-quest  
│  │  ├─Nissan-rogue-select  
│  │  ├─Subaru-outback  
│  │  ├─Toyota-tacoma  
│  │  └─Volkswagen-cc  
│  ├─train  
│  │  ├─Audi-a3  
│  │  ├─Audi-a5   
│  │  ├─Audi-q5  
│  │  ├─BMW-1-series  
│  │  ├─BMW-4-series  
│  │  ├─BMW-x3  
│  │  ├─Honda-pilot  
│  │  ├─Jeep-wrangler  
│  │  ├─Mazda-mazda5  
│  │  ├─Mercedes-Benz-gla  
│  │  ├─Mercedes-Benz-glk  
│  │  ├─MINI-clubman  
│  │  ├─MINI-countryman  
│  │  ├─Mitsubishi-outlander  
│  │  ├─Nissan-370z  
│  │  ├─Nissan-quest  
│  │  ├─Nissan-rogue-select  
│  │  ├─Subaru-outback  
│  │  ├─Toyota-tacoma  
│  │  └─Volkswagen-cc  
│  └─valid  
│      ├─Audi-a3  
│      ├─Audi-a5  
│      ├─Audi-q5  
│      ├─BMW-1-series  
│      ├─BMW-4-series  
│      ├─BMW-x3  
│      ├─Honda-pilot  
│      ├─Jeep-wrangler  
│      ├─Mazda-mazda5  
│      ├─Mercedes-Benz-gla  
│      ├─Mercedes-Benz-glk  
│      ├─MINI-clubman  
│      ├─MINI-countryman  
│      ├─Mitsubishi-outlander  
│      ├─Nissan-370z  
│      ├─Nissan-quest  
│      ├─Nissan-rogue-select  
│      ├─Subaru-outback  
│      ├─Toyota-tacoma  
│      └─Volkswagen-cc  