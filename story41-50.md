# Numpy100本ノックの感想文41〜50

## 目次
- [np.add.reduceはnp.sumより早いのよ](#npaddreduceはnpsumより早いのよ)
- [numpy.ufunc.reduceは強メソッド](#numpyufuncreduceは強メソッド)
- [randintの引数について](#randintの引数について)
- [np.allcloseでarray内が全て等しいかチェック(float版)](#npallcloseでarray内が全て等しいかチェックfloat版)
- [np.array_equalでarray内が全て等しいかチェック(int版)](#nparray_equalでarray内が全て等しいかチェックint版)
- [flags.writeablearrayをイミュータブルにする(read-onlyにする)](#flagswriteablearrayをイミュータブルにするread-onlyにする)
- [sqrtとarctan2を使った極座標への変換方法](#sqrtとarctan2を使った極座標への変換方法)
- [argmaxを使った配列内の一番大きな数字と0を入れ替える処理](#argmaxを使った配列内の一番大きな数字と0を入れ替える処理)
- [np行列で次元ごとに名前を与える方法](#np行列で次元ごとに名前を与える方法)
- [meshgridで行列に値を(動的に…？)入れる](#meshgridで行列に値を動的に入れる)
- [np.subtract.outerは全要素に引き算するけど情報量が多い](#npsubtractouterは全要素に引き算するけど情報量が多い)
- [np.linalg.detにより一発で行列式が計算できます…w](#nplinalgdetにより一発で行列式が計算できますw)
- [int8,32,64とfloat32,64が取れる制限について](#int83264とfloat3264が取れる制限について)
- [np.set_printoptionsでarrayの表示上限を開放せよ！](#npset_printoptionsでarrayの表示上限を開放せよ)
- [ベルトルの中で与えられたスカラと一番近い値を探すNumpyの呪文](#ベルトルの中で与えられたスカラと一番近い値を探すNumpyの呪文)


## 感想

### np.add.reduceはnp.sumより早いのよ
- 引数がarrayだけだと合計を出力するだけのやつになる

```python:jupyter.py
Z = np.arange(10)
np.add.reduce(Z)
```

### numpy.ufunc.reduceは強メソッド
- `numpy.ufunc.reduce`とかいう列or行で演算する強メソッド
- `ufunc`に演算メソッド入れる。
- reduceの引数で行列の箇所を指定できる(axisの引数を入れることによって指定可能)
- [リファレンスはこちら](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ufunc.reduce.html)

```python:jupyter.py
X = np.arange(8).reshape((2,2,2))
X
# array([[[0, 1],
#         [2, 3]],
#        [[4, 5],
#         [6, 7]]])
np.add.reduce(X, 0)
# array([[ 4,  6],
#        [ 8, 10]])
np.add.reduce(X) # confirm: default axis value is 0
# array([[ 4,  6],
#        [ 8, 10]])
np.add.reduce(X, 1)
# array([[ 2,  4],
#        [10, 12]])
np.add.reduce(X, 2)
# array([[ 1,  5],
#        [ 9, 13]])
```

### randintの引数について
- 引数1: 最低値
- 引数2: 最大値 - 1
- 引数3: 要素数(タプルを使うことで多次元も作成可)

```python:jupyter.py
A = np.random.randint(0,2,5)
B = np.random.randint(0,2,(2,3))
display(A, B)
# array([1, 0, 0, 1, 0])
# array([[0, 0, 0],
#        [1, 0, 1]])
```

### np.allcloseでarray内が全て等しいかチェック(float版)
- 8乗までチェック可能
- Nanがarrayに存在する時点でFalse(`equal_nan=True`で解除可)
- [ドキュメント](https://docs.scipy.org/doc/numpy/reference/generated/numpy.allclose.html)

```python:jupyter.py
equal = np.allclose(A,B)
print(equal)
# False
```

### np.array_equalでarray内が全て等しいかチェック(int版)
- [ドキュメント](https://docs.scipy.org/doc/numpy/reference/generated/numpy.array_equal.html)

```python:jupyter.py
equal = np.array_equal(B,B)
print(equal)
# True
```

### flags.writeablearrayをイミュータブルにする(read-onlyにする)

```python:jupyter.py
Z = np.zeros(10)
Z.flags.writeable = False
Z[0] = 1
```

### sqrtとarctan2を使った極座標への変換方法
- ポイントはアークタンジェント関数と引数の設定
- 関数: `arctan2`
- 引数: どうやらY軸が先でX軸が後らしいw

```python:jupyter.py
Z = np.random.random((10,2))
X,Y = Z[:,0], Z[:,1]
R = np.sqrt(X**2+Y**2)
T = np.arctan2(Y,X)
print(R)
print(T)
```

### argmaxを使った配列内の一番大きな数字と0を入れ替える処理

```python:jupyter.py
Z = np.random.random(10)
print(Z)
Z[Z.argmax()] = 0
print(Z)
# ↓
# 出力結果
# [0.95704672 0.55496033 0.92706841 0.09479154 0.45701951 0.76041408
#  0.77221718 0.87812746 0.07474368 0.86133307]
# [0.         0.55496033 0.92706841 0.09479154 0.45701951 0.76041408
#  0.77221718 0.87812746 0.07474368 0.86133307]
```

### np行列で次元ごとに名前を与える方法
- `np.zeros`で定義するとして、第2引数に設定する

```python:jupyter.py
Z = np.zeros((5,5), [('x',float),('y',float)])
display(Z)
# ↓出力結果
# array([[(0., 0.), (0., 0.), (0., 0.), (0., 0.), (0., 0.)],
#        [(0., 0.), (0., 0.), (0., 0.), (0., 0.), (0., 0.)],
#        [(0., 0.), (0., 0.), (0., 0.), (0., 0.), (0., 0.)],
#        [(0., 0.), (0., 0.), (0., 0.), (0., 0.), (0., 0.)],
#        [(0., 0.), (0., 0.), (0., 0.), (0., 0.), (0., 0.)]],
#       dtype=[('x', '<f8'), ('y', '<f8')])
```

### meshgridで行列に値を(動的に…？)入れる
- `sparse`で値をx軸,y軸でそれぞれ代入することもできる
- [ドキュメント](https://docs.scipy.org/doc/numpy/reference/generated/numpy.meshgrid.html)

```python:jupyter.py
Z['x'], Z['y'] = np.meshgrid(np.linspace(0,1,5),
                             np.linspace(0,1,5))
print(Z)
# ↓出力結果
# [[(0.  , 0.  ) (0.25, 0.  ) (0.5 , 0.  ) (0.75, 0.  ) (1.  , 0.  )]
#  [(0.  , 0.25) (0.25, 0.25) (0.5 , 0.25) (0.75, 0.25) (1.  , 0.25)]
#  [(0.  , 0.5 ) (0.25, 0.5 ) (0.5 , 0.5 ) (0.75, 0.5 ) (1.  , 0.5 )]
#  [(0.  , 0.75) (0.25, 0.75) (0.5 , 0.75) (0.75, 0.75) (1.  , 0.75)]
#  [(0.  , 1.  ) (0.25, 1.  ) (0.5 , 1.  ) (0.75, 1.  ) (1.  , 1.  )]]
```

### np.subtract.outerは全要素に引き算するけど情報量が多い
- [参考文献](https://www.randpy.tokyo/entry/numpy_ufunc)

### np.linalg.detにより一発で行列式が計算できます…w
- [参考文献](https://www.mathpython.com/ja/numpy-matrix-determinant/)

### int8,32,64とfloat32,64が取れる制限について
- [ドキュメント](#https://docs.scipy.org/doc/numpy/reference/generated/numpy.finfo.html)
- intの(8,32,64)について

```python:jupyter.py
for dtype in [np.int8, np.int32, np.int64]:
   print(np.iinfo(dtype).min)
   print(np.iinfo(dtype).max)
# ↓実行結果
# -128
# 127
# -2147483648
# 2147483647
# -9223372036854775808
# 9223372036854775807
```

- floatの(32,64)について

```python:jupyter.py
for dtype in [np.float32, np.float64]:
   print(np.finfo(dtype).min)
   print(np.finfo(dtype).max)
   print(np.finfo(dtype).eps)
↓実行結果
# -3.4028235e+38
# 3.4028235e+38
# 1.1920929e-07
# -1.7976931348623157e+308
# 1.7976931348623157e+308
# 2.220446049250313e-16
```

### np.set_printoptionsでarrayの表示上限を開放せよ！
- `np.set_printoptions`の初期値は1000
- [参考文献](https://note.nkmk.me/python-numpy-set-printoptions-threshold/)

```python
print(np.get_printoptions())
# ↓実行結果
# {'edgeitems': 3, 'threshold': 1000, 'floatmode': 'maxprec', 
# 'precision': 8,'suppress': False, 'linewidth': 75, 'nanstr': 'nan', 
# 'infstr': 'inf', 'sign': '-', 'formatter': None, 'legacy': False}
Z = np.zeros(1001)
print(Z)
# ↓実行結果
# [0. 0. 0. ... 0. 0. 0.]
```

```python
np.set_printoptions(threshold=1001)
Z = np.zeros(1001)
print(Z)
# ↓実行結果
# 無事全て表示されました。(内容は多いから割愛w)
```

### ベルトルの中で与えられたスカラと一番近い値を探すNumpyの呪文
- `uniform`で0~100の間のfloatを出す
- `np.abs(Z-v)`で行列(中には数字)-floatをしてる
- それを`argmin`で最小値とってきてる
- 最後に`Z[index]`で共通する`index`の出力してる

```python
Z = np.arange(100)
v = np.random.uniform(0,100)
index = (np.abs(Z-v)).argmin()
print(Z[index])
```
