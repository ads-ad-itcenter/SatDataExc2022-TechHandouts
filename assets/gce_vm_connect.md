# GCE仮想マシンへの接続(ssh)、ファイル転送(scp)

Google Cloud CLI (gcloudコマンド) を利用して、接続(ssh)、ファイル転送(scp)

## 接続: `gcloud compute ssh`

* コマンド例1:
  ```sh
  gcloud compute ssh --zone "us-central1-a" "instance-1" --project "project-a"
  ```
  `project-a` プロジェクトの `us-central1-a` ゾーンの `instance-1`インスタンス(仮想マシン)にSSH接続


## ファイル転送: `gcloud compute scp`

### アップロード

* コマンド例1:

  ```sh
  gcloud compute scp sample1.txt instance-1:~ --zone "us-central1-a" --project "project-a"
  ```
  - ローカルの `sample1.txt` ファイルを
  - `project-a` プロジェクトの `us-central1-a` ゾーンの `instance-1`インスタンス(仮想マシン)の
  - `~` （ホームディレクトリ）にアップロード

* コマンド例2:
  ```sh
  gcloud compute scp -r folder1 instance-1:~ --zone "us-central1-a" --project "project-a"
  ```
  - ローカルの `folder1` フォルダを
  - `project-a` プロジェクトの `us-central1-a` ゾーンの `instance-1` インスタンス(仮想マシン)の
  - `~` （ホームディレクトリ）にアップロード

### ダウンロード

* コマンド例1: 
  ```sh
  gcloud compute scp instance-1:~/sample2.txt ~  --zone "us-central1-a" --project "project-a"
  ```
  - `project-a` プロジェクトの `us-central1-a` ゾーンの `instance-1` インスタンス(仮想マシン)の
  - `~/sample2.txt` ファイルを
  - ローカルの `~` （ホームディレクトリ） にダウンロード

* コマンド例2:
  ```sh
  gcloud compute scp –r instance-1:~/folder2 ~  --zone "us-central1-a" --project "project-a"
  ```
  - `project-a` プロジェクトの `us-central1-a` ゾーンの `instance-1` インスタンス(仮想マシン) の
  - `~/folder2` フォルダを
  - ローカルの `~` （ホームディレクトリ） にダウンロード

## その他、参考資料

* [Compute Engine / SSH 接続について # メタデータ マネージド SSH 接続 | Google Cloud公式](https://cloud.google.com/compute/docs/instances/ssh?hl=ja#gcloud)
* [Compute Engine / Linux VMにファイルを転送する # Google Cloud CLI を使用してファイルを転送する | Google Cloud公式](https://cloud.google.com/compute/docs/instances/transfer-files?hl=ja#transfergcloud)

