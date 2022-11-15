# Pythonプログラムのサンプル

## 散布図を表示する

```python
import matplotlib.pyplot as plt

# データを定義
jp_score_list   = [83, 68, 62, 58, 45, 43, 58, 85, 65, 51, 63]
math_score_list = [36, 77, 47, 42, 75, 19, 39, 46, 51, 75, 69]
pass_list = [True, True, False, False, False, False, False, True, False, True, True]

# 散布図をプロット
marker_size = 25
color = 'black'
plt.scatter(jp_score_list, math_score_list, s=marker_size, c=color)
plt.show()
```

## 2つの散布図を重ねる

```python
import matplotlib.pyplot as plt

# データを定義
jp_score_list   = [83, 68, 62, 58, 45, 43, 58, 85, 65, 51, 63]
math_score_list = [36, 77, 47, 42, 75, 19, 39, 46, 51, 75, 69]
pass_list = [True, True, False, False, False, False, False, True, False, True, True]

# 合格・不合格に分けて配列に入れる
pass_jp_score_list   = []
pass_math_score_list = []
not_pass_jp_score_list   = []
not_pass_math_score_list = []
for i in range(len(jp_score_list)):
  jp_score   = jp_score_list[i]
  math_score = math_score_list[i]
  pass_      = pass_list[i] # passは予約語なので後に_をつけて回避
  if pass_:
    pass_jp_score_list.append(jp_score)
    pass_math_score_list.append(math_score)
  else:
    not_pass_jp_score_list.append(jp_score)
    not_pass_math_score_list.append(math_score)

# 散布図をプロット
marker_size = 25
color = 'blue'
plt.scatter(pass_jp_score_list, pass_math_score_list, s=marker_size, c=color)
marker_size = 25
color = 'red'
plt.scatter(not_pass_jp_score_list, not_pass_math_score_list, s=marker_size, c=color)
plt.show()
```

## 平均等の値を計算する

```python
import numpy as np

# データを定義
jp_score_list   = [83, 68, 62, 58, 45, 43, 58, 85, 65, 51, 63]
math_score_list = [36, 77, 47, 42, 75, 19, 39, 46, 51, 75, 69]
pass_list = [True, True, False, False, False, False, False, True, False, True, True]

# 数理演算用ライブラリnumpyの管理するリスト形式に変換
jp_score_array   = np.array(jp_score_list)
math_score_array = np.array(math_score_list)

# 平均を算出
jp_average   = np.mean(jp_score_array)
math_average = np.mean(math_score_array)

# 分散を算出
jp_var   = np.var(jp_score_array)
math_var = np.var(math_score_array)

# 標準偏差を算出
jp_std   = np.std(jp_score_array)
math_std = np.std(math_score_array)

# 表示
# {:.1f}と書き、その後のformat関数で数値を指定すると、小数第1桁まで表示する
print('国語の平均: {:.1f}, 分散: {:.1f}, 標準偏差: {:.1f}'.format(jp_average,   jp_var,   jp_std))
print('算数の平均: {:.1f}, 分散: {:.1f}, 標準偏差: {:.1f}'.format(math_average, math_var, math_std))
```

## Yahooニュースのトップニュースの一覧を表示する

```python
import requests
from bs4 import BeautifulSoup

url = 'https://news.yahoo.co.jp/'
res = requests.get(url)

soup = BeautifulSoup(res.text)

topic_tag_list = soup.select('#uamods-topics > div > div > div > ul > li')
print(f'全{len(topic_tag_list)}件:')
for topic_tag in topic_tag_list:
  topic_title = topic_tag.text
  print(topic_title)
```