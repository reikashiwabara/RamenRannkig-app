# RamenRanking - Weather-Based Ramen Recommendation

## 概要
「天気deラーメン」は、その日の天気に合わせてラーメン店をランキング形式でおすすめするアプリケーションです。気象庁の天気情報と食べログの店舗データを活用し、暑い日にはあっさり系（塩ラーメンなど）、寒い日にはこってり系（濃厚ラーメンなど）を優先的に提案します。

このリポジトリには、Google Colab上で動作するデータ処理部分のコードが含まれています。

## 機能
1. **データ取得**: 気象庁の天気情報と食べログのラーメン店舗データをCSVファイルとしてGoogle Driveから読み込み。
2. **データ処理**: 天気に応じて店舗の評価値を調整（例: くもりであっさり系+0.5、雨や雪でこってり系+0.5）。
3. **ランキング生成**: 評価値に基づいてラーメン店をソートし、新しいランキングを作成。
4. **出力**: 結果をGoogle DriveにCSVファイルとして保存。

## 使用技術
- **Python**: データ処理とスクレイピング
- **pandas**: CSVデータの操作
- **Google Colab**: 実行環境
- **Google Drive**: データの入出力

## セットアップ
1. Google Colabでこのノートブックを開きます。
2. Google Driveをマウントするために、`drive.mount('/content/drive')`を実行。
3. 以下の入力ファイルをGoogle Driveの指定フォルダ（`/content/drive/MyDrive/project_assari_share/`）に配置:
   - `example_assari.csv`: 食べログの店舗データ
   - `weather_data.csv`: 気象庁の天気データ

## 入力データ形式
- **`weather_data.csv`**  

- 列: 店舗名、評価値（5段階）、食べログURL

## コードの流れ
1. **Google Driveのマウントとデータ読み込み**  
 - `pandas`を使用してCSVファイルを読み込み、データフレームとリストに変換。
2. **ラーメンの分類**  
 - 店舗名ごとにあっさり系（1）かこってり系（2）を定義した辞書を使用。
3. **評価値の調整**  
 - 天気に応じて評価値を変更する関数`adjust_ramen_ratings`を実行。
4. **ランキングのソート**  
 - 調整後の評価値でリストを降順にソート。
5. **結果の保存**  
 - ソート済みのデータを`analysis_data.csv`としてGoogle Driveに保存。

## サンプル出力
- 入力例:  
- 天気: `くもり`  
- 店舗: `まほろば` (評価値: 3.25, カテゴリ: あっさり系)  
- 処理後: 評価値が3.25 → 3.75に上昇  
- 最終ランキングがCSVに保存されます。

## 注意点
- CSVファイルのパスは環境に合わせて調整してください。
- 店舗のカテゴリが辞書に定義されていない場合、デフォルトで`0`（調整なし）となります。
