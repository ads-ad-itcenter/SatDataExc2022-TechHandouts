# ワークショップ#3 コードコピー用

## 工程1

### 工程1-①-4-3

```sh
gsutil -m cp -r \
gs://sat-pbl-2022-dist/data/sentinel2_tokyo_20220412_limited \
gs://sat-pbl-2022-team-☆-general/data/sentinel2_tokyo_20220412_limited
```

### 工程1-④-3-2

```
gs://sat-pbl-2022-team-☆-general/data/sentinel2_tokyo_20220412_limited/importfile_team_☆.csv
```

## 工程2

### 工程2-②-5

```
sat-pbl-2022-team-☆-general/data/sentinel2_tokyo_20220412_limited
```

## 工程3

### 工程3-寄り道

[こちら](https://github.com/ads-ad-itcenter/SatDataExc2022-TechHandouts/blob/main/assets/workbench_example.md)を参照

### 工程3-②-2

```sh
gsutil cp \
gs://sat-pbl-2022-dist/src/frcnn_asset.zip \
.
```

### 工程3-②-3

```sh
unzip frcnn_asset.zip && \
rm frcnn_asset.zip
```
