# Prompt Bridge V2 & Manager V3

**Prompt Bridge V2** は，VS Code 上で選択したソースコードに対して，定型プロンプトを付加して AI アシスタント（Roo Code 等）へシームレスに送信するための拡張機能です．
併随する **Manager V3** を使用することで，ネットワーク接続のないクローズド環境でも，自身の業務に最適化したカスタム拡張機能を自在にビルド・配布することが可能です．

---

## 1. Prompt Bridge V2 (VS Code 拡張機能)

エディタ上の右クリックメニューから，あらかじめ定義された 3 種類のプロンプトを即座に実行できます．

### 主な機能

* **AI アシスタント連携**: インストール済みの Roo Code (Cline) を自動検出し，API 経由でプロンプトを直接送信します．
* **オフライン対応**: Roo Code が未検出の場合でも，プロンプトとコードを結合したテキストを自動的にクリップボードへコピーします．

**設定の柔軟性**: インストール後，VS Code の設定画面（`promptBridgeV2.customPrompt1-3`）からプロンプトの内容を直接編集できます ．



### 標準搭載プロンプト

1. **PB1: コード解説**: 概要，処理フロー，キーポイント，補足の 4 構成でロジックを詳細に解説します ．


2. **PB2: テスト観点**: 正常・異常・境界値を含むテスト項目をマークダウンの表形式で抽出します ．


3. **PB3: CDI レビュー**: 信頼性・保守性・効率性の観点からコードを厳格に査読し，修正案を提示します ．



---

## 2. Prompt Bridge V2 Manager V3 (ビルドツール)

`prompt-bridge-manager-v3.html` は，自分専用の `Prompt Bridge V2` を作成するためのバニラ JS（HTML5）製マネージャーです ．

### 活用メリット

* **ノーコード・ビルド**: ブラウザ上でメニュー名や初期プロンプトを入力するだけで，複雑なエスケープ処理済みの PowerShell コマンドを生成します ．


* **クローズド環境への最適化**: インターネットに接続できない環境へ持ち込むための `.vsix` パッケージを，指定したディレクトリへ直接ビルド・出力します ．


* **ビルド・プロセスの自動化**: `package.json` および `extension.js` の生成から，`vsce` によるパッケージングまでをワンライナーで実行します ．



---

## 3. クローズド環境での導入手順

### 搬入資材リスト（オフライン環境用）

インターネット接続がない環境では，依存関係をすべて事前にパッケージ化して持ち込む必要があります． 以下の資産を準備してください．

#### (1) 必須ソフトウェア（インストーラ）

* **VS Code 本体**: Windows用 System Installer (x64) の最新版． 


* **Node.js 本体**: Windows用 `.msi` インストーラ (LTS推奨，v20系以上)． 



#### (2) 拡張機能パッケージ (.vsix)

* **Prompt Bridge V2 本体**: `prompt-bridge-v2-2.2.0.vsix`． 


* **Roo Code (Cline)**: 連携先となる `RooVeterinaryInc.roo-cline` の `.vsix` ファイル． 



#### (3) ビルドツールおよび関連資産

* **Prompt Bridge Manager V3**: `prompt-bridge-manager-v3.html`． 


* **ビルドツール**: `vsce` 等を含む `node_modules` 資産一式（外部で `npm install` 済みのプロジェクトフォルダごと持ち込むか，バイナリ化したもの）． 



---

### 環境構築および導入フロー

搬入後のセットアップ手順です． 

#### (1) インフラストラクチャの設置

1. **Node.js のインストール**: インストーラを実行し，コマンドプロンプトで `node -v` が動作することを確認します． 


2. **VS Code のインストール**: 通常のセットアップを行います． 



#### (2) 基盤拡張機能の導入

1. VS Code を起動し，「VSIXからインストール」を使用して **Roo Code** を先にインストールします． 


* これにより，Prompt Bridge からの API 送信先が確保されます． 





### 3. Prompt Bridge V2 の個別最適化（Manager使用）

1. クローズド環境内で `prompt-bridge-manager-v3.html` をブラウザで開きます． 


2. 現場の特性に合わせてプロンプト内容を微調整します． 


3. 
**[Windows用ビルドコマンド生成]** を実行し，出力されたコマンドを PowerShell で実行して，その場で最新の `.vsix` を生成します． 


* これにより，環境に最適化された最新版が作成されます． 





### 4. 最終インストールと動作確認

1. 生成された最新の `.vsix` をインストールします． 


2. 右クリックメニューの **[Prompt Bridge]** から AI（Roo Code）へテキストが転送されることを確認します． 



---
### INFO  Files included in the VSIX:
prompt-bridge-v2-2.1.0.vsix

├─ [Content_Types].xml

├─ extension.vsixmanifest

└─ extension/

   ├─ extension.js [1.85 KB]
   
   ├─ package.json [2.92 KB]
   
   ├─ prompt-bridge-manager-v3.html [13.73 KB]
   
   └─ OLD/
   
      ├─ extension.js [1.79 KB]
      
      └─ package.json [2.92 KB]


---

## 4. 仕様情報

* **Extension ID**: `prompt-bridge-v2` 


* **Version**: 2.2.0 


* **Publisher**: takasoft 


* **Requirements**: VS Code ^1.74.0 以上 



---

**Next Step**:
この `README.md` をプロジェクトのルートディレクトリに配置しますか？ また， Manager V3 の UI デザインや生成されるプロンプトのさらなる調整が必要であればお知らせください．
