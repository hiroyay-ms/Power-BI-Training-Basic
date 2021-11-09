# Power BI Hands-on training

## Power BI Desktop での Cognitive Services の利用

<br />

### **INDEX**
- [CSV ファイルからデータを取得](#CSV-ファイルからデータを取得)

- [Power BI ビジュアルの追加](#Power-BI-ビジュアルの追加)

- [ワード クラウドの作成](#ワード-クラウドの作成)

- [Cognitive Services の Text Analytics を使用したキーフレーズ抽出](#Cognitive-Services-の-Text-Analytics-を使用したキーフレーズ抽出)

- [レポートの完成](#レポートの完成)

<br />

### **CSV ファイルからデータを取得**

- Power BI Desktop を起動

- **データを取得** - **テキスト/CSV** をクリック

  <img src="images/get-data-from-text.png" />

- **reviews.xlsx** を選択し **開く** をクリック

- ナビゲーター画面が表示

  **テーブル1** を選択し、**読み込み** をクリック

  <img src="images/get-review-01.png" />

- データにテーブル1が追加

  <img src="images/get-review-02.png" />

<br />

### **Power BI ビジュアルの追加**

- 視覚化の **...** をクリックし、**その他のビジュアルを取得** を選択

  <img src="images/install-custom-visual-02.png" />

- Power BI のビジュアル画面が表示

  画面右上の検索ボックスに **word cloud** と入力

  フィルター処理された結果から **Word Cloud** をクリック

  <img src="images/install-custom-visual-03.png" />

- **今すぐ入手** をクリック

  <img src="images/install-custom-visual-04.png" />

- **正常にインポートされました** の通知が表示されるので **OK** をクリック

  <img src="images/install-custom-visual-05.png" />

- 視覚化に Word Cloud のアイコンが追加されることを確認

  <img src="images/install-custom-visual-06.png" />

<br />

### **ワード クラウドの作成**

- 視覚化で追加した Word Cloud のアイコンをクリック

  <img src="images/word-cloud-01.png" />

- フィールドから **テーブル1** の **Comment** を **カテゴリ** へドラッグ＆ドロップ

  <img src="images/word-cloud-02.png" />

- レポート上で Word Cloud の高さ、幅を調整

  <img src="images/word-cloud-03.png" />

  ※文章内の単語を可視化（頻出する単語ほど大きく表示）
  ※意味のない単語が多く含まれていることを確認

### **Cognitive Services の言語サービスを使用したキーフレーズ抽出**

- **ホーム** タブの **データの変換** をクリック

  <img src="images/edit-data-01.png" />

- Power Query エディターが起動

- **新しいソース** をクリックし **空のクエリ** を選択

  <img src="images/create-new-query-01.png" />

- 名前を **KyePhrases** に変更

  <img src="images/create-new-query-02.png" />

- **ホーム** タブの **詳細エディター** をクリック

  <img src="images/create-new-query-03.png" />

- 詳細エディターに以下のコードを貼り付け

  ```
  (text) => let
      apikey      = "<YOUR_API_KEY>",
      endpoint    = "https://<YOUR_CUSTOM_DOMAIN>/text/analytics/v3.0/keyPhrases",
      jsontext    = Text.FromBinary(Json.FromValue(Text.Start(Text.Trim(text), 5000))),
      jsonbody    = "{ documents: [ { language: ""en"", id: ""0"", text: " & jsontext & " } ] }",
      bytesbody   = Text.ToBinary(jsonbody),
      headers     = [#"Ocp-Apim-Subscription-Key" = apikey],
      bytesresp   = Web.Contents(endpoint, [Headers=headers, Content=bytesbody]),
      jsonresp    = Json.Document(bytesresp),
      keyphrases  = Text.Lower(Text.Combine(jsonresp[documents]{0}[keyPhrases], ", "))
  in  keyphrases
  ```

  <img src="images/create-new-query-04.png" />

  ※ **<YOUR_API_KEY>** と **<YOUR_CUSTOM_DOMAIN>** 使用する言語サービスのキーとエンドポイントへ変更

  <img src="images/cognitive-services-key.png" />

  ※ キーとエンドポイントは Azure ポータルより取得

- **完了** をクリック

- 画面左のクエリから **テーブル1** を選択

  <img src="images/create-merge-column-01.png" />

- **Ctr** キーを押しながら **Subject** 列と **Comment** 列をクリックし選択

  **列の追加** タブの **列のマージ** をクリック

  <img src="images/create-merge-column-02.png" />

- **区切り記号** と **新しい列名** を入力し **OK** をクリック

  - **区切り記号**： **タブ**

  - **新しい列名**： **Merged**

    <img src="images/create-merge-column-03.png" />

- Merged 列が追加

  <img src="images/create-merge-column-04.png" />

- **カスタム関数の呼び出し** をクリック

  <img src="images/call-custom-functions-01.png" />

- **関数クエリ** で **KeyPhrases** を選択

  **text** に **Merged** 列を選択し **OK** をクリック

  <img src="images/call-custom-functions-02.png" />

  - 「接続方法を指定してください」のバナーが表示された場合は、**資格情報の編集** ボタンをクリック

    <img src="images/call-custom-functions-03.png" />

  - **Web コンテンツへのアクセス** ダイアログで **匿名** を選択し **接続** をクリック

    <img src="images/call-custom-functions-04.png" />

  - 「データのプライバシーに関する情報が必要です」のバナーが表示された場合は **続行** ボタンをクリック

    <img src="images/call-custom-functions-05.png" />

  - ダイアログ内の各データソースに対して **パブリック** を選択し **保存** をクリック
  <img src="images/call-custom-functions-06.png" />

- **ホーム** タブの **閉じて適用** をクリック

  <img src="images/call-custom-functions-07.png" />

- レポートにデータを読み込み

- Word Cloud の **カテゴリ** から Comment を削除

  **テーブル1** の **KeyPhrases** を **カテゴリ** にドラッグ＆ドロップ

  <img src="images/word-cloud-04.png" />

- 頻出単語が変更されることを確認

  <img src="images/word-cloud-05.png" />

<br />

### ****Cognitive Services の言語サービスを使用した感情分析**

- **ホーム** タブの **データの変換** をクリック

  <img src="images/edit-data-01.png" />

- Power Query エディターが起動

- **新しいソース** をクリックし **空のクエリ** を選択

  <img src="images/create-new-query-01.png" />

- 名前を **Sentiment** に変更

  <img src="images/sentiment-query-01.png" />

- **ホーム** タブの **詳細エディター** をクリック

  <img src="images/sentiment-query-02.png" />

- 詳細エディターに以下のコードを貼り付け

  ```
  (text) => let
      apikey = "<YOUR_API_KEY>",
      endpoint = "https://<YOUR_CUSTOM_DOMAIN>" & "/text/analytics/v3.1/sentiment",
      jsontext = Text.FromBinary(Json.FromValue(Text.Start(Text.Trim(text), 5000))),
    　jsonbody = "{ documents: [ { language: ""en"", id: ""0"", text: " & jsontext & " } ] }",
    　bytesbody = Text.ToBinary(jsonbody),
    　headers = [#"Ocp-Apim-Subscription-Key" = apikey],
    　bytesresp = Web.Contents(endpoint, [Headers=headers, Content=bytesbody]),
    　jsonresp = Json.Document(bytesresp),
    　sentiment   = jsonresp[documents]{0}[sentiment] 
    　in sentiment
  ```

  <img src="images/sentiment-query-03.png" />

  ※ **<YOUR_API_KEY>** と **<YOUR_CUSTOM_DOMAIN>** 使用する言語サービスのキーとエンドポイントへ変更

- **カスタム関数の呼び出し** をクリック

  <img src="images/call-custom-functions-01.png" />

- **カスタム関数の呼び出し** ダイアログで以下の設定を行い **OK** をクリック

  - **新しい列名**： **SentimentScore**

  - **関数クエリ**： **Sentiment**

  - **text**： **Merged**

    <img src="images/sentiment-query-04.png" />

- **ホーム** タブの **閉じて適用** をクリック

  <img src="images/call-custom-functions-07.png" />

- レポートにデータを読み込み

- 画面左のデータ（<img src="images/icon-Table.png" width="15" />）をクリック

- **新しいメジャー** をクリック

  <img src="images/create-new-measure-01.png" />

- 以下の式を入力

  ```
  Number of Reviews = COUNTROWS('テーブル1')
  ```

  <img src="images/create-new-measure-02.png" />

- **Enter** キーを押下し、メジャーを作成

  <img src="images/create-new-measure-03.png" />

- 画面左のレポート（<img src="images/icon-Report.png" width="15" />）をクリック

- 視覚化の **積み上げ縦棒グラフ** をクリックして配置

  <img src="images/create-column-chart-01.png" />

- 積み上げ縦棒グラフのフィールドを設定

  - **軸**： **日**

  - **値**： **Numer or Reviews**

  <img src="images/create-column-chart-02.png" />

  <img src="images/create-column-chart-03.png" />

- **凡例** に **SentimentScore** をドラッグ＆ドロップ

  <img src="images/create-column-chart-04.png" />

  <img src="images/create-column-chart-05.png" />

<br />

### **レポートの完成**

- Word Cloud, 積み上げ縦棒グラフの高さを調整し、画面上部に空白を作成

  <img src="images/ai-report-01.png" />

- 視覚化の **スライサー** をクリックして配置

  <img src="images/create-slicer-01.png" />

- フィールドに **Hotel** をドラッグ＆ドロップ

  <img src="images/create-slicer-02.png" />

- **書式**（<img src="images/icon-Format.png" width="15" />）をクリック

  **全般** を展開し **方向** を **横** に設定

  <img src="images/create-slicer-03.png" />

- スライサーの高さ、幅を調整

  <img src="images/ai-report-02.png" />

- スライサーの項目を選択

  Word Cloud, 積み上げ縦棒グラフの双方にフィルター処理が適用されることを確認

  <img src="images/ai-report-03.png" />

- Word Cloud のフォーカス モード（<img src="images/icon-Focus.png" width="15" />）をクリック

  <img src="images/ai-report-04.png" />

  ※ Word Cloud が拡大して表示されることを確認

- **ファイル** メニューの **名前を付けて保存** を選択し、ファイルを保存
