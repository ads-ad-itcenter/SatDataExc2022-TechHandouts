# GCSコマンド例（gsutilツール）

## 一覧: `gsutil ls`

### バケットの一覧

* コマンド例1

  ```sh
  $ gsutil ls
  ```

  プロジェクトのバケットを一覧


### バケットの中身の一覧

* コマンド例1

  ```sh
  gsutil ls gs://bucket1/
  ```

  「bucket1」バケットのフォルダ・ファイルを一覧

* コマンド例2

  ```sh
  gsutil ls gs://bucket1/folder1/
  ```

  「bucket1」バケットの「folder1」フォルダ内のフォルダ・ファイルを一覧

* コマンド例3

  ```sh
  gsutil ls -r gs://bucket1/
  ```

  「bucket1」バケットの全階層のフォルダ・ファイルを一覧
