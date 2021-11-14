# Power BI Hands-on training 

## はじめてのレポートの作成

<br />

### **INDEX**

- [CSV ファイルからデータを読み込み](#CSV-ファイルからデータを読み込み)

- [レポート作成 (1)](#レポート作成-(1))

- [メジャーの作成](#メジャーの作成)

- [レポート作成 (2)](#レポート作成-(2))

- [比率を求めるメジャーの作成](#比率を求めるメジャーの作成)

- [レポート作成 (3)](#レポート作成-(3))

- [テーブルの追加](#テーブルの追加)

- [レポートの作成 (4)](#レポートの作成-(4))

<br />

### **CSV ファイルからデータを読み込み**

- Power BI Desktop を起動

- **データを取得** をクリックし、**テキスト/CSV** を選択

  <img src="images/get-data-from-text.png" />

- **顧客.csv** を選択し、**開く** をクリック

- **元のファイル**、**区切り記号**、**データ型検出** を設定し、**読み込み** をクリック

  - **元のファイル**： **65001: Unicode(UTF-8)**

  - **区切り記号**： コンマ

  - **データ型検出**： 最初の 200 行に基づく

    <img src="images/get-customer-01.png" />

- レポートのモデルにデータが追加

  <img src="images/get-customer-02.png" />

<br />

### **レポート作成 (1)**

- **視覚化** の **テーブル** をクリック

  <img src="images/get-customer-03.png" />

- **値** に **顧客名**, **性別**, **学歴**, **年代** フィールドをドラッグ＆ドロップ

  <img src="images/get-customer-04.png" />

- テーブルに選択したフィールドの情報が表示

  <img src="images/get-customer-05.png" />

<br />

### **メジャーの作成**

- 画面左の **データ**（<img src="images/icon-Table.png" width="15" />）をクリック

- **新しいメジャー** をクリック

  <img src="images/create-measure-01.png" />

- 顧客の総数を求めるメジャーを作成

  ```
  総人数 = COUNTROWS('顧客') 
  ```

- **書式設定** の **,** をクリック

  <img src="images/create-measure-02.png" />

<br />

### **レポート作成 (2)**

- 画面左の **レポート**（<img src="images/icon-Report.png" width="15" />）をクリック

- **視覚化** の **カード** をクリックし、レポートへ配置

  <img src="images/card-01.png" />

- **フィールド** に **顧客** の **総人数** をドラッグ＆ドロップ

  <img src="images/create-measure-03.png" />

- 大きさを調整し、テーブルの左へ配置

  <img src="images/create-measure-04.png" />

- **視覚化** の **マトリックス** をクリックして、レポートへ配置

  <img src="images/matrix-01.png" />

- **行**、**値** にフィールドをドラッグ＆ドロップ

  **行**： **顧客** - **性別**

  **値**： **顧客** - **総人数**

  <img src="images/create-measure-05.png" />

- 大きさを調整し、カードの下に配置

  <img src="images/create-measure-06.png" />

<br />

### **比率を求めるメジャーの作成**

- 画面左の **データ**（<img src="images/icon-Table.png" width="15" />）をクリック

- **新しいメジャー** をクリック

  <img src="images/create-measure-01.png" />

- 以下の式を入力し Enter キーを押下

  ```
  人数比 = DIVIDE([総人数], CALCULATE([総人数], REMOVEFILTERS()))
  ```

- **メジャー ツール** タブを選択

  **書式設定** の **書式** を **パーセンテージ** に設定

  <img src="images/create-measure-07.png" />

- 画面左の **レポート**（<img src="images/icon-Report.png" width="15" />）をクリック

- レポート上のマトリックスを選択

- **値** に **顧客** の **人数比** をドラッグ＆ドロップ

  <img src="images/create-measure-08.png" />

- マトリックスに人数比が表示

  <img src="images/create-measure-09.png" />

- **行** に **顧客** - **年代** をドラッグ＆ドロップ

  <img src="images/create-measure-10.png" />

- **書式**（<img src="images/icon-Format.png" width="15" />）をクリック

- **行見出し** を展開し、**階段状レイアウト** を **オフ** に設定

  <img src="images/create-measure-11.png" />

- マトリックスの「<img src="images/icon-DrillDown.png" width="15" />」をクリック

  <img src="images/create-measure-12.png" />

- 行に指定されたフィールドをドリルダウンして表示

  <img src="images/create-measure-13.png" />

- 画面左の **データ**（<img src="images/icon-Table.png" width="15" />）をクリック

- **新しいメジャー** をクリック

  <img src="images/create-measure-01.png" />

- 以下の式を入力し Enter キーを押下

  ```
  総人数 ％ 年代 = DIVIDE([総人数], CALCULATE([総人数], REMOVEFILTERS('顧客'[年代])))
  ```

- **メジャー ツール** タブを選択

  **書式設定** の **書式** を **パーセンテージ** に設定

  <img src="images/create-measure-14.png" />

- レポート上のマトリックスを選択

- **値** に **顧客** の **総人数 % 年代** をドラッグ＆ドロップ

  <img src="images/create-measure-15.png" />

- 性別の年代比が表示

  <img src="images/create-measure-16.png" />

- 画面左の **データ**（<img src="images/icon-Table.png" width="15" />）をクリック

- **新しいメジャー** をクリック

  <img src="images/create-measure-01.png" />

- 以下２つのメジャーを作成

  ```
  総人数 % 性別 = DIVIDE([総人数], CALCULATE([総人数], REMOVEFILTERS('顧客'[性別]))) 
  ```

  ※ 性別フィルターを除外した比率

  ```
  総人数 % 学歴 = DIVIDE([総人数], CALCULATE([総人数], REMOVEFILTERS('顧客'[学歴]))) 
  ```

  ※ 学歴フィルターを除外した比率

- **メジャー ツール** タブの書式設定で作成したメジャーの書式を **パーセンテージ** に設定

  <img src="images/create-measure-17.png" />

- 画面左の **モデル**（<img src="images/icon-Model.png" width="15" />）をクリック

  <img src="images/create-measure-18.png" />

- 画面右のフィールド欄で作成した５つのメジャーを選択

  <img src="images/create-measure-19.png" />

- **プロパティ** の **フォルダーの表示** に **メジャー** と入力

  <img src="images/create-measure-20.png" />

  ※論理的にフィールドをグループ化

- 画面右のフィールド欄で作成した **年齢** と **顧客ID** を選択

- **プロパティ** の **非表示** を **はい** に設定

  <img src="images/create-measure-21.png" />

  ※レポート作成に使用しないフィールドを非表示に設定

<br />

### **レポート作成 (3)**

- 画面左の **レポート**（<img src="images/icon-Report.png" width="15" />）をクリック

- **視覚化** の **マトリックス** をクリックして、レポートへ配置

  <img src="images/matrix-01.png" />

- **行**、**値** にフィールドをドラッグ＆ドロップ

  - **行**： **顧客** - **性別**, **学歴**

  - **値**： **顧客** - **総人数**, **総人数 % 学歴**, **人数比**

  <img src="images/create-measure-22.png" />

- **書式**（<img src="images/icon-Format.png" width="15" />）をクリック

- **行見出し** を展開し、**階段状レイアウト** を **オフ** に設定

  <img src="images/create-measure-11.png" />

- マトリックスの「<img src="images/icon-DrillDown.png" width="15" />」をクリック

- 行に指定されたフィールドをドリルダウンして表示

  <img src="images/create-measure-23.png" />

- ここまでの操作で作成したレポート

  <img src="images/create-measure-24.png" />

-  テーブルをクリックして選択

- **視覚化** の **複数の行カード** をクリック

  <img src="images/multi-card-01.png" />

- テーブルからカードへ変更

  <img src="images/create-measure-25.png" />

- マトリックス上のフィールドをクリックすると、レポート上の各視覚化コンポーネントにフィルターが適用

  <img src="images/create-measure-26.png" />

<br />

### **テーブルの追加**

- **ホーム** タブの **データの変換** をクリック

  <img src="images/edit-data-01.png" />

- Power Query エディターが起動

- **新しいソース** をクリックし **Excel ブック** を選択

  <img src="images/get-data-from-text-2.png" />

- **売上データ.csv** を選択し **開く** をクリック

- **元のファイル**、**区切り記号**、**データ型の検出** を確認し、**OK** をクリック

  - **元のファイル**： **65001: Unicode (UTF-8)**

  - **区切り記号**： コンマ

  - **データ型の検出**： 最初の 200 行に基づく

    <img src="images/get-sales-data-01.png" />

- 同様の操作で **商品.csv** へ接続

  - **元のファイル**： **65001: Unicode (UTF-8)**

  - **区切り記号**： コンマ

  - **データ型検出**： 最初の 200 行に基づく

    <img src="images/get-product-data.png" />

- ** ホーム** タブの **閉じて適用** をクリック

  レポートへデータを読み込み

- 画面左の **モデル**（<img src="images/icon-Model.png" width="15" />）をクリック

- **売上データ** と **顧客**, **商品** テーブルが関連付けられていることを確認

  <img src="images/model-sales-01.png" />

  ※同名の列がある場合は、自動的にリレーション シップを作成

- 画面左の **データ**（<img src="images/icon-Table.png" width="15" />）をクリック

- 画面左のフィールドで **売上データ** - **売上** を選択

  <img src="images/model-sales-02.png" />

- **書式** を **通貨** に変更 

  <img src="images/model-sales-03.png" />

- ＄ 左の矢印をクリックし **￥ 日本語 (日本)** を選択

  <img src="images/model-sales-04.png" />

- **テーブル ツール** タブを選択し、**新しいメジャー** をクリック

  <img src="images/model-sales-06.png" />

- SUM 関数を使用し売上合計のメジャーを作成

  ```
  売上合計 = SUM('売上データ'[売上]) 
  ```

- **書式** を **通貨** に設、**通貨単位** を **￥ 日本語 (日本)** に設定

  <img src="images/model-sales-07.png" />

- 同様の手順で **数量** メジャーを作成

  ```
  数量 = COUNTROWS('売上データ') 
  ```

- 書式設定で **,** をクリックし、３桁区切り記号のコンマをつけて表示するよう設定

  <img src="images/model-sales-08.png" />

<br />

### **レポートの作成 (4)**

- 画面左の **レポート**（<img src="images/icon-Report.png" width="15" />）をクリック

- 画面したの「＋」をクリックし、ページを追加

  <img src="images/create-new-page-01.png" />

- **視覚化** の **カード** をクリックし、レポートへ配置

  <img src="images/card-01.png" />

- **フィールド** へ **売上データ** - **売上合計** をドラッグ＆ドロップ

  <img src="images/report-4-01.png" />

- **書式**（<img src="images/icon-Format.png" width="15" />）をクリック

- **データ ラベル** を展開し **表示単位** を **千** に設定

  <img src="images/report-4-02.png" />

- **視覚化** の **カード** をクリックし、レポートへ配置

- **フィールド** へ **売上データ** - **数量** をドラッグ＆ドロップ

  <img src="images/report-4-03.png" />

- **書式**（<img src="images/icon-Format.png" width="15" />）をクリック

- **データ ラベル** を展開し **表示単位** を **なし** に設定

  <img src="images/report-4-04.png" />

- 大きさを調整し、画面左上に並べて表示

  <img src="images/report-4-05.png" />

- 視覚化の **スライサー** をクリックして配置

  <img src="images/create-slicer-01.png" />

- フィールドに **商品** の **カテゴリ** をドラッグ＆ドロップ

  <img src="images/report-4-06.png" />

- **全般** を展開し **方向** を **横** に設定

  <img src="images/create-slicer-03.png" />

- 大きさを調整し、カードの左側に配置

  <img src="images/report-4-07.png" />

- 視覚化の **スライサー** をクリックして配置

  <img src="images/create-slicer-01.png" />

- フィールドに **売上データ** の **日付の階層** - **年** をドラッグ＆ドロップ

  <img src="images/report-4-08.png" />

- 大きさを調整し、先の手順で作成したスライサーの左に配置

  <img src="images/report-4-09.png" />
