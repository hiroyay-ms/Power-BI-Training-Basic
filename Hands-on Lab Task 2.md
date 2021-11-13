# Power BI Hands-on training

## オープンデータを使用したレポートの作成

<br />

### **INDEX**

- [オープンデータの取得](#オープンデータの取得)

- [CSV ファイルからデータを読み込み](#CSV-ファイルからデータを読み込み)

- [レポートの作成（1）](#レポートの作成（1）)

- [Excel ファイルからデータを取得](#Excel-ファイルからデータを取得)

- [日付テーブルの作成](#日付テーブルの作成)

- [データ モデリング](#データ-モデリング)

- [レポートの作成（2）](#レポートの作成（2）)

<br />

### **オープンデータの取得**

- [厚生労働省](#https://www.mhlw.go.jp/stf/covid-19/open-data.html) のサイトへアクセス

- **新規陽性者数の推移（日別）** をクリックし、CSV ファイルをダウンロード

<br />

### **CSV ファイルからデータを読み込み**

- Power BI Desktop を起動

- **データを取得** をクリックし、**テキスト/CSV** を選択

  <img src="images/get-data-from-text.png" />

- ダウンロードした **newly_confirmed_cases_daily.csv** を選択し **開く** をクリック

- 文字コード、区切り記号、データ型検出の値を確認し、**データ変の換** をクリック

  - **元のファイル**： **65001: Unicode (UTF-8)**

  - **区切り記号**： **コンマ**

  - **データ型検出**： 最初の 200 行に基づく

    <img src="images/get-open-data-01.png" />

- Power Query エディターが起動

  <img src="images/get-open-data-02.png" />

- **Prefecture** 列の「**▼**」をクリック

- **ALL** のチェックをし **OK** をクリック

  <img src="images/get-open-data-03.png" />

- 行った操作が **適用したステップ** に記録されることを確認

  <img src="images/get-open-data-04.png" />

  ※ 次回以降もデータ読み込み時に同様の操作を実行

- **閉じて適用** をクリック

  <img src="images/get-open-data-05.png" />

- データを読み込み

  画面右のフィールドに取得したデータが表示

  <img src="images/get-open-data-06.png" />

<br />

### **レポートの作成（1）**

- **視覚化** の **折れ線グラフ** をクリックしてレポートに配置

  <img src="images/create-line-chart-02.png" />

- **軸** に **Date**, **値** に **Newly confirmed cases** をフィールドからドラッグ＆ドロップ

  <img src="images/create-line-chart-02.png" />

- 折れ線グラフが画面の半分くらいの大きさとなるよう、幅と高さを調整

  <img src="images/create-line-chart-03.png" />

- 「<img src="images/icon-DrillDown.png" width="15" />」を３回クリックし、軸を日までドリルダウン

  <img src="images/create-line-chart-04.png" />

- レポートの空白部分をクリック

  **視覚化** の **集合横棒グラフ** をクリックしてレポートに配置

  <img src="images/create-bar-chart-01.png" />

- **軸** に **Prefecture**, **値** に **Newly confirmed cases** をフィールドからドラッグ＆ドロップ

  <img src="images/create-bar-chart-02.png" />

  <img src="images/create-bar-chart-03.png" />

- ページ1 の完成

  <img src="images/create-bar-chart-04.png" />

<br />

### **Excel ファイルからデータを取得**

- **ホーム** タブの **データの変換** をクリック

  <img src="images/edit-data-01.png" />

- Power Query エディターが起動

- **新しいソース** をクリックし **Excel ブック** を選択

  <img src="images/get-data-from-excel-2.png" />

- **都道府県.xlsx** を選択し **開く** をクリック

- ナビゲーター ダイアログで **都道府県マスタ** をチェックし、**OK** をクリック

  <img src="images/get-prefecture-master-01.png" />

- **クエリ** に **都道府県マスタ** が追加

  <img src="images/get-prefecture-master-02.png" />

- **行の削除** をクリックし **上位の行の削除** を選択

  <img src="images/get-prefecture-master-03.png" />

- 行数に **2** を入力し **OK** をクリック

  <img src="images/get-prefecture-master-04.png" />

- 不要な２行が削除

  <img src="images/get-prefecture-master-05.png" />

- **都道府県別地方一覧** 列を選択し、**列の削除** - **列の削除** をクリック

  <img src="images/get-prefecture-master-06.png" />

- **１行目をヘッダーとして使用** をクリック

  <img src="images/get-prefecture-master-07.png" />

- **No** 列を選択

  **変換** タブの **名前の変更** をクリック

  <img src="images/get-prefecture-master-08.png" />

- 列名を **地方区分No** に変更

  <img src="images/get-prefecture-master-09.png" />

- **Ctrl** キーを押しながら **地方区分No** と **地方区分** 列を選択

  **フィル** をクリックし **下** を選択

  <img src="images/get-prefecture-master-10.png" />

- null 値が上の行の値で埋められることを確認

  <img src="images/get-prefecture-master-11.png" />

- **列の追加** タブの **インデックス列** をクリックし **１から** を選択

  <img src="images/get-prefecture-master-12.png" />

- インデックス列を選択したまま **変換** タブの **名前の変更** をクリック

- 列名を **都道府県No** に変更

  <img src="images/get-prefecture-master-13.png" />

- **都道府県No** 列をドラッグし、１番左へ移動

  <img src="images/get-prefecture-master-14.png" />

- **適用したステップ** に、ここまでの操作内容が記録

  <img src="images/get-prefecture-master-15.png" />

- **ホーム** タブの **閉じて適用** をクリック

  <img src="images/get-prefecture-master-16.png" />

- データがファイルから読み込まれ、レポートへ追加

  <img src="images/get-prefecture-master-17.png" />

<br />

### **日付テーブルの作成**

- 画面左の **データ**（<img src="images/icon-Table.png" width="15" />）をクリック

- **新しいテーブル** をクリック

  <img src="images/create-calendar-01.png" />

- **CALENDAR** 関数を入力し **日付マスタ** テーブルを作成

  ```
  日付マスタ = CALENDAR("2020/1/1", "2021/12/31")
  ```

  <img src="images/create-calendar-02.png" />

- 指定した日付が入力された Date 列を持つテーブルが完成

  <img src="images/create-calendar-03.png" />

- **新しい列** をクリック

  <img src="images/create-calendar-04.png" />

- **YEAR** 関数を使用し「年」列を作成

  ```
  年 = YEAR('日付マスタ'[Date]) & "年" 
  ```

  <img src="images/create-calendar-05.png" />

- **年** 列が追加

  <img src="images/create-calendar-06.png" />

- 同様の手順で以下の列を作成

  - 「月」列

    ```
    月 = FORMAT('日付マスタ'[Date], "MM月")
    ```

  - 「曜日No」列

    ```
    曜日No = WEEKDAY('日付マスタ'[Date])
    ```

  - 「曜日」列

    ```
    曜日 = SWITCH(WEEKDAY('日付マスタ'[Date]), 1, "日曜日", 2, "月曜日", 3, "火曜日", 4, "水曜日", 5, "木彫日", 6, "金曜日", "土曜日")
    ```

  - 「半期No」列

    ```
    半期No = IF(MONTH('日付マスタ'[Date]) < 7, 1, 2)
    ```

  - 「半期」列

    ```
    半期 = IF(MONTH('日付マスタ'[Date]) < 7, "上半期", "下半期") 
    ```

  - 列を追加後のテーブル

    <img src="images/create-calendar-07.png" />

- **曜日** 列を選択

  **列の並び替え** をクリックし**曜日No** を選択

  <img src="images/create-calendar-08.png" />

- 同様の手順で **半期** 列を選択

  **列の並び替え** をクリックし **半期No** を選択

  <img src="images/create-calendar-09.png" />

- **テーブル ツール** タブを選択

  **日付テーブルとしてマークする** をクリックし **日付テーブルとしてマークする** を選択

  <img src="images/create-calendar-10.png" />

- **日付列** に **Date** を選択し **OK** をクリック

  <img src="images/create-calendar-11.png" />

<br />

### **データ モデリング**

- **都道府県マスタ** を選択

- **都道府県区分** 列を選択

  **列の並び替え** をクリックし **都道府県No** を選択

  <img src="images/create-calendar-12.png" />

- **地方区分** 列を選択

  **列の並び替え** をクリックし **地方区分No** を選択

  <img src="images/create-calendar-13.png" />

- **newly_confirmed_cases_daily** を選択

- **新しいメジャー** をクリック

  <img src="images/create-calendar-14.png" />

- 合計を算出する **Total** を作成

  ```
  Total = SUM('newly_confirmed_cases_daily'[Newly confirmed cases])
  ```

- 再度 **新しいメジャー** をクリックし、前月比を算出する **MoM%** メジャーを作成

  ```
  MoM% = DIVIDE('newly_confirmed_cases_daily'[Total], CALCULATE('newly_confirmed_cases_daily'[Total], DATEADD('日付マスタ'[Date], -1, MONTH))) - 1
  ```

- **書式設定** で **,（カンマ）** をクリック

  <img src="images/create-calendar-15.png" />

- 画面左の **モデル**（<img src="images/icon-Model.png" width="15" />）をクリック

- レポートに含まれるテーブルが表示

  <img src="images/model-covid-01.png" />

  ※ newly_confirmed_cases_daily テーブルと都道府県マスタの間にリレーションが設定されていることを確認

  ※ データ読み込み時に同名列を自動的に関連付け

- **日付マスタ** の **Date** 列を **newly_confirmed_cases_daily** テーブルの **Date** 列へドラッグ＆ドロップ

- newly_confirmed_cases_daily テーブルと日付マスタ間にリレーションが作成

  <img src="images/model-covid-02.png" />

- テーブル間のリレーションは **リレーションシップの管理** からも管理（作成/削除）が可能

  <img src="images/model-covid-03.png" />

<br />

### **レポートの作成（2）**

- 画面左の **レポート**（<img src="images/icon-Report.png" width="15" />）をクリック

- 画面したの「＋」をクリックし、ページを追加

  <img src="images/create-new-page-01.png" />

- 視覚化の **スライサー** をクリックして配置

  <img src="images/create-slicer-01.png" />

- フィールドに **都道府県マスタ** の **地方区分** をドラッグ＆ドロップ

  <img src="images/create-new-page-02.png" />

- **書式**（<img src="images/icon-Format.png" width="15" />）をクリック

  **全般** を展開し **方向** を **横** に設定

  <img src="images/create-slicer-03.png" />

- 幅、高さを調整

  <img src="images/create-new-page-03.png" />

- **書式**（<img src="images/icon-Format.png" width="15" />）をクリック

- **項目** を展開し、**フォントの色**、**背景** を任意の色に設定

  <img src="images/create-new-page-04.png" />

  <img src="images/create-new-page-05.png" />

  ※ 例：フォントの色：白、背景：テーマの色 2（#12239E）に設定

  - **表示** タブの **テーマ** から全体のデザインを変更することも可

    <img src="images/create-new-page-06.png" />

- **視覚化** の **カード** をクリックし、レポートへ配置

  <img src="images/card-01.png" />

- **フィールド** に **newly_confirmed_cases_daily** の **Total** をドラッグ＆ドロップ

  <img src="images/card-02.png" />

- **書式**（<img src="images/icon-Format.png" width="15" />）をクリック

- **データ ラベル** を展開し、**表示単位** を **なし** に設定

  <img src="images/card-03.png" />

- 大きさを調整し、スライサーの右に配置

  <img src="images/card-04.png" />

- **視覚化** の **マップ** をクリックし、レポートへ配置

  <img src="images/map-01.png" />

- **場所** と **サイズ** にフィールドをドラッグ＆ドロップ

  場所： **都道府県マスタ** - **都道府県区分**

  サイズ： **newly_confirmed_cases_daily** - **Total**

  <img src="images/map-02.png" />

- **書式**（<img src="images/icon-Format.png" width="15" />）をクリック

- **データの色** を展開し、任意の色に設定

  <img src="images/map-03.png" />

  ※ テーマの色 5（#E044A7）に設定

- 大きさを調整し、スライサーの下に配置

  <img src="images/map-04.png" />

- **視覚化** の **積み上げ面グラフ** をクリックし、レポートへ配置

  <img src="images/area-chart-01.png" />

- **軸**、**凡例**、**値** にフィールドをドラッグ＆ドロップ

  **軸**： **日付マスタ** - **月**

  **凡例**： **日付マスタ** - **年**

  **値**： **newly_confirmed_cases_daily** - **Total**

  <img src="images/area-chart-02.png" />

- 積み上げ面グラフの左上にある **...** をクリック

  **軸の並べ替え** をクリックし **月** を選択

  <img src="images/area-chart-03.png" />

- 同様の手順で **軸の並べ替え** をクリックし **昇順で並べ替え** を選択

- 大きさを調整しマップの横に配置

  <img src="images/area-chart-04.png" />

- **視覚化** の **積み上げ法グラフ** をクリックして、レポートへ配置

  <img src="images/column-chart-01.png" />

- **軸**、**値** にフィールドをドラッグ＆ドロップ

  **軸**： **日付マスタ** - **曜日**

  **値**： **newly_confirmed_cases_daily** - **Total**

  <img src="images/column-chart-02.png" />

- 大きさを調整し、カードの下に配置

  <img src="images/column-chart-03.png" />

- **視覚化** の **マトリックス** をクリックして、レポートへ配置

  <img src="images/matrix-01.png" />

- **行**、**列**、**値** にフィールドをドラッグ＆ドロップ

  **行**： **日付マスタ** - **月**

  **列**： **日付マスタ** - **年**

  **値**： **newly_confirmed_cases_daily** - **Total**, **MoM%**

  <img src="images/matrix-02.png" />

- **書式**（<img src="images/icon-Format.png" width="15" />）をクリック

- **小計** を展開し、**行の小計**、**列の小計** を **オフ** に設定

  <img src="images/matrix-03.png" />

- **条件付き書式** を展開

  **Total** を選択し **背景色** を **オン** に設定

  <img src="images/matrix-04.png" />

- 同様の手順で **MoM%** の **背景色** を **オン** に設定

  <img src="images/matrix-05.png" />

- 大きさを調整し、積み上げ縦棒グラフの下に配置

  <img src="images/matrix-06.png" />

- スライサーで任意の項目を選択

  マップ、グラフ、マトリックスにフィルター処理が適用されることを確認

  <img src="images/matrix-07.png" />

- ファイル メニューで名前を付けて保存を実行し、終了
