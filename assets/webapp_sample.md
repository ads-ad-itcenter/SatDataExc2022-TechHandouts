# Webアプリケーション(Python)のサンプル集

## Sample-1

* webapp-sample1.py
  ```python
  from flask import Flask

  app = Flask(__name__)


  @app.route("/")
  def hello_world():
      return "<p>Hello, World!</p>"

  ```

* 実行（コマンド）

  1. 環境セットアップ
 
      ```sh
      pip install flask
      ```
      ※その環境で一度だけ行えばOK

  2. 実行

      ```
      flask --app webapp-sample1 run
      ```
  
  3. 終了

      `Ctrl + c`押下


## Sample-2

* webapp-sample2.py
  ```python
  from flask import Flask, request
  from markupsafe import escape

  app = Flask(__name__)


  @app.route('/', methods=['GET', 'POST'])
  def simple_calculator():
      message = ""
      if request.method == 'POST':
          input_number_raw = request.form['input-number']
          if input_number_raw == '' \
                  or not input_number_raw.isdecimal():
              message = f'input: {input_number_raw} => Invalid Value'
          else:
              input_number = int(input_number_raw)
              calculated = input_number * 2
              message = f'input: {input_number:,} => result: {calculated:,}'

      return f'''
      <!doctype html>
      <title>Simple Calculator</title>
      <h1>Simple Calculator</h1>
      <h2>Input:</h2>
      <form method=post>
        <input type=text name=input-number>
        <button type=submit>submit</button>
      </form>
      <h2>Result:</h2>
      <div>{escape(message)}</div>
      '''

  ```

* 実行（コマンド）

  1. 環境セットアップ

      ```sh
      pip install flask
      ```
      ※その環境で一度だけ行えばOK

  2. 実行

      ```
      flask --app webapp-sample2 run
      ```
  
  3. 終了

      `Ctrl + c`押下

## Sample-3

* webapp-sample3.py
  ```python
  from pathlib import Path

  import cv2
  from flask import Flask, request, send_from_directory
  from markupsafe import escape
  from werkzeug.utils import secure_filename

  IMAGE_FOLDER = './webapp-images'
  ALLOWED_EXTENSIONS = ['.png', '.jpg', '.jpeg']

  Path(IMAGE_FOLDER).mkdir(parents=True, exist_ok=True)

  app = Flask(__name__)
  app.config['IMAGE_FOLDER'] = IMAGE_FOLDER


  def allowed_file(filename):
      return Path(filename).suffix in ALLOWED_EXTENSIONS


  @app.route('/', methods=['GET', 'POST'])
  def upload_file():
      message = ""
      result_html = ""
      if request.method == 'POST':
          # check if the post request has the file part
          if 'input-file' not in request.files:
              message = 'No file part'
          else:
              input_file_raw = request.files['input-file']
              # If the user does not select a file, the browser submits an
              # empty file without a filename.
              if input_file_raw.filename == '':
                  message = 'No selected file'
              elif not allowed_file(input_file_raw.filename):
                  message = 'Invalid file'
              else:
                  filename = secure_filename(input_file_raw.filename)
                  input_file_save_path = Path(app.config['IMAGE_FOLDER']) / filename
                  input_file_raw.save(input_file_save_path)

                  image = cv2.imread(str(input_file_save_path))
                  height, width = image.shape[:2]

                  gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
                  gray_filename = 'gray-' + filename
                  gray_image_save_path = Path(app.config['IMAGE_FOLDER']) / gray_filename
                  cv2.imwrite(str(gray_image_save_path), gray_image)

                  message = f'height: {height:,} px, width: {width:,} px'

                  result_html = f'''
                  <img src="/images/{filename}">
                  <img src="/images/{gray_filename}">
                  '''

      return f'''
      <!doctype html>
      <title>Image file upload sample</title>
      <h1>Image file upload sample</h1>
      <h2>Input:</h2>
      <form method=post enctype=multipart/form-data>
        <input type=file name=input-file>
        <button type=submit>submit</button>
      </form>
      <h2>Result:</h2>
      <div>{escape(message)}</div>
      <div>{result_html}</div>
      '''


  @app.route('/images/<name>')
  def download_image_file(name):
      return send_from_directory(app.config["IMAGE_FOLDER"], name)

  ```
  
  * 参考:
    * [Uploading Files | Flask公式ドキュメント](https://flask.palletsprojects.com/patterns/fileuploads/)
    * [opencv-python | PyPI](https://pypi.org/project/opencv-python/)
    * [ゼロからはじめるPython(34) OpenCVをインストールしてみよう | TECH+ マイナビニュース](https://news.mynavi.jp/techplus/article/zeropython-34/)

* 実行（コマンド）

  1. 環境セットアップ

      ```sh
      pip install flask opencv-python
      ```
      ※その環境で一度だけ行えばOK
      
      * APPENDIX: `Debian 10 based Deep Learning VM for TensorFlow Enterprise 2.7 M88` 仮想マシンで`opencv-python`を導入する場合
        
        pip(pip3) でインストールすると、エラーになります。
        代わりに、以下のコマンドでインストールしてください
        ```
        sudo apt update && sudo apt install python3-opencv
        ```

  2. 実行

      ```
      flask --app webapp-sample3 run
      ```
  
  3. 終了

      `Ctrl + c`押下

## その他、参考資料

* [Flask | PyPI](https://pypi.org/project/Flask/)
* [Flask公式ドキュメント](https://flask.palletsprojects.com/)
  * [Quickstart](https://flask.palletsprojects.com/quickstart/)
