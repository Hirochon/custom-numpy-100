# Numpy100本ノックの感想文1〜10

## 目次

- [identify matrixとは単位行列を意味しますw(np.eye)](#identifymatrixとは単位行列を意味しますwnpeye)
- [np.random.randomでランダムな値の行列を作成](#nprandomrandomでランダムな値の行列を作成)
- [Numpy行列でもmaxとminは使える話](#Numpy行列でもmaxとminは使える話)
- [meanで平均値求めます](#meanで平均値求めます)
- [Numpyでの参照の仕方(スライスの使い方も)](#Numpyでの参照の仕方スライスの使い方も)
- [np.padが配列の周りをパディングしよるw](#nppadが配列の周りをパディングしよるw)
- [ヤバ面(nan, inf, 掛け算)](#ヤバ面naninf掛け算)
- [スライス使ってボーダーチェックつくる！！](#スライス使ってボーダーチェックつくる)


## 感想

### identify matrixとは単位行列を意味しますw(np.eye)
- n × n の単位行列がほしいときは`np.eye(n)`

```python:jupyter.py
Z_id = np.eye(3)
```

### np.random.randomでランダムな値の行列を作成
- タプルで囲む必要がある
- 3×3なら`np.random.random((3,3))`

```python:jupyter.py
Z_ran = np.random.random((3,3,3))
```

### Numpy行列でもmaxとminは使える話

```python:jupyter.py
Z_10 = np.random.random((10, 10))
print(Z_10)
print(Z_10.max(), Z_10.min())
```

### meanで平均値求めます
- 以下だとだいたい0.5らへん

```python:jupyter.py
Z = np.random.random(30)
ans = Z.mean()
print(ans)
```

### Numpyでの参照の仕方(スライスの使い方も)
- Numpyでは`Z[4][6]`を`Z[4,6]`と書ける
- またNumpyでは`Z[2:4, 4:6]`のようなことができる！！！

- 例えば↓だと１の枠を作れる

```python:jupyter.py
Z_one = np.ones((10,10))
Z_one[1:-1,1:-1] = 0
print(Z_one)
```

- つまり↓コンナ書き方も…

```python:jupyter.py
Z_on = np.arange(1,101)
Z_on = Z_on.reshape((10, 10))
print(Z_on)
print(Z_on[2:4, 3:6])
```

### np.padが配列の周りをパディングしよるw
- 見た感じパディングの幅も決めれるみたい？
- `constant_value`で埋める値を決めてる
- `mode`の種類は色々あるっぽい
- てかめっちゃすごい。画像処理とかで使えそう。
- [numpy.padの使い方が分からなかったのでメモ - Qiita](https://qiita.com/horitaku1124/items/6ae979b21ddc7256b872)

```python:jupyter.py
Z = np.ones((5,5))
Z = np.pad(Z, pad_width=1, mode='constant', constant_values=0)
print(Z)
```

### ヤバ面(nan, inf, 掛け算)
- nanは何してもnan。
- infとは無限大のこと。Pythonの許容を超えたらinfになる
- 一番下のやつはbの値がやばかった

```python;jupyter.py
print(np.nan) → nan
print(0 * np.nan) → nan
print(np.nan == np.nan) → False
print(np.inf) → inf
print(np.inf > np.nan) → False
print(np.nan - np.nan) → nan
print(np.nan in set([np.nan])) → True
print(0.3 == 3 * 0.1) → False
```

### スライス使ってボーダーチェックつくる！！
- スライスを使いこなしてる感半端ない

```python:jupyter.py
Z_chebo = np.zeros((8,8), dtype=int)
display(Z_chebo)
Z_chebo[::2, ::2] = 1
Z_chebo[1::2, 1::2] = 1
display(Z_chebo)
```

### np.unravel_indexで1次元を多次元で取得しよう！
- 応用力半端なさそう...

```python:jupyter.py
# これで100個目の6×7×8の行列の座標を取得可能！
print(np.unravel_index(99, (6,7,8)))

# またこれで行列の最大値の座標を取得することも可能！
print(np.unravel_index(np.argmax(array), array.shape)
```
