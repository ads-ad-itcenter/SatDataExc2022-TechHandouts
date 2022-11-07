# 各種Tips

## Google Cloud / Cloud Shell Editor

### cv2関連のPylintチェックエラーが消えない: `Module 'cv2' has no 'XXXXXX' member`

環境は問題ないにも関わらず（※1）、Cloud Shell Editor上でPyLintによるチェックエラー（`Module 'cv2' has no 'XXXXX' member`）が消えない。
※1: `cv2`(`opencv-python`ライブラリ)は導入済み。プログラムは正常に動作する。

![image](https://user-images.githubusercontent.com/3213035/200119609-c71b0926-b5ed-43b0-beb6-37f8d26a4b35.png)

**💡解決方法:**

Pylintチェック実行時に、 `--generated-members=cv2.*` オプションを指定する。

1. Cloud Shell Editor の 設定画面を表示 (File > Preferences > Open Settings)
2. `Python › Linting: Pylint Args`設定 (設定検索ボックス:Search Settingsに`Python.linting.pylintArgs`)に、以下を追加
    ```
    --generated-members=cv2.*
    ```
    ![image](https://user-images.githubusercontent.com/3213035/200120019-681d412a-c320-4d70-a9af-9d0c15edf753.png)

参考:
* [opencv - PyLint not recognizing cv2 members | Stack Overflow](https://stackoverflow.com/questions/50612169/pylint-not-recognizing-cv2-members)
