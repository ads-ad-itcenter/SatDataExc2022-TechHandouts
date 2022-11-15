# ワークショップ#4 ハンズオン2-1 の準備作業

作業環境（Vertex AI Workbenchのノートブック環境など）に、サンプルソース・データをダウンロードする

## サンプルソースをダウンロード

ターミナルにて、以下のコマンドを実行

```sh
wget https://raw.githubusercontent.com/ads-ad-itcenter/SatDataExc2022-TechHandouts/main/assets/use_vertex_ai_endpoint_sample.ipynb
```

## サンプルデータをダウンロード

ターミナルにて、以下のコマンドを実行

※複数行(3行)ありますが、一度に全てを実行してください
```sh
gsutil cp \
gs://sat-pbl-2022-dist/data/ws4_test_data.zip \
.
```
→ バケットからサンプルデータをダウンロード

※複数行(2行)ありますが、一度に全てを実行してください
```sh
unzip ws4_test_data.zip && \
rm ws4_test_data.zip
```
→ ダウンロードしたzipファイルを解凍し、不要になったzipファイルは削除
