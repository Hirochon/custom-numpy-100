# Numpy100本ノックの感想文41〜50

## 目次
- [np.add.reduceはnp.sumより早いのよ](#npaddreduceはnpsumより早いのよ)
- [numpy.ufunc.reduceは強メソッド](#numpyufuncreduceは強メソッド)
- [randintの引数について](#randintの引数について)
- [np.allcloseでarray内が全て等しいかチェック(float版)](#npallcloseでarray内が全て等しいかチェックfloat版)
- [np.array_equalでarray内が全て等しいかチェック(int版)](#nparray_equalでarray内が全て等しいかチェックint版)
- [flags.writeablearrayをイミュータブルにする(read-onlyにする)](#flagswriteablearrayをイミュータブルにするread-onlyにする)
- [sqrtとarctan2を使った極座標への変換方法](#sqrtとarctan2を使った極座標への変換方法)


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


