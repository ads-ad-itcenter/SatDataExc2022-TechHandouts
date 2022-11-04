# GCSプログラム例（Python + google-cloud-storageライブラリ）

## ダウンロード

* プログラム例1
  ```py
  from google.cloud import storage

  storage_client = storage.Client()

  bucket_name = "bucket1"
  src_path    = "folder1/sample1.txt"
  dst_path    = "sample1.txt"

  bucket = storage_client.bucket(bucket_name)
  blob = bucket.blob(src_path)
  blob.download_to_filename(dst_path)
  ```

  「bucket1」バケットの「folder1/sample1.txt」ファイルを、ローカルに「sample1.txt」ファイルとしてダウンロード


## アップロード

* プログラム例1
  ```py
  from google.cloud import storage

  storage_client = storage.Client()

  src_path    = "sample1.txt"
  bucket_name = "bucket1"
  dst_path    = "folder2/sample1.txt"

  bucket = storage_client.bucket(bucket_name)
  blob = bucket.blob(dst_path)
  blob.upload_from_filename(src_path)
  ```

  ローカルの「sample1.txt」 ファイルを、「bucket1」バケットの「folder2/sample1.txt」ファイルとしてアップロード


## その他、参考資料

* [Cloud Storage / Cloud Storage client libraries # Python | Google Cloud公式](https://cloud.google.com/storage/docs/reference/libraries#client-libraries-install-python)
* [google-cloud-storage | PyPI](https://pypi.org/project/google-cloud-storage/)

